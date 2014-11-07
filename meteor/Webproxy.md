###Webproxy for meteor

##### Reffrence:
* http://nginx.org/en/docs/http/configuring_https_servers.html
* http://www.meteorpedia.com/read/nginx
* https://www.digitalocean.com/community/tutorials/how-to-deploy-a-meteor-js-application-on-ubuntu-14-04-with-nginx


##### Reffrence for mup deployment
* http://code.krister.ee/hosting-multiple-instances-of-meteor-on-digitalocean/
* https://github.com/arunoda/meteor-up#installation

##### Meteor Configuration for nginx
```
# we're in the http context here
map $http_upgrade $connection_upgrade {
default upgrade;
''      close;
}

# the Meteor / Node.js app server
server {
    server_name yourdomain.com;

    access_log /etc/nginx/logs/yourapp.access;
    error_log /etc/nginx/logs/yourapp.error error;

location / {
    proxy_pass http://localhost:3000;
    proxy_set_header X-Real-IP $remote_addr;  # http://wiki.nginx.org/HttpProxyModule
    proxy_set_header Host $host;  # pass the host header - http://wiki.nginx.org/HttpProxyModule#proxy_pass
    proxy_http_version 1.1;  # recommended with keepalive connections - http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_http_version
    # WebSocket proxying - from http://nginx.org/en/docs/http/websocket.html
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection $connection_upgrade;
}

}
```
