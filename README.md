# QMK-Keychron_C3_Pro
Build Keychron C3 Pro QMK
# Quick and dirty way to compile and flash Keychron C3 Pro QMK firmware with linux (Ubuntu 22.04 and varients) 

*Disclaimer* There are surely better ways to do this, but I couldn't find anything on the internet about how to do this.
Below is my _very_ hacky way of getting this Keychron fork to work

sudo apt install -y git python3-pip
python3 -m pip install --user qmk
qmk setup --home /home/user/Documents/qmk_firmware
sudo apt install libudev-dev
sudo apt install cmake
cd ~/Downloads
git clone --branch keychron_c3_pro https://github.com/Keychron/qmk_firmware.git
cd /home/user/Documents/qmk_firmware/lib
git clone https://github.com/qmk/ChibiOS.git
rm -r chibios
mv ChibiOS chibios
cd /home/user/Documents/qmk_firmware/lib/
rm -r lufa
git clone https://github.com/abcminiuser/lufa.git
cd /home/user/Documents/qmk_firmware/
make git submodule
qmk compile -kb keychron/c3_pro/ansi/red -km default 
qmk flash -kb keychron/c3_pro/ansi/red -km default
unplug keyboard -> press button under space key -> plug keyboard back in -> should see keyboard flashing
