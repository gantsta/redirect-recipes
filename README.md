# .htaccess 301 Redirect Recipes
A recipe book of useful 301 redirects for use within an Apache .htaccess file

Curly braces ({}) indicate optional characters. IE the rule will work with or without these characters.

All redirects assume that your rewrite base is the web root: `RewriteBase /`.

For more awesome Rewrite recipes, see [this Gist](https://gist.github.com/ScottPhillips/1721489) from Scott Philips.

```ApacheConf
# Redirects a URL such as http{s}://domain.com/about{/} to https://domain.com/about-us
RewriteRule ^about/?$ https://domain.com/about-us [L,R=301]

# Redirects a URL such as http{s}://domain.com/how/this-bit-stays-the-same/ to https://domain.com/what/this-bit-stays-the-same/
# Also handles the redirection of the parent directory so will redirect domain.com/how/ to domain.com/what/
RewriteRule ^how/?(.*)$ https://domain.com/what/$1/ [L,R=301]

# Redirect domain URLs (with or without a trailing slash) to the same URL on a new domain
# This should probably be the last redirect rule that runs
# Yeah, this one needs some more testing
RewriteCond %{REQUEST_URI} ^(.*)([^/]+)/?$
RewriteRule ^ https://newdomain.com%1%2 [L,R=301]

# NB: You can add the following, secondary Rewrite Condition to the above rule to exclude some URLs from being redirected.
RewriteCond %{REQUEST_URI} !^/privacy-policy/?

# Redirect any domains that point to the site to their https:// and www. equivalents
# Props to https://wpjohnny.com/301-redirects-to-https-with-and-without-www/
# BEGIN Redirects
RewriteEngine On
# 301 redirect to www
RewriteCond %{HTTP_HOST} !^www\.
RewriteRule ^(.*)$ https://www.%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
# 301 redirect to https
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
# END Redirects
```
