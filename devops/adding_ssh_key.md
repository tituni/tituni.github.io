## Adding ssh-key to gitlab

These instructions are for Ubuntu

1. Create a new private key

```cmd
ssh-keygen -t ed25519 -C "your.email@address.fi"
```

2. Add key to your ssh-agent

```cmd
 ssh-add /home/your_user/.ssh/id_ed25519
 ```

 NOTE:
 - if that didn't work you might need to start ssh-agent

 ```cmd
eval $(ssh-agent -s)
```

3. Copy the public key to gitlab

Go to the location of you keys:

```cmd
 cd /home/tiipar/.ssh
 cat id_ed25519.pub
 ```

Copy the public key (starts with ssh-ed25519) and store it in gitlab (User settings -> SSH Keys -> Add new key)
 

