# Compile code to run on Vector

todo: finish

Vector has an armv7l CPU with vfpv4 and neon extensions. It's a capable CPU with a surprising (to some) amount of headroom. There is also plenty of space in the flash if you know what you are doing.

This CPU handles armhf instructions, but the filesystem is linked with armel due to drivers which were given binary-only, so you must statically compile if you want to use the full capability of the CPU.

If you don't want to statically compile, this [Linaro arm-linux-gnueabi gcc 5.5 toolchain](http://releases.linaro.org/components/toolchain/binaries/5.5-2017.10/arm-linux-gnueabi/) works.

If you would rather statically compile, you can use whatever arm-linux-gnueabihf toolchain suits your needs and add "-static" to the ld flags.

A workaround I use for programs which don't nicely statically compile (like Go programs which have CGO) is to rsync over a recent sysroot from the linaro toolchain site, compile the program with the corresponding toolchain, and when running it on the robot to set the LD_LIBRARY_PATH towards the linaro sysroot's lib folder. You may also need to copy the ld-linux-armhf.so.3 to the robot's /lib folder.