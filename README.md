# Ansible Role: kismet-rpi-wardriving

An Ansible Role that installs, configures and runs [Kismet](http://www.kismetwireless.net) on a Raspberry Pi.
This Role provides the following features:

- Install Kismet and dependencies.
- Configure Kismet by deploying an customized `kismet.conf`.
- Download MAC Addresses Manufacturer List.
- Enable `monitor mode` in the Raspberry Pi before starting Kismet.
- Run Kismet as a `systemd` service.

## Requirements

- One Raspberry Pi to install and run Kismet.
- An WIFI adaptor where you are able to configure It in `monitor mode`.
- A Raspberry Pi connected to your Local LAN with assigned IP address.

## Role Variables

Default variables are in `defaults/main.yml`, `vars/main.yml`.

## Dependencies

None.

## Example Playbook

Using the Ansible Role in a Raspberry Pi for installing and configuring pre-compiled Kismet.

```
---
- hosts: pikismets
  become: yes

  vars_files:
    - vars.yml

  roles:
    - { role: chilcano.kismet-rpi-wardriving }
```

The `inventory` file contains:
```
[pikismets]
192.168.1.35

[pibuilder]
192.168.1.204
```


## License

MIT / BSD

## Author Information

This role was created in 2017 by [Roger Carhuatocto](https://www.linkedin.com/in/rcarhuatocto), author of [HolisticSecurity.io Blog](https://holisticsecurity.io).
