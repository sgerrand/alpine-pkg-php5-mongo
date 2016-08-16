# alpine-pkg-php5-mongo

[![CircleCI](https://img.shields.io/circleci/project/sgerrand/alpine-pkg-php5-mongo/master.svg)](https://circleci.com/gh/sgerrand/alpine-pkg-php5-mongo)

This is the [PHP driver for Mongo][php-mongo] as a Alpine Linux package.

## Releases

See the [releases page](https://github.com/sgerrand/alpine-pkg-php5-mongo/releases) for the latest
download links.

## Installing

The current installation method for these packages is to pull them in using
`wget` or `curl` and install the local file with `apk`:

    apk --no-cache add ca-certificates
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://raw.githubusercontent.com/sgerrand/alpine-pkg-php5-mongo/master/sgerrand.rsa.pub
    wget https://github.com/sgerrand/alpine-pkg-php5-mongo/releases/download/1.16.4-r0/php5-mongo-1.6.14-r0.apk
    apk add php5-mongo-1.6.14-r0.apk

[php-mongo]: https://github.com/mongodb/mongo-php-driver-legacy
