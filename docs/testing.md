## 3. Testing and Validation

### SSH Access

- Ensure you can log in with SSH keys only:
  ```sh
  ssh user@your-server-ip
  ```
- Verify password authentication is disabled:
  ```sh
  ssh -o PubKeyAuthentication=no -i ~/.ssh/id_rsa user@your-server-ip
  ```
  This should fail.

#### NGINX Validation

- Check if your server is reachable via browser.
- Validate configuration:
  ```sh
  sudo nginx -t
  ```
- Restart NGINX if necessary:
  ```sh
  sudo systemctl restart nginx
  ```
