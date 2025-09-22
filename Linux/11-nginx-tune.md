### Nginx Tuning Config (for static frontend)

```worker_processes auto;

events {
    worker_connections 65535;   # each worker will be   connection handle 
    multi_accept on;
    use epoll;                  # Linux high-performance I/O
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile on;
    tcp_nopush on;
    tcp_nodelay on;
    keepalive_timeout 65;
    types_hash_max_size 2048;

    # Compression (gzip or brotli)
    gzip on;
    gzip_comp_level 5;
    gzip_types text/plain text/css application/json application/javascript application/xml+rss image/svg+xml;

    # Cache control
    add_header Cache-Control "public, max-age=31536000, immutable";

    # Buffer settings
    client_body_buffer_size 128k;
    client_max_body_size 100m;
    large_client_header_buffers 4 64k;

    # Static file serving
    server {
        listen 80 default_server;
        server_name _;

        root /var/www/frontend;   # you build folder path
        index index.html;

        location / {
            try_files $uri /index.html;
        }

        location ~* \.(?:ico|css|js|gif|jpe?g|png|woff2?|eot|ttf|svg)$ {
            expires 6M;
            access_log off;
            add_header Cache-Control "public";
        }
    }
}
