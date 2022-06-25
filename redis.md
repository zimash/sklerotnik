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
