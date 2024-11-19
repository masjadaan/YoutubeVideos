
## Installing GCC compiler for ARM
```sh
sudo apt-get install gcc-arm-linux-gnueabihf
```

## Installing GNU C Library (glibc)  for ARM
```sh
sudo apt install libc6-armhf-cross 
```

## Compile using dynamic linking
```sh
arm-linux-gnueabihf-gcc -g hello.c -o hello-arm-dyn
```

## Compile using static linking
```sh
arm-linux-gnueabihf-gcc -static -g hello.c -o hello-arm-static 
```

## QEMU for statically compiled 
```sh
qemu-arm-static hello-arm-static 
```

## QEMU for dynamically compiled 
```sh
qemu-arm-static -L /usr/arm-linux-gnueabihf/ hello-arm-dyn 
```
