# IP Address

An **IP (Internet Protocol) address** is a unique identifier assigned to each device connected to a network that uses the Internet Protocol for communication. It serves two main purposes:

1. **Identifying a host or network interface.**
2. **Providing the location of the host in the network.**

IP addresses are analogous to home addresses for computers on the internet. They allow devices to find each other and communicate by sending and receiving data.

### **Types of IP Addresses**

There are several types of IP addresses, categorized primarily by the version of the IP protocol they use:

#### **1. IPv4 (Internet Protocol version 4)**

- **Format:** IPv4 addresses are 32-bit numbers, typically represented in decimal format as four octets separated by periods (e.g., `192.168.0.1`).
- **Address Space:** It provides about 4.3 billion unique addresses.
- **Example:** `192.168.1.1`

#### **2. IPv6 (Internet Protocol version 6)**

- **Format:** IPv6 addresses are 128-bit numbers, written as eight groups of four hexadecimal digits, separated by colons (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`).
- **Address Space:** It vastly increases the number of available addresses, providing a virtually limitless supply.
- **Example:** `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

#### **3. Public IP Address**

- **Definition:** Public IP addresses are used to identify devices on the wider internet. They are unique across the entire web.
- **Assignment:** Managed by global organizations such as IANA (Internet Assigned Numbers Authority).
- **Example:** Your home router’s IP address as seen by the external world.

#### **4. Private IP Address**

- **Definition:** Private IP addresses are used within private networks (e.g., home or office networks). They are not routable on the internet.
- **Example:** `192.168.1.1` for a router within a home network.

#### **5. Static IP Address**

- **Definition:** A static IP address doesn’t change. It is manually assigned to a device and remains the same over time.
- **Use Cases:** Servers, printers, and other devices that need a constant IP address.

#### **6. Dynamic IP Address**

- **Definition:** A dynamic IP address is assigned by a DHCP server and can change over time.
- **Use Cases:** Most home and office devices use dynamic IP addresses to simplify network management.

# DNS (Domain Name System)

The **Domain Name System (DNS)** is like the phonebook of the internet. It translates human-readable domain names (e.g., `www.example.com`) into IP addresses (e.g., `93.184.216.34`) that computers use to identify each other on the network.

### **How DNS is Resolved?**

**DNS resolution** is the process by which a domain name is translated into an IP address. Here's how it generally works:

1. **DNS Query:** When you type a URL into your browser, a DNS query is made to resolve the domain name into an IP address.
2. **Local Cache:** The browser first checks its cache to see if it has recently visited the domain and already knows the IP address.
3. **DNS Recursive Resolver:** If the IP address isn't in the cache, the query is sent to a DNS resolver (often managed by your ISP). The resolver acts as an intermediary between your device and the DNS name servers.
4. **Root Name Server:** If the resolver doesn’t have the answer, it forwards the request to a root name server, which responds with the address of a TLD (Top-Level Domain) name server (e.g., `.com` or `.org`).
5. **TLD Name Server:** The resolver queries the TLD name server, which returns the address of the domain's authoritative name server.
6. **Authoritative Name Server:** Finally, the resolver queries the authoritative name server, which responds with the IP address associated with the domain name.
7. **Returning the IP:** The resolver returns the IP address to the browser, which then connects to the server to retrieve the webpage.

### **DNS Providers**

DNS services are provided by various organizations. Some common DNS providers include:

1. **Google Public DNS**
   - **IP Addresses:** `8.8.8.8` and `8.8.4.4`
2. **Cloudflare DNS**
   - **IP Address:** `1.1.1.1`
3. **OpenDNS (by Cisco)**
   - **IP Addresses:** `208.67.222.222` and `208.67.220.220`
4. **ISP-provided DNS:** Your Internet Service Provider often provides DNS services automatically.

### **How DNS Works?**

DNS works through a distributed database of domain names and IP addresses. The process involves several steps:

1. **Domain Name Hierarchy:** DNS uses a hierarchical structure. Domains are divided into multiple levels, such as:

   - **Root Level:** Represented as a dot (`.`), it’s the top of the DNS hierarchy.
   - **Top-Level Domain (TLD):** This includes `.com`, `.org`, `.net`, country codes like `.uk`, `.us`, etc.
   - **Second-Level Domain:** The main part of the domain name, like `example` in `example.com`.
   - **Subdomain:** Optional prefixes to the main domain, such as `www` or `blog`.

2. **Zones and Records:**
   - **Zones:** DNS is divided into zones, each managed by different organizations.
   - **Records:** DNS records are entries that map domain names to IP addresses or other data. Common types of DNS records include:
     - **A Record:** Maps a domain name to an IPv4 address.
     - **AAAA Record:** Maps a domain name to an IPv6 address.
     - **CNAME Record:** Maps one domain name to another (canonical name).
     - **MX Record:** Specifies mail servers for a domain.

### **DNS Levels**

DNS levels refer to the hierarchical nature of the domain name system. Each part of a domain name corresponds to a different level:

1. **Root Level (.):** The highest level in the DNS hierarchy.
2. **Top-Level Domain (TLD):** The second level in the DNS hierarchy (e.g., `.com`, `.org`).
3. **Second-Level Domain:** Directly below the TLD (e.g., `example` in `example.com`).
4. **Subdomain:** Any domain that is a part of a larger domain (e.g., `www` in `www.example.com`).

### **Summary**

- **IP Address:** A unique identifier for devices on a network. There are various types, including IPv4, IPv6, public, private, static, and dynamic IP addresses.
- **DNS:** The system that translates domain names into IP addresses, enabling browsers to locate and access websites.
- **DNS Resolution:** Involves a series of queries to resolve a domain name into an IP address, passing through local caches, DNS resolvers, root servers, TLD servers, and authoritative servers.
- **DNS Providers:** Organizations like Google, Cloudflare, and OpenDNS offer DNS services.
- **DNS Levels:** Refers to the hierarchical structure of domain names, starting from the root level and going down to TLDs, second-level domains, and subdomains.
