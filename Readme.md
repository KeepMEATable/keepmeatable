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

Now, you can add 2 new hosts to your machine.

```shell
$ sudo nano /etc/hosts
```

```shell
127.0.0.1 app.keepmeatable.dev
127.0.0.1 mercure.keepmeatable.dev
```

You can now open [your favorite browser](https://app.keepmeatable.dev) to test it.
For testing purposes, the topic used to test is the same UUID used to create the QrCode => `A17CF9AD-C964-4CB5-90C2-2BED8F8BCE67`

## Aliases for Submodule while working.

```shell
$ git config alias.sdiff '!'"git diff && git submodule foreach 'git diff'" # will execute a diff on each submodule.
$ git config alias.spush 'push --recurse-submodules=on-demand' # will push only if your submodule does not contains any changes.
$ git config alias.supdate 'submodule update --remote --merge' # will update a submodule.
```

## Running

To consume the mercure messages.

```shell
$ docker-compose exec php bin/console messenger:consume amqp
```
