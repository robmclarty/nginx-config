# Nginx Config

This is just a sample nginx config making using of SSL and reverse proxy to an
app server for reference.

The idea is to have one of app-specific config file, with a singular `server`
block, per website/app which is being controlled by nginx. These settings are
different from the "global" settings found in the main `nginx.conf` file and
should be tailored to the needs of your website/app.

I am loading a Node.js app behind a reverse proxy using nginx's `upstream`
syntax to point to the Node.js server. This makes it much easier to let nginx
handle terminating TLS connections and then (behind nginx) using a plain http
connection to the Node.js server (this connection is internal, so it should be
secured by the host's network security). The Node.js server will have no outside
public-facing ports opened so that the only way of connecting to it will be
*through* nginx.

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
