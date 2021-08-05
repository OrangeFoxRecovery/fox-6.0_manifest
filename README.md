# fox_6.0 (android-6.0) Based Manifest for OrangeFox Recovery #

### Notes ###
- This is NOT an Official Manifest.
- This Manifest uses the Official twrp-6.0 source, with a Patched Build System for OrangeFox, and the OFFICIAL OrangeFox `bootable/recovery` and `vendor/recovery` trees.
- The Build Environment Setup Guide Below, is the same till Step Number 4 (except for apt). For Other Linux Distros, Read [This](https://github.com/akhilnarang/scripts.git).


## How to Build ##
 1. ### Set up the Build Environment ###
    ```bash
    cd ~
    sudo apt install git aria2 -y
    git clone https://github.com/akhilnarang/scripts.git ~/scripts
    cd ~/scripts
    sudo bash setup/android_build_env.sh 
    ```
 2. ### Sync the OrangeFox (fox_6.0) Source ###
    ```bash
    mkdir ~/OrangeFox_6
    cd ~/OrangeFox_6
    repo init -u https://github.com/OrangeFoxRecovery/fox-6.0_manifest.git -b fox_6.0
    repo sync -j$(nproc --all) --force-sync
    ```
      #### Tip: ####
      - Use ```repo init --depth=1 -u https://github.com/OrangeFoxRecovery/fox-6.0_manifest.git -b fox_6.0``` to initialize a Shallow Clone to save Disk Space.
 3. ### Place Trees and Kernel
    #### For Example: (Yours may be Different) ####
    ```bash
    cd ~/OrangeFox_6
    git clone https://github.com/OrangeFoxRecovery/device_samsung_fortuna3g.git device/samsung/fortuna3g
    ```
 4. ### Build it! ###
    ```bash
    cd ~/OrangeFox_6
    . build/envsetup.sh
    export ALLOW_MISSING_DEPENDENCIES=true
    export FOX_USE_TWRP_RECOVERY_IMAGE_BUILDER=1
    export LC_ALL="C"
    export OF_LEGACY_SHAR512=1
    lunch omni_<device>-eng
    mka recoveryimage
    ```
       #### Notes: ####
       - If you are getting errors like "Keymaster2" during Compilation, run ```export OF_DISABLE_KEYMASTER2=1``` and then Build Again.
 5. ### Take your OrangeFox Build ###
       #### Find your build: ####
       ```bash
       cd ~/OrangeFox_6
       ls out/target/product/*/
       ```
 6. ### Enjoy! ###
    Now enjoy the Latest OrangeFox Recovery on an old device too! :)
## Credits: ##
- TeamWin - for TWRP Manifest
- The OrangeFox Team - for the Amazing Recovery!
- [@DarthJabba9](https://gitlab.com/DarthJabba9) - For the fox_6.0 Build System Patch File.
- [@Sushrut1101](https://github.com/Sushrut1101) - For adding the patches in a proper Manifest.
