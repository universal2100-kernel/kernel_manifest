# **Exynos 2100 Kernel Build System**

This script automates the process of compiling and signing a custom kernel for **Samsung Exynos 2100 devices** (`o1s`, `p3s`, `t2s`). It handles everything from **kernel compilation, DTBO/DTB creation, vendor_boot packaging, and AVB signing**.


## Sync Repository

```
repo init -u https://github.com/universal2100-kernel/kernel_manifest/ -b main
repo sync
```

## Generate AVB Keys

```
# Navigate to the root directory of the project
mkdir keys && cd keys

# Generate a 4096-bit RSA private key
openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:4096

# Extract the public key
openssl rsa -in private_key.pem -pubout -out public_key.pem
```

--> you can also import those keys from your rom builds.

## Build kernel

it's as simple as:
```
./build.sh
```


## Why this build system

Since Google Pixel phones use a kernel build system that generates all the necessary kernel images (e.g., boot.img, vendor_boot.img, dtbo.img), I've found it to be very practical and helpful for testing new kernel patches.
For the same reason, I decided to create my own build system for the GKI 1.0 Samsung kernel.
