# KeepMEATable

## Install

```shell
$ git clone git@github.com:KeepMEATable/keepmeatable
$ cd ascustomer
$ git submodule init
$ git submodule update
$ cd ..
$ cd asholder
$ git submodule init
$ git submodule update
$ cd ..
$ cd api
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

Now, you can add 5 new hosts to your machine.

```shell
$ sudo nano /etc/hosts
```

```shell
127.0.0.1       app.keepmeatable.dev
127.0.0.1       mercure.keepmeatable.dev
127.0.0.1       api.keepmeatable.dev
127.0.0.1       holder.keepmeatable.dev
127.0.0.1       rabbit.keepmeatable.dev
```

Create the ssh keys to secure and access the API

```shell
$ docker-compose exec php mkdir -p config/jwt # For Symfony3+, no need of the -p option
$ docker-compose exec php openssl genrsa -out config/jwt/private.pem -aes256 4096
$ docker-compose exec php openssl rsa -pubout -in config/jwt/private.pem -out config/jwt/public.pem
```

You can now open your favorite browser [as customer](https://app.keepmeatable.dev) or [as holder](https://holder.keepmeatable.dev) to test it.

## Aliases for Submodule while working.

```shell
$ git config alias.sdiff '!'"git diff && git submodule foreach 'git diff'" # will execute a diff on each submodule.
$ git config alias.spush 'push --recurse-submodules=on-demand' # will push only if your submodule does not contains any changes.
$ git config alias.supdate 'submodule update --remote --merge' # will update a submodule.
```

or just work inside each sub directory.

## Running

To consume the mercure messages.

```shell
$ docker-compose exec php bin/console messenger:consume amqp
```
