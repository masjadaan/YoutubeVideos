## GDB Plugin
```sh
git clone https://github.com/apogiatzis/gdb-peda-pwndbg-gef.git
cd gdb-geda-pwndbg-gef
./install.sh
```

## GDB with QEMU
```sh
qemu-arm-static -L /usr/arm-linux-gnueabihf/ -g 1234 hello-arm-dyn
```

## GDB
```sh
gdb-multiarch -q -ex 'init-gef' -ex 'set architecture arm' -ex 'set solib-absolute-prefix /usr/arm-linux-gnueabihf/'

gef-remote --qemu-user --qemu-binary /tmp/userMode/hello-arm-dyn localhost 1234
```
