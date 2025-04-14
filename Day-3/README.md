# Day 3 – Introduction to AWS IAM & Basics of Docker

---

## AWS IAM (Identity and Access Management)

We learned how to create and manage users using IAM in AWS for secure access.

### Steps to Create an IAM User

1. Go to IAM in the AWS Console.
2. Navigate to **Access Management > Users**.
3. Click **Create User**.
4. Provide a **User Name**.
5. Enable AWS Console access.
6. Require password reset on first login.
7. Attach the policy: **AdministratorAccess**.
8. Click **Create User**.
9. Save the **Sign-in link**, **Username**, and **Password**.

---

## AWS EC2 – Launching a Linux Instance

### Steps to Launch EC2 Instance

1. Go to EC2 in AWS Console.
2. Click **Launch Instance**.
3. Choose **Amazon Linux AMI**.
4. Select instance type (e.g., `t2.micro` – Free Tier).
5. Configure settings and add default storage.
6. Configure **Security Group** to allow:
   - **SSH (Port 22)**
   - **HTTP (Port 80)** if deploying web app.
7. Create and download **Key Pair** (.pem or .ppk).
8. Launch the instance.

### Connecting to EC2 using PuTTY

1. Install **PuTTY** and **PuTTYgen**.
2. Convert `.pem` to `.ppk` using PuTTYgen.
3. Open **PuTTY**.
4. Host Name: `ec2-user@<Public-IP>`.
5. Go to **SSH > Auth** and browse the `.ppk` file.
6. Click **Open** and connect.

---

## Docker Installation on EC2 (Amazon Linux)

```bash
sudo yum update -y
sudo yum install -y docker
sudo systemctl start docker
sudo systemctl enable docker
docker --version
```

---

## Creation of a Docker Container in AWS and Deploy a Static Application

1. **Create a New Instance and Launch It.**

2. **Update and Install Docker:**

    ```bash
    sudo yum update -y
    sudo yum install docker -y
    ```

    Check Docker version:

    ```bash
    docker --version
    ```

3. **Install Git and Clone the Static Website:**

    ```bash

    sudo yum install git -y
    git clone https://github.com/Apeksha-L-Naik/Skill_lab_portfolio.git
    cd portfolio
    ```

4. **Create a Dockerfile:**

    ```dockerfile

    FROM nginx:alpine

    COPY . /usr/share/nginx/html

    EXPOSE 80

    EOF
    ```

5. **Build the Docker Image:**

    ```bash
    docker build -t static-app .
    ```

6. **Run the Docker Container:**

    ```bash
    docker run -d -p 80:80 static-app
    ```

    If port 80 (HTTP) is not allowed in your EC2 instance's Security Group:

    1. Go to the EC2 Dashboard → Click “Instances”.
    2. Select your instance → Scroll to Security → Click on the Security Group name.
    3. Go to the Inbound Rules tab → Click Edit Inbound Rules.
    4. Click “Add Rule”:
        - Type: HTTP
        - Protocol: TCP
        - Port Range: 80
        - Source: Anywhere (0.0.0.0/0) or your preferred IP
    5. Click Save rules.

7. **Access the App:**
    Open a browser and visit:

    ```bash
    http://<your-ec2-public-ip>
    ```
