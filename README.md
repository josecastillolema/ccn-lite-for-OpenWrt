# ccn-lite-for-OpenWrt
*ccn-lite v.0.3.0* cross-compiled for OpenWrt.

## Installation

1. Dowload *ccn-lite* from the Github account.
```
git clone https://github.com/cn-uofbasel/ccn-lite
```

2. Place the [Makefile](https://github.com/josecastillolema/ccn-lite-for-OpenWrt/blob/master/Makefile) under the **ccn-lite** directory.

3. Download the OpenWrt SDK development environment from http://downloads.openwrt.org. The SDK varies depending on the architecture of your development box, the architecture of your router and the version/release of OpenWrt your router is running. I currently have Attitude Adjustment v12.09 installed locally on a VMWare virtual machine, and my development box is an i686, so the SDK I use is [this one](https://downloads.openwrt.org/attitude_adjustment/12.09/x86/generic/OpenWrt-SDK-x86-for-linux-i486-gcc-4.6-linaro_uClibc-0.9.33.2.tar.bz2).

4. Extract the SDK files from the downloaded archive, and enter the SDK directory, which should have the same name as the tar.bz2 file (in my case *OpenWrt-SDK-x86-for-linux-i486-gcc-4.6-linaro_uClibc-0.9.33.2*).
```
tar xfj OpenWrt-SDK-x86-for-linux-i486-gcc-4.6-linaro_uClibc-0.9.33.2.tar.bz2
```

5. Copy the modified **ccn-lite** directory we made earlier into the **package** subdirectory of the SDK.
```
cp -r ccn-lite OpenWrt-SDK-x86-for-linux-i486-gcc-4.6-linaro_uClibc-0.9.33.2/package/
```

6. Now we’re all set to compile the *ccn-lite* package. Go to the root SDK directory (if you’re not already there) and type *make V=s* The *V=s* option is optional, but it is useful for debugging as it instructs the compiler to be “verbose” and output all the details of what it is doing.

7. If it compiled correctly, the newly created package (*ccn-lite_0.3.0_x86.ipk* in my case) is now located in the bin/packages subdirectory of the root SDK directory. This file is a *.ipk* file which is used by the *opkg* (Open PacKaGe management) system. *opkg* is a lightweight package management system for embedded devices, where space is an issue.

8. Copy this package onto the router, which is located at 192.168.1.1 on my network.
```
scp ccn-lite_0.3.0_x86.ipk root@192.168.1.1:~
```

9. Now, ssh into the router. We just copied the package to root’s home directory so we are finally ready to install our program. In root’s home directory (where we end up immediately after connecting to the router via ssh) type *opkg install helloworld_1_mipsel.ipk* and the *opkg* system will do the rest.

10. The executables have now been installed into the */bin* directory on the router, per our instructions in the OpenWrt Makefile. So, all we have to do to run the programs is type **ccn-lite-***  at the prompt. Note that because the executables have been installed to the */bin* directory, you should be able to execute the program no matter what directory you are in on the router.

## Alternative installation

If you are using Attitude Adjustment v12.09 and your development box is an i686 you can download a prepacked version from [here](). Now follow the [Installation instructions](https://github.com/josecastillolema/ccn-lite-for-OpenWrt/blob/master/README.md#installation) from step 8.