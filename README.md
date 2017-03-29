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

Default variables is in `defaults/main.yml`.

### Actions to be executed
```
kismet_rpi_wardriving_clean: true
kismet_rpi_wardriving_install: true
kismet_rpi_wardriving_run: true
```

### General variables
```
kismet_rpi_wardriving_id: "kismet"
kismet_rpi_wardriving_version_number: "2016-07"
kismet_rpi_wardriving_version_release: "R1"
kismet_rpi_wardriving_architecture: "armhf"
kismet_rpi_wardriving_version: "{{ kismet_rpi_wardriving_version_number }}-{{ kismet_rpi_wardriving_version_release }}"
```

### Variables to download the installer
```
kismet_rpi_wardriving_localmirror_dir_name_www: "localmirror"
kismet_rpi_wardriving_localmirror_dir_name_local: "/Users/Chilcano/1github-repo/binaries/"
### to download installer from tasks
kismet_rpi_wardriving_bin_installer: "{{ kismet_rpi_wardriving_id }}_{{ kismet_rpi_wardriving_version }}_{{ kismet_rpi_wardriving_architecture }}.deb"
#kismet_rpi_wardriving_bin_installer_url: "{{ kismet_rpi_wardriving_localmirror_dir_name_local }}{{ kismet_rpi_wardriving_bin_installer }}"
kismet_rpi_wardriving_bin_installer_url: "http://{{ groups['pibuilder'][0] }}/{{ kismet_rpi_wardriving_localmirror_dir_name_www }}/{{ kismet_rpi_wardriving_bin_installer }}"
```
### Variables to cleand and run Kismet systemd
```
kismet_rpi_wardriving_remove_dependencies: false
kismet_rpi_wardriving_warpi_start_script: warpi.sh
kismet_rpi_wardriving_warpi_service_name: warpi.service
```
### Variables for `kismet.conf`
```
kismet_rpi_wardriving_conf_wifinic: wlan0
kismet_rpi_wardriving_conf_logdir: /var/log/kismet
kismet_rpi_wardriving_conf_logdefault: kismet
#kismet_rpi_wardriving_conf_logtypes: pcapdump,gpsxml,netxml,nettxt,alert
kismet_rpi_wardriving_conf_logtypes: pcapdump,netxml
kismet_rpi_wardriving_conf_cfgdir: .kismet
```

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
