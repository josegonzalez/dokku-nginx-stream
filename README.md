# Dokku NGINX Stream plugin (Alpha)

**Note:** Alpha software. Pull Requests are welcome

Dokku NGINX Stream gives the ability to open up tcp/udp ports
to the outside world. This can be usefull when your application
speaks more than http.

**Note:** Your app must use the proxy plugin.

## Install and usage

```sh
# dokku 0.25.0+
$ sudo dokku plugin:install https://github.com/josegonzalez/dokku-nginx-stream.git
```
## Usage
Nginx Stream leverages the proxy plugin for enabling tcp ports:

```
dokku proxy:ports-add myapp tcp:EXTERNAL_PORT:INTERNAL_PORT
dokku proxy:ports-add myapp udp:EXTERNAL_PORT:INTERNAL_PORT
dokku ps:rebuild
```

**Note** The Nginx-stream only configures the ports after
a rebuild or deploy.

More information on proxy configuration can be found here:
[dokku port management](https://dokku.com/docs/networking/port-management/)

## Technical

Nginx can loadbalance tcp and udp ports via:
[ngx_stream_core_modules](http://nginx.org/en/docs/stream/ngx_stream_core_module.html)

A `nginx-stream.conf` is generated from the proxy settings
and included in the main nginx.conf via
```
stream {
    include /home/dokku/*/nginx-stream.conf;
}
```
