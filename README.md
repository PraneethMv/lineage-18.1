# Lineage OS 18.1 Build for LeEco 2 X526

Building in WSL - Ubuntu - Windows Subsystem for Linux

Followed this guide from XDA - https://xdaforums.com/t/guide-how-to-building-lineageos-for-an-unsupported-device.4419263/

All credit to the original poster - thisisludachris

# Step 1: Setup the environment.
sudo apt install -y bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev python-is-python3

mkdir -p ~/LineageProject/bin

mkdir -p ~/LineageProject/android/lineage

curl https://storage.googleapis.com/git-repo-downloads/repo > ~/LineageProject/bin/repo

chmod a+x ~/bin/repo

git config --global user.email "you@example.com"

git config --global user.name "Your Name"


Note: Before repo init - do this:

  cd ~
  
  PATH=~/LineageProject/bin:$PATH


Then:
cd ~/LineageProject/android/lineage

repo init -u https://github.com/LineageOS/android.git -b lineage-18.1

# Step 2: Get the device manifest file:
mkdir ~/LineageProject/android/lineage/.repo/local_manifests

Then copy the manifest files for the deivce into the local_manifests folder

For LeEco 2:

  git clone https://github.com/PraneethMv/lineage-18.1.git -b main .repo/local_manifests


Next: repo sync

# Step 3: Turn on caching to speed up build
mkdir ~/ccache

export CCACHE_DIR=~/ccache

export USE_CCACHE=1

export CCACHE_EXEC=/usr/bin/ccache

ccache -M 50G

# Step 4: Select Build
source ~/LineageProject/android/lineage/build/envsetup.sh

lunch


From the list select - lineageos_[codename}-userdebug

# Step 5: Prepare the output:
make clean

make apache-xml

make ims-common

# Step 6: Build it:
brunch [codename]

# Changes to Repo - Notes to self:
# 1 - VINTF
Reason: Switch VINTF manifests

Location: android_device_leeco_s2/proprietary-files-qc.txt

Change: 
