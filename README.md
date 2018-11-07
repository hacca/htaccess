# htaccess

##ssl リダイレクト
```
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
 
# httpからの通信を、httpsにリダイレクト（www有り無し）
RewriteCond %{HTTPS} off
RewriteRule ^(.*$) https://example.com/$1 [R=301,L]
 
# httpsからの通信でwww有りの場合、www無しにリダイレクト
RewriteCond %{HTTPS} on
RewriteCond %{HTTP_HOST} ^www.example.com$
RewriteRule ^(.*)$ https://example.com/$1 [R=301,L]
</IfModule>
```
