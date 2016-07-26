### SSL Settings
As of July 2016, we employ a variety of SSL settings to harden our Apache webserver configuration.
- OCSP stapling
- Disabling old SSL Protocols
- Specifying Cipher order
- Turning off SSL compression
- Allowing only modern ciphers
- Enabling HSTS
As of July 2016, this gives the server an A+ rating on ssllabs.com. See ssl vhost in /etc/apache for information on how these settings are enabled.
