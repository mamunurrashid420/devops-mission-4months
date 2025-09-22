### Nginx configuration 
- This is not set ssl due to this nginx file using cloudflare

-  `Frontend`
```yaml
server {
    listen 80;
    server_name example.com;
    root /var/www/html/project/dist;
    index index.html index.htm index.php;
    location / {
        try_files $uri $uri/ /index.html;
    }
    access_log /var/log/nginx/frontend.front.access.log;
    error_log /var/log/nginx/frontend.front.error.log;
}

```
-  `Backend`
```yaml
server {
    listen 80;
    server_name api.example.com;

    root /var/www/html/backend/public;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;

        # CORS headers for cross-origin requests
        proxy_hide_header Access-Control-Allow-Origin;
        add_header 'Access-Control-Allow-Origin' '*' always;
        add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS, PUT, DELETE' always;
        add_header 'Access-Control-Allow-Headers' 'Authorization, Content-Type, X-Requested-With' always;
        add_header 'Access-Control-Allow-Credentials' 'true' always;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }

    access_log /var/log/nginx/backend.access.log;
    error_log /var/log/nginx/backend.error.log;
}
```
- Restricting Access by `IP`  which `IP` can you allow
```yaml
server {
    listen 80;
    server_name example.com;
    root /var/www/html/project/dist;
    index index.html index.htm index.php;
    location / {
        allow 127.0.0.1; # Allow your public IP or local IP
        deny all;           # Deny all other IPs
        try_files $uri $uri/ /index.html;
    }
    access_log /var/log/nginx/frontend.front.access.log;
    error_log /var/log/nginx/frontend.front.error.log;
    
}
```
- `SSL` added in this nginx file 
```yaml

server {
    listen 80;
    server_name chatbot.example.com;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name chatbot.example.com;

    # SSL Certificate and Key paths (replace with your actual certificate paths)
    ssl_certificate /etc/ssl/example.crt;
    ssl_certificate_key /etc/ssl/examplepvt.key;
    ssl_trusted_certificate /etc/ssl/example.ca-bundle;

    # SSL configuration
    ssl_protocols TLSv1.2 TLSv1.3;  # Enable TLSv1.2 and TLSv1.3 only
    ssl_ciphers 'TLS_AES_128_GCM_SHA256:TLS_AES_256_GCM_SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384';
    ssl_prefer_server_ciphers on;
    ssl_session_cache shared:SSL:10m;

    # Additional SSL configurations for security
    ssl_stapling on;
    ssl_stapling_verify on;
    ssl_ecdh_curve secp384r1;

    location / {

        proxy_pass http://ip:port;
        #proxy_pass http://127.0.0.1:5000;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;


         # Ensure proper WebSocket handling if needed
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';

        # Timeout settings
        proxy_connect_timeout 60s;
        proxy_read_timeout 120s;
        proxy_send_timeout 120s;
        send_timeout 120s;
        add_header 'Access-Control-Allow-Origin' '*' always;
        add_header 'Access-Control-Allow-Credentials' 'true' always;
    }

    # Logging
    access_log /var/log/nginx/chat-example.access.log;
    error_log /var/log/nginx/chat-example.error.log;
}

```

- If you use `Let's encrypt `
```yaml
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d example.com -d www.example.com
```
