## Harbor - package registry

Selfhosted Gitlab might not have a build-in package registry configured, so additional package registry needs to be installed. 

[Harbor - package registry](https://goharbor.io) can be installed in linux server following these instructions:

1. Allocate a new virtual machine from your cloud provider (ubuntu 22.04). [Minimum requirements](https://goharbor.io/docs/2.13.0/install-config/installation-prereqs/) are: 2 CPUs, 4GB memory, 40 GB disk. 
2. Allocate a public IP address and reserve a domain name for your server.
3. Configure security group to allow port 22 (ingress) from your IP address, also allow ports 80 and 443.
4. Connect to the server via SSH
5. Install Docker [instructions](https://docs.docker.com/engine/install/ubuntu/)
6. Down load installer for the version you want (this is just an example). [See avaible versions](https://github.com/goharbor/harbor/releases)

    ```cmd
    wget https://github.com/goharbor/harbor/releases/download/v2.13.2/harbor-offline-installer-v2.13.2.tgz
    ```
7. Use tar to extract the installer package:

    ```cmd
    tar xzvf  https://github.com/goharbor/harbor/releases/download/v2.13.2/harbor-offline-installer-v2.13.2.tgz
    ```
8. Configure HTTPS connection:
    - [install certbot](https://certbot.eff.org/instructions?ws=other&os=snap)
    ```cmd
    sudo snap install --classic certbot
    ```
    - obtain certificate for your server:
    ```cmd
    sudo certbot certonly --standalone
    ```
    - The certificate is saved at: /etc/letsencrypt/live/your.domain.com/fullchain.pem
    - Key is saved at: /etc/letsencrypt/live/your.domain.com/privkey.pem 
    - Rename and copy the created files:
    ```cmd
    sudo cp /etc/letsencrypt/live/your.domain.com/privkey.pem /data/cert/your.domain.key
    sudo cp /etc/letsencrypt/live/your.domain.com/fullchain.pem /data/cert/your.domain.crt
    ```
    - copy these also for docker to use (note the change in crt file name -> cert)
    ```cmd
    sudo cp /data/cert/your.domain.key /etc/docker/certs.d/yourdomain.com/
    sudo cp /data/cert/your.domain.crt /etc/docker/certs.d/yourdomain.com/your.domain.cert
    ``` 
9. Configure Harbor. Open harbor.yml - file using nano and set the followin values:
    - hostname: your.domain.com
    - certificate: /data/cert/your.domain.com.crt
    - private_key: /data/cert/your.domin.com.key
10. Run Harbor-install script
    ```cmd
    sudo bash ./harbor/install.sh
    ```
11. Start Harbor
    ```cmd
    docker compose up -d
    ```
12. Admin credentials are: user: admin, password: Harbor12345 (will be changed after initial login)

---
## If it still doesn't work...

- to reconfigure HTTPS afterwards run this:
    ```cmd
    sudo bash ./harbor/prepare
    ```
- might help to restart docker
    ```cmd
     sudo systemctl restart docker
     ```
- this is needed if configs are changed:
    ```cmd
    sudo docker compose down
    sudo docker compose up -d
    ```
