# EC2 - User Data Demonstration

When you launch an Amazon EC2 instance, you can pass "user data" to the instance that is used to perform automated configuration tasks, or to run scripts after the instance starts.

This simple User Data script can be used with an Amazon Linux 2023 instance to configure the Apache web server listening on port 80 (http://) and 443 (https://) - using a self signed certificate.

A simple static web page is displayed.

## User Data 

```
#!/bin/bash

# Update system packages
dnf update -y

# Install Apache web server and SSL module
dnf install -y httpd mod_ssl

# Create a simple "Hello, World!" HTML page
cat > /var/www/html/index.html << 'EOF'
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello World</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
        }
        .container {
            text-align: center;
            background-color: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Hello, World!</h1>
        <p>Your Apache web server is running successfully!</p>
        <p>Server: Amazon Linux 2023</p>
    </div>
</body>
</html>
EOF

# Set proper permissions
chown apache:apache /var/www/html/index.html
chmod 644 /var/www/html/index.html

# Create a self-signed SSL certificate for HTTPS
mkdir -p /etc/ssl/private
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/apache-selfsigned.key \
    -out /etc/ssl/certs/apache-selfsigned.crt \
    -subj "/C=US/ST=State/L=City/O=Organization/CN=localhost"

# Configure Apache SSL
cat > /etc/httpd/conf.d/ssl-custom.conf << 'EOF'
<VirtualHost *:443>
    DocumentRoot /var/www/html
    ServerName localhost

    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/apache-selfsigned.crt
    SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key

    <Directory "/var/www/html">
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
EOF

# Start and enable Apache
systemctl start httpd
systemctl enable httpd
```