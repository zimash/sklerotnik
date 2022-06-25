# Some notes for working with redis

## 3 operating modes
* standalone
* sentinnel
* cluster

## build

* default
```
$ git clone https://github.com/redis/redis
$ cd redis
$ make -j $(nproc)
$ make test
```
