# C Loadable Kernel Module Template

A simple template to get started with writing a C LKM. Supports hot-reloading and a qemu VM.

## Setup

The default paths for scripts in this template are:

- `KERNEL`: `../linux`
- `BUSYBOX`: `../busybox`

So, you should have a `KERNEL` dir with a rust enabled kernel already built and
a `BUSYBOX` dir with a **ALREADY** built and configured busybox.

For automating the setup of the environment, run the `setup` script:

```bash
./scripts/setup
```

Refer to the script for more info.

## Building

I wrote a simple wrapper script for the `make` command for compiling this LKM.
It is located in the `scripts` directory. You can use it like this:

```bash
./scripts/build
./scripts/build -t help
./scripts/build -t clean
./scripts/build -k /path/to/linux -b /path/to/busybox
# ... and so on
```

Please refer to the
[kernel docs](https://www.kernel.org/doc/html/latest/kbuild/kbuild.html) for
more info on basic Kbuild usage.

## Running

First, build the LKM. Then, you can use the `run` script to run it in a qemu VM:

```bash
# Default locations: KERNEL=../linux, BUSYBOX=../busybox
./scripts/run
# Custom locations
./scripts/run -k /path/to/linux -b /path/to/busybox
```

This script will simply copy all the `.ko` files to the initramfs and run the
VM.

## Hot-reloading

You can use the `hot-reload` script to hot-reload the LKM in the running VM:

```bash
./scripts/hot-reload
```

It uses the [entr](https://github.com/clibs/entr) utility to watch for changes in the source code and then
running `./scripts/build` to build the LKM and `./scripts/run` to run it in the
VM. Please refer to the script for more info.

## References

- [Linux Kernel Docs](https://www.kernel.org/doc/html/latest/index.html)
- [Linux Kernel Module Programming Guide](https://www.tldp.org/LDP/lkmpg/2.6/html/index.html)
- [Linux Kernel Development](https://www.amazon.com/Linux-Kernel-Development-Robert-Love/dp/0672329468)
- [Linux Device Drivers](https://www.amazon.com/Linux-Device-Drivers-3rd-Edition/dp/0596005903)
