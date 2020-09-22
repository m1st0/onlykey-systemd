# onlykey-systemd

Enable the OnlyKey app GUI upon insertion of the OnlyKey USB  device.

## Udev implementation

Provides a device unit alias that systemd can initiate to act on with user
permissions.

## Systemd implementation

Provides a user defined device unit. The OnlyKey app GUI will be launched by
systemd.
