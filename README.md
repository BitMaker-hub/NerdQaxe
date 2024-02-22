# Qaxe 

Qaxe is a  quad-BM1366 Miner based on the [PiAxe](https://github.com/shufps/piaxe) and [BitAxe](https://github.com/skot/bitaxe/tree/ultra-v1.3).

![image](https://github.com/shufps/qaxe/assets/3079832/4f741daf-940c-4ba4-a477-e8de91f4513c)

**rev1:** is tested and operating at about 1.7TH/s average speed.<br>
**rev2:** working fine with the expected speed of ~1.8TH/s avg after some minor modifications (330µF caps are wrongly placed, see rev3)<br>
**rev3:** Fixed Caps placement and added Boot-Switch. It should put the STM32 into DFU bootloader but not tested yet.


ASICs
=====

The QAxe uses 4 ASICs of type BM1366.

![image](https://github.com/shufps/qaxe/assets/3079832/da4b85cf-e7ba-4073-ae0d-08c4e82d4b8e)

Installation via CMSIS-DAP Programmer
=====================================

As programming/debug adapter the Picoprobe firmware running on a Raspi Pico works best: <br>
https://github.com/rp-rs/rp2040-project-template/blob/main/debug_probes.md / https://github.com/raspberrypi/picoprobe/releases/tag/picoprobe-cmsis-v1.0.3
<br>
<br>
There also is a little board with only 3 parts that gives a nice low-cost solution to flash the Qaxe:<br>
https://github.com/shufps/raspi-pico-dap

On `rev3` there should be the option to boot the stm32 (by pressing the `boot`-button on reset) into DFU-Bootloader mode what makes flashing via USB and without CMSIS-DAP programmer possible.

## Compiling and Flashing

Instructions for flashing using the CMSIS-DAP adapter:

```bash
# install curl
sudo apt install curl

# install rust
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh

# add to ~/.bash.rc (afterwards, opening a new terminal is needed)
echo 'source "$HOME/.cargo/env"' >> ~/.bashrc

# clone repository
git clone https://github.com/shufps/qaxe

# clone submodules
cd qaxe
git submodule init
git submodule update

# add rust target for rev2/3
rustup target add thumbv7m-none-eabi

# or add rust target for rev1
rustup target add thumbv6m-none-eabi

# build firmware for rev2
cd firmware/fw-rev2
# or
cd firmware/fw-rev3
./build.sh

# run firmware (this also flashes it to the stm32)
./run.sh

```

Installation via USB Bootloader on rev3
=======================================
The STM32L151CC variant has an integrated DFU Bootloader that should be started when pressing the `boot` button during reset.

Afterwards it should be possible to flash the firmware without CMSIC-DAP:

```
# install cargo-binutils and llvm tools
cargo install cargo-binutils
rustup component add llvm-tools-preview

# create the firmware.bin
cargo objcopy --release --bin qaxe -- -O binary qaxe-rev3.bin

# install dfu-utils
sudo apt-get install dfu-util

now start the stm32 in DFU mode by pressing `boot` on the `rev3` board (only works with the STM32L151CC variant)

# after booting, list the devices
dfu-util --list

# flash the binary
dfu-util -a 0 -s 0x08000000:leave -D qaxe-rev2.bin
```

Mining Client
=============

![image](https://github.com/shufps/qaxe/assets/3079832/5afb98b6-9153-454f-adc0-137706cad032)




Stratum Mining Client:<br>
https://github.com/shufps/piaxe-miner

Misc
====
If you like this project and want to support future work, feel free to donate to:
`bc1q29hp4fqtks2wzpmfwtpac64fnr8ujw2nvnra04`
