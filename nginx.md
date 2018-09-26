<!-- TITLE: Nginx -->
<!-- SUBTITLE: NGINX is a free, open-source, high-performance HTTP server and reverse proxy, as well as an IMAP/POP3 proxy server. NGINX is known for its high performance, stability, rich feature set, simple configuration, and low resource consumption -->

# Reverse Proxy Server
Een webapplicatie luistert op een bepaalde poort. Wanneer meerdere applicaties op dezelfde poort zitten, dan gebruik je een reversed proxy om het onderscheid te maken. (bijv. luisteren naar poort 80)

Hieronder een voorbeeld om bijv. wiki.js door te lussen van poort 80 naar 3000; wiki.js draait lokaal en luistert op poort 3000, we zetten nginx in om via poort 80 gewoon door te lussen naar 3000;

```yaml
server {
    listen 80;
    listen [::]:80;
    server_name  wiki.example.com;
    location / {
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_pass http://127.0.0.1:3001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_next_upstream error timeout http_502 http_503 http_504;
    }
}
```
