sa-nginx-compile-module
=======================
[![Build Status](https://travis-ci.org/softasap/sa-nginx-compile-module.svg?branch=master)](https://travis-ci.org/softasap/sa-nginx-compile-module)


Helper role to compile custom set of dynamic modules for nginx.
Compiled modules would be in /tmp/nginx_modules/out ;

Important: you need to compile using the same libraries as your production environment.
Example: if your prod env is ubuntu trusty with openssl 1.0.1f -your module will compile
on ubuntu 16.04 with openssl 1.0.2g.  But would it work? No.  Watch out.


Example of use: check box-example

Simple:

```YAML

my_nginx_version: 1.10.3

my_nginx_modules:
  - {
      repo: "https://github.com/openresty/redis2-nginx-module.git",
      name: ngx_redis2
    }


...

roles:

     - {
         role: "sa-nginx-compile-module",
         nginx_version: "{{my_nginx_version}}",
         nginx_modules: "{{my_nginx_modules"}}"
       }

```

Advanced:

```YAML

my_nginx_version: 1.10.3

my_nginx_modules:
  - {
      repo: "https://github.com/openresty/lua-nginx-module.git",
      name: ngx_http_lua
    }
  - {
      repo: "https://github.com/simpl/ngx_devel_kit.git",
      name: ngx_ndk
    }

my_nginx_core_configure: # for ubuntu
  - "--prefix=/etc/nginx"
  - "--sbin-path=/usr/sbin/nginx"
  - "--modules-path=/usr/lib/nginx/modules"
  - "--conf-path=/etc/nginx/nginx.conf"
  - "--error-log-path=/var/log/nginx/error.log"
  - "--http-log-path=/var/log/nginx/access.log"
  - "--pid-path=/var/run/nginx.pid"
  - "--lock-path=/var/run/nginx.lock"
  - "--http-client-body-temp-path=/var/cache/nginx/client_temp"
  - "--http-proxy-temp-path=/var/cache/nginx/proxy_temp"
  - "--http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp"
  - "--http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp"
  - "--http-scgi-temp-path=/var/cache/nginx/scgi_temp"
  - "--user=nginx"
  - "--group=nginx"
  - "--with-file-aio"
  - "--with-threads"
  - "--with-ipv6"
  - "--with-http_addition_module"
  - "--with-http_auth_request_module"
  - "--with-http_dav_module"
  - "--with-http_flv_module"
  - "--with-http_gunzip_module"
  - "--with-http_gzip_static_module"
  - "--with-http_mp4_module"
  - "--with-http_random_index_module"
  - "--with-http_realip_module"
  - "--with-http_secure_link_module"
  - "--with-http_slice_module"
  - "--with-http_ssl_module"
  - "--with-http_stub_status_module"
  - "--with-http_sub_module"
  - "--with-http_v2_module"
  - "--with-mail"
  - "--with-mail_ssl_module"
  - "--with-stream"
  - "--with-stream_ssl_module"
  - "--with-cc-opt='-g -O2 -fstack-protector --param=ssp-buffer-size=4 -Wformat -Werror=format-security -Wp,-D_FORTIFY_SOURCE=2 -fPIC'"
  - "--with-ld-opt='-Wl,-Bsymbolic-functions -Wl,-z,relro -Wl,-z,now -Wl,--as-needed -pie'"

my_nginx_modules_dependencies:
  - liblua5.1-dev




```


```YAML

     - {
         role: "sa-nginx-compile-module",
         nginx_version: "{{my_nginx_version}}",
         nginx_modules: "{{my_nginx_modules"}}",
         nginx_core_configure: "{{my_nginx_core_configure}}",
         nginx_modules_dependencies: "{{my_nginx_modules_dependencies}}"
       }

```


Usage with ansible galaxy workflow
----------------------------------

If you installed the sa-nginx-compile-module role using the command


`
   ansible-galaxy install softasap.sa-nginx-compile-module
`

the role will be available in the folder library/softasap.sa-nginx-compile-module
Please adjust the path accordingly.

```YAML

     - {
         role: "softasap.sa-nginx-compile-module"
       }

```



Copyright and license
---------------------


Code licensed under the [BSD 3 clause] (https://opensource.org/licenses/BSD-3-Clause) or the [MIT License] (http://opensource.org/licenses/MIT).

Subscribe for roles updates at [FB] (https://www.facebook.com/SoftAsap/)

Join gitter discussion channel at [Gitter](https://gitter.im/softasap)
