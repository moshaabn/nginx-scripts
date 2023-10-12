## nextjs for nginx configurations

#### first install following package for routing
```
npm i next-nginx-routes
```
or
```
yarn add next-nginx-routes
```

#### second add this script to scripts in package.json file
"deploy": "next build && next export && next-nginx-routes"
####  next export may be deprecated
"deploy": "next build && next-nginx-routes"
#### git clone repo
```
npm i --legacy-peer-deps
```
```
npm run deploy
```

#### now go to /etc/nginx/sites-available
#### create file domain.com and add the following
```
server {
        server_name domain.com www.domain.com;
        root /var/www/site_location/out;

        index index.html;

        location / {
                try_files $uri $uri.html $uri/ =404;
        }

        error_page 404 /404.html;
        location = /404.html {
                internal;
        }
    include /var/www/site_location/next-routes.conf;
    listen 80;
}
````

#### not link them to sites enabled
ln -s /etc/nginx/sites-awailable/domain.com /etc/nginx/sites-awailable
#### ensure that everything ok
nginx -t
#### now restart nginx
systemctl restart nginx

Go to your domain it should be all set good
