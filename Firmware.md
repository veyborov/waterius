# Прошивка Attiny85

Фьюзы: E:FF, H:DF, L:62

Расположение выводов на разъеме для ESP-01 (вид сверху):

| **GND** | **SCK 15** | **MOSI 16** | nc  | 
| ---- | ---- | ---- | ---- |
|  nc | **MISO 14** | nc  | **Vcc** |
+ 10й пин на ресет Attiny85

nc - не используется
Vcc - в любой 3.3в или 5в.

## Arduino в качестве ISP программатора (3.3в-5в).

Распиновка, при прошивки с помощью Arduino Micro или Arduino UNO:

| Micro | UNO | ISP | Attiny85 |   
| ---- | ---- | ---- | ---- |
| 15pin | 13pin | SCK | 7pin |
| 14pin | 12pin | MISO | 6pin |
| 16pin | 11pin | MOSI | 5pin |
| 10pin | 10pin | RESET | 1pin |
+ питание!

В platfomio.ini:
upload_protocol = arduino
upload_flags = -P$UPLOAD_PORT
upload_speed = 19200

## Китайский USB-ISP программатор
Плата MX-USBISP-V5.00
Программа [ProgISP V1.7.2](https://yandex.ru/search/?text=ProgISP%20V1.7.2&&lr=213)
Фьюзы: E:FF, H:DF, L:62
HEX файл взять из platfomio или Arduino IDE.

## USBasp программатор
Я купил китайский USB-ISP и перепрошил его по [инструкции](https://vochupin.blogspot.com/2016/12/usb-isp.html) в USBasp ([прошивка](https://www.fischl.de/usbasp/)). В диспетчере устройств он стал виден, как USBasp. 

В platfomio.ini:
upload_protocol = usbasp
upload_flags = 
    -Pusb 
    -B5


## Работа с platfomio
Platformio бывает в виде консольной утилиты или как дополнение в Visual Studio Code. 
[Инструкция по установки утилиты](http://docs.platformio.org/en/latest/installation.html#python-package-manager)

- откройте в командной строке папку waterius/Attiny85
- измените в файле platfomio.ini порт на свой:
upload_port = /dev/tty.usbmodem1421
- выполните:
platformio run --target upload

Используемые библиотеки:
* [WiFiManager](https://github.com/tzapu/WiFiManager) для настройки wi-fi точки доступа
* [USIWire](https://github.com/puuu/USIWire) i2c слейв для attiny
    

# Прошивка ESP8266
### c помощью platfomio
- откройте в командной строке папку waterius/ESP8266
- измените в файле platfomio.ini порт на свой:
upload_port = /dev/tty.usbmodem1411
- выполните:
platformio run --target upload

## с помощью Arduino IDE
I try with Arduino IDE 1.8.5 

### Additional Libraries Требуемые библиотеки  
- WifiManager by tzapu (0.12.0)
- Blynk by Volodymyr Shymanskyy (0.5.2)

(!) Patch WifiManager library: 
1. Open WiFiManager.h file
2. Move WiFiManagerParameter class 'init' function from private to public 


### Additional Boards Managers URLs:
http://arduino.esp8266.com/stable/package_esp8266com_index.json

Board settings:
* Board: Generic ESP8266 Module
* Flash Mode: DIO
* Flash Size: 512K (no SPIFFS)
* Debug port: Disable
* Debug Level: None
* IwIP Varian: v2 Lover Memory
* Reset Method: ck
* Crystal Frequency: 26 MHz
* Flash Frequency: 40MHz
* CPU Frequency: 80 MHz
* Buildin Led: 0
* Upload Speed: 115200
* Port: select your port

### Sketch
1. rename main.cpp to src.ino 
2. open src.ino in Arduino IDE
3. compile









