



WITH NGINX-PROXY-MANAGER:
Add this on your advanced tab while creating a proxy host for mediaflow-proxy:

# Headers for forwarded information
proxy_set_header Host $host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $scheme;
proxy_set_header X-Forwarded-Host $host;
proxy_set_header X-Forwarded-Port $server_port;

# Headers for streaming support
proxy_set_header Range $http_range;
proxy_set_header If-Range $http_if_range;
proxy_set_header Connection "";

# Timeout settings for streaming
proxy_connect_timeout 60s;
proxy_send_timeout 300s;
proxy_read_timeout 300s;

# Disable buffering for streaming
proxy_buffering off;
proxy_request_buffering off;
proxy_max_temp_file_size 0;

# Client settings
client_max_body_size 0;
client_body_timeout 60s;
client_header_timeout 60s;

# Handle redirects
proxy_redirect off;

# HTTP version
proxy_http_version 1.1;

# Security headers
add_header X-Frame-Options DENY always;
add_header X-Content-Type-Options nosniff always;
add_header X-XSS-Protection "1; mode=block" always;
add_header Referrer-Policy "strict-origin-when-cross-origin" always;

# Hide server information
proxy_hide_header X-Powered-By;
server_tokens off;

Step 2: MediaFlow Proxy Configuration

Configure MediaFlow Proxy to trust Nginx Proxy Manager:

If running on the same server:

FORWARDED_ALLOW_IPS=127.0.0.1
If running in Docker with custom network:

# Use the Docker network range
FORWARDED_ALLOW_IPS=172.18.0.0/16
