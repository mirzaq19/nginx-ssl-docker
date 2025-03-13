# How to setup

1. Clone this repository
2. Copy file `config.init.txt` and rename with your domain name with suffix .conf, eg: `web.conf`
3. Replace `[domain_name]` and `[host]` inside `web.conf` file with your own domain name and host server
4. Running file docker-compose.yml with this command
   
   ```bash
   docker compose up -d
   ```
   
5. Enter to certbot container to create new certificate with this command

   ```bash
   docker container exec -it cerbbot sh
   ```

6. Check that your domain can accessed
7. Create new ssl certificate with this command, replace `[domain_name]` with your own domain name

   ```bash
   certbot certonly --webroot --webroot-path /var/www/certbot -d [domain_name]
   ```

7. If success to create new certificate try to simulate renew certificate

   ```bash
   certbot renew --webroot -w /var/www/certbot --dry-run
   ```

8. Exit from the certbot container, copy content `config.ssl.txt` file to your nginx configuration and fit with your own config before. Note: this is for set the https
9. Restart nginx container with this command to load ssl certificate

   ```bash
   docker compose restart nginx
   ```

10. Done, your domain can accessed with https 🚀👍!!!
