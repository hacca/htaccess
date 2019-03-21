## ssl リダイレクト
```
# httpからの通信を、httpsにリダイレクト（www有り無し）
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [R,L]

# httpsからの通信でwww有りの場合、www無しにリダイレクト
RewriteCond %{HTTPS} on
RewriteCond %{HTTP_HOST} ^www.example.com$
RewriteRule ^(.*)$ https://example.com/$1 [R=301,L]
</IfModule>

# さくら
RewriteEngine On
RewriteCond %{HTTP:X-SAKURA-FORWARDED-FOR} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]

```

<br><br><br>
# ファイルがない場合403返す
```
Options -Indexes
```

<br><br><br>
# 転送
```
RewriteRule ^creative-partner/$ https://goo.gl/forms/Si2KVpXClcuu8qji1 [R=301,L]
```

<br><br><br>
# HSTS設定
```
Header set Strict-Transport-Security “max-age=31536000″ env=HTTPS
```

<br><br><br>
# http-equiv="X-UA-Compatible"
```
<IfModule mod_headers.c>
Header set X-UA-Compatible "IE=Edge,chrome=1"
</IfModule>
```

<br><br><br>
# wp-config.php守る
```
<files wp-config.php>
order allow,deny
deny from all
</files>
```

<br><br><br>
# ブラウザへのキャッシュの設定
```
<IfModule mod_expires.c>
  ExpiresActive On

  # キャッシュの初期化（1秒に設定）
  ExpiresDefault "access plus 1 seconds"

  # MIME Type ごとのキャッシュ設定
  ExpiresByType text/css "access plus 1 weeks"
  ExpiresByType text/js "access plus 1 weeks"
  ExpiresByType text/javascript "access plus 1 weeks"
  ExpiresByType image/gif "access plus 1 weeks"
  ExpiresByType image/jpeg "access plus 1 weeks"
  ExpiresByType image/png "access plus 1 weeks"
  ExpiresByType image/svg+xml "access plus 1 year"
  ExpiresByType application/pdf "access plus 1 weeks"
  ExpiresByType application/javascript "access plus 1 weeks"
  ExpiresByType application/x-javascript "access plus 1 weeks"
  ExpiresByType application/x-shockwave-flash "access plus 1 weeks"
  ExpiresByType application/x-font-ttf "access plus 1 year"
  ExpiresByType application/x-font-woff "access plus 1 year"
  ExpiresByType application/x-font-opentype "access plus 1 year"
  ExpiresByType application/vnd.ms-fontobject "access plus 1 year"
</IfModule>
```

<br><br><br>
# gzip
```
<IfModule mod_deflate.c>
SetOutputFilter DEFLATE

BrowserMatch ^Mozilla/4 gzip-only-text/html
BrowserMatch ^Mozilla/4\.0[678] no-gzip
BrowserMatch \bMSI[E] !no-gzip !gzip-only-text/html

SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png|ico)$ no-gzip dont-vary

Header append Vary User-Agent env=!dont-vary
</IfModule>
```

<br><br><br>
# rewrite example
```
RewriteRule ^about/(.*)$ /kinmemai/about/$1 [R=301,L]
RewriteRule ^com/(.*)$ /kinmemai/ [R=301,L]
RewriteRule ^information/toyoseimaiki/$ /info/ [R=301,L]
RewriteRule ^kinmemai_pv/(.*)$ /kinmemai/kinmemai_pv/$1 [R=301,L]
RewriteRule ^news/(.*)$ /info/ [R=301,L]
RewriteRule ^quiz/(.*)$ /bg_musenmai/quiz/$1 [R=301,L]
RewriteRule ^saikashiki/(.*)$ / [R=301,L]
RewriteRule ^nihonkenkougakkai.pdf$ /info/upload/nihonkenkougakkai.pdf [R=301,L]
RewriteRule ^100801yomiuri.pdf$ /info/upload/100801yomiuri.pdf [R=301,L]
RewriteRule ^movie.html$ /bg_musenmai/movie.html [R=301,L]
RewriteRule ^news.html$ /info/ [R=301,L]
RewriteRule ^policy.html$ /site_policy.html [R=301,L]
RewriteRule ^privacy.html$ /privacy_policy.html [R=301,L]
RewriteRule ^recruit.html$ /recruit/ [R=301,L]
RewriteRule ^sitemap.html$ /site_map.html [R=301,L]
RewriteRule ^release2.html$ /info/release.html [R=301,L]
RewriteRule ^shopping/(.*)$ /kinmemai/$1 [R=301,L]
RewriteRule ^shopping/company.html$ /about.html [R=301,L]
RewriteRule ^shopping/policy.html$ /privacy_policy.html [R=301,L]
RewriteRule ^inquiry/form_bg.html$ https://pro.form-mailer.jp/fms/2a59ac9784973 [R=301,L]
RewriteRule ^inquiry/form.html$ https://pro.form-mailer.jp/fms/f8d792f584972 [R=301,L]
RewriteRule ^kinmemai/form.html$ https://pro.form-mailer.jp/fms/f8d792f584972 [R=301,L]
RewriteRule ^cup/form/(.*)$ https://mdh.fm/e?kA5033RFSV [R=301,L]
# RewriteRule ^kinmemai/genryo/best/(.*)$ http://bemss.jp/toyo-rice/cont124_001.php [R=301,L]
# RewriteRule ^kinmemai/genryo/gold/(.*)$ http://bemss.jp/toyo-rice/cont124_002.php [R=301,L]
# RewriteRule ^kinmemai/genryo/hai/(.*)$ http://bemss.jp/toyo-rice/cont124_003.php [R=301,L]
# RewriteRule ^kinmemai/genryo/tanita/okinawa/(.*)$ http://bemss.jp/toyo-rice/cont112_002_004.php [R=301,L]
RewriteRule ^kinmemai/genryo/tanita/okinawa/(.*)$ http://www.okishoku.co.jp/syouhin_tanita-genryo.html [R=301,L]
RewriteRule ^kinmemai/genryo/tanita/hokaido/(.*)$ http://bemss.jp/toyo-rice/cont112_002_003.php [R=301,L]
# RewriteRule ^kinmemai/genryo/tanita/$ http://bemss.jp/toyo-rice/cont122_001_001.php [R=301,L]
# RewriteRule ^kinmemai/genryo/$ http://bemss.jp/toyo-rice/cont124.php [R=301,L]
RewriteRule ^saikoumai/anniversary/$ https://pro.form-mailer.jp/fms/1a2a1e1c126266 [R=301,L]
RewriteRule ^seminar/$ https://pro.form-mailer.jp/fms/27321475133633 [R=301,L]
RewriteRule ^lowprotein/enquete/$ https://pro.form-mailer.jp/fms/5c16e56a150680 [R=301,L]
RewriteRule ^koukoku/$ http://www.toyorice.jp/fs/toyorice/c/otameshi2 [R=301,L]
```
