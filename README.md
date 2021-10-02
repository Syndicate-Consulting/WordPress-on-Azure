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

## App Service Scale out issues
Using the automatic Scale out option on a App Service Plan host can have unpredictable results on the responds times of a WordPress website on Azure. Enabling the custom autoscale option can result in a 300% increase in the responds time of a WordPress website on that host.

## External Links
Special thanks to

[Geert Baeke at baeke.info](https://blog.baeke.info/2019/11/29/front-door-with-wordpress-on-azure-app-service/)

[Marcus Rath over at Matrix Post](https://blog.matrixpost.net/deploy-wordpress-in-azure-app-service-with-staging-slots-for-the-production-and-development-environment/)


### Stuff for wp-config.php if you don't use headers in Front Door
define('WP_HOME', 'https://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
define('WP_SITEURL', 'https://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));

This will work, only redirects your /wp-admin/ folders to the full Web App URL and not your custom domain name. So please just use the headers in Front Door. :)
