# rustl8710
Rust on RTL8710

TODO, but for now you can read background and usage instructions at: [https://polyfractal.com/post/rustl8710/](https://polyfractal.com/post/rustl8710/)

## Updates by Lup Yuen

Updated scripts to use OpenOCD instead of JLink as JTAG tool, because JLink no longer works with PADI JTAG dongle. See https://forum.pine64.org/archive/index.php?thread-4579-2.html

### Start OpenOCD for flashing and debugging

```
debug.sh
```

### Select openocd instead of jlink as JTAG tool

```
make setup GDB_SERVER=openocd
```

### Write Flash Memory (using RTL SDK)

```
make flash
```

### Debug Flash Code

```
make debug
```

### Write Flash Memory (using rtl8710.ocd)

```
openocd -f interface/jlink.cfg -f rtl8710.ocd \
        -c "init" \
        -c "reset halt" \
        -c "rtl8710_flash_auto_erase 1" \
        -c "rtl8710_flash_auto_verify 1" \
        -c "rtl8710_flash_write application/Debug/bin/ram_all.bin 0" \
        -c "shutdown"
```

### Read Flash Memory (using rtl8710.ocd)

```
sudo apt install openocd

openocd -f interface/jlink.cfg -f rtl8710.ocd \
        -c "init" \
        -c "reset halt" \
        -c "rtl8710_flash_read_id" \
        -c "rtl8710_flash_read dump.bin 0 1048576" \
        -c "shutdown"
```

### References

https://bitbucket.org/rebane/rtl8710_openocd/src

http://openocd.org/doc-release/html/Debug-Adapter-Configuration.html#SWD-Transport

https://forum.pine64.org/archive/index.php?thread-4579-2.html
