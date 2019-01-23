# .htaccess 301 Redirect Recipes
A recipe book of useful 301 redirects for use within an Apache .htaccess file

Curly braces ({}) indicate optional characters. IE the rule will work with or without these characters.

```
# Redirects a URL such as http{s}://domain.com/about{/} to https://domain.com/about-us
RewriteRule ^about/?$ https://domain.com/about-us [L,R=301]

# Redirects a URL such as http{s}://domain.com/how/this-bit-stays-the-same/ to https://domain.com/what/this-bit-stays-the-same/
# Also handles the redirection of the parent directory so will redirect domain.com/how/ to domain.com/what/
RewriteRule ^how/?(.*)$ https://domain.com/what/$1/ [L,R=301]
```
