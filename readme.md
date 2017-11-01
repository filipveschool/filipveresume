#Install on shared hosting

## Step 1: pull git repository inside domain or subdomain

```
git clone https://github.com/githubaccountname/gitreponame.git
git clone https://github.com/filipveschool/changegitreponamehere.git
```

## Important:

### Make .htaccess file

```
RewriteEngine on
RewriteCond %{REQUEST_URI} !^public
RewriteRule ^(.*)$ public/$1 [L]
```

### Make .htaccess file for https sites

```
RewriteEngine on

RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

#RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R,L]

RewriteCond %{REQUEST_URI} !^public
RewriteRule ^(.*)$ public/$1 [L]
```


## Make index.php file in root folder

```
<?php

/**
 * Laravel - A PHP Framework For Web Artisans
 *
 * @package  Laravel
 * @author   Taylor Otwell <taylor@laravel.com>
 */

$uri = urldecode(
    parse_url($_SERVER['REQUEST_URI'], PHP_URL_PATH)
);

// This file allows us to emulate Apache's "mod_rewrite" functionality from the
// built-in PHP web server. This provides a convenient way to test a Laravel
// application without having installed a "real" web server software here.
if ($uri !== '/' && file_exists(__DIR__.'/public'.$uri)) {
    return false;
}

require_once __DIR__.'/public/index.php';

```