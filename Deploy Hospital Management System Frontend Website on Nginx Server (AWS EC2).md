# Deploy "Hospital Management System" Frontend Website on Nginx Server (AWS EC2)

## Prerequisites

1. **AWS Account:** Ensure you have an active AWS account.
2. **Frontend Application Files:** Prepare your "Hospital Management System" frontend website files (`index.html`, `style.css`, etc.).
3. **AWS CLI (Optional):** Install the AWS Command Line Interface for convenience.

---

## Step 1: Launch an EC2 Instance

1. **Log in to the AWS Management Console:**  
   Navigate to the **EC2 Dashboard**.

2. **Launch an Instance:**  
   - Click on **Launch Instance**.  
   - **Choose an AMI:** Select an Amazon Machine Image (AMI), such as **Amazon Linux 2** or **Ubuntu Server**.  
   - **Instance Type:** Select **t2.micro** (free tier eligible).  
   - **Configure Security Group:** Allow the following inbound rules:  
     - **HTTP (Port 80):** Open to `0.0.0.0/0`.  
     - **SSH (Port 22):** Restrict to your IP or open to `0.0.0.0/0` (not recommended for production).  
   - **Key Pair:** Create or select an existing key pair for SSH access.  
   - **Launch the Instance.**

---

## Step 2: Connect to Your EC2 Instance

1. **SSH into the Instance:**  
   Use the `.pem` key file to connect:  
   ```bash
   ssh -i "your-key-file.pem" ec2-user@<INSTANCE_PUBLIC_IP>
   ```

2. **Update the Package Manager:**  
   Run the following commands to update the system:  
   ```bash
   sudo yum update -y   # For Amazon Linux
   sudo apt update -y   # For Ubuntu
   ```

---

## Step 3: Install Nginx Web Server

1. **Install Nginx:**  
   ```bash
   sudo yum install nginx -y   # For Amazon Linux
   sudo apt install nginx -y   # For Ubuntu
   ```

2. **Start and Enable Nginx:**  
   ```bash
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```

3. **Verify Nginx Installation:**  
   Access the EC2 instance's public IP in your browser:  
   ```
   http://<INSTANCE_PUBLIC_IP>
   ```  
   You should see the default Nginx welcome page.

---

## Step 4: Deploy "Hospital Management System" Frontend

1. **Transfer Website Files to EC2 Instance:**  
   Use the `scp` command to upload your website files:  
   ```bash
   scp -i "your-key-file.pem" path/to/your/files/* ec2-user@<INSTANCE_PUBLIC_IP>:/tmp
   ```

2. **Move Files to the Web Directory:**  
   ```bash
   sudo mv /tmp/* /usr/share/nginx/html/
   ```

3. **Verify Deployment:**  
   Open the public IP in a browser to check if the "Hospital Management System" frontend is displayed:  
   ```
   http://<INSTANCE_PUBLIC_IP>
   ```

---

## Step 5: Secure and Clean Up

1. **Remove Unused Files:**  
   Delete unnecessary files from `/usr/share/nginx/html` to keep the server clean.

2. **Enhance Security:**  
   - Restrict SSH access to specific IPs in the security group.  
   - Regularly update and patch the system.

---

## Testing

1. Open a browser and navigate to the public IP of your EC2 instance.
2. Confirm that the "Hospital Management System" frontend website is displayed as expected.

---

Save this file as `deploy_hms_nginx.md` to document the deployment process for Nginx.
