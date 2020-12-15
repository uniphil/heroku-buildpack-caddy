Heroku buildpack: Caddy
=======================

NOTE: probably don't use this-- it's currently heavily adapted for a specific use-case

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) that runs [Caddy](https://caddyserver.com).

Usage
-----

Example usage:

    $ ls
    Caddyfile

    $ heroku create --buildpack http://github.com/twistly/heroku-buildpack-caddy.git

    $ git push heroku master
    ...
    -----> Heroku receiving push
    -----> Fetching custom buildpack
    -----> Caddy app detected
    -----> Found a Caddyfile

The buildpack will detect that your app has a `Caddyfile` in the root and start caddy with that config file.
To build your Single page app, etc. please use another build pack before this one.

Buildpack Config Variables
--------------------------

The environment variable `CADDY_VERSION` overrides the default caddy version set by this buildpack (currently `2.2.1`). See the [releases page over at Caddy's GitHub repo](https://github.com/caddyserver/caddy/releases) for available versions.

Your app will need to touch `/tmp/app-initialized` when it's ready for traffic, similar to the [nginx buildpack](https://github.com/heroku/heroku-buildpack-nginx/tree/38b77474edc6ac59b463a45e540b0aaec3277b44). See that buildpack also for how to define a Procfile with `bin/start-caddy`.


note: current bundled caddy build includes `caddy-l4` and `cloudflare` :(

```bash
GOOS=linux ./xcaddy build v2.2.1 --with github.com/mholt/caddy-l4 --with github.com/caddy-dns/dnspod
```
