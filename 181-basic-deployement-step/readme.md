# Node.Js Deployment Steps for EC2

Deploying a Node.js application on an EC2 instance involves several steps, including setting up the EC2 instance, configuring the environment, installing necessary dependencies, uploading the application, and ensuring that the app runs smoothly. Here’s a detailed step-by-step guide:

### **1. Set Up an EC2 Instance**

1. **Login to AWS Console**  
   Log in to your AWS Management Console.

2. **Launch a New EC2 Instance**

   - Go to **EC2** under the **Services** menu.
   - Click on **Launch Instance**.
   - Choose an Amazon Machine Image (AMI). For a Node.js application, a good option is an **Ubuntu** AMI (e.g., Ubuntu 20.04 LTS).
   - Select an instance type based on your requirements. A small instance like `t2.micro` is fine for low-traffic applications (and eligible for the free tier).
   - Configure the instance details and set up a key pair (you’ll use this key pair to SSH into your instance later).
   - Configure the security group to allow traffic on the necessary ports:
     - **SSH (port 22)** for accessing the EC2 instance.
     - **HTTP (port 80)** if you want the app to be accessible over the web.
     - **HTTPS (port 443)** if you plan to use SSL.

3. **Launch the Instance**  
   Once configured, click **Launch**. It will take a few minutes for the instance to be created.

### **2. Connect to Your EC2 Instance**

1. **Find Your Public IP**
   - In the **Instances** section of the EC2 Dashboard, find your instance and copy the **Public IP** address.
2. **SSH into the EC2 Instance**  
   From your terminal, use SSH to connect:
   ```bash
   ssh -i /path/to/your-key.pem ubuntu@your-ec2-public-ip
   ```
   (Make sure to replace `/path/to/your-key.pem` with the path to your private key file and `your-ec2-public-ip` with your EC2 instance's IP address.)

### **3. Install Dependencies**

1. **Update the Package Repository**  
   Once logged into your EC2 instance, run the following commands to update the package repository and install dependencies:

   ```bash
   sudo apt update
   sudo apt upgrade -y
   ```

2. **Install Node.js and npm**  
   Install the latest version of Node.js and npm (Node Package Manager):

   ```bash
   sudo apt install nodejs -y
   sudo apt install npm -y
   ```

   Verify the installation:

   ```bash
   node -v
   npm -v
   ```

3. **Install Git (if necessary)**  
   If you're using Git to clone your repository, you can install it with:
   ```bash
   sudo apt install git -y
   ```

### **4. Upload Your Node.js Application**

There are multiple ways to upload your application to the EC2 instance:

#### **Option 1: Using Git**

1. **Clone Your Application Repository**  
   If your Node.js app is hosted on a version control platform like GitHub, you can clone it directly:
   ```bash
   git clone https://github.com/username/repository-name.git
   cd repository-name
   ```

#### **Option 2: Using SCP (Secure Copy)**

1. **Copy Files from Local to EC2**  
   If you have your Node.js application locally, you can use `scp` to upload files:

   ```bash
   scp -i /path/to/your-key.pem -r /local/app/path ubuntu@your-ec2-public-ip:/home/ubuntu/app
   ```

   Replace `/local/app/path` with the local directory of your Node.js application.

### **5. Install Application Dependencies**

Once the app is on your EC2 instance, navigate to the project directory and install the necessary dependencies:

```bash
cd /path/to/your/app
npm install
```

### **6. Configure Your Application**

1. **Configure Environment Variables**  
   If your Node.js app uses environment variables (e.g., for database connections), you can either:

   - Create a `.env` file.
   - Set environment variables directly in the terminal:
     ```bash
     export DB_HOST=your-db-host
     export DB_USER=your-db-user
     ```

2. **Set up a Process Manager (Optional)**  
   For keeping your app running continuously, you can use a process manager like **PM2**:

   ```bash
   sudo npm install pm2@latest -g
   pm2 start app.js
   pm2 startup
   pm2 save
   ```

   This ensures your application starts automatically when the server reboots.

### **7. Set Up a Web Server (Optional but Recommended)**

It’s a good idea to use a web server (like Nginx) as a reverse proxy in front of your Node.js application to handle HTTP requests more efficiently.

1. **Install Nginx**  
   On your EC2 instance, install Nginx:

   ```bash
   sudo apt install nginx -y
   ```

2. **Configure Nginx as a Reverse Proxy**  
   Create or modify an Nginx configuration file to forward traffic to your Node.js application. Example configuration in `/etc/nginx/sites-available/default`:

   ```nginx
   server {
       listen 80;
       server_name your-domain.com;

       location / {
           proxy_pass http://localhost:3000;  # Port your Node.js app is running on
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
           proxy_cache_bypass $http_upgrade;
       }
   }
   ```

3. **Restart Nginx**  
   Restart Nginx to apply the changes:
   ```bash
   sudo systemctl restart nginx
   ```

### **8. Open Ports in Security Group**

Ensure the security group attached to your EC2 instance allows traffic on port 80 (HTTP) and 443 (HTTPS). You can do this by modifying the security group settings in the AWS Console.

### **9. Access Your Application**

Once your Node.js app is running and Nginx is configured, you can access it by navigating to your EC2 instance’s public IP address or domain name in a browser.

```bash
http://your-ec2-public-ip
```

If you configured a domain, use `http://your-domain.com`.

### **10. (Optional) Set Up HTTPS**

For secure traffic (HTTPS), you can set up SSL certificates. Use **Let's Encrypt** for a free SSL certificate:

1. **Install Certbot**:

   ```bash
   sudo apt install certbot python3-certbot-nginx
   ```

2. **Obtain SSL Certificate**:

   ```bash
   sudo certbot --nginx
   ```

   Follow the prompts to configure HTTPS for your domain.

### **11. Monitor and Maintain Your App**

1. **Monitor the Application**

   - You can use tools like **PM2** or **monit** for monitoring Node.js apps.
   - Set up log files and consider using a logging service.

2. **Regular Updates**

   - Keep your server and application updated with security patches.

3. **Backups**
   - Set up regular backups of your EC2 instance or databases.

---

### Summary of the Process:

1. **Set up an EC2 instance.**
2. **SSH into the EC2 instance.**
3. **Install Node.js and necessary dependencies.**
4. **Upload your Node.js application (via Git or SCP).**
5. **Install npm dependencies (`npm install`).**
6. **Configure environment variables.**
7. **Use PM2 for process management.**
8. **Set up Nginx as a reverse proxy (optional).**
9. **Allow necessary ports (80/443) in the security group.**
10. **Access the app through a browser.**
11. **Optionally set up SSL/HTTPS.**

By following these steps, you should have a Node.js application running on an EC2 instance.
