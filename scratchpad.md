``` shell
return 200 "NGINX has routed this request to the default site.\n
http_x_realip:\t $http_x_real_ip\n
http_x_forwarded_for:\t $http_x_forwarded_for\n
geoip_country_code:\t $geoip_country_code\n";
```

https://www.viget.com/articles/split-test-traffic-distribution-with-nginx/

https://openresty.org/download/agentzh-nginx-tutorials-en.html
