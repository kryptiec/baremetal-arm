# baremetal-arm

Build:
```
arm-none-eabi-as -o build/startup.o boot/startup.s
arm-none-eabi-ld -T linker/linker.ld -o build/fw.elf build/startup.o
arm-none-eabi-objcopy -O binary build/fw.elf build/fw.bin
```

Clean:
```
rm -rf build/*
```

Run:
```
qemu-system-arm -M vexpress-a9 -m 32M -no-reboot -nographic -monitor telnet:127.0.0.1:1234,server,nowait -kernel build/fw.bin
```
Open a new terminal.
```
telnet 127.0.0.1 1234
```
run `info registers` to verify that R0 contains `0xDEADBEEF` 