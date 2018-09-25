<!-- TITLE: Nginx -->
<!-- SUBTITLE: NGINX is a free, open-source, high-performance HTTP server and reverse proxy, as well as an IMAP/POP3 proxy server. NGINX is known for its high performance, stability, rich feature set, simple configuration, and low resource consumption -->

# Reverse Proxy Server
Een webapplicatie luistert op een bepaalde poort. Wanneer meerdere applicaties op dezelfde poort zitten, dan gebruik je een reversed proxy om het onderscheid te maken. (bijv. luisteren naar poort 80)

```yaml
http {
    proxy_cache_path  /data/nginx/cache  levels=1:2    keys_zone=STATIC:10m
    inactive=24h  max_size=1g;
    server {
        location / {
            proxy_pass             http://1.2.3.4;
            proxy_set_header       Host $host;
            proxy_buffering        on;
            proxy_cache            STATIC;
            proxy_cache_valid      200  1d;
            proxy_cache_use_stale  error timeout invalid_header updating
                                   http_500 http_502 http_503 http_504;
        }
    }
}
```
