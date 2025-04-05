# OpenBook - E-book Reader

## Descriere generala

OpenBook este un dispozitiv de citit carti electronice (e-book reader) conceput pentru a fi ieftin si open-source.

## Diagrama bloc

![Diagrama bloc](Images/block_diagram.png)

## BOM (Bill Of Materials)

| Componenta | Descriere | Link Mouser | Link Datasheet |
|------------|-----------|-------------|----------------|
| ESP32-C6-WROOM-1-N8 | Modul WiFi/BLE | [Mouser ESP32-C6-WROOM-1-N8](https://www.mouser.com/ProductDetail/Espressif-Systems/ESP32-C6-WROOM-1-N8) | [Datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-c6-wroom-1_datasheet_en.pdf) |
| USB4110-GF-A | Conector USB Type-C | [Mouser USB4110-GF-A](https://www.mouser.com/ProductDetail/GCT/USB4110-GF-A) | [Datasheet](https://gct.co/files/drawings/usb4110.pdf) |
| USBLC6-2SC6Y | Protectie ESD USB | [Mouser USBLC6-2SC6Y](https://www.mouser.com/ProductDetail/STMicroelectronics/USBLC6-2SC6Y) | [Datasheet](https://www.st.com/resource/en/datasheet/usblc6-2.pdf) |
| XC6220A331MR-G | Regulator LDO 3.3V | [Mouser XC6220A331MR-G](https://www.mouser.com/ProductDetail/Torex-Semiconductor/XC6220A331MR-G) | [Datasheet](https://www.torexsemi.com/file/xc6220/XC6220.pdf) |
| MCP73831 | Controller incarcare Li-Po | [Mouser MCP73831](https://www.mouser.com/ProductDetail/Microchip-Technology/MCP73831T-2ACI-OT) | [Datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/MCP73831-Family-Data-Sheet-DS20001984H.pdf) |
| W25Q512JVEIQ | Memorie Flash SPI 64MB | [Mouser W25Q512JVEIQ](https://www.mouser.com/ProductDetail/Winbond/W25Q512JVEIQ) | [Datasheet](https://www.winbond.com/resource-files/w25q512jv_spi_revd_112320.pdf) |
| DS3231SN | RTC cu backup | [Mouser DS3231SN](https://www.mouser.com/ProductDetail/Maxim-Integrated/DS3231SN) | [Datasheet](https://datasheets.maximintegrated.com/en/ds/DS3231.pdf) |
| BME680 | Senzor de mediu | [Mouser BME688](https://www.mouser.com/ProductDetail/Bosch-Sensortec/BME688) | [Datasheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme688-ds000.pdf) |
| MAX17048G+T10 | Controller de monitorizare baterie | [Mouser MAX17048G+T10](https://www.mouser.com/ProductDetail/Maxim-Integrated/MAX17048G+T10) | [Datasheet](https://datasheets.maximintegrated.com/en/ds/MAX17048-MAX17049.pdf) |
| 744043680 | Bobina 6.8uH | [Mouser 744043680](https://www.mouser.com/ProductDetail/Wurth-Elektronik/744043680) | [Datasheet](https://www.we-online.com/catalog/datasheet/744043680.pdf) |
| CEL0014 | Baterie Li-Po 2000mAh | [Comet CEL0014](https://www.comet.srl.ro/index.php?main_page=product_info&products_id=9078) | [Datasheet](https://www.tme.eu/Document/e0683d8c34e6d878124489f71bffb6ee/cel0014.pdf) |
| FH34SRJ-24S-0.5SH | Conector display e-paper | [Mouser FH34SRJ-24S-0.5SH](https://www.mouser.com/ProductDetail/Hirose-Connector/FH34SRJ-24S-05SH99) | [Datasheet](https://www.hirose.com/product/document?clcode=CL0580-1255-6-99&productname=FH34SRJ-24S-0.5SH(99)) |
| DMG2305UX-7 | MOSFET Canal P | [Mouser DMG2305UX-7](https://www.mouser.com/ProductDetail/Diodes-Incorporated/DMG2305UX-7) | [Datasheet](https://www.diodes.com/assets/Datasheets/DMG2305UX.pdf) |
| BD5229G-TR | Supervisor tensiune | [Mouser BD5229G-TR](https://www.mouser.com/ProductDetail/ROHM-Semiconductor/BD5229G-TR) | [Datasheet](https://fscdn.rohm.com/en/products/databook/datasheet/ic/power/voltage_detector/bd52xxg-e.pdf) |
| CPH3225A | Capacitor supercondensator | [Mouser CPH3225A](https://www.mouser.com/ProductDetail/Seiko-Instruments/CPH3225A) | [Datasheet](https://www.sii.co.jp/en/me/datasheets/chip-capacitor/cph3225a/) |

## Descrierea functionalitatii hardware

### Alimentare si managementul energiei

Dispozitivul poate fi alimentat fie prin USB-C, fie prin bateria Li-Po incorporata. Circuitul de incarcare MCP73831 asigura incarcarea corecta a bateriei cand dispozitivul este conectat la USB. Tensiunea de la USB sau baterie este convertita la 3.3V prin regulatorul LDO XC6220A331MR-G pentru alimentarea componentelor interne.

Un circuit special pentru ecranul e-paper a fost implementat pentru a genera tensiunile necesare acestuia prin utilizarea bobinei 744043680 si a diodelor Schottky pentru redresare.

La mufa USB au fost aprobate 2 erori in DRC pentru respectarea dimensiunilor mecanice specificate.

### Microcontroller ESP32-C6

ESP32-C6 este responsabil pentru controlul tuturor functionalitatilor dispozitivului. Am utilizat versiunea cu modul WiFi integrat (ESP32-C6-WROOM-1-N8) ce ofera si conectivitate Bluetooth. Dispozitivul include un buton de reset si un buton de boot pentru programare.

### Conectori si interfete

- **USB-C**: Pentru incarcare si transfer de date
- **Slot microSD**: Pentru extinderea memoriei si stocarea cartilor
- **Conector pentru ecran e-paper**: Interfata FPC cu 24 de pini pentru ecranul e-Paper de 7.5 inch
- **Conector Qwiic/Stemma QT**: Pentru extinderea cu senzori si periferice I2C

### Memorii si accesorii

- **Memorie Flash SPI**: W25Q512JVEIQ de 64MB pentru stocarea firmware-ului si a cartilor
- **RTC DS3231**: Ceas in timp real cu backup prin supercapacitor pentru mentinerea timpului
- **Senzor de mediu BME688**: Pentru monitorizarea temperaturii, umiditatii si calitatii aerului
- **Circuit de monitorizare baterie MAX17048**: Pentru a furniza utilizatorului informatii precise despre nivelul bateriei

## Descrierea pinilor ESP32-C6 utilizati

| Pin ESP32-C6 | Functie | Descriere |
|--------------|---------|-----------|
| IO0 | INT_RTC | Semnal de intrerupere de la RTC |
| IO1 | 32KHZ | Semnal de ceas de la RTC |
| IO2, IO3 | EPD_BUSY, SPI | Comunicatii cu display-ul si cardul SD |
| IO4, IO5 | SS_SD, EPD_DC | Selectie card SD si control date/comanda e-paper |
| IO6, IO7 | SCK, MOSI | Clock SPI si date de iesire |
| IO8 | GPIO8 | Pin de uz general |
| IO9 | IO/BOOT | Buton de boot |
| IO10, IO11 | EPD_CS, FLASH_CS | Selectie chip pentru display si memoria flash |
| IO12, IO13 | USB_D-, USB_D+ | Comunicatii USB |
| IO15 | IO/CHANGE | Buton de schimbare pagina |
| IO18 | RTC_RST | Reset pentru RTC |
| IO19 | I2C_PW | Control alimentare pentru perifericele I2C |
| IO20 | EPD_3V3_C | Control alimentare pentru display |
| IO21, IO22 | SDA, SCL | Comunicatii I2C |
| IO23 | EPD_RST | Reset pentru display |
| EN | RESET | Semnal de reset pentru ESP32 |
