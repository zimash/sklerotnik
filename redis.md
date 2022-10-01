# Some notes for working with redis

## 3 operating modes
* standalone
* sentinel
* cluster

## build

* default
```
$ git clone https://github.com/redis/redis
$ cd redis
$ make -j $(nproc)
$ make test
```
To run only the necessary tests (written in Tcl)
```
$ ./runtest # equal to make test, runs all tests in test/... directory
$ ./runtest-moduleapi # runs all test in tests/unit/moduleapi, such as commandfilter, basic, and etc
$ ./runtest-sentinel # runs Redis Sentinel tests
$ ./runtest-cluster # runs Redis Cluster tests
```

## [Redis data types](https://redis.io/docs/manual/data-types/data-types-tutorial/)
* strings - binary safe data, can contain any kind of data (jpeg, serialized objects and etc)
* lists - lists of strings, sorted by insertion order
* sets - undordered collection of strings
* hashes - maps between string fields and string values
* sorted sets - similary sets, non repeating collections of string
* streams - is a data structure that acts like an append-only log
* geospatial indexes - indexes, which are useful for finding locations within a given geographic radius.
* bitmaps and hyperlologs - which are actually data types based on the string base type, but having their own semantics

## [Clients, browse by language](https://redis.io/docs/clients/)

## Useful links
* [Redis Explained](https://architecturenotes.co/redis/) 
