# Trouble Shooting

This pages contains some of the common problems and the known solutions to them.

## Communication

***Problem*: incompatible CH340 driver of some types of models. Unable to establish connection, and the device does not show up under `\dev`.**

***Solution***:
run `sudo apt-get autoremove brltty`. `brytty` sometimes interfere the functionality of certain drivers for CH340.

***Problem*: want to use multiple USB2CAN devices, but the naming for the device is not fixed.**

***Solution***: If you are using a [Canable](https://canable.io/getting-started.html) device, you can use the `slcan` related command. If you are using a device with [CandleLight](https://github.com/normaldotcom/candleLight_fw) firmware, you should checkout [this section of the Canable Documentation](https://canable.io/getting-started.html#udev-rules) and see how you can set udev rules properly.

All the socketcan devices should be under `/sys/class/net`. You can check the properties of the device using `sudo udevadm info -ap <device_path>`. udev file should be created at `/etc/udev/rules.d/99-candlelight.rules`.

Considering writing udev so that it can be deteremined using solely `idVendor`, `idProduct`, `serial`. If not possible, use `KERNELS` property to assign name based on physical port locations of its parent usb device. Below is an example udev file.

```bash
SUBSYSTEM=="net", ATTRS{idProduct}=="606f", ATTRS{idVendor}=="1d50", ATTRS{serial}=="004C00375646571520363132", NAME="can_bytewrek_0" # using serial number
SUBSYSTEM=="net", KERNELS=="3-1", ATTRS{product}=="XCAN-USB", ATTRS{idProduct}=="000c", ATTRS{idVendor}=="0c72", NAME="can_xcan_0" # using kernel
```

After creating udev file, run this command and unplug/replug to activate:
```bash
sudo udevadm control --reload-rules && sudo systemctl restart systemd-udevd && sudo udevadm trigger
```