# Device Tree for OnePlus 6 (enchilada)

The OnePlus 6 (codenamed _"enchilada"_) is a flagship smartphone from OnePlus.
It was released in May 2018.

| Basic                   | Spec Sheet                                                                                                                     |
| -----------------------:|:------------------------------------------------------------------------------------------------------------------------------ |
| CPU                     | Octa-core (4x2.8 GHz Kryo 385 Gold & 4x1.7 GHz Kryo 385 Silver)                                                                |
| Chipset                 | Qualcomm SDM845 Snapdragon 845                                                                                                 |
| GPU                     | Adreno 630                                                                                                                     |
| Memory                  | 6/8 GB RAM                                                                                                                     |
| Shipped Android Version | 8.1                                                                                                                            |
| Storage                 | 64/128/256 GB                                                                                                                  |
| Battery                 | Non-removable Li-Po 3300 mAh battery                                                                                           |
| Display                 | Optic AMOLED, 1080 x 2280 pixels, 19:9 ratio (~402 ppi density)                                                                |
| Camera (Back)           | Dual: 16 MP (f/1.7, 27mm, 1/2.6", 1.22µm, gyro-EIS, OIS) + 20 MP (16 MP effective, f/1.7, 1/2.8", 1.0µm), PDAF, dual-LED flash |
| Camera (Front)          | 16 MP (f/2.0, 25mm, 1/3", 1.0µm), gyro-EIS, Auto HDR, 1080p                                                                    |

Copyright 2018 - The LineageOS Project.

![OnePlus 6](https://cdn2.gsmarena.com/vv/pics/oneplus/oneplus-6-5.jpg "OnePlus 6")


## Build instructions

You will need Ubuntu 16.04 to build custom ROMs. You need some knowledge about Github and Linux commands. If you do not know that then don't worry I will teach you some basics here. But if you want to learn like a pro then just Google it. You also require a GitHub Account.

RAM :8GB OR Higher.
Storage :200GB?+

Enter these commands to get your system ready for building:

sudo su

add-apt-repository ppa:openjdk-r/ppa  (press enter when you are asked to)

apt-get update

apt-get install bison build-essential curl ccache flex lib32ncurses5-dev lib32z1-dev libesd0-dev libncurses5-dev libsdl1.2-dev libxml2 libxml2-utils lzop pngcrush schedtool squashfs-tools xsltproc zip zlib1g-dev git-core make phablet-tools gperf openjdk-8-jdk -y

exit

mkdir ~/bin

PATH=~/bin:$PATH

cd ~/bin

curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo

chmod a+x ~/bin/repo

git clone https://github.com/akhilnarang/scripts.git scripts

cd scripts

bash setup/android_build_env.sh    (You will be asked to enter your GitHub username and email here. Enter it in.)

mkdir ancient

cd ancient

repo init -u https://github.com/Ancient-Lab/manifest -b ten

repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags    (You will now need to wait for maybe an hour.)

sudo git clone https://github.com/AshutoshSundresh/ancient_device_oneplus_enchilada -b ten device/oneplus/enchilada

sudo git clone https://github.com/ancient-devices/device_oneplus_sdm845-common -b ten device/oneplus/sdm845-common

sudo git clone https://github.com/ancient-devices/vendor_google_camera -b ten vendor/google/camera

sudo git clone https://github.com/ancient-devices/kernel_oneplus_sdm845 -b ten kernel/oneplus/sdm845

sudo git clone https://github.com/ancient-devices/device_oneplus_common -b ten device/oneplus/common

sudo git clone https://github.com/AshutoshSundresh/vendor_oneplus -b ten vendor/oneplus

sudo git clone https://gitlab.com/PixelExperience/packages_apps_PixelLiveWallpaper -b ten packages/apps/PixelLiveWallpaper

. build/envsetup.sh

export USE_CCACHE=1 && ccache -M 50G && export CONFIG_STATE_NOTIFIER=y && export SELINUX_IGNORE_NEVERALLOWS=true

lunch ancient_enchilada-userdebug

mka bacon              (This may take upto 8 hours so stay put. If you get errors, feel free to ask the ANCIENT OFFICIAL FAJITA group.)

cd out/target/product/enchilada

ls            (You can now see the ROM filename. Copy the name. You must have a Mega account for the next step.)

sudo apt-get install ruby gem

sudo gem install rmega

rmega-up 'filename' -u 'email address'       (Replace filename and email address with your values. Simply download from your Mega account and voila! Good luck!)
 





