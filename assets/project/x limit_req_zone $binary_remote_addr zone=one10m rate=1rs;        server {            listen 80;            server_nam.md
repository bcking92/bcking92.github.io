    limit_req_zone $binary_remote_addr zone=one:10m rate=1r/s;
        
        server {
                listen 80;
                server_name 13.125.102.179;
                location / {
                        return 301 https://i02a104.p.ssafy.io/$request_uri;
                }
        }
    
        server {
                listen 443 ssl;
                server_name i02a104.p.ssafy.io;
    
                ssl_certificate /certs/certificate.crt;
                ssl_certificate_key /certs/private.key;
    
                location / {
                        limit_req zone=one burst=5;
                        root /home/ubuntu/tripdairy-deploy/Client/dist;
                        index index.htm index.html;
                        try_files $uri $uri/ /index.html;
                }
        }
        server {
                listen 443 ssl;
                server_name i02a104.p.ssafy.io;
    
                ssl_certificate /certs/certificate.crt;
                ssl_certificate_key /certs/private.key;
    
                location / {
                        proxy_pass https://13.125.102.179:8080;
                }
        }