# Lab-01: Deploying a Web Server on Cloud Infrastructure

---

# Objectives

- Sign in to the AWS Console using the sandbox environment.
- Create and configure an EC2 virtual machine.
- Connect to the EC2 instance and install Nginx.
- Deploy a sample HTML webpage.
- Verify the webpage through a web browser.

---

# Background / Theory

... (same as before)

---

# Procedure

## Step 1: Access AWS Console

- Open the AWS Academy Sandbox.
- Log in to the AWS Management Console.

---

## Step 2: Launch an EC2 Instance

- Navigate to **EC2 Dashboard**.
- Click **Launch Instance**.
- Select **Ubuntu Linux AMI**.
- Choose the **t2.micro** instance type.
- Configure the Security Group:
  - Allow SSH (Port 22)
  - Allow HTTP (Port 80)
- Launch the instance.

---

## Step 3: Connect to the EC2 Instance

```bash
ssh -i key.pem ubuntu@<public-ip>
```

---

## Step 4: Install Nginx

```bash
sudo apt update
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```

---

## Step 5: Deploy a Sample Web Page

```bash
sudo nano /var/www/html/index.html
```


# Output

```html
<!DOCTYPE html>
<html>
<head>
    <title>Cloud Web Server</title>
</head>
<body>
    <h1>Welcome to Nginx on AWS EC2</h1>
</body>
</html>
```

### Output

![alt text](Screenshot%202026-07-07%20145301.png)
**Figure 1:** Successfully hosted webpage running on the AWS EC2 instance using the Nginx web server.

---



---

![Web Page Output](Screenshot%202026-05-28%20161428.png)
**Figure 2:** 

- ✅ EC2 instance launched successfully.
- ✅ Nginx installed successfully.
- ✅ HTML webpage deployed.
- ✅ Webpage accessible through the browser.

---

# Conclusion

This laboratory exercise demonstrated the deployment of a web server on an Amazon EC2 instance using the Nginx web server. The experiment provided practical experience with launching cloud infrastructure, configuring server software, and hosting a static webpage. It also illustrated the importance of cloud computing in supporting scalable and reliable web and IoT applications.

---
