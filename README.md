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



Installation
=============

As programming/debug adapter the Picoprobe firmware running on a Raspi Pico works best: <br>
https://github.com/rp-rs/rp2040-project-template/blob/main/debug_probes.md / https://github.com/raspberrypi/picoprobe/releases/tag/picoprobe-cmsis-v1.0.3
<br>
<br>
There also is a little board with only 3 parts that gives a nice low-cost solution to flash the Qaxe:<br>
https://github.com/shufps/raspi-pico-dap


TBD

Mining Client
=============

![image](https://github.com/shufps/qaxe/assets/3079832/5afb98b6-9153-454f-adc0-137706cad032)




Stratum Mining Client:<br>
https://github.com/shufps/piaxe-miner

Misc
====
If you like this project and want to support future work, feel free to donate to:
`bc1q29hp4fqtks2wzpmfwtpac64fnr8ujw2nvnra04`
