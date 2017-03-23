sa-nginx-compile-module
=======================
[![Build Status](https://travis-ci.org/softasap/sa-nginx-compile-module.svg?branch=master)](https://travis-ci.org/softasap/sa-nginx-compile-module)


Helper role to compile custom set of dynamic modules for nginx.
Compiled modules would be in /tmp/nginx_modules/out ;


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
      repo: "https://github.com/openresty/redis2-nginx-module.git",
      name: ngx_redis2
    }

```


```YAML

     - {
         role: "sa-nginx-compile-module",
         nginx_version: "{{my_nginx_version}}",
         nginx_modules: "{{my_nginx_modules"}}"
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
