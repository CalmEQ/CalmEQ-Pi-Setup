# CalmEQ Raspberry Pi Finder and Setup Program

The Pi Finder is intended to work with the [latest version of Raspbian][1],
so please make sure you have installed Raspbian on your SD card before continuing.

You have your brand new Raspberry Pi, and you are ready to get hacking...  Only
problem is, you dont have an extra HDMI monitor and keyboard.  So how can you
find out the IP network address? PI FINDER TO THE RESCUE!  Run this
cross-platform application to locate your Raspberry Pi's IP address.

This version is forked from Adafruit's Pi Finder application.

After the device is located, an Ansible Playbook is executed to configure the device.
It is recommended that this playbook change the default user password, and perform
the key handoffs to allow the machine to safely register on the CalmEQ devices website,
and allow further remote configuration through ansible.

The playbook should also configure the wifi password.

## Finding the Pi & Starting the Bootstrap

We have created a utility that will find a Raspberry Pi connected to your
local network and start the bootstrap process. The utility requires you to
connect your Pi to your local network **via an ethernet cable** to start. 
Once the Pi is bootstrapped, it will be able to use ethernet or WiFi but we
need to be able to connect to the Pi the first time around.

### Windows, Mac, & Linux App:

[![finder GUI](/docs/rpi_bootstrap.png?raw=true)][2]

**Note for Mac users:** *If you are prevented from launching the app because of
your security settings, you can right click on the app and click Open to bypass
the warnings*

[Download the latest release][2] of the Pi Bootstrap utility.

### Bootstrap via CLI on Linux or Mac:

```sh
$ curl -SLs https://apt.adafruit.com/bootstrap | bash
```

## occidentalis.txt

Occidentalis comes with a configuration helper script called `occi`, which may
be used to set various system options from a text file on your SD card.

The bootstrapping process will help you create the file by prompting for your
desired hostname and wifi credentials, but it can also be created as
`occidentalis.txt` on the card at any time.  When the Pi is running, edit
`/boot/occidentalis.txt`.

![screencast of opening occidentalis.txt in nano](/docs/edit_occi_settings.gif?raw=true)

Here's an example file:

```
# hostname for your Raspberry Pi:
hostname=mypiname

# basic wireless networking options:
wifi_ssid=your network here
wifi_password=your password or passphrase here
```

Right now, these are the only configuration values supported.  Others will
be added in time.

By default, `occi` will run whenever the Pi boots, but can also be run manually
with:

```sh
sudo occi
```

Looking for code? occi is maintained [in its own GitHub repository][occi].

[1]: http://www.raspberrypi.org/downloads/
[2]: https://github.com/CalmEQ/CalmEQ-Pi-Setup/releases/latest
[occidentalis]: https://github.com/adafruit/Adafruit-Occidentalis
[occi]: https://github.com/adafruit/Adafruit-Occi
