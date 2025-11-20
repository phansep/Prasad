## Config MAP with TSL 1 and TLS 2###
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-tls-config
data:
  default.conf: |
    server {
        listen 443 ssl;

        ssl_certificate /etc/tls/tls.crt;
        ssl_certificate_key /etc/tls/tls.key;

        # Allow only TLS 1.2 and 1.3
        ssl_protocols TLSv1.2 TLSv1.3;
        ssl_prefer_server_ciphers on;

        location / {
            proxy_pass http://localhost:8080;
        }
    }
