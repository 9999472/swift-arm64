# Swift for Arm64/AArch64 Servers and SBC's
## Latest build info from our CI server
The awesome Cavium ThunderX from [Packet Bare Metal Servers](https://www.packet.com/cloud/servers/c1-large-arm/)
   
### Swift 4.2.3 &nbsp; [![Build Status](http://futurejones.xyz:8080/job/swift-4.2-aarch64-RELEASE/5/badge/icon)](http://futurejones.xyz:8080/job/swift-4.2-aarch64-RELEASE)
### Swift 5.0 &nbsp;&nbsp;&nbsp;&nbsp; [![Build Status](http://futurejones.xyz:8080/job/swift-5.0-aarch64/badge/icon)](http://futurejones.xyz:8080/job/swift-5.0-aarch64)
### Master &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [![Build Status](http://futurejones.xyz:8080/job/swift-master-aarch64/badge/icon)](http://futurejones.xyz:8080/job/swift-master-aarch64)

# Swift-Arm64
Swift for Arm64/aarch64 Servers and SBC's - Rock64, RaspberryPi3 and many more

Install packages are now available for arm64/aarch64 compatible Servers and SBC's.

for Ubuntu/Debian/Stretch

Add repo -

```bash
$ curl -s https://packagecloud.io/install/repositories/swift-arm/release/script.deb.sh | sudo bash
``` 

Install Swift - 

```bash
$ sudo apt-get install swift4
```
### Tested Servers
*c1-large-arm from Packet* - [Packet Bare Metal Servers](https://www.packet.com/cloud/servers/c1-large-arm/)  
*Amazon EC2 A1 instances* - [AWS](https://aws.amazon.com/ec2/instance-types/a1/)
### Tested Boards and OS's

*Rock64* - Debian/Stretch Ubuntu/Xenial - [http://pine64.org](http://pine64.org)  
*RaspberryPi 3 models* - Ubuntu 18.04 64bit  
*ODROID-C2* - Ubuntu 16.04.4 LTS xenial

### RaspberyPi 3 64bit OS

An official 64 bit Ubuntu "Bionic" 18.04 install image is now available for Raspberry Pi 3.

*Note: This is a lite server image for headless operation.*  
*Tested on RPi3B and RPi3B+.*  
*Should also install on RPi3A+ and maybe the Compute Module 3.*

Download image here - [http://cdimage.ubuntu.com/releases/18.04/release/](http://cdimage.ubuntu.com/releases/18.04/release/)

Swift 4.2 AArch64 for Ubuntu 18.04 is available here - [swift4_4.2.2_arm64.deb](https://packagecloud.io/app/swift-arm/release/search?dist=ubuntu%2Fbionic)

## Swift 5.0 Developer Snapshots
Swift 5.0 developer snapshots are now available for Ubuntu 16.04.  
Download here - [Snapshots](https://github.com/futurejones/swift-arm64/releases)

## Swift for TensorFlow
[Developer Snapshot](https://github.com/futurejones/swift-arm64/releases/tag/swift-for-tensorflow-dev-2019-01-14)  
[Build instructions](https://github.com/futurejones/swift-arm64/blob/master/swift-for-tensorflow-patches/BUILD.md#build-instructions-for-swift-for-tensorflow-on-ubuntu-1604)

## Building Swift

*Swift development on AArch64 systems is currently possible on Ubuntu 16.04 and 18.04.*  
*The following build instructions are for Ubuntu 16.04.*

### Setting up the Swift development environment
* If possible start with a new clean install of Ubuntu 16.04 and then update and upgrade your system:  
```$ sudo apt-get update```  
```$ sudo apt-get upgrade```
* Install development dependencies:  
```$ sudo apt-get install git cmake ninja-build clang python uuid-dev libicu-dev icu-devtools libbsd-dev libedit-dev libxml2-dev libsqlite3-dev swig libpython-dev libncurses5-dev pkg-config libblocksruntime-dev libcurl4-openssl-dev systemtap-sdt-dev tzdata rsync```  

### Getting Sources for Swift and Related Projects
* First create a directory for all of the Swift sources:  
```mkdir swift-source```  
```cd swift-source```

* Next clone the Swift repository:  
```$ git clone https://github.com/apple/swift.git```

* Next use the "update-checkout" utility to clone the related repositories. When using this utility we can use either a `--tag` to specify a release or `--scheme` to specify a branch. If no tag or scheme is used then the master will be used as default.  
The following command will clone and checkout all necessary repositories to build a 4.2.1 release.  
```$ ./swift/utils/update-checkout --clone --tag swift-4.2.1-RELEASE```  
The following command will clone and checkout all necessary repositories to build the swift-5.0-branch.  
```$ ./swift/utils/update-checkout --clone --scheme swift-5.0-branch```

### Applying Patches
* Some branches require additional patches for successful builds.  
  * swift-4.2-branch:  
  ```$ cd swift```  
  ```$ wget https://github.com/futurejones/swift-arm64/raw/master/swift-4.2-patches/swift-4.2-aarch64-VarArgs.patch```  
  ```$ git apply swift-4.2-aarch64-VarArgs.patch```  
  ```$ wget https://github.com/futurejones/swift-arm64/raw/master/swift-4.2-patches/swift-4.2-pm-fix.patch```  
  ```$ git apply swift-4.2-pm-fix.patch```  
  ```$ cd -```  
  NOTE: From v4.2.3 swift-4.2-branch no longer needs patching.
  
  * swift-5.0-branch:  
  From 2019-01-30 changes have been merged with the `swift-5.0-branch` so patches are no longer required.

  * master:  
  No patches required.

### Building with Ninja
* The ```build-script``` is a high-level build automation script that supports basic options such as building a Swift-compatible LLDB, building the Swift Package Manager, building for various platforms, running tests after builds, and more.  
We will be using ```buildbot_linux``` presets to specify OS, install directories and package names.  
*NOTE: Replace [USER] with your user name. You should also rename "swift-4.2.1-aarch64-RELEASE-Ubuntu-16.04.tar.gz" tarball to match your build if needed*  
```$ ./swift/utils/build-script --preset=buildbot_linux,no_test install_destdir=/home/[USER]/swift-source/install installable_package=/home/[USER]/swift-source/install/swift-4.2.1-aarch64-RELEASE-Ubuntu-16.04.tar.gz -n```  
Using the "-n" tag on the end of the command enables a "dry run" to check the commands are correct before running the actual build.  
If everything is correct then you can remove "-n" and proceed with the build.  
Depending on your build system the build can take from 1.5hrs to 15hrs or more.  
