# Nginx Config

This is just a sample nginx config making using of SSL and reverse proxy to an
app server for reference.

## Upgrading nginx on Ubuntu

The default nginx version on Ubuntu 14 is a bit old (e.g., 1.4), but it's easy
to upgrade to the latest version using nginx's own stable repo:

```
sudo add-apt-repository ppa:nginx/stable
sudo apt-get update
sudo apt-get upgrade
sudo apt-get upgrade nginx
sudo service nginx restart
```

## Mozilla SSL Configuration Generator

Mozilla has a great online [SSL Config Generator](https://mozilla.github.io/server-side-tls/ssl-config-generator/)
that you can use to get some solid suggestions for your setup (not just nginx).
