# Fork of Silverstripe CDN Rewrite by Dorset Digital

Provides a simple method of rewriting the URLs of assets and resources to allow the use of a subdomain or external CDN service. This fork is for development purposes internally. Please use the original instead:

https://github.com/DorsetDigital/silverstripe-cdnrewrite

# Requirements
*Silverstripe 4.x

# Installation
* Add the following to your projects composer.json file
```
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/springload/silverstripe-cdnrewrite.git"
        }
    ],
    "require": {
        "dorsetdigital/silverstripe-cdnrewrite": "dev-master"
    },
   ``` 
* Composer install
* Run a `dev/build?flush` to update your project

# Usage

The module won't make any changes to your site unless you do a bit of configuration.  There are a few options you can set, done in a yml file:


```yaml
---
Name: cdnconfig
---

DorsetDigital\CDNRewrite\CDNMiddleware:
  cdn_rewrite: true
  cdn_domain: 'https://cdn.example.com'
  rewrite_assets: true
  rewrite_resources: true
  rewrite_themes: true
  add_debug_headers: true
  enable_in_dev: true
  subdirectory: ''
  cdnpath: ''
  add_prefetch: true
```

The options are hopefully fairly self explanatory:

* `cdn_rewrite` - globally enables and disables the module (default false - disabled)
* `cdn_domain` - the full domain name of the CDN (required to enable module)
* `rewrite_assets` - whether to rewrite references to the 'assets' directory (default false)
* `rewrite_resources` - whether to rewrite references to the 'resources' directory (default false)
* `rewrite_themes` - whether to rewrite references to the 'themes' directory (default false)
* `add_debug_headers` - if enabled, adds extra HTML headers to show the various operations being applied (default false)
* `enable_in_dev` - enable the CDN in dev mode (default false)
* `subdirectory` - set this if your site is in a subdirectory (eg. for http://www.example.com/silverstripe - set this to 'silverstripe')
* `cdnpath` - arb path on cdn
* `add_prefetch` - set this to true if you want the module to automatically add a `<link rel="dns-prefetch">` tag to your html head to improve performance

# Notes

* The module is disabled in the CMS / admin system, so rewrites do not currently happen here
* When enabled, the module will always add an HTTP header of `X-CDN: Enabled` to show that it's working, even if none of the other rewrite operations are carried out.  If this is not present and you think it should be, ensure that you have set `cdn_rewrite` to true, that you have specified the `cdn_domain` in your config file and that you have `enable_in_dev` set to true if you are testing in dev mode.


# Credits
* Very much inspired by [Werner Krauss' silverstripe-cdnrewrite](https://github.com/wernerkrauss/silverstripe-cdnrewrite)
* As always, thanks to the core team for all their hard work.  
