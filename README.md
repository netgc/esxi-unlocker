# macOS Unlocker v3.0.5 for VMware ESXi

## Download ESXi 8.0 (integrated Unlocker & OEM BIOS)

Powered by [sysin.org](https://sysin.org/)

- [VMware ESXi 8.0 Unlocker standard & Custom Image](https://sysin.org/blog/vmware-esxi-8-oem/)
- [VMware ESXi 8.0 Unlocker with driver](https://sysin.org/blog/vmware-esxi-8-sysin/)

## Download ESXi 7.0 (integrated Unlocker & OEM BIOS)

- [VMware ESXi 7.0 U3 & Unlocker standard & Custom Image](https://sysin.org/blog/vmware-esxi-7-u3-oem/)
- [VMware ESXi 7.0 U3 & Unlocker with driver](https://sysin.org/blog/vmware-esxi-7-u3-sysin/)
- [VMware ESXi 7.0 U2 & Unlocker standard & Custom Image](https://sysin.org/blog/vmware-esxi-7-u2-oem/)
- [VMware ESXi 7.0 U2 & Unlocker with driver](https://sysin.org/blog/vmware-esxi-7-u2-sysin/)
- [VMware ESXi 7.0 U1 Unlocker standard & Custom Image](https://sysin.org/blog/vmware-esxi-7-u1-oem/)
- [VMware ESXi 7.0 Unlocker standard & Custom Image](https://sysin.org/blog/vmware-esxi-7-ome/)

## 1. Introduction

Unlocker 3 for ESXi is designed for VMware ESXi 6.5, 6.7 and 7.0

The patch code carries out the following modifications dependent on the product being patched:

- Fix vmware-vmx to allow macOS to boot
- Fix libvmkctl to allow vSphere to control the guest

The code is written in Python as it makes the Unlocker easier to run and maintain on ESXi.

> IMPORTANT:
>
> Always uninstall the previous version of the Unlocker before using a new version. Failure to do this could render VMware unusable.

## 2. Installation

Copy the distribution file to the ESXi host datastore using scp or some other data transfer system. If you want to use the source version (i.e. from GIT) see "5. Building" fist.

Decompress the file from the ESXi console or via SSH:

    tar xzvf esxi-unlocker-xxx.tgz

(xxx - will be the version number, for example, 300)

Run the command from the terminal:

    ./esxi-install.sh

Finally reboot the server.

## 3. Uninstallation

Open the ESXi console or login via SSH and change to the folder where the files were extracted.

Run the command from the terminal:

    ./esxi-uninstall.sh

Finally reboot the server.

## 4. Notes

A. There is a command added called esxi-smctest.sh which can show if the patch is successful. It must be run from a terminal or SSH session. The output should be:

    /bin/vmx
    smcPresent = true
    custom.vgz     false   32486592 B

> Note: The uncompressed size reported for custom.vgz will vary depending on the ESXi version.

B. The unlocker can be temporarily disabled during boot by editing the boot options and adding "nounlocker".

## 5. Building

If you want to use a version which is not availbale as a distribution (e.g. the code from "master" branch) you need to first build the package.

Checkout the repository:

    git clone https://github.com/netgc/esxi-unlocker.git

(if you don't have git installed you can download ZIP archive from GitHub instead)

Enter the directory and build:

    cd esxi-unlocker
    ./esxi-build.py

If everything went correctly the ouput should be:

    ESXi-Build for macOS

    Timestamping files...

    Creating unlocker.tgz...
    etc/
    etc/rc.local.d/
    etc/rc.local.d/unlocker.py

    Creating esxi-unlocker-300.tgz...
    unlocker.tgz
    esxi-install.sh
    esxi-uninstall.sh
    esxi-smctest.sh
    readme.txt

The package you need to copy in the example above is esxi-unlocker-300.tgz (NOT unlocker.tgz!).

## 6. Thanks

Thanks to Zenith432 for originally building the C++ unlocker and Mac Son of Knife (MSoK) for all the testing and support.

Thanks also to Sam B for finding the solution for ESXi 6 and helping me with debugging expertise. Sam also wrote the code for patching ESXi ELF files and modified the unlocker code to run on Python 3 in the ESXi 6.5 environment.

## 7. History

- 26/09/2018 3.0.0 - First release
- 01/05/2020 3.0.1 - Fix for ESXi 7.0
- 10/18/2020 3.0.2 - Fix for ESXi 7.0 U1 (7.0.1)
- 10/17/2020 3.0.3 - Fix for ESXi 7.0 U3 (7.0.3)
- 02/05/2022 3.0.5 - Fix for ESXi 7.0 U3c (7.0.3)

(c) 2011-2018 Dave Parsons

Powered by [sysin.org](https://sysin.org/)
