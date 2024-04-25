## Programming the ESP32 S3 with touchscreen

This is for the ESP32-S3 Development Board, with 1.28inch Round Touch LCD. Embedded GC9A01 Display Driver And CST816S Capacitive Touch Control Chip

Product page (shop): https://www.waveshare.com/esp32-s3-touch-lcd-1.28.htm
Wiki page: https://www.waveshare.com/wiki/ESP32-S3-Touch-LCD-1.28

This repository is to share some notes of mine. Hope that helps not only me to make it reproduceable.

## Prerequisites

or what I am using.

- MS VSCode (1.88.1)
- ESP-IDF Extension
- MacOS (M1 with Sohoma 14.4.1)
- USB-C cable
- Python 3.11.3

You might need the driver for the USB chip CH34X, https://www.wch-ic.com/downloads/CH34XSER_MAC_ZIP.html

### Installing the ESP-IDF

Either install with the VSCode extension ("ESP-IDF Extension") or manually.

#### Manually

Follow the installation guide from [Espressif](https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/get-started/linux-macos-setup.html)

In my case it required the minimal commands:

```
brew install cmake ninja dfu-util
git clone -b v5.2.1 --recursive https://github.com/espressif/esp-idf.git esp-idf-v5.2.1
ln -s esp-idf-v5.2.1 esp-idf
cd esp-idf
./install.sh esp32s3
. ./export.sh
```

The last command (with the correct path) is needed everytime you want to use the idf tools.

## Get started

Using the VSCode Extension, seems to be the most comfortable version. But here the manual instructions:

Make sure exports for esp-idf are set. Test with: `idf.py --version`

Find your USB-C connected board like:

```shell
ls  /dev/cu*
/dev/cu.Bluetooth-Incoming-Port      /dev/cu.wchusbserial57350172051        /dev/cu.usbmodem57350172051     /dev/cu.wlan-debug
```

So in my case the device is available via `/dev/cu.wchusbserial57350172051`

You can follow the https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/get-started/linux-macos-setup.html#configure-your-project

Or TL;DR in the examples directory:

```
idf.py set-target esp32s3
idf.py build
idf.py /dev/cu.wchusbserial57350172051 flash
```

If you get an error like:

```
A fatal error occurred: Failed to write to target RAM (result was 01070000: Operation timed out)
```

Install the CH34X driver. If the driver is correctly installed you should see `/dev/cu.wchusbserialXXXX` and `/dev/cu.usbserialXXXX`, where you should now use the prefixed one starting with: `wch`

Monitoring and checking the output:

```
idf.py -p /dev/cu.wchusbserial57350172051 monitor
```

### Questions

- How to display the current weather on it?
- How to power the thing with a small battery? What battery I need?
- Python on it?

#### Running Python on it

#### Using the display
