# SETUP VSCODE 

<br/>

* TEST Board and Envs 
    * ESP-IDF:5.4.0
    * UART (left) not USB 
    * ESP32-S3-DevKitC-1        

<br/>

![](../../esp-radar/console_test/docs/setup/esp32-s3_devkit_00.png)

<br/>

[Go Back ESP32-S TEST](../../../ESP32-S3_TEST.md)  

<br/>

* TEST 
  * only check ESP32-S3 CSI data 

<br/>

## SETUP VSCODE Setup  in Window 

<br/>

* Please check your setting.json if you use VSCode based ESP-IDF in Window

<br/>

.vscode/settings.json 
```
  "idf.openOcdConfigs": [
    "interface/ftdi/esp32_devkitj_v1.cfg",
    "target/esp32s3.cfg"
  ],

  "idf.portWin": "COM4",
  "idf.customExtraVars": {
    "OPENOCD_SCRIPTS": "----(PATH based on Window Your profile)\.espressif\\tools\\openocd-esp32\{xxxxxx}",
    "IDF_CCACHE_ENABLE": "1",
    "ESP_ROM_ELF_DIR": "----(PATH based on Window Your profile)\.espressif\\tools\\esp-rom-elfs\{xxxxxx}",
    "IDF_TARGET": "esp32s3"
  },
```

<br/>

![](../../esp-radar/console_test/docs/setup/vscode_setup_00.png)

<br/>

## Setup Build/Monitor in VSCODE 

<br/>

have to use ESP-IDF Termianl , not used Power Shell 


* Build Radar Setup 

```ESP-IDF Terminal in Window   
cd .\examples\get-started\csi_recv_router\
esp-csi\examples\get-started\csi_recv_router>  idf.py --version                # Check ESP-IDF Version 
esp-csi\examples\get-started\csi_recv_router>  idf.py set-target esp32s3       # Setup your CPU  and create sdkconfig 
```

<br/>

* Please check your CPU and WIFI SSID/PW in sdkconfig 
```ESP-IDF Terminal in Window
esp-csi\examples\get-started\csi_recv_router> idf.py menuconfig               # edit sdkconfig based on sdkconfig.defaults and IDF_TARGET in your json 
```
Example Connection Configuration --> 
```
CONFIG_EXAMPLE_WIFI_SSID="myssid"
CONFIG_EXAMPLE_WIFI_PASSWORD="mypassword"
```

<br/>

*  Build and Flash 
```ESP-IDF Terminal in Window

esp-csi\examples\get-started\csi_recv_router> idf.py build
esp-csi\examples\get-started\csi_recv_router> idf.py -p COM4 flash -b 921600 # Serial COM4 
```

<br/>

* Option-Project Fullclean or clean 
```ESP-IDF Terminal in Window
esp-csi\examples\get-started\csi_recv_router> idf.py fullclean # remove all build 
esp-csi\examples\get-started\csi_recv_router> idf.py clean     # remove build 
```


<br/>

* Check Working 
```
esp-csi\examples\get-started\csi_recv_router> idf.py -p COM4 monitor
```


````
> idf.py -p COM4 monitor         
Executing action: monitor
Running idf_monitor in directory D:\Works\Project_personal\esp-csi\examples\get-started\csi_recv_router
Executing "C:\Users\jhlee\.espressif\python_env\idf5.4_py3.11_env\Scripts\python.exe C:\Users\jhlee\esp\v5.4\esp-idf\tools/idf_monitor.py -p COM4 -b 921600 --toolchain-prefix xtensa-esp32s3-elf- --target esp32s3 --revision 0 D:\Works\Project_personal\esp-csi\examples\get-started\csi_recv_router\build\csi_recv_router.elf --force-color -m 'C:\Users\jhlee\.espressif\python_env\idf5.4_py3.11_env\Scripts\python.exe' 'C:\Users\jhlee\esp\v5.4\esp-idf\tools\idf.py' '-p' 'COM4'"...
--- Warning: GDB cannot open serial ports accessed as COMx
--- Using \\.\COM4 instead...
--- esp-idf-monitor 1.5.0 on \\.\COM4 921600
--- Quit: Ctrl+] | Menu: Ctrl+T | Help: Ctrl+T followed by Ctrl+H
����������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������I (27) boot: ESP-IDF v5.4 2nd stage bootloader
I (27) boot: compile time Oct 17 2025 18:16:06
I (27) boot: Multicore bootloader
I (27) boot: chip revision: v0.1
I (27) boot: efuse block revision: v1.2
I (27) boot.esp32s3: Boot SPI Speed : 80MHz
I (28) boot.esp32s3: SPI Mode       : DIO
I (28) boot.esp32s3: SPI Flash Size : 2MB
I (29) boot: Enabling RNG early entropy source...
I (29) boot: Partition Table:
I (30) boot: ## Label            Usage          Type ST Offset   Length
I (30) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (31) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (32) boot:  2 factory          factory app      00 00 00010000 00100000
I (33) boot: End of partition table
I (33) esp_image: segment 0: paddr=00010020 vaddr=3c090020 size=1935ch (103260) map
I (53) esp_image: segment 1: paddr=00029384 vaddr=3fc98b00 size=04860h ( 18528) load
I (57) esp_image: segment 2: paddr=0002dbec vaddr=40374000 size=0242ch (  9260) load
I (59) esp_image: segment 3: paddr=00030020 vaddr=42000020 size=81d28h (531752) map
I (153) esp_image: segment 4: paddr=000b1d50 vaddr=4037642c size=1263ch ( 75324) load
I (170) esp_image: segment 5: paddr=000c4394 vaddr=600fe100 size=0001ch (    28) load
I (178) boot: Loaded app from partition at offset 0x10000
I (178) boot: Disabling RNG early entropy source...
I (180) cpu_start: Multicore app
I (189) cpu_start: Pro cpu start user code
I (189) cpu_start: cpu freq: 240000000 Hz
I (189) app_init: Application information:
I (189) app_init: Project name:     csi_recv_router
I (189) app_init: App version:      6d74377-dirty
I (190) app_init: Compile time:     Oct 17 2025 18:24:46
I (191) app_init: ELF file SHA256:  eaabdf17e...
I (191) app_init: ESP-IDF:          v5.4
I (192) efuse_init: Min chip rev:     v0.0
I (192) efuse_init: Max chip rev:     v0.99
I (193) efuse_init: Chip rev:         v0.1
I (193) heap_init: Initializing. RAM available for dynamic allocation:
I (194) heap_init: At 3FCA1000 len 00048710 (289 KiB): RAM
I (195) heap_init: At 3FCE9710 len 00005724 (21 KiB): RAM
I (195) heap_init: At 3FCF0000 len 00008000 (32 KiB): DRAM
I (196) heap_init: At 600FE11C len 00001ECC (7 KiB): RTCRAM
I (197) spi_flash: detected chip: generic
I (197) spi_flash: flash io: dio
W (198) spi_flash: Detected size(8192k) larger than the size in the binary image header(2048k). Using the size in the binary image header.
I (199) sleep_gpio: Configure to isolate all GPIO pins in sleep state
I (200) sleep_gpio: Enable automatic switching of GPIO sleep configuration
I (201) main_task: Started on CPU0
I (247) main_task: Calling app_main()
I (254) example_connect: Start example_connect.
I (255) pp: pp rom version: e7ae62f
I (256) net80211: net80211 rom version: e7ae62f
I (257) wifi:wifi driver task: 3fcaac90, prio:23, stack:6656, core=0
I (259) wifi:wifi firmware version: 48ea317a7
I (259) wifi:wifi certification version: v7.0
I (260) wifi:config NVS flash: enabled
I (260) wifi:config nano formatting: disabled
I (260) wifi:Init data frame dynamic rx buffer num: 128
I (261) wifi:Init static rx mgmt buffer num: 5
I (261) wifi:Init management short buffer num: 32
I (262) wifi:Init dynamic tx buffer num: 32
I (262) wifi:Init static tx FG buffer num: 2
I (263) wifi:Init static rx buffer size: 2212
I (263) wifi:Init static rx buffer num: 10
I (264) wifi:Init dynamic rx buffer num: 128
I (265) wifi_init: accept mbox: 6
I (265) wifi_init: tcpip mbox: 32
I (265) wifi_init: udp mbox: 6
I (265) wifi_init: tcp mbox: 6
I (266) wifi_init: tcp tx win: 5760
I (266) wifi_init: tcp rx win: 5760
I (266) wifi_init: tcp mss: 1440
I (267) wifi_init: WiFi IRAM OP enabled
I (267) wifi_init: WiFi RX IRAM OP enabled
I (269) phy_init: phy_version 680,a6008b2,Jun  4 2024,16:41:10
I (305) wifi:mode : sta (f4:12:fa:f9:80:54)
I (306) wifi:enable tsf
I (308) example_connect: Connecting to JHLEE_AP...
W (308) wifi:Password length matches WPA2 standards, authmode threshold changes from OPEN to WPA2
I (310) example_connect: Waiting for IP(s)
I (3001) wifi:new:<2,1>, old:<1,0>, ap:<255,255>, sta:<2,1>, prof:1, snd_ch_cfg:0x0
I (3003) wifi:state: init -> auth (0xb0)
I (3009) wifi:state: auth -> assoc (0x0)
I (3013) wifi:state: assoc -> run (0x10)
I (3022) wifi:connected with JHLEE_AP, aid = 15, channel 2, 40U, bssid = 90:9f:33:d4:80:0a
I (3022) wifi:security: WPA2-PSK, phy: bgn, rssi: -31
I (3023) wifi:pm start, type: 1

I (3023) wifi:dp: 1, bi: 102400, li: 3, scale listen interval from 307200 us to 307200 us
I (3024) wifi:set rx beacon pti, rx_bcn_pti: 0, bcn_timeout: 25000, mt_pti: 0, mt_time: 10000
I (3066) wifi:AP's beacon interval = 102400 us, DTIM period = 3
I (4064) esp_netif_handlers: example_netif_sta ip: 192.168.1.59, mask: 255.255.255.0, gw: 192.168.1.1
I (4064) example_connect: Got IPv4 event: Interface "example_netif_sta" address: 192.168.1.59
I (4255) example_connect: Got IPv6 event: Interface "example_netif_sta" address: fe80:0000:0000:0000:f612:faff:fef9:8054, type: ESP_IP6_ADDR_IS_LINK_LOCAL
I (4255) example_common: Connected to example_netif_sta
I (4256) example_common: - IPv4 address: 192.168.1.59,
I (4257) example_common: - IPv6 address: fe80:0000:0000:0000:f612:faff:fef9:8054, type: ESP_IP6_ADDR_IS_LINK_LOCAL
I (4258) csi_recv_router: got ip:192.168.1.59, gw: 192.168.1.1
I (4260) main_task: Returned from app_main()
I (4260) csi_recv_router: ================ CSI RECV ================
type,id,mac,rssi,rate,sig_mode,mcs,bandwidth,smoothing,not_sounding,aggregation,stbc,fec_coding,sgi,noise_floor,ampdu_cnt,channel,secondary_channel,local_timestamp,ant,sig_len,rx_state,len,first_word,data
CSI_DATA,0,90:9f:33:d4:80:0a,-42,11,1,7,1,0,1,0,1,0,1,-95,0,2,1,4260728,0,82,0,128,0,"[0,0,0,0,0,0,0,0,0,0,0,0,6,2,5,1,5,0,5,-1,5,-3,5,-4,6,-6,7,-7,9,-8,10,-8,11,-8,12,-7,13,-6,13,-5,12,-4,11,-3,9,-3,7,-3,5,-3,3,-5,1,-6,0,-8,-1,-10,-1,-13,0,-14,1,-15,0,0,3,-16,4,-15,4,-14,4,-13,4,-11,3,-9,1,-7,-1,-6,-3,-4,-6,-4,-8,-3,-10,-3,-12,-4,-13,-5,-14,-6,-15,-7,-15,-8,-14,-8,-13,-8,-11,-8,-9,-7,-8,-5,-7,-3,-6,-1,-5,2,-5,4,0,0,0,0,0,0,0,0,0,0]"
CSI_DATA,1,90:9f:33:d4:80:0a,-42,11,1,7,1,0,1,0,1,0,1,-95,0,2,1,4269273,0,83,0,128,0,"[0,0,0,0,0,0,0,0,0,0,0,0,-4,-6,-4,-5,-4,-4,-5,-3,-6,-1,-7,0,-8,0,-10,1,-11,0,-12,0,-13,-1,-13,-2,-14,-3,-13,-4,-12,-4,-10,-4,-9,-4,-7,-3,-6,-1,-5,1,-5,3,-5,5,-5,7,-6,9,-7,9,-9,10,0,0,-11,10,-11,9,-11,8,-10,6,-9,5,-7,4,-5,4,-3,4,0,4,2,5,4,5,6,7,7,8,7,9,8,10,7,11,7,12,6,12,5,11,4,10,4,9,3,7,3,5,4,2,4,0,6,-2,0,0,0,0,0,0,0,0,0,0]"
CSI_DATA,2,90:9f:33:d4:80:0a,-42,11,1,7,1,0,1,0,1,0,1,-95,0,2,1,4274233,0,83,0,128,0,"[0,0,0,0,0,0,0,0,0,0,0,0,-6,-5,-6,-4,-5,-3,-5,-1,-6,0,-7,1,-8,2,-10,3,-11,3,-13,3,-14,3,-14,2,-15,1,-14,0,-13,-1,-12,-2,-10,-2,-8,-1,-7,1,-5,2,-4,4,-4,7,-4,9,-4,11,-5,12,-6,13,0,0,-8,13,-9,12,-9,11,-9,9,-8,8,-6,6,-4,5,-2,4,1,4,3,4,5,5,7,5,9,7,10,8,10,9,10,10,10,10,9,11,8,10,7,10,6,8,5,6,4,4,4,2,5,-1,5,-3,0,0,0,0,0,0,0,0,0,0]"
CSI_DATA,3,90:9f:33:d4:80:0a,-42,11,1,7,1,0,1,0,1,0,1,-95,0,2,1,4280121,0,83,0,128,0,"[0,0,0,0,0,0,0,0,0,0,0,0,-7,-1,-7,-1,-6,0,-5,1,-5,3,-5,5,-5,6,-6,8,-7,9,-9,9,-10,9,-11,9,-12,8,-12,7,-12,6,-11,5,-9,4,-7,4,-5,4,-3,4,-1,6,1,7,2,9,3,11,3,12,3,14,0,0,1,15,0,14,-1,14,-2,12,-2,10,-1,8,0,6,1,4,3,2,5,1,7,0,9,0,11,0,13,0,14,1,15,2,14,2,14,3,13,3,12,3,10,3,8,2,6,0,4,-2,3,-4,3,-6,0,0,0,0,0,0,0,0,0,0]"
CSI_DATA,4,90:9f:33:d4:80:0a,-42,11,1,7,1,0,1,0,1,0,1,-95,0,2,1,4289954,0,83,0,128,0,"[0,0,0,0,0,0,0,0,0,0,0,0,-5,-5,-5,-5,-5,-4,-5,-2,-6,-1,-7,0,-9,1,-10,1,-11,1,-13,1,-14,0,-14,-1,-15,-2,-14,-3,-13,-4,-11,-4,-10,-3,-8,-2,-7,-1,-5,2,-5,4,-5,6,-5,8,-6,9,-8,10,-9,11,0,0,-11,11,-11,10,-11,9,-10,7,-9,6,-7,5,-5,4,-3,4,0,4,2,5,4,6,6,7,7,8,8,10,8,11,8,12,7,12,7,13,6,12,5,11,4,9,4,7,3,5,4,3,4,0,6,-2,0,0,0,0,0,0,0,0,0,0]"
CSI_DATA,5,90:9f:33:d4:80:0a,-41,11,1,7,1,0,1,0,1,0,1,-95,0,2,1,4300499,0,83,0,128,0,"[0,0,0,0,0,0,0,0,0,0,0,0,-6,-3,-6,-3,-5,-2,-5,0,-6,1,-6,3,-7,4,-8,5,-9,5,-11,6,-12,5,-13,5,-13,4,-13,3,-12,2,-11,1,-10,1,-8,1,-6,2,-4,3,-2,5,-2,7,-1,8,-1,10,-2,12,-2,13,0,0,-4,14,-5,13,-6,12,-6,10,-5,9,-4,7,-2,5,0,4,2,3,4,3,6,2,8,3,10,3,11,4,12,5,12,6,12,7,12,7,10,7,9,7,7,6,6,4,5,2,4,0,4,-2,4,-5,0,0,0,0,0,0,0,0,0,0]"
CSI_DATA,6,90:9f:33:d4:80:0a,-41,11,1,7,1,0,1,0,1,0,1,-95,0,2,1,4309977,0,83,0,128,0,"[0,0,0,0,0,0,0,0,0,0,0,0,3,4,3,4,3,3,4,1,5,0,6,-1,7,-1,9,-2,10,-1,11,-1,12,0,12,1,13,2,12,3,11,3,9,4,8,3,6,2,5,0,4,-2,4,-4,4,-6,5,-8,6,-10,7,-10,8,-11,0,0,10,-10,10,-9,10,-9,9,-7,8,-6,6,-5,4,-4,2,-4,0,-5,-3,-6,-4,-7,-6,-8,-7,-9,-8,-11,-8,-12,-7,-13,-7,-13,-6,-13,-5,-13,-4,-12,-4,-10,-4,-8,-4,-6,-4,-4,-5,-2,-7,1,0,0,0,0,0,0,0,0,0,0]"
CSI_DATA,7,90:9f:33:d4:80:0a,-42,11,1,7,1,0,1,0,1,0,1,-95,0,2,1,4319929,0,83,0,128,0,"[0,0,0,0,0,0,0,0,0,0,0,0,6,2,5,2,5,1,4,-1,5,-2,5,-4,6,-5,8,-6,9,-7,11,-7,11,-7,12,-6,13,-5,13,-4,12,-3,11,-2,9,-2,7,-2,5,-3,3,-4,2,-6,1,-8,0,-10,0,-12,1,-13,2,-15,0,0,4,-15,5,-14,5,-13,5,-12,4,-10,4,-8,2,-7,0,-5,-3,-4,-5,-4,-7,-4,-10,-4,-11,-5,-13,-6,-13,-7,-14,-8,-13,-9,-13,-9,-11,-9,-10,-8,-9,-7,-7,-6,-6,-4,-5,-1,-5,1,-6,4,0,0,0,0,0,0,0,0,0,0]"  
CSI_DATA,8,90:9f:33:d4:80:0a,-42,11,1,7,1,0,1,0,1,0,1,-95,0,2,1,43299
````
* [Manual](README.md)  