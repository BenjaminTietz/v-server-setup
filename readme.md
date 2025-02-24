# V-Server Setup

## Short Description

This repository contains step-by-step instructions for setting up a virtual Ubuntu server, including SSH configuration, web server installation, and Git setup.

## Table of Contents

- [1. Prerequisites](#prerequisites)
- [2. Quickstart](#quickstart)
- [3. Usage](#usage)
- [4. Setting Up the V-Server](docs/setup.md)
- [5. Git Configuration](docs/git.md)
- [6. Testing and Validation](docs/testing.md)
- [7. Additional Resources](#additional-resources)

## Prerequisites

Before setting up this project, ensure you have the following:

- A virtual Ubuntu server (tested on Ubuntu 20.04 and 22.04)
- A user with `sudo` privileges
- SSH access to the server
- A registered GitHub account (for Git integration)
- Basic knowledge of Linux command-line usage

## Quickstart

Follow these steps to quickly set up the V-Server:

1. **Clone the repository:**
   ```sh
   git clone https://github.com/BenjaminTietz/v-server-setup.git
   cd v-server-setup
   ```
2. **Generate an SSH key (if not already created) and copy it to the server:**
   ```sh
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ssh-copy-id user@your-server-ip
   ```
3. **Verify SSH key-based authentication:**
   ```sh
   ssh user@your-server-ip
   ```
4. **Disable password authentication:**
   ```sh
   sudo nano /etc/ssh/sshd_config
   ```
   Change `PasswordAuthentication yes` to `PasswordAuthentication no`, then restart SSH:
   ```sh
   sudo systemctl restart ssh
   ```
5. **Update packages and install NGINX:**
   ```sh
   sudo apt update && sudo apt install nginx -y
   ```
6. **Start NGINX and check status:**
   ```sh
   sudo systemctl enable --now nginx
   sudo systemctl status nginx
   ```
7. **Configure Git:**
   ```sh
   git config --global user.name "Your Name"
   git config --global user.email "your_email@example.com"
   ```
8. **Generate and add SSH key to GitHub:**
   ```sh
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   cat ~/.ssh/id_rsa.pub
   ```
9. **Restart NGINX after configuration changes:**
   ```sh
   sudo systemctl restart nginx
   ```
10. **Validate setup:**
    ```sh
    sudo nginx -t
    ```
    Open `http://your-server-ip` in a browser to check the web server.

## Usage

### Configuration Options

Once the server is set up, you can customize it with:

- **NGINX Custom Configuration**

  - Modify `/etc/nginx/sites-enabled/default` or create a new config under `/etc/nginx/sites-enabled/`.
  - Example custom configuration file:

    ```nginx
    server {
        listen 8081;
        listen [::]:8081;

        root /var/www/alternatives;
        index alternate-index.html;

        location / {
            try_files $uri $uri/ =404;
        }
    }
    ```

  - Apply changes:
    ```sh
    sudo systemctl restart nginx
    ```

- **Git SSH Key Authentication**
  - Ensure SSH authentication is working:
    ```sh
    ssh -T git@github.com
    ```
- **Adding New Services**

  - Install additional packages:

    ```sh
    sudo apt install <package-name>
    ```

    - Recommended package:
    - `certbot` for SSL certificate management with Let's Encrypt

## Additional Resources

- 📄 [V-Server Setup Checklist (PDF)](docs/v-server-checklist.pdf)
- [NGINX Documentation](https://nginx.org/en/docs/)
- [GitHub SSH Key Setup Guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)

  ## Contact

### 👤 Personal

- [Portfolio](https://benjamin-tietz.com/)
- [Drop me a mail](mailto:mail@benjamin-tietz.com)

### 🌍 Social

- [LinkedIn](https://www.linkedin.com/in/benjamin-tietz/)

### 💻 Project Repository

- [GitHub Repository](https://github.com/BenjaminTietz/v-server-setup)
