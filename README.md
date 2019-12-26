# ansible-deconz

[![Ansible Role](https://img.shields.io/ansible/role/30394.svg)](https://galaxy.ansible.com/hannseman/deconz)
[![Build Status](https://travis-ci.com/hannseman/ansible-deconz.svg?branch=master)](https://travis-ci.com/hannseman/ansible-deconz)

This role will setup and configure a headless [deCONZ](https://github.com/dresden-elektronik/deconz-rest-plugin/) installation.

Additional configuration needs to be made to allow the serial port to communicate with the RaspBee adapter as described on the [deCONZ documenation](https://github.com/dresden-elektronik/deconz-rest-plugin/#software-requirements).
This configuration is out of scope for this role but by using the role [hannseman.raspbian](https://github.com/hannseman/ansible-raspbian) one can configure this quite easily.
Setting the following variables for that role will enable serial communication:

```yaml
rpi_boot_config:
  enable_uart: 1
rpi_cmdline_config:
  serial: 1
```

## Variables

```yaml
# The user that if running deCOnZ
deconz_user: deconz
# Home directory of the above configured user
deconz_dir: /var/deconz
# WiringPI version - http://wiringpi.com
deconz_wiringpi_version: "2.50"
deconz_wiringpi_deb_url: "https://archive.raspberrypi.org/debian/pool/main/w/wiringpi/wiringpi_{{ deconz_wiringpi_version }}_armhf.deb"
# deCONZ version - https://github.com/dresden-elektronik/deconz-rest-plugin/releases
deconz_version: "2.05.71"
deconz_deb_url: "http://deconz.dresden-elektronik.de/raspbian/beta/deconz-{{ deconz_version }}-qt5.deb"
# Path to deCONZ binary
deconz_bin: /usr/bin/deCONZ
# Port to run the deCONZ web GUI on
deconz_http_port: 8080
# Port to run the deCONZ websocket on
deconz_websocket_port: 8088
```

## Example Playbook
```yaml
- hosts: servers
  roles:
     - hannseman.deconz
  vars:
    deconz_wiringpi_version: 2.46
    deconz_version: 2.05.39
    deconz_http_port: 8080
    deconz_websocket_port: 8088
```
