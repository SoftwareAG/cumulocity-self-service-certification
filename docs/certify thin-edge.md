# Certify Devices Running thin-edge.io
Using thin-edge.io version 0.6 and above, you can self-certify your thin-edge.io device integration for Cumulocity IoT cloud. 
All you have to do is to create a simple JSON file at `/etc/tedge/device/inventory.json` as root user, with some basic device information as follows:

``` json5
{
  "c8y_RequiredAvailability": {
      "responseInterval": 5
  },
  "c8y_Firmware": {
      "name": "raspberrypi-bootloader",
      "version": "1.20140107-1",
      "url": "31aab9856861b1a587e2094690c2f6e272712cb1"
  },
  "c8y_Hardware": {
      "model": "BCM2708",
      "revision": "000e",
      "serialNumber": "00000000e2f5ad4d"
  }
}
```

Once this file is created, you can connect your device to the Cumulocity IoT cloud, run the certification process and view your device certification results.
