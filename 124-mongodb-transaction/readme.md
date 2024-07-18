# Transactions in MongoDB

A **transaction** in MongoDB allows you to execute multiple read and write operations across multiple documents and collections in a single atomic operation. This means that all the operations within a transaction will either succeed or fail together, ensuring data consistency.

### Multi-Document Transactions

MongoDB supports multi-document transactions in replica sets starting from version 4.0 and in sharded clusters starting from version 4.2. Multi-document transactions provide **ACID** (Atomicity, Consistency, Isolation, Durability) properties across multiple documents.

### ACID Properties

1. **Atomicity**: All the operations in a transaction are completed successfully or none of them are.
2. **Consistency**: The database will remain in a consistent state before and after the transaction.
3. **Isolation**: Multiple transactions can occur concurrently without causing inconsistencies.
4. **Durability**: Once a transaction has been committed, it will remain committed even in the case of a system failure.

### Implementing Transactions in MongoDB

To use transactions in MongoDB, you need to use a session. Here is a step-by-step guide with examples:

#### Example: Implementing a Transaction

Suppose you have two collections: `accounts` and `transactions`. You want to transfer an amount from one account to another atomically.

1. **Start a Session**

```javascript
const { MongoClient } = require("mongodb");

async function main() {
  const uri =
    "mongodb+srv://<username>:<password>@cluster0.mongodb.net/test?retryWrites=true&w=majority";
  const client = new MongoClient(uri, {
    useNewUrlParser: true,
    useUnifiedTopology: true,
  });

  try {
    await client.connect();
    const session = client.startSession();

    // Define the transaction options
    const transactionOptions = {
      readPreference: "primary",
      readConcern: { level: "local" },
      writeConcern: { w: "majority" },
    };

    // Transaction operations
    const transferMoney = async (session) => {
      const accountsCollection = client.db("bank").collection("accounts");
      const transactionsCollection = client
        .db("bank")
        .collection("transactions");

      const sourceAccount = "1234567890";
      const destinationAccount = "0987654321";
      const amount = 100;

      const sourceAccountDoc = await accountsCollection.findOne(
        { accountNumber: sourceAccount },
        { session }
      );
      const destinationAccountDoc = await accountsCollection.findOne(
        { accountNumber: destinationAccount },
        { session }
      );

      if (!sourceAccountDoc || !destinationAccountDoc) {
        throw new Error("Account not found");
      }

      if (sourceAccountDoc.balance < amount) {
        throw new Error("Insufficient funds");
      }

      await accountsCollection.updateOne(
        { accountNumber: sourceAccount },
        { $inc: { balance: -amount } },
        { session }
      );

      await accountsCollection.updateOne(
        { accountNumber: destinationAccount },
        { $inc: { balance: amount } },
        { session }
      );

      await transactionsCollection.insertOne(
        {
          from: sourceAccount,
          to: destinationAccount,
          amount: amount,
          date: new Date(),
        },
        { session }
      );
    };

    // Run the transaction
    try {
      await session.withTransaction(transferMoney, transactionOptions);
      console.log("Transaction completed successfully");
    } catch (error) {
      console.error("Transaction failed: ", error);
    } finally {
      await session.endSession();
    }
  } finally {
    await client.close();
  }
}

main().catch(console.error);
```

#### Explanation

1. **Start a Session**: `const session = client.startSession();`

   - This initiates a session that will be used for the transaction.

2. **Transaction Options**: Define transaction options like `readPreference`, `readConcern`, and `writeConcern`.

3. **Transaction Operations**:

   - Retrieve source and destination account documents.
   - Check if the accounts exist and if the source account has sufficient funds.
   - Update the account balances and insert a transaction record within the same session.

4. **Run the Transaction**: `await session.withTransaction(transferMoney, transactionOptions);`

   - This runs the `transferMoney` function within a transaction. If any operation fails, the entire transaction will be aborted.

5. **Error Handling**: Handle any errors that occur during the transaction and ensure the session is ended properly.

### Considerations

- **Performance**: Transactions can introduce overhead, so they should be used judiciously.
- **Isolation Level**: MongoDB uses "snapshot isolation" which ensures that transactions read a consistent snapshot of the data.
- **Storage Engine**: Transactions are supported only on the WiredTiger storage engine.

By understanding and effectively using transactions in MongoDB, you can ensure data consistency and integrity in your applications.
