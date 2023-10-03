# Dokumentasi Board NRF52840 V1.0723


﷽

Semoga sehat selalu untuk kita semua.
.
.
.
.
.


# Flash bootloader NRF52840

Bootloader diperlukan karena SOC **NRF52840** dari JLC masih kosong, jadi  fitur-fitur yang ada seperti DFU USB tidak dapat terbaca di PC.

File bootloader bisa apa menggunakan apa saja, sebagai contoh saya menggunakan bootloader **NRF52840 DK** (PCA10056), kemudian semua config pinout mengikuti board tersebut.
 

## Peralatan Tempur

- OpenOCD, [gas di sini](https://openocd.org/).
- ST-link V.2
- File bootloader PCA10056
- Arduino IDE, [gas di sini](https://www.arduino.cc/en/software).
- Kabel USB type C


## Langkah - Langkah

1. Install semua peralatan tempurnya. Pastikan sudah **OK** ya...
2. Hubungkan board `NRF52840` dengan `ST-Link V.2` via SWD.
	> */3V3*
	> */GND*
	> */SWCLK*
	> */SWDIO/*
3. Buka Terminal:
    - Cek versi `openocd`,
       >*> openocd -v*
    - Run `openocd`, direktori nya disesuaikan ya...
       >*> openocd -f share/openocd/scripts/interface/stlink.cfg -f share/openocd/scripts/target/nrf52.cfg*
    - `Openocd` sekarang sudah running. Sekarang kita buka terminal lagi untuk menggunakan `telnet`.
       >*> telnet localhost 4444*
    - `Stop execution` bisa gunakan, 
       > *> halt*
    - Hapus `flash` memory,
       > *> nrf5 mass_erase*
    - `Flash NRF52840`
       > *> program /your/path/to/the/pca10056_bootloader-0.6.2_s140_6.1.1.hex verify*
    - Resume the execution,
       > *> resume*
       
4. Jika berhasil maka pada `Device Manager`, board akan terbaca sebagai *`USB Serial Device(COM...)`*
5. Untuk masuk ke mode `DFU` tekan 2 kali tombol `reset`.
 

## Pemrograman NRF52840 menggunakan Arduino IDE
1. Buka Arduino IDE, lalu pilih tab `File` dan pilih `Preferences` dan masukkan URL berikut:
    >*https://adafruit.github.io/arduino-board-index/package_adafruit_index.json*
2. Restart Arduino IDE.
3. Pilih `Tools` > `Board` > `Board Manager`. Kemudian pada textbox filter pencarian filter dengan `NRF` dan install `Arduino nRF52 Boars` dan `Adafruit nRF52`
4. Setelah selesai, silahkan digasken ngodingnya... (saya mencoba dengan program template `bleuart`).....
