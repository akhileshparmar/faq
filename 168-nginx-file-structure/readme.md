# Nginx file structure

The **Nginx file structure** consists of directories and configuration files that are essential for running and managing the Nginx web server. Each folder and file serves a specific purpose, from holding the main configuration files to storing logs and hosting site-specific configurations. Let's break down the file structure with a detailed explanation of each folder and its contents in a **tree-like structure**:

### Nginx File Structure (Typical on Linux-based systems)

```plaintext
/etc/nginx/                  # Nginx configuration directory (main directory)
│
├── nginx.conf                # Main Nginx configuration file (Global configuration)
│
├── mime.types                # MIME types for file extensions
│
├── conf.d/                   # Directory for additional configuration files
│     ├── default.conf        # Default server configuration (often used for generic settings)
│     └── *.conf              # Any custom or additional configuration files
│
├── sites-available/          # Available virtual hosts configuration files
│     ├── example.com         # Example server block for a domain
│     └── another-site.conf   # Another virtual host configuration
│
├── sites-enabled/            # Enabled virtual hosts (symlinks to `sites-available`)
│     ├── example.com         # Symlink to `sites-available/example.com`
│     └── another-site.conf   # Symlink to `sites-available/another-site.conf`
│
├── snippets/                 # Reusable configuration snippets
│     ├── ssl-params.conf     # Example SSL settings
│     └── fastcgi-php.conf    # FastCGI settings for PHP
│
└── modules-enabled/          # Nginx modules (dynamic modules loaded at runtime)
      └── *.conf              # Each module's configuration file
```

---

### 1. **`/etc/nginx/`** (Main Configuration Directory)

- **Description**: This is the root directory where all the Nginx configuration files are stored. It contains the global configuration file (`nginx.conf`), MIME types, and other directories for handling specific server configurations.
- **Includes**:
  - `nginx.conf`: The main configuration file for Nginx.
  - `mime.types`: File defining various MIME types.
  - `conf.d/`: A directory to hold additional configuration files.
  - `sites-available/` and `sites-enabled/`: For managing virtual hosts.
  - `snippets/`: Reusable configuration snippets.

---

### 2. **`/etc/nginx/nginx.conf`** (Main Configuration File)

- **Description**: The **main configuration file** for Nginx, where global settings and directives are defined. This file is the starting point for the Nginx configuration and can include references to other files or directories (like `conf.d/` or `sites-enabled/`).
- **Contains**:

  - **Global directives** for Nginx, such as worker processes, logging, and event settings.
  - **HTTP block** to configure the handling of HTTP/HTTPS traffic.
  - **Include directives** to pull in configurations from `conf.d/` or other directories.

- **Example**:
  ```nginx
  worker_processes auto;
  events {
      worker_connections 1024;
  }
  http {
      include mime.types;
      default_type application/octet-stream;
      include /etc/nginx/conf.d/*.conf;    # Includes all configurations from conf.d/
  }
  ```

---

### 3. **`/etc/nginx/mime.types`** (MIME Types File)

- **Description**: The **MIME types file** is used by Nginx to map file extensions (like `.html`, `.css`, `.jpg`, etc.) to their correct MIME types. This ensures that browsers and clients interpret files correctly.
- **Contains**:

  - A list of file extensions and their associated MIME types.

- **Example**:
  ```nginx
  types {
      text/html    html;
      text/css     css;
      image/jpeg   jpg jpeg;
      image/png    png;
      application/javascript js;
  }
  ```

---

### 4. **`/etc/nginx/conf.d/`** (Additional Configuration Directory)

- **Description**: The **`conf.d/` directory** is where additional or modular configuration files can be placed. These files are typically included into the main configuration using an `include` directive in `nginx.conf`.
- **Contains**:

  - Additional configuration files, each typically having a `.conf` extension.
  - Files such as `default.conf` or custom configurations for specific servers or services.

- **Example**:

  ```nginx
  /etc/nginx/conf.d/
  ├── default.conf           # Default configuration file
  ├── ssl.conf               # SSL configuration
  └── caching.conf           # Caching settings
  ```

- **Example File (`default.conf`)**:
  ```nginx
  server {
      listen 80;
      server_name example.com;
      root /var/www/html;
      location / {
          try_files $uri $uri/ =404;
      }
  }
  ```

---

### 5. **`/etc/nginx/sites-available/`** (Available Virtual Hosts)

- **Description**: The **`sites-available/` directory** contains configuration files for virtual hosts (server blocks), which define how Nginx handles requests for specific domains or IP addresses. Each domain or application typically has its own configuration file here.
- **Contains**:

  - Server block configuration files for each virtual host (domain).
  - Each file is not enabled by default; you enable them by creating symbolic links in the `sites-enabled/` directory.

- **Example**:

  ```nginx
  /etc/nginx/sites-available/
  ├── example.com.conf          # Configuration for example.com
  ├── another-site.com.conf     # Configuration for another domain
  ```

- **Example File (`example.com`)**:
  ```nginx
  server {
      listen 80;
      server_name example.com;
      root /var/www/example.com;
      location / {
          try_files $uri $uri/ =404;
      }
  }
  ```

---

### 6. **`/etc/nginx/sites-enabled/`** (Enabled Virtual Hosts)

- **Description**: The **`sites-enabled/` directory** contains **symbolic links** to the configuration files in the `sites-available/` directory. Only the files linked in this directory will be **active** and used by Nginx.
- **Contains**:

  - Symbolic links to configuration files in `sites-available/`.

- **Example**:
  ```plaintext
  /etc/nginx/sites-enabled/
  ├── example.com.conf -> /etc/nginx/sites-available/example.com.conf
  ├── another-site.conf -> /etc/nginx/sites-available/another-site.conf
  ```

---

### 7. **`/etc/nginx/snippets/`** (Reusable Configuration Snippets)

- **Description**: The **`snippets/` directory** holds reusable configuration fragments. These snippets can be included in multiple server blocks to avoid redundancy and simplify configurations (e.g., SSL settings, FastCGI configurations, etc.).
- **Contains**:

  - Configuration files with reusable settings, such as SSL configurations, common redirects, or FastCGI settings.

- **Example**:

  ```nginx
  /etc/nginx/snippets/
  ├── ssl-params.conf         # Reusable SSL settings
  ├── fastcgi-php.conf        # FastCGI settings for PHP
  ```

- **Example File (`ssl-params.conf`)**:
  ```nginx
  ssl_protocols TLSv1.2 TLSv1.3;
  ssl_prefer_server_ciphers on;
  ssl_ciphers HIGH:!aNULL:!MD5;
  ```

---

### 8. **`/etc/nginx/modules-enabled/`** (Nginx Dynamic Modules)

- **Description**: The **`modules-enabled/` directory** contains configuration files for Nginx **dynamic modules**. These modules provide additional functionality and are loaded dynamically at runtime.
- **Contains**:
  - Configuration files for dynamically loaded modules (e.g., `http_geoip_module`, `http_image_filter_module`).
- **Example**:

  ```nginx
  /etc/nginx/modules-enabled/
  ├── 50-mod-http-image-filter.conf   # Image filter module configuration
  └── 50-mod-http-geoip.conf          # GeoIP module configuration
  ```

- **Example File (`50-mod-http-image-filter.conf`)**:
  ```nginx
  load_module modules/ngx_http_image_filter_module.so;
  ```

---

### Additional Nginx Directories and Files:

#### 9. **`/var/log/nginx/`** (Log Files)

- **Description**: This directory contains **access** and **error logs** generated by Nginx.
- **Contains**:

  - `access.log`: Logs every request handled by Nginx.
  - `error.log`: Logs Nginx errors (warnings, critical errors, etc.).

- **Example**:
  ```plaintext
  /var/log/nginx/
  ├── access.log                 # General access log
  └── error.log                  # General error log
  ```

#### 10. **`/var/www/`** (Web Content Directory)

- **Description**: The **document root** directory where web content (HTML, CSS, JS, images) is stored. Virtual hosts

typically point their `root` or `alias` to subdirectories inside `/var/www/`.

- **Contains**:

  - Subdirectories for different sites or applications hosted by Nginx.

- **Example**:
  ```plaintext
  /var/www/
  ├── example.com/                # Document root for example.com
  │    └── index.html             # Index page for the site
  └── another-site/               # Document root for another site
  ```

---

### Summary of Nginx File Structure:

| **Directory/File**     | **Description**                                                                   |
| ---------------------- | --------------------------------------------------------------------------------- |
| **`/etc/nginx/`**      | Main directory containing all Nginx configuration files.                          |
| **`nginx.conf`**       | Global configuration file that includes directives for the entire Nginx instance. |
| **`mime.types`**       | File that maps file extensions to MIME types.                                     |
| **`conf.d/`**          | Directory for modular configuration files (e.g., SSL, caching, etc.).             |
| **`sites-available/`** | Contains configuration files for virtual hosts (domains).                         |
| **`sites-enabled/`**   | Symbolic links to `sites-available/` files to activate virtual hosts.             |
| **`snippets/`**        | Reusable configuration fragments (e.g., SSL settings).                            |
| **`modules-enabled/`** | Configuration for dynamically loaded Nginx modules.                               |
| **`/var/log/nginx/`**  | Log files generated by Nginx (access and error logs).                             |
| **`/var/www/`**        | Directory for hosting web content (HTML, CSS, JS).                                |

This structure provides flexibility in managing Nginx configurations, allowing you to separate, reuse, and manage settings for various components (like virtual hosts, SSL, caching, and modules).
