# NGINX with libModSecurity + ModSecurity-nginx connector
The dockerfile of this container has been copied from the [official nginx repo (alpine variant)](https://raw.githubusercontent.com/nginxinc/docker-nginx/3e8a6ee0603bf6c9cd8846c5fa43e96b13b0f44b/mainline/alpine/Dockerfile)  and has been modified to add [ModSecurity library (v3)](https://github.com/SpiderLabs/ModSecurity/tree/v3/master)  + [ModSecurity nginx connector](https://github.com/SpiderLabs/ModSecurity-nginx).

You can refer to the [official nginx image documentation](https://hub.docker.com/_/nginx/) for instructions on how to use this image.

When you provide your configuration you can enable modsecurity. Please refer to [their wiki](https://github.com/SpiderLabs/ModSecurity/wiki) for documentation.

NOTE: no rules are shipped with this container, if you enable modsecurity you need to provide your own


sudo docker build --tag="kateel:001" .


sudo docker run -p 6080:80 kateel:001

Point browser to http://ipaddr:6080/IN.html

To Test use : 

```sh
sudo curl -i http://localhost:6080/
```

https://www.webpagetest.org/

https://www.locabrowser.com/

https://www.geoscreenshot.com

https://geopeeker.com

Status
Currently blocks Countries
Hardened

ToDo

Redirection

https://amplify.nginx.com/docs/

https://docs.nginx.com/nginx-waf/
