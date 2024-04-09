# About 
The DEFCON 32 CPEC badge design, done in kicad 6. Repo contains both a schematic and PCB design. 

This design uses the pervasive displays E2266QS0F1 E-Ink display; https://www.pervasivedisplays.com/product/2-66-e-ink-displays/

## Goal (functional requirements)
Design of the final board will do these functions. Many of them will be implemented in embedded software, which the board hardware will enable. 

- When the user attaches a lanyard to the two holes cut into the top of the board, the user will be able to wear this board around their neck. 
- When the user turns on the board, the board will read the contents of the SD card, and will display the first BMP file on the e-ink display.
- When the user pushes the image select button, SW4, the board will display the next BMP on the SD card.
- When the user plugs in an SAO board to J3, J4, or J5, the board will supply 3.3v DC power to the SAO board. 
- Board will be programmed over UART with a FTDI cable. When the developer switches SW5 to program, plugs a FTDI cable into J1, and presses SW3 to reset the board, the developer will load their ESP32 image over the serial bus. 
- When the user switches switch SW2 to "Be Evil" the board will do something mischievous. 
- LEDs will blink in a cool pattern. 

# Questions/Risks  (non-functional requirements)
This section covers specific questions and possible risks, which may lead to non-functional requirements on the design. 

## Specific Questions
- Can the ESP32-S2-WROOM-1 "EN" in be used as a Chip Pullup?
- Can the ESP32-S2-WROOM-1 "GPIO2" be used as a SPI Data Out pin?
- Can the ESP32-S2-WROOM-1 "GPIO3" be used as a SPI Chip Select pin? 
- Can the ESP32-S2-WROOM-1 "GPIO6" be used as a SPI Clock pin? 
- Can the ESP32-S2-WROOM-1 "GPIO7" be used as a SPI Data In pin? 

## Risks
- The SPI clock line is longer than the data line on the PCB layout. This may lead to a drift in the SPI clock from the data. May lead to an inability to use the Display or SD card. 
- Something about this design may be non-manufacturable 
  - Are vias too close to lines? 
  - Are there too many vias? 
  - Are some lines too close to the edge? 
  - Are some lines too close together? 
  - Are some pads too small? 

# Details 

Kicad version
```
Application: KiCad

Version: 6.0.11+dfsg-1, release build

Libraries:
	wxWidgets 3.2.2
	libcurl/7.88.1 OpenSSL/3.0.11 zlib/1.2.13 brotli/1.0.9 zstd/1.5.4 libidn2/2.3.3 libpsl/0.21.2 (+libidn2/2.3.3) libssh2/1.10.0 nghttp2/1.52.0 librtmp/2.3 OpenLDAP/2.5.13

Platform: Linux 6.1.0-18-amd64 x86_64, 64 bit, Little endian, wxGTK, gnome, wayland

Build Info:
	Date: Jan 26 2023 05:35:43
	wxWidgets: 3.2.1 (wchar_t,wx containers) GTK+ 3.24
	Boost: 1.74.0
	OCC: 7.6.3
	Curl: 7.87.0
	ngspice: 38
	Compiler: GCC 12.2.0 with C++ ABI 1017

Build settings:
	KICAD_USE_OCC=ON
	KICAD_SPICE=ON
```

