# This is to locally test your new service configuration before send to the server

## First edit /etc/hosts

> OBS: On windows it's normally under \WINDOWS\system32\drivers\etc (If there isn't one, just create it).

Then insteall the certificates

```bash
sudo pacman -S mkcert
mkcert -install
mkcert ldap.example.local#
```

Merge both certificates into one for haproxy:

```bash
cat /etc/letsencrypt/live/$1/fullchain.pem /etc/letsencrypt/live/$1/privkey.pem > /etc/haproxy/certs/$1.pem
```

Then, edit haproxy to view the ceritificates:

```
bind                        *:443 ssl crt /certs/ldap.example.local-full.pem
```
