# Compile and flash QMK - Keychron C3 Pro firmware 

### A quick & dirty way to create QMK firmware w/ Linux(Ubuntu 22.04,) using a Keychron QMK fork

#### *Disclaimer - There are surely better ways of doing this, but I couldn't find anything on the internet, so here we are...*

#### Below is my _very_ hacky way of getting QMK firmware flashed on the [Keychron C3 Pro](https://www.keychron.com/products/keychron-c3-pro-qmk-via-wired-mechanical-keyboard "Keychron C3 Pro") found on Amazon.
```
sudo apt install -y git python3-pip
python3 -m pip install --user qmk
qmk setup --home /home/user/Documents/qmk_firmware
sudo apt install libudev-dev
sudo apt install cmake
cd /home/user/Documents/
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
# -> unplug keyboard -> press button under space key -> plug keyboard back in -> keyboard should start flashing
```
