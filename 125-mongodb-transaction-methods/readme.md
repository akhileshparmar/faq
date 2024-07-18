# Transaction Methods

In MongoDB, handling transactions involves using specific methods provided by the MongoDB Node.js driver. Here's a detailed explanation of the main transaction-related methods:

### Key Transaction Methods

1. **`startSession()`**

   - **Purpose**: Initializes a new session. This session is necessary for creating transactions.
   - **Usage**:
     ```javascript
     const session = client.startSession();
     ```
   - **Details**: A session allows you to group operations into a single transaction.

2. **`startTransaction()`**

   - **Purpose**: Starts a new transaction within an active session.
   - **Usage**:
     ```javascript
     session.startTransaction(transactionOptions);
     ```
   - **Details**: This method is used to begin a transaction within a session. The `transactionOptions` parameter is optional and can include settings like `readPreference`, `readConcern`, and `writeConcern`.

3. **`commitTransaction()`**

   - **Purpose**: Commits the current transaction, making all changes made during the transaction permanent.
   - **Usage**:
     ```javascript
     await session.commitTransaction();
     ```
   - **Details**: Once this method is called, all operations within the transaction are applied to the database. If the transaction fails, you should handle the error and potentially roll back changes using `abortTransaction()`.

4. **`abortTransaction()`**

   - **Purpose**: Aborts the current transaction, discarding all changes made during the transaction.
   - **Usage**:
     ```javascript
     await session.abortTransaction();
     ```
   - **Details**: This method undoes any operations performed within the transaction. It is typically used when an error occurs or when you want to discard changes.

5. **`endSession()`**
   - **Purpose**: Ends the session. This is necessary after finishing a transaction to release resources.
   - **Usage**:
     ```javascript
     await session.endSession();
     ```
   - **Details**: After committing or aborting a transaction, you should end the session to clean up.

### Example of Using Transaction Methods

Here’s a practical example illustrating the use of these methods:

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
    const transactionOptions = {
      readPreference: "primary",
      readConcern: { level: "local" },
      writeConcern: { w: "majority" },
    };

    try {
      session.startTransaction(transactionOptions);

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

      await session.commitTransaction();
      console.log("Transaction completed successfully");
    } catch (error) {
      console.error("Transaction failed: ", error);
      await session.abortTransaction();
    } finally {
      await session.endSession();
    }
  } finally {
    await client.close();
  }
}

main().catch(console.error);
```

### Summary of Methods

| Method                | Purpose                                       | Usage Example                                   |
| --------------------- | --------------------------------------------- | ----------------------------------------------- |
| `startSession()`      | Initializes a new session for transactions    | `const session = client.startSession();`        |
| `startTransaction()`  | Begins a new transaction within the session   | `session.startTransaction(transactionOptions);` |
| `commitTransaction()` | Commits the transaction, applying all changes | `await session.commitTransaction();`            |
| `abortTransaction()`  | Aborts the transaction, discarding changes    | `await session.abortTransaction();`             |
| `endSession()`        | Ends the session, releasing resources         | `await session.endSession();`                   |

By understanding and effectively using these methods, you can manage transactions in MongoDB and ensure data integrity and consistency in your applications.
