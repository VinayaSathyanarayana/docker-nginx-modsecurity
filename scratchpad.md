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

