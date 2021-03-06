# Fingerprint for Kirby 2

## What is it?

The Fingerprint plugin adds fingerprints to css and js filenames based on their contents.

## Why use it?

As the fingerprint on the file changes after the contents of the file have been changed it will help you bust the browsercache.

## How to use it?

Add it using git: `git submodule add https://github.com/iksi/kirby-fingerprint.git site/plugins/kirby-fingerprint` or do it manually by downloading the repository, renaming the folder to `kirby-fingerprint` and placing it in `/site/plugins`. You can use the normal Kirby `css()` and `js()` helper functions.

Add the following lines to your htaccess file (after `RewriteBase`):

```
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^(.+)-([0-9a-z]+)\.(js|css)$ $1.$3 [L]
```

Or for Nginx you can add the following to your virtual host setup:

```
location /assets {
    if (!-e $request_filename) {
        rewrite "^/(.+)-([0-9a-z]+)\.(js|css)$" /$1.$3 break;
    }
}
```

Enable fingerprinting by adding the following to you `config.php` file:

```PHP
c::set('plugin.fingerprint', true);
c::set('plugin.fingerprint.trim', 20);
c::set('plugin.fingerprint.algorithm', 'md5');
```

You can also use Kirby’s `@auto` for autoloading and fingerprinting template specific assets.

### External urls

External urls won’t be fingerprinted.

## Author

Jurriaan Topper <jurriaan@iksi.eu> (http://www.iksi.eu/)
