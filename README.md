# Introduction
This project use NeuroSky Mindwave mobile 2 as EEG sensor to detect human brain wave, and use HC-05 bluetooth module to communicate with Arduino to control LED state. 

本專題使用NeuroSky Mindwave mobile 2 作為EEG感測器偵測腦電圖，並使用HC-05藍芽模組做為無線通訊界面，與Arduino做通訊，並且控制LED燈亮滅。 

# Material needed

Arduino UNO 

NeuroSky Mindwave Mobile 2 

LED 

220 ohm resistor 

USB-TTL cable 

wire

# How to use

First, make sure all your equipments works fine, then setup your HC-05 Bluetooth module using USB-TTL converter or Arduino UNO as below.
Second, connect the LED and resistor properly.
Third, upload the code for Arduino in this repositery.
Finally, you can mind control the LED, and test how concentrate you can.

# HC05 Bluetooth module setup

First, Connect the USB-TTL converter to your HC-05 BT module,  the TX of converter connect to RX of HC-05, RX of converter connect to TX of HC-05.
Second, use serial software such as RealTerm or Putty to transmit the AT commant to the bluetooth module.
Third, press the button on the module before powering up, then keep pressing until the LED on HC-05 start blinking slowly (about once per second).
This means HC-05 is operation in AT command mode.
Then, follow the guide below to  setup your HC-05 module.
1. Test your BT module is alive
Command: AT
Responce: OK
2. Set the baudrete of UART of HC-05 as 57600
Command: AT+UART=57600,0,0
Responce: OK
3. Assign HC-05 as Master (to connect to the Mindwave mobile)
Command: AT+ROLE=1
Responce:OK
4. Set the password of device (Mindwave mobile2), default maybe 0000 or 1234, you can use your smartphone or computer to confirm the password.
Command:AT+PSWD=0000
Responce:OK
5. Set the HC-05 can only connect to the specifict device.
Command:AT+CMODE=1
Responce:OK
6. Set the device ID of Mindwave Mobile2 (there is a sticker on the earphone)
Command: AT+BIND=2471,89,e9d8cb
Responce:OK
7. IAC setup
Command: AT+IAC=9e8b33
Responce: OK
8. CLASS setup
Command: AT+CLASS=0
Responce:OK
9. INQM setup
Command:AT+INQM=1,7,48
Responce:OK

After setting the module, turn off the Mindwave mobile 2, and ensure all of the device which connected to the headset are disconnected, or turned off.
Then repower the HC-05, the LED onboard will flash fast (about once per 500mS )
It means the HC-05 is operat in data mode.
Wait about 10s for HC-05 initialize, then turn on the mindwave mobile 2, if HC-05 and Mindwave mobile 2 are connected, the LED will fast flash twice per second and turning off.
If not, please check the command above, and double check the connection of your hardware and the password of the Mindwave mobile 2 using "AT+PSWD=(1234/0000)"
Now the basic setup of HC-05 is done, continue reading to connect the HC-05 with Arduino.

可以使用USB-TTL轉接線直接透過串列埠通訊軟體進行設定，或者將Arduino當作串列埠轉換器。
將藍芽模組的VCC TX RX GND 連接妥當後，進行模組設定。

首先，先將HC05進入AT模式，將HC05上的按鈕按住不放，接上電源後LED燈會慢速閃爍，表示模組已經進入AT模式。
接下來，利用AT指令將模組設定好
1. 確認藍芽模組沒問題
Command: AT
Responce: OK
2. 將藍芽模組的UART通訊鮑率設為57600
Command: AT+UART=57600,0,0
Responce: OK
3. 將藍芽模組腳色設定為主端(Master)
Command: AT+ROLE=1
Responce:OK
4. 設定欲連接裝置(Mindwave mobile2)的配對密碼，預設為0000或1234，請先使用手機或電腦配對嘗試正確密碼。
Command:AT+PSWD=0000
Responce:OK
5. 將藍芽模組設定成只連接到特定裝置
Command:AT+CMODE=1
Responce:OK
6. 設定要連接的特定裝置的ID(Mindwave Mobile2 的裝置ID貼在耳機上)
Command: AT+BIND=2471,89,e9d8cb
Responce:OK
7. 設定IAC
Command: AT+IAC=9e8b33
Responce: OK
8. 設定CLASS
Command: AT+CLASS=0
Responce:OK
9. 設定INQM
Command:AT+INQM=1,7,48
Responce:OK

完成後，先將Mindwave關閉，並確認其他配對過的裝置都已經斷線並關閉藍芽。
將HC05模組接上電源，板載LED燈會快速閃爍代表進入資料模式。
等待約10秒鐘後，將Mindwave啟動，若連線成功板載LED燈會快速閃爍兩下並熄滅一秒，並重複。
若板載LED燈閃爍速度忽快忽慢，則表示密碼錯誤，重新設定AT+PSWD的密碼(0000或1234)
建立連線後即完成。

# 硬體接線
將HC05的TX連接到Arduino的Pin0(RX)
將Pin3 ~ Pin12 每個腳位串連LED燈以及220歐姆電阻，並且接地。 

Arduino Code: 
將本Repo的程式碼燒錄到ArduinoUno上即可。 

# Reference 

## Official Website: 

http://neurosky.com/ 

台灣代理商: 勝宏精密科技 [http://brain-sh.tw/index.php]

## Example on Youtube:
https://www.youtube.com/watch?v=iFBhTHGXcMQ
https://www.youtube.com/watch?v=kbzIDT0Aby8

## Official Arduino support
http://developer.neurosky.com/docs/doku.php?id=mindwave_mobile_and_arduino

## Sensor used:
EEG (Electro Encephalo Graphy) sensor
http://neurosky.com/biosensors/eeg-sensor/biosensors/
https://zh.wikipedia.org/wiki/%E8%85%A6%E9%9B%BB%E5%9C%96

## HC-05 AT command wiki 

https://www.itead.cc/wiki/Serial_Port_Bluetooth_Module_(Master/Slave)_:_HC-05

## Some tutorial but not useful

https://www.pantechsolutions.net/interfacing-mindwave-mobile-with-arduino
