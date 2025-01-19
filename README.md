# Android-Automotive-OS for Rasbperry Pi 4
This guide provides step-by-step instructions for building and installing Android Automotive OS and flashing on SD Card for a Raspberry Pi 4, suitable for developers and enthusiasts interested in experimenting with in-vehicle infotainment systems on affordable hardware.

## 1. Prerequisites
List the necessary hardware and software requirements:
- Computer with Linux or macOS
- Minimum (more than)16GB RAM and 400GB free disk space (my recommendation is 32 or 64 is the best)
- Stable internet connection
- Java Development Kit (JDK) 8 or higher

- [official rquirements](https://source.android.com/docs/setup/start/requirements)

## 2. Installation Steps
### 2.1 Set up the environment
```
bash
mkdir ~/bin
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
export PATH=~/bin:$PATH
```
### 2.2 Install packages
```
sudo apt-get install bc coreutils dosfstools e2fsprogs fdisk kpartx mtools ninja-build pkg-config python3-pip rsync
sudo pip3 install meson mako jinja2 ply pyyaml dataclasses
```
### 2.3 Download the Android source code
```
mkdir ~/android-automotive
cd ~/android-automotive
repo init -u https://android.googlesource.com/platform/manifest -b android-15.0.0_r10
curl -o .repo/local_manifests/manifest_brcm_rpi.xml -L https://raw.githubusercontent.com/raspberry-vanilla/android_local_manifest/android-15.0/manifest_brcm_rpi.xml --create-dirs
repo sync
```
### 2.4  Configure the build
```
source build/envsetup.sh
lunch aosp_rpi4-ap4a-userdebug
```

### 2.5 Build Android Automotive OS
```
make bootimage systemimage vendorimage -j$(nproc)
```

## 3. Making Flashable image
```
./rpi4-mkimg.sh
```
## 4. Flash the image in the SD Card
- for this purpose I have used [Balena Etcher](https://etcher.balena.io/)

## Useful Links
- https://medium.com/make-android/android-automotive-os-14-on-a-raspberry-pi-4-e83b2f8ca353
- https://github.com/raspberry-vanilla/android_local_manifest?tab=readme-ov-file


  

  

