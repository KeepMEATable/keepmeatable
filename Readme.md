# KeepMEATable

## Install

```shell
$ git clone git@github.com:KeepMEATable/keepmeatable
$ cd ascustomer
$ git submodule init
$ git submodule update
$ cd ..
$ docker-compose pull
$ docker-compose build
```

From here, you need to get the certificate freshly created in the h2-proxy container path `/etc/nginx/certs/localhost.crt` for testing purposes and authorize it on your computer.

```shell
$ docker-compose up -d
```

You can now open [your favorite browser](https://localhost) to test it.

## Update Submodule while working.

```shell
$ git submodule update --remote asCustomer
```
