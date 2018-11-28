## Latest build info from our CI server
The awesome Cavium ThunderX from [Packet Bare Metal Servers](https://www.packet.com/cloud/servers/c1-large-arm/)

### Swift 4.1.3 &nbsp; [![Build Status](http://futurejones.xyz:8080/job/swift-4.1-branch-aarch64/badge/icon)](http://futurejones.xyz:8080/job/swift-4.1-branch-aarch64)   
### Swift 4.2.1 &nbsp; [![Build Status](http://futurejones.xyz:8080/job/swift-4.2-aarch64-RELEASE/5/badge/icon)](http://futurejones.xyz:8080/job/swift-4.2-aarch64-RELEASE)
### Swift 5.0 &nbsp;&nbsp;&nbsp;&nbsp; [![Build Status](http://futurejones.xyz:8080/job/swift-5.0-aarch64/badge/icon)](http://futurejones.xyz:8080/job/swift-5.0-aarch64)
### Master &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [![Build Status](http://futurejones.xyz:8080/job/swift-5.0-aarch64/badge/icon)](http://futurejones.xyz:8080/job/swift-master-aarch64)

# Swift-Arm64
Swift for Arm64/aarch64 SBC's - Rock64, RaspberryPi3 and many more

Install package now available for arm64/aarch64 compatible SBC's.

for Debian/Stretch

Tested on the Rock64 from http://pine64.org

Add repo -

```bash
$ curl -s https://packagecloud.io/install/repositories/swift-arm/debian/script.deb.sh | sudo bash
```

Install Swift - 

```bash
$ sudo apt-get install swift4
```

### Tested Boards and OS's

*Rock64* - Debian/Stretch Unbutu/Xenial  
*RaspberryPi 3* - Debian 10 64bit preview  
*ODROID-C2* - Ubuntu 16.04.4 LTS xenial

### RaspberyPi 3 64bit OS

A 64 bit Debian 10 "Buster" preview with Swift 4.1.1 pre-installed is available for testing.

Note: This is a lite server image for headless operation.

https://github.com/futurejones/swift-arm64/releases/download/rpi3-debian-buster-64bit/debian_10_64bit_rpi3.img.tar.gz

- Download and untar
- copy "bionic_rpi3.img" image to sd card
- boot and `ssh pi@rpi3.local`
- username "pi"
- password "raspberry"

Test with some server side swift examples from Kitura
```bash
$ git clone https://github.com/IBM-Swift/Kitura-Sample.git
$ cd Kitura-Sample
$ swift build
$ swift run Kitura-Sample
```

