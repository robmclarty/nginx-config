# Nginx Config

This is a sample nginx config which demonstrates a number of useful settings for
using it as both a static file server and reverse proxy (and load balancer) to
1 or more server applications. I've put this here mostly for my own reference,
but that doesn't mean it can't be a good reference for you too :)

The idea is to have one `app-specific.conf` file, with a singular `server`
block, per website/app which is being controlled by nginx. These settings are
different from the global settings found in the main `nginx.conf` file and
should be tailored to the needs of your website/app.

NOTE: what I mean by "app specific config" is a config file that would live in
`/etc/nginx/sites-available` which you would link to from
`/etc/nginx/sites-enabled`. The main `nginx.conf` will automatically load
anything that's in `sites-enabled` ;)

I find that using nginx in front of my (in my case, Nodejs) applications is a
really great (read: feature-rich, performant, and easy-to-setup) solution for
handling low to decently-sized loads that helps me hit the ground running. When
I have later proven my app to be successful, and as it develops resource
requirements  which can no longer be handled by simple vertical scaling
techniques, I can then implement a more sophisticated, automated, horizontal
scaling solution (e.g., a la kubernetes/docker variety). But when I'm just
starting a new project, proving an MVP, or deploying something that isn't
intended for mass bandwidth, using nginx as my server's frontend is just about
right.

Nginx can handle terminating TLS connections and then (behind nginx) use a plain
http connection to the application (this connection is internal, so it should be
secured by the host's network security). The application itself will have no
outside public-facing ports opened so that the only way of connecting to it will
be *through* nginx.

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

That said, Ubuntu 16 comes with nginx 1.10 which is compatible with the configs
I'm showing here.

## Mozilla SSL Configuration Generator

Mozilla has a great online [SSL Config Generator](https://mozilla.github.io/server-side-tls/ssl-config-generator/)
that you can use to get some solid suggestions for your setup (not just nginx).
