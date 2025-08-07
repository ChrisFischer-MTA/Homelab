# Homelab


Containers:
gateway: Modsec WAF container, running core rule set. Passes requests onto the proxy server*.
proxy: 
keycloak: SSO/IDP
watchtower: contains auto-update functionality

Note:
Gateway is technically a reverse proxy itself. I could include a apache.conf file that has all the options specific to modsec. However, I don't do this here because modsec changes often enough in my experience I'd rather have the container autogenerate the configuration and have a secondary container that contains my proxy hosts.

Proxy:
- Using an Entrypoint here to install the `/usr/lib/apache2/modules/mod_auth_openidc.so` which provides openidc auth for frontdooring my applications. This is very hacky and not ideal, plus requires our frontdoor to have internet which seems like a huge vulnerability.
- Added to httpd `LoadModule auth_openidc_module /usr/lib/apache2/modules/mod_auth_openidc.so`; note that you have to specify the full path here because apt for some reason puts it in /lib/ and not /local/ where everything else is.

Notes:
 - The internal and external DNS resolution must work due to the way IDC is configured.
