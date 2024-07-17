# Authentication and Authorization

**Authentication** and **Authorization** are fundamental concepts in security, especially for web applications and services. They are often used together but serve different purposes.

## Authentication

**Authentication** is the process of verifying the identity of a user or system. It ensures that users are who they claim to be. This process often involves:

- **Username and Password:** The most common form of authentication where users provide a username and password.
- **Two-Factor Authentication (2FA):** An additional layer of security requiring a second form of verification, such as a code sent to a mobile device.
- **Biometrics:** Using physical characteristics (like fingerprints or facial recognition) to verify identity.
- **OAuth Tokens:** Tokens issued by an identity provider (like Google or Facebook) to authenticate a user.

**Example:** When you log into a website with your username and password, the site verifies your credentials to confirm your identity.

## Authorization

**Authorization** is the process of determining what an authenticated user or system is allowed to do. Once a user’s identity is confirmed, authorization controls their access to resources and actions based on their roles and permissions.

- **Role-Based Access Control (RBAC):** Grants permissions based on the user’s role in an organization.
- **Attribute-Based Access Control (ABAC):** Grants permissions based on attributes of users, resources, and the environment.
- **Discretionary Access Control (DAC):** Grants permissions based on user ownership and discretion.

**Example:** After logging in, you might have access to certain parts of a website based on your role (e.g., admin, editor, viewer).

### Role-Based Access Control (RBAC)

**RBAC** is a widely used method for managing authorization. It assigns permissions based on roles, which are associated with users. This model simplifies permission management by grouping users into roles and then assigning permissions to those roles.

#### Key Concepts:

- **Roles:** Define a set of permissions. For example, roles might include `Admin`, `Editor`, and `Viewer`.
- **Permissions:** Define what actions can be performed. For example, `read`, `write`, `delete`.
- **Users:** Assigned to one or more roles. Users inherit the permissions associated with their roles.

**Example of RBAC Implementation:**

1. **Define Roles:**

   - `Admin`: Full access to all resources.
   - `Editor`: Can create and edit content but not delete.
   - `Viewer`: Can only view content.

2. **Assign Permissions to Roles:**

   - `Admin`: `read`, `write`, `delete`
   - `Editor`: `read`, `write`
   - `Viewer`: `read`

3. **Assign Users to Roles:**

   - User `John` is assigned the `Admin` role.
   - User `Jane` is assigned the `Editor` role.

4. **Access Control:**
   - When User `John` accesses a resource, they can perform any action (read, write, delete).
   - When User `Jane` accesses a resource, they can only read and write.

### Different Ways to Perform Authorization

1. **Role-Based Access Control (RBAC):**

   - Assign roles to users and permissions to roles.
   - Simple and effective for many applications.
   - Example: Admin, Editor, Viewer roles with defined permissions.

2. **Attribute-Based Access Control (ABAC):**

   - Makes access decisions based on attributes (user attributes, resource attributes, environment conditions).
   - More flexible and fine-grained compared to RBAC.
   - Example: Access based on the department (HR, Finance) or time of day.

3. **Discretionary Access Control (DAC):**

   - Users have control over their resources and can grant access to other users.
   - Common in file systems (e.g., NTFS permissions).
   - Example: File owners can set permissions for other users.

4. **Mandatory Access Control (MAC):**

   - Access is based on security labels assigned to resources and users.
   - Often used in high-security environments.
   - Example: Government or military systems where access is based on security clearance levels.

5. **Context-Based Access Control:**

   - Decisions are based on contextual information like location, time, device used, etc.
   - Example: Allow access only if the request comes from within the corporate network.

6. **Policy-Based Access Control:**
   - Uses policies to define access rules.
   - Policies are often written in a declarative language and can be more dynamic.
   - Example: Access granted based on a policy that includes user role, time of day, and IP address.

### Summary

- **Authentication** is about verifying who you are.
- **Authorization** is about determining what you are allowed to do.
- **RBAC** is a method of authorization that assigns permissions based on roles.
- Other methods of authorization include ABAC, DAC, MAC, context-based, and policy-based control.
- Each method has its use cases, advantages, and trade-offs depending on the application's requirements and complexity.
