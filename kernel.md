* compile

```
zcat /proc/config.gz > ./.config
make mrproper
make clean
make [-j $(nproc)]
make modules
```

# LINKS
* [KUnit - Linux Kernel Unit Testing » Getting Started](https://docs.kernel.org/dev-tools/kunit/start.html)
* [Linux kernel source](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git)
