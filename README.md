# WordPress-on-Azure
Running WordPress on Azure WebApp's and Font Door

## .htaccess content
RewriteEngine On

RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^.*$ /index.php [L,QSA]

## Additional settings for wp-config.php
/** Azure WebApp Settings */
if ($_SERVER['HTTP_X_FORWARDED_PROTO'] == 'https') $_SERVER['HTTPS']='on';

/** Sets Persistent Database Connection */
define('USE_PCONNECT', true);
