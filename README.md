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

## External Links
Special thanks to 
[Geert Baeke at baeke.info](https://blog.baeke.info/2019/11/29/front-door-with-wordpress-on-azure-app-service/)

[Marcus Rath over at Matrix Post](https://blog.matrixpost.net/deploy-wordpress-in-azure-app-service-with-staging-slots-for-the-production-and-development-environment/)



