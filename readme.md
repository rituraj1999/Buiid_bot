

First of all have a brief look at xda threads about compiling rom from source dont follow all stuff from there tho.. just have a look on those threads specially that jackeagle thread. 

now first what you need :
    If on local
   -> Fast internet connection (fast enough to download 50GB rom source without waiting for a day or two xD )
   -> 4core cpu(or higher)
   -> 8gb minimum ram 
   -> Linux (Ubuntu for this guide)
   -> storage : 80GB + 50 to 100GB (rom source(approx) + Compiling space and ccache)
   if using ssh or cloud
 then above specs + more spec wiill be cool.. 

Now what is buildbot ?
- this guide wont make you developer you can become buildbot which is making rom frrom source with already made sources such as device tree and fixes for such stuff .. inshort total kanging lmao xD... 


After installing linux .. Need to setup environment for compiling 
for that  if on locally then start without sudo -s 

if on ssh(Gcloud) then first type 
     sudo -s   
this will let you enter in root... There is a guide on xda how to setup Gcloud for rom deving.. 

now Get yourself fimiliar with Basic Linux... 
if u donno how to use linux .. then leave reading this post :P


now install the required packages >.. just copy and paste the given command 


for setting environment 


sudo apt-get update && sudo apt-get upgrade 

sudo dpkg --add-architecture i386

sudo apt-get update && sudo apt-get upgrade 

sudo apt-get install bc bison build-essential curl flex g++-multilib gcc-multilib git gnupg gperf lib32ncurses5-dev lib32readline6-dev lib32z1-dev libesd0-dev
liblz4-tool libncurses5-dev libsdl1.2-dev libwxgtk2.8-dev libxml2 libxml2-utils lzop pngcrush schedtool squashfs-tools xsltproc zip zlib1g-dev imagemagick

sudo apt-get update && sudo apt-get upgrade 

sudo add-apt-repository ppa:webupd8team/java
sudo apt install oracle-java8-installer

you can use openjdk-8-jdk too 
then , 

sudo ln -s /usr/lib/i386-linux-gnu/mesa/libGL.so.1 /usr/lib/i386-linux-gnu/libGL.so

now .. edit bashrc

nano ~/.bashrc 

and then add given 2 lines at end of bashrc

export PATH=~/bin:$PATH
export USE_CCACHE=true

then Ctrl+O to save and press enter then Ctrl+X to exit(basic linux ya'know)
at last ..


mkdir ~/bin && curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo && chmod a+x ~/bin/repo







here environment is set.. 

Now make a directory and name it anything accordingly to rom name (lineage for here) 

cd ~/ && mkdir los && cd los

now we have to clone source code .. 

for that in the rom main dir( los in this guide)


goto their github page suppose github.com/LineageOS/android for here ... 
choose the branch .. take Nougat if beginner .. 
then scroll down read their readme.md then u can see repo init command copy their command and execute .. 

you can see some lines will be shown in therminal and will ask for github username and email .. Just add (this is one time adding of github id fromnext time you will just shown as your id this and username this)

then type 
  repo sync 
or 
  repo sync -c --no-tags --no-clone-bundle --force-sync 
you will be used to with second one 


then wait for some minutes if on ssh server or wait for several hours or days if locally (depends on your internet connection)


after source gets sync clone your device tree, vendor blobs, and kernel sources from your lead dev :P .. we are kangers tho xD 
for that lets learn git a little >>

git clone <url> -b <branch-name> <file-path>
 
for example for a device
git clone https://github.com/Username/android_device_vendorname_devicename -b branchname device/vendorname/devicename

eg. for mido 
git clone https://github.com/TheScarastic/android_device_xiaomi_mido -b cm-14.1 device/xiaomi/mido


here consider _ as /

other stuff like git status, cherry-picking , commiting pushing etc .. you have to learn from google.. 

after that clone kernel and vendor blobs as same way.. 
hint: you can find the required repos in .dependencies file 
so clone from there ... 
you can get vendor blobs from TheMuppets or ask your lead dev to give those stuff ... 

now rom other than lineage .. for example ... 


for glaze os, aicp or other lineage based roms .. 

most of changes are in device tree ... 

and those files are .. 
lineage.mk  to -> glaze.mk 
and change common vendor path in rom-name.mk 
 like call-inherit... vendor/cm/config/common_full_phone.mk to-> vendor/glaze/common.mk (for glaze os here.. you can check for other official devices on the rom repo ... )
then change in PRODUCT_NAME from lineage_mido to glaze_mido and some other shits... 


for some aosp based roms like JDC and Aex you need to make these achanges along with some additional change like adding AndroidProducts.mk etc.. 

then after clonning 

you have to bringup your device in rom source ..

for that initiate with ... 

./build/envsetup.sh

this will include all build makefiles .. which required for bringup .. 


then for your device type

breakfast lineage_mido-userdebug 


there are 2 ways to bringup breakfast and lunch 
eg. lunch aicp_kenzo-userdebug 

then you can see your device info on screen ... 
if not and saw some errors like romname_devicename not found 
do you have proper manifest for this deice and etc.. then look for your device tree and correct it ... 

then ... 
for building type ... 

brunch devicename 
or 
make otapackage(for aosp roms such as aosp-caf)

sometimes u need to add like this too 
brunch nitrogen_kenzo-userdebug 
to start build ... 


after that wait for several hours to get compiled and you can see they will tell you where the rom is stored as .zip in output folder ... 
Tip: as you go further dont forget to learn gerrit and cherry-picking.. and reading errors .. 

I've found a good group to learn in telegram as @Android_Building ...

Havefun!! keep learning!
