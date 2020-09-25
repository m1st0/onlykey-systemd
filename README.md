# onlykey-systemd

Enable the OnlyKey app GUI upon insertion of the OnlyKey USB  device.

## Udev implementation

Provides an aliased path that systemd can initiate to act on with
user permissions.

## Systemd implementation

Provides a user defined path and service unit. The OnlyKey app GUI
will be activated by systemd if the determined path exists, even on
reinsertion of the USB device on any USB port.

## Installation

1. The OnlyKey GUI app must be installed
2. In a terminal, alias the udev rules file in the default location at
`/etc/udev/rules.d/` by this command

    ```bash
    ln -s udev/49-onlykey.rules /etc/udev/rules.d/49-onlykey.rules
    ```

3. Reload udev rules next by running

    ```bash
    sudo udevadm control --reload-rules
    sudo udevadm trigger
    ```

4. Afterward, alias systemd files in user's systemd location at
`.config/systemd/user/` with the following commands

    ```bash
    ln -s systemd/onlykey-attach.path \
    /home/${USER}/.config/systemd/user/onlykey-attach.path

    ln -s systemd/onlykey-attach.service \
    /home/${USER}/.config/systemd/user/onlykey-attach.service
    ```

5. The systemd path unit will take care of the service unit, so there
only exists a need to enable the path unit using

    ```bash
    systemctl --user enable onlykey-attach.path
    ```

6. You may reload the user's systemd units if desired with

    ```bash
    systemctl --user daemon-reload
    ```

7. Insert the OnlyKey USB device and the GUI should activate
