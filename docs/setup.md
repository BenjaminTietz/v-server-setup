## 1. Setting Up the V-Server

### SSH Configuration

1. Generate an SSH key pair on your local machine (if not already created):
   ```sh
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```
2. Copy your public key to the server:
   ```sh
   ssh-copy-id user@your-server-ip
   ```
3. Verify SSH key-based authentication works before disabling password login:
   ```sh
   ssh user@your-server-ip
   ```
4. Disable password authentication by editing `/etc/ssh/sshd_config`:
   ```sh
   sudo nano /etc/ssh/sshd_config
   ```
   Change or add the following line:
   ```
   PasswordAuthentication no
   ```
5. Restart SSH service:
   ```sh
   sudo systemctl restart ssh
   ```

### Install and Configure NGINX

1. Update packages:
   ```sh
   sudo apt update
   ```
2. Install NGINX:
   ```sh
   sudo apt install nginx -y
   ```
3. Check NGINX status:
   ```sh
   systemctl status nginx
   ```
4. Modify default HTML file:
   ```sh
   sudo nano /var/www/html/index.html
   ```
   Add your custom content, then save and exit.
5. Restart NGINX to apply changes:
   ```sh
   sudo systemctl restart nginx
   ```
6. Validate configuration:
   ```sh
   sudo nginx -t
   ```

### Alternative NGINX Configuration

1. Create a new directory for an alternative entry point:
   ```sh
   sudo mkdir /var/www/alternatives
   ```
2. Create a new HTML file:
   ```sh
   sudo touch /var/www/alternatives/alternate-index.html
   ```
3. Modify NGINX configuration:

   ```sh
   sudo nano /etc/nginx/sites-enabled/alternatives
   ```

   Add the following content:

   ```nginx
   server {
       listen 8081;  # The server listens for incoming connections on port 8081.
       listen [::]:8081;  # Enables IPv6 support on the same port.

       root /var/www/alternatives;  # Sets the root directory for this server block.
       index alternate-index.html;  # Defines the default file to serve.

       location / {
           try_files $uri $uri/ =404;  # Tries to serve the requested file, otherwise returns a 404 error.
       }
   }
   ```

4. Restart NGINX:
   ```sh
   sudo systemctl restart nginx
   ```
