# Homelab


Containers:
gateway: Modsec WAF container, running core rule set. Passes requests onto the proxy server*.
proxy: 


Note:
Gateway is technically a reverse proxy itself. I could include a apache.conf file that has all the options specific to modsec. However, I don't do this here because modsec changes often enough in my experience I'd rather have the container autogenerate the configuration and have a secondary container that contains my proxy hosts.
