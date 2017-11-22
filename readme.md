## Getting started

### 1. OAuth2 client registration

[client registration- ChatWork](https://www.chatwork.com/service/packages/chatwork/subpackages/oauth/client_create.php)

### 2. Enable SSL & and generate a self-signed cert

```bash
$ cd laradoc
$ vi caddy/Caddyfile
```

```diff
diff --git a/caddy/Caddyfile b/caddy/Caddyfile
--- a/caddy/Caddyfile
+++ b/caddy/Caddyfile
@@ -1,5 +1,5 @@
 # Docs: https://caddyserver.com/docs/caddyfile
-0.0.0.0:80 {
+https://oauth2-chatwork.local {
     root /var/www/public
     fastcgi / php-fpm:9000 php {
         index index.php
@@ -17,7 +17,7 @@
     errors /var/log/caddy/error.log
     # Uncomment to enable TLS (HTTPS)
     # Change the first list to listen on port 443 when enabling TLS
-    #tls self_signed
+    tls self_signed

     # To use Lets encrpt tls with a DNS provider uncomment these
     # lines and change the provider as required
```

```bash
$ cd laradoc
$ docker-compose up caddy
(press CTRL+C after generating a self-signed cert)
```

### 3. Start servers

```bash
$ docker-compose up -d mysql caddy
```


### 4. Access client

```bash
$ echo '127.0.0.1       oauth2-chatwork.local' >> /etc/hosts
```

Access https://oauth2-chatwork.local via browser


## License

[MIT license](http://opensource.org/licenses/MIT).