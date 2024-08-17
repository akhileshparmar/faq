# URL, URI and URN

The terms **URL**, **URI**, and **URN** are essential concepts in understanding how resources are identified and accessed on the internet. Let's break down each of these terms in detail, using the analogy provided and the technical explanations to clarify their differences.

### 1. **URI: Uniform Resource Identifier**

- **Definition:** A URI is a general term for anything that uniquely identifies a resource on the internet. This could be a name, location, or both.
- **Analogy (House Identification):** Imagine you tell someone, "I live in the only yellow house in town." Here, you're identifying your house based on a unique characteristic (its yellow color), without specifying how to find it. Similarly, a URI can uniquely identify a resource without necessarily providing the means to access it.
- **Components:**
  - **Scheme/Protocol:** Indicates the method or protocol to access the resource (e.g., `http`, `https`, `ftp`).
  - **Authority:** Optionally includes information like domain name and port number.
  - **Path:** Specifies the location of the resource within the host.
  - **Query:** Optional parameters passed to the server for dynamic content.
  - **Fragment:** Optional part that identifies a specific section within the resource.
- **Example:** `https://www.example.com/resource`

### 2. **URL: Uniform Resource Locator**

- **Definition:** A URL is a specific type of URI that not only identifies a resource but also provides the exact location on the internet and how to access it.
- **Analogy (House Identification with Directions):** Now, if you say, "I live in the only yellow house at 123 Main Street. Go down Oak Avenue, turn right, and you'll find it," you're not only identifying your house but also providing precise directions to reach it. Similarly, a URL gives the address (location) of a resource along with the protocol (directions) to access it.
- **Components:**
  - **Scheme/Protocol:** Specifies the communication protocol (e.g., `http://`, `https://`).
  - **Domain Name:** Identifies the specific website or server (e.g., `www.example.com`).
  - **Port:** Optional part that specifies the communication endpoint on the server.
  - **Path to File:** Indicates the specific location of the resource on the server (e.g., `/resource`).
  - **Query:** Allows passing additional parameters to the server.
  - **Anchor/Fragment:** Directs to a specific section within a webpage (e.g., `#section`).
- **Example:** `https://www.example.com/resource`

### 3. **URN: Uniform Resource Name**

- **Definition:** A URN is a subset of URI that provides a persistent, location-independent identifier for a resource. It focuses on uniquely naming a resource, without concern for where it is located.
- **Analogy (Identifying by Name):** Suppose you tell someone, "My house is named 'The Yellow Haven'." This doesn't tell them where to find it, but the name is unique and can be used to refer to the house anywhere. Similarly, a URN uniquely identifies a resource by name, regardless of its location.
- **Components:**
  - **Scheme:** Always uses the prefix `urn:` to indicate it's a URN.
  - **Namespace Identifier (NID):** Defines a namespace (e.g., `isbn` for books).
  - **Namespace Specific String (NSS):** The unique identifier within the namespace.
- **Example:** `urn:isbn:1234567890` (identifies a specific book by its ISBN)

### **Summarizing the Differences:**

- **URI (Uniform Resource Identifier):** A broad term that refers to anything that uniquely identifies a resource. It can be a name, location, or both.
- **URL (Uniform Resource Locator):** A specific type of URI that provides the location of a resource on the internet and the protocol to access it. Essentially, it’s the complete address of a resource.
- **URN (Uniform Resource Name):** A specific type of URI that provides a unique name to a resource, independent of its location. It’s used to give a resource a stable, persistent identifier.

### **In Short:**

- **URI** is the most general term and can identify a resource by name, location, or both.
- **URL** is a URI that specifies the exact location and means to access a resource.
- **URN** is a URI that provides a persistent, location-independent identifier for a resource.
