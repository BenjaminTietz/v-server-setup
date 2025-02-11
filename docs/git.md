## 2. Git Configuration

1. Set up Git with your details:
   ```sh
   git config --global user.name "Your Name"
   git config --global user.email "your_email@example.com"
   ```
2. Generate an SSH key pair for GitHub on the server:
   ```sh
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```
3. Copy the public key and add it to GitHub under "SSH and GPG keys":
   ```sh
   cat ~/.ssh/id_rsa.pub
   ```
4. Test the connection:
   ```sh
   ssh -T git@github.com
   ```
