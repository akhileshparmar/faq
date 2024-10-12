# Nginx configuration hierarchy

Nginx configuration files are organized into a hierarchy of blocks, each with a specific purpose, allowing for flexibility in defining server behavior. These blocks are arranged in a parent-child hierarchy, where the parent blocks can contain one or more child blocks, each of which defines certain directives.

Here's a detailed breakdown of the Nginx block hierarchy:

Let’s go through **everything related to the Nginx configuration hierarchy** in a tree-like structure, explaining each block and their relationships in the configuration. The configuration is divided into blocks that handle different functionalities, and each block is nested within another, forming a hierarchical structure.

### Full Nginx Configuration Hierarchy

```plaintext
MAIN BLOCK (Global Configuration)
│
├── events {                # Configures connection handling (e.g., concurrency)
│     ├── worker_connections 1024;   # Max connections per worker process
│     └── use epoll;                 # Event-driven architecture for Linux
│
├── http {                  # Handles HTTP/HTTPS traffic (most common use)
│     │
│     ├── include mime.types;        # MIME types for various file extensions
│     ├── default_type application/octet-stream;  # Default file type if not defined
│     ├── sendfile on;               # Enables efficient file transfers
│     ├── keepalive_timeout 65;      # How long to keep connections open
│     ├── gzip on;                   # Enables gzip compression for HTTP responses
│     │
│     ├── log_format main '$remote_addr - $remote_user [$time_local] "$request"';  # Custom log format
│     ├── access_log /var/log/nginx/access.log main;  # Location of access logs
│     │
│     ├── upstream backend {         # Load balancing or reverse proxy backend servers
│     │     ├── server backend1.example.com;   # First backend server
│     │     └── server backend2.example.com;   # Second backend server
│     │
│     ├── server {                   # Virtual host: A domain or IP-based server block
│     │     ├── listen 80;            # Port Nginx listens on (e.g., port 80 for HTTP)
│     │     ├── server_name example.com www.example.com;  # Domain names for this server block
│     │     └── root /var/www/example;  # Root directory for this server's document root
│     │
│     │     ├── location / {          # Location block for root URL ("/")
│     │     │     ├── index index.html;   # Default file to serve (if no specific file is requested)
│     │     │     └── try_files $uri $uri/ =404;  # Try different options for missing files
│     │     │
│     │     ├── location /images/ {   # Location block for serving images
│     │     │     ├── root /var/www/static;   # Location where image files are stored
│     │     │     └── autoindex on;          # Enable directory listing if no index file is found
│     │     │
│     │     ├── location ~* \.(jpg|jpeg|png|gif)$ {   # Regex-based location block for image files
│     │     │     ├── expires 30d;            # Cache images for 30 days
│     │     │     └── access_log off;         # Disable access logging for these requests
│     │     │
│     │     ├── location /api/ {      # Location block for an API
│     │     │     └── proxy_pass http://backend;  # Reverse proxy API requests to the upstream backend
│     │     │
│     │     └── error_page 404 /404.html;    # Custom error page for 404 errors
│     │
│     ├── server {                   # Second virtual host (for another domain)
│     │     ├── listen 443 ssl;       # HTTPS on port 443
│     │     ├── server_name secure.example.com;
│     │     ├── ssl_certificate /etc/nginx/ssl/cert.pem;  # SSL certificate path
│     │     ├── ssl_certificate_key /etc/nginx/ssl/cert.key;  # SSL private key path
│     │     └── root /var/www/secure;
│     │
│     │     ├── location / {          # Root URL for secure.example.com
│     │     │     └── try_files $uri $uri/ =404;
│     │     │
│     │     ├── location ~ \.php$ {   # Handling PHP requests
│     │     │     ├── include fastcgi_params;      # Include FastCGI parameters
│     │     │     └── fastcgi_pass 127.0.0.1:9000; # Forward PHP to FastCGI server (e.g., PHP-FPM)
│     │
│     └── include /etc/nginx/conf.d/*.conf;  # Include additional configuration files
│
├── stream {                 # Handles TCP/UDP traffic (Optional)
│     ├── upstream tcp_backend {  # TCP load balancing
│     │     ├── server backend1.example.com:12345;  # First TCP server
│     │     └── server backend2.example.com:12345;  # Second TCP server
│     │
│     └── server {           # TCP/UDP server block
│         ├── listen 12345;     # TCP server listens on port 12345
│         └── proxy_pass tcp_backend;   # Load balance TCP traffic to backend
│
└── mail {                   # Mail proxy (Optional, rarely used)
      └── server {           # Mail server block
          ├── listen 587;     # SMTP over TLS port (optional for email)
          └── proxy_pass mail_backend;  # Forward mail traffic to backend mail server
}
```

Let’s dive deeper into the description of each block in Nginx configuration, detailing what each one includes, its purpose, and a practical example for each block.

### 1. **Main Block (Global Configuration)**

- **Description**: The **Main Block** is the top-level configuration in the Nginx hierarchy. It sets global directives that apply to the entire Nginx instance, including process management, logging, and other core server configurations.
- **Includes**:

  - **worker_processes**: Defines the number of worker processes.
  - **error_log**: Configures the location of the error logs.
  - **pid**: Sets the location of the file containing the process ID.

- **Example**:
  ```nginx
  worker_processes auto;             # Automatically determines the number of processes
  error_log /var/log/nginx/error.log warn;  # Log location and log level
  pid /var/run/nginx.pid;            # PID file location
  ```

### 2. **Events Block**

- **Description**: The **Events Block** controls how Nginx handles connections. It defines concurrency settings such as how many simultaneous connections each worker process can handle.
- **Includes**:

  - **worker_connections**: The maximum number of simultaneous connections per worker process.
  - **use**: Defines the event model used (e.g., `epoll` for Linux or `kqueue` for BSD).

- **Example**:
  ```nginx
  events {
      worker_connections 1024;   # Each worker process can handle 1024 connections
      use epoll;                 # Use epoll for event handling (Linux-based)
  }
  ```

### 3. **HTTP Block**

- **Description**: The **HTTP Block** handles all HTTP/HTTPS traffic and contains most of the web-related settings. Inside this block, you can define **server**, **upstream**, and **location** blocks to configure how Nginx serves content and proxies requests.
- **Includes**:

  - **gzip**: Enable or disable gzip compression.
  - **log_format**: Customizes how access logs are formatted.
  - **access_log**: Specifies the location of access logs.
  - **proxy_pass**: Defines a reverse proxy to another server or backend.

- **Example**:

  ```nginx
  http {
      include       mime.types;                # Include file for MIME types
      default_type  application/octet-stream;  # Default file type if not specified
      sendfile      on;                        # Enable sendfile for faster file transfers
      keepalive_timeout 65;                    # Keep connection alive for 65 seconds
      gzip on;                                 # Enable gzip compression

      log_format main '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
      access_log /var/log/nginx/access.log main;   # Location of access logs
  }
  ```

### 4. **Upstream Block**

- **Description**: The **Upstream Block** is used for defining groups of backend servers for load balancing or reverse proxying. Nginx can forward requests to one or more servers defined in the upstream block.
- **Includes**:

  - **server**: Defines each backend server. Multiple servers can be grouped for load balancing.
  - **ip_hash**: Can be used for session persistence, ensuring the same client is forwarded to the same backend server.

- **Example**:

  ```nginx
  upstream backend {
      server backend1.example.com;  # First backend server
      server backend2.example.com;  # Second backend server
  }

  server {
      location /api/ {
          proxy_pass http://backend;  # Forward requests to the upstream backend
      }
  }
  ```

### 5. **Server Block**

- **Description**: The **Server Block** defines an individual server or virtual host that listens for incoming connections on a specific port and domain name. It’s used to configure domain-specific behavior such as routing, SSL, and error pages.
- **Includes**:

  - **listen**: Specifies the port and optionally the IP address the server listens on (e.g., 80 for HTTP or 443 for HTTPS).
  - **server_name**: Defines the domain names that this server block should respond to.
  - **root**: Specifies the root directory for serving static files.

- **Example**:

  ```nginx
  server {
      listen 80;                            # Listen on port 80 (HTTP)
      server_name example.com www.example.com;  # Domain names

      root /var/www/html;                   # Root directory for serving files
      index index.html;                     # Default file to serve if none specified

      error_page 404 /404.html;             # Custom 404 error page
  }
  ```

### 6. **Location Block**

- **Description**: The **Location Block** defines how Nginx should handle requests for specific URLs or patterns. You can serve static files, proxy requests to a backend, or return custom responses.
- **Includes**:

  - **root** or **alias**: Defines the file system path for serving static files.
  - **proxy_pass**: Forwards the request to a backend server.
  - **try_files**: Tries different file paths or returns a specific status if not found.
  - **regex**: Can use regular expressions to match specific URL patterns.

- **Example**:

  ```nginx
  server {
      location / {
          root /var/www/html;                # Root directory for static content
          index index.html;                  # Default file to serve
      }

      location /images/ {
          root /data;                        # Serve files from /data directory for /images/ path
      }

      location ~* \.(jpg|jpeg|png|gif)$ {    # Regex to match image file extensions
          expires 30d;                       # Cache images for 30 days
          access_log off;                    # Disable logging for image requests
      }

      location /api/ {
          proxy_pass http://backend;         # Reverse proxy for API requests
      }
  }
  ```

### 7. **Stream Block (Optional)**

- **Description**: The **Stream Block** is used for handling non-HTTP traffic, such as TCP/UDP connections. It’s useful when Nginx is acting as a load balancer for services like databases, mail servers, or custom protocols.
- **Includes**:

  - **listen**: Specifies the port that Nginx listens on for TCP/UDP traffic.
  - **proxy_pass**: Forwards TCP/UDP traffic to a backend server.

- **Example**:

  ```nginx
  stream {
      upstream tcp_backend {
          server backend1.example.com:12345;   # First backend server for TCP traffic
          server backend2.example.com:12345;   # Second backend server
      }

      server {
          listen 12345;                        # Listen for TCP traffic on port 12345
          proxy_pass tcp_backend;              # Forward traffic to upstream servers
      }
  }
  ```

### 8. **Mail Block (Optional)**

- **Description**: The **Mail Block** is used for proxying email traffic (SMTP, IMAP, POP3). Nginx can handle load balancing and authentication for mail servers.
- **Includes**:

  - **listen**: Specifies the port for handling mail traffic (e.g., port 587 for SMTP).
  - **proxy_pass**: Forwards email traffic to backend mail servers.

- **Example**:
  ```nginx
  mail {
      server {
          listen 587;                           # Listen for SMTP over TLS
          protocol smtp;                        # SMTP protocol
          proxy_pass mail_backend;              # Forward traffic to mail backend
      }
  }
  ```

---

### Summary Table:

| **Block**          | **Description**                                                      | **Common Directives**                      | **Example**                                                    |
| ------------------ | -------------------------------------------------------------------- | ------------------------------------------ | -------------------------------------------------------------- |
| **Main Block**     | Global configuration for the entire Nginx server.                    | `worker_processes`, `error_log`, `pid`     | `worker_processes auto;`                                       |
| **Events Block**   | Configures connection-related settings.                              | `worker_connections`, `use`                | `worker_connections 1024;`                                     |
| **HTTP Block**     | Handles all HTTP/HTTPS traffic. Contains server and location blocks. | `gzip`, `log_format`, `access_log`         | `gzip on;`                                                     |
| **Upstream Block** | Defines backend servers for load balancing.                          | `server`, `ip_hash`                        | `upstream backend { server backend1.example.com; }`            |
| **Server Block**   | Defines virtual hosts or domain-based servers.                       | `listen`, `server_name`, `root`            | `server { listen 80; server_name example.com; }`               |
| **Location Block** | Handles specific URL paths or patterns within a server block.        | `root`, `proxy_pass`, `try_files`, `regex` | `location /images/ { root /data; }`                            |
| **Stream Block**   | Configures TCP/UDP traffic handling (optional).                      | `listen`, `proxy_pass`                     | `stream { listen 12345; proxy_pass tcp_backend; }`             |
| **Mail Block**     | Handles email traffic (SMTP/IMAP/POP3) (optional).                   | `listen`, `proxy_pass`, `protocol`         | `mail { listen 587; protocol smtp; proxy_pass mail_backend; }` |

This table and the detailed explanations provide a comprehensive understanding of the Nginx configuration hierarchy and its blocks. Each block plays a crucial role in Nginx’s functionality, from handling simple HTTP requests to complex load balancing and traffic forwarding setups.

### Summary:

- **Main Block** is the top-level configuration.
- **Events Block** handles connection-related settings like concurrency.
- **HTTP Block** is the most commonly used and deals with web traffic (contains **upstream**, **server**, and **location** blocks).
- **Stream Block** deals with non-HTTP traffic like TCP/UDP (optional).
- **Mail Block** deals with email traffic (rarely used).
- Inside the **HTTP Block**, the **Upstream Block** manages load balancing, while the **Server Block** configures individual servers (virtual hosts), and the **Location Block** manages specific URL paths or regex-based routing.

This hierarchy allows Nginx to be highly flexible, enabling configurations from the global level down to specific URLs, balancing traffic, or handling specific protocols.
