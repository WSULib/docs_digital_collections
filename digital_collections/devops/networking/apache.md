# Apache

Packaged installed web server. All web traffic goes through Apache. Although a fairly generic install, its complexity lies in the configuration. It makes large use of [reverse proxies](https://httpd.apache.org/docs/current/mod/mod_proxy.html) as well as custom [location directives](https://httpd.apache.org/docs/current/mod/core.html#location). Two other areas of note are custom SSL configuration settings and Loris configuration. More on those later.

## Reverse Proxy
Reverse proxying allows us to route all http traffic (which is mainly the protocol all our applications use) over Port 80. This prevents us from using or exposing strange ports over the network--ports which probably would not be accessible outside of the WSU network. Apache serves as the main valve for all traffic, so if Apache is down, nothing works.

See [here](https://github.com/WSULib/fedora-stack-prod/blob/master/install_scripts/lamp.sh#L32) for the modules installed with Apache that allows proxying to work.

Proxying follows the example:

```
ProxyPass /place  http://localhost:PORT/WHEREVER
ProxyPassReverse /place http://localhost:PORT/WHEREVER
```

## Location Directives


### Loris

### SSL Settings
As of July 2016, we employ a variety of SSL settings to harden our Apache webserver configuration.
- OCSP stapling
- Disabling old SSL Protocols
- Specifying Cipher order
- Turning off SSL compression
- Allowing only modern ciphers
- Enabling HSTS

As of July 2016, this gives the server an A+ rating on ssllabs.com. See ssl vhost in /etc/apache for information on how these settings are enabled.

:tomato:
- location Directives
- Loris
