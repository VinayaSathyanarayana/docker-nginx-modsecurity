``` shell
return 200 "NGINX has routed this request to the default site.\n
http_x_realip:\t $http_x_real_ip\n
http_x_forwarded_for:\t $http_x_forwarded_for\n
geoip_country_code:\t $geoip_country_code\n";
```

https://www.viget.com/articles/split-test-traffic-distribution-with-nginx/

https://openresty.org/download/agentzh-nginx-tutorials-en.html

https://hub.docker.com/r/wernight/alpine-nginx-pagespeed/~/dockerfile/

https://www.modpagespeed.com/doc/build_ngx_pagespeed_from_source


https://www.cyberciti.biz/tips/linux-unix-bsd-nginx-webserver-security.html

 ## Start: Size Limits & Buffer Overflows ##
  client_body_buffer_size  1K;
  client_header_buffer_size 1k;
  client_max_body_size 1k;
  large_client_header_buffers 2 1k;
 ## END: Size Limits & Buffer Overflows ##
 
 ## Start: Timeouts ##
  client_body_timeout   10;
  client_header_timeout 10;
  keepalive_timeout     5 5;
  send_timeout          10;
## End: Timeouts ##

https://www.cyberciti.biz/faq/nginx-enable-and-see-current-status-page/

2020-Apr-12
https://www.nginx.com/blog/compiling-and-installing-modsecurity-for-open-source-nginx/
https://www.nginx.com/blog/modsecurity-and-project-honeypot/
https://www.nginx.com/blog/modsecurity-logging-and-debugging/
Alpine Installation:
https://nginx.org/en/linux_packages.html?_ga=2.181998631.1251754332.1586653422-1698467903.1586653422#Alpine


Dockerfile 2020Apr
Alpine Install
Install the prerequisites:

sudo apk add openssl curl ca-certificates
To set up the apk repository for stable nginx packages, run the following command:

printf "%s%s%s\n" \
    "http://nginx.org/packages/alpine/v" \
    `egrep -o '^[0-9]+\.[0-9]+' /etc/alpine-release` \
    "/main" \
    | sudo tee -a /etc/apk/repositories
If you would like to use mainline nginx packages, run the following command instead:

printf "%s%s%s\n" \
    "http://nginx.org/packages/mainline/alpine/v" \
    `egrep -o '^[0-9]+\.[0-9]+' /etc/alpine-release` \
    "/main" \
    | sudo tee -a /etc/apk/repositories
Next, import an official nginx signing key so apk could verify the packages authenticity. Fetch the key:

curl -o /tmp/nginx_signing.rsa.pub https://nginx.org/keys/nginx_signing.rsa.pub
Verify that downloaded file contains the proper key:

openssl rsa -pubin -in /tmp/nginx_signing.rsa.pub -text -noout
The output should contain the following modulus:

Public-Key: (2048 bit)
Modulus:
    00:fe:14:f6:0a:1a:b8:86:19:fe:cd:ab:02:9f:58:
    2f:37:70:15:74:d6:06:9b:81:55:90:99:96:cc:70:
    5c:de:5b:e8:4c:b2:0c:47:5b:a8:a2:98:3d:11:b1:
    f6:7d:a0:46:df:24:23:c6:d0:24:52:67:ba:69:ab:
    9a:4a:6a:66:2c:db:e1:09:f1:0d:b2:b0:e1:47:1f:
    0a:46:ac:0d:82:f3:3c:8d:02:ce:08:43:19:d9:64:
    86:c4:4e:07:12:c0:5b:43:ba:7d:17:8a:a3:f0:3d:
    98:32:b9:75:66:f4:f0:1b:2d:94:5b:7c:1c:e6:f3:
    04:7f:dd:25:b2:82:a6:41:04:b7:50:93:94:c4:7c:
    34:7e:12:7c:bf:33:54:55:47:8c:42:94:40:8e:34:
    5f:54:04:1d:9e:8c:57:48:d4:b0:f8:e4:03:db:3f:
    68:6c:37:fa:62:14:1c:94:d6:de:f2:2b:68:29:17:
    24:6d:f7:b5:b3:18:79:fd:31:5e:7f:4c:be:c0:99:
    13:cc:e2:97:2b:dc:96:9c:9a:d0:a7:c5:77:82:67:
    c9:cb:a9:e7:68:4a:e1:c5:ba:1c:32:0e:79:40:6e:
    ef:08:d7:a3:b9:5d:1a:df:ce:1a:c7:44:91:4c:d4:
    99:c8:88:69:b3:66:2e:b3:06:f1:f4:22:d7:f2:5f:
    ab:6d
Exponent: 65537 (0x10001)
Finally, move the key to apk trusted keys storage:

sudo mv /tmp/nginx_signing.rsa.pub /etc/apk/keys/
To install nginx, run the following command:

sudo apk add nginx

Source Packages
Packaging sources can be found in the packaging sources repository.

The default branch holds packaging sources for the current mainline version, while stable-* branches contain latest sources for stable releases. To build binary packages, run make in debian/ directory on Debian/Ubuntu, or in rpm/SPECS/ on RHEL/CentOS/SLES, or in apk/ on Alpine.

Packaging sources are distributed under the same 2-clause BSD-like license used by nginx.

Dynamic Modules
Main nginx package is built with all modules that do not require additional libraries to avoid extra dependencies. Since version 1.9.11, nginx supports dynamic modules and the following modules are built as dynamic and shipped as separate packages:

nginx-module-geoip
nginx-module-image-filter
nginx-module-njs
nginx-module-perl
nginx-module-xslt
Signatures
Since our PGP keys and packages are located on the same server, they are equally trusted. It is highly advised to additionally verify the authenticity of the downloaded PGP key. PGP has the “Web of Trust” concept, when a key is signed by someone else’s key, that in turn is signed by another key and so on. It often makes possible to build a chain from an arbitrary key to someone’s key who you know and trust personally, thus verify the authenticity of the first key in a chain. This concept is described in details in GPG Mini Howto. Our keys have enough signatures, and their authenticity is relatively easy to check.

----------------
https://www.nginx.com/blog/compiling-and-installing-modsecurity-for-open-source-nginx/
Step 1: Install nginx
step 2: Install Prerequisite Packages
apt-get install -y apt-utils autoconf automake build-essential git libcurl4-openssl-dev libgeoip-dev liblmdb-dev libpcre++-dev libtool libxml2-dev libyajl-dev pkgconf wget zlib1g-dev
Step 3: Download and Compile the ModSecurity 3.0 Source Code
git clone --depth 1 -b v3/master --single-branch https://github.com/SpiderLabs/ModSecurity
$ cd ModSecurity
$ git submodule init
$ git submodule update
$ ./build.sh
$ ./configure
$ make
$ make install

Step 4: 4 – Download the NGINX Connector for ModSecurity and Compile It as a Dynamic Module
git clone --depth 1 https://github.com/SpiderLabs/ModSecurity-nginx.git
Determine which version of NGINX is running on the host where the ModSecurity module will be loaded
nginx -v
Download the source code corresponding to the installed version of NGINX (the complete sources are required even though only the dynamic module is being compiled):
wget http://nginx.org/download/nginx-1.13.1.tar.gz
$ tar zxvf nginx-1.13.1.tar.gz

Compile the dynamic module and copy it to the standard directory for modules:
$ cd nginx-1.13.1
$ ./configure --with-compat --add-dynamic-module=../ModSecurity-nginx
$ make modules
$ cp objs/ngx_http_modsecurity_module.so /etc/nginx/modules

Step 5 – Load the NGINX ModSecurity Connector Dynamic Module
load_module modules/ngx_http_modsecurity_module.so;

Step 6 6 – Configure, Enable, and Test ModSecurity

Set up the appropriate ModSecurity configuration file. Here we’re using the recommended ModSecurity configuration provided by TrustWave Spiderlabs, the corporate sponsors of ModSecurity.
$ mkdir /etc/nginx/modsec
$ wget -P /etc/nginx/modsec/ https://raw.githubusercontent.com/SpiderLabs/ModSecurity/v3/master/modsecurity.conf-recommended
$ mv /etc/nginx/modsec/modsecurity.conf-recommended /etc/nginx/modsec/modsecurity.conf

Change the SecRuleEngine directive in the configuration to change from the default “detection only” mode to actively dropping malicious traffic.
sed -i 's/SecRuleEngine DetectionOnly/SecRuleEngine On/' /etc/nginx/modsec/modsecurity.conf

Configure one or more rules. For the purposes of this blog we’re creating a single simple rule that drops a request in which the URL argument called testparam includes the string test in its value. Put the following text in /etc/nginx/modsec/main.conf:

# From https://github.com/SpiderLabs/ModSecurity/blob/master/
# modsecurity.conf-recommended
#
# Edit to set SecRuleEngine On
Include "/etc/nginx/modsec/modsecurity.conf"

# Basic test rule
SecRule ARGS:testparam "@contains test" "id:1234,deny,status:403"

Add the modsecurity and modsecurity_rules_file directives to the NGINX configuration to enable ModSecurity:

server {
    # ...
    modsecurity on;
    modsecurity_rules_file /etc/nginx/modsec/main.conf;
}

Issue the following curl command. The 403 status code confirms that the rule is working.

$ curl localhost?testparam=test
<html>
<head><title>403 Forbidden</title></head>
<body bgcolor="white">
<center><h1>403 Forbidden</h1></center>
<hr><center>nginx/1.13.1</center>
</body>
</html>


