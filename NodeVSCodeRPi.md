# Installing NodeJS and VSCode on Raspberry Pi

This page describes how to install and use NodeJS and VSCode on a Raspberry Pi (RPi):

If you are new to Raspberry Pi (RPi), you can find a general introduction for setup, installation and usage on the "Raspberry Pi Documentation" page at https://www.raspberrypi.org/documentation/. Please make sure you have SSH-access as described in _"Remote&nbsp;Access"_->_"SSH"_ (direct link: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md).

**Contents of this page**
<!-- TOC depthFrom:2 depthTo:3 -->

- [NodeJS on RPi](#nodejs-on-rpi)
  - [A short description for RPi experts](#a-short-description-for-rpi-experts)
  - [A longer description for RPi newbies](#a-longer-description-for-rpi-newbies)
- [VSCode on RPi](#vscode-on-rpi)
  - [Installation](#installation)
  - [Run VSCode remotely via SSH and X11-Forwarding](#run-vscode-remotely-via-ssh-and-x11-forwarding)

<!-- /TOC -->

## NodeJS on RPi

### A short description for RPi experts

Preparation: As usual, you should update your RPi os and packages:

```bash
sudo apt-get update       # This will update the package list
sudo apt-get dist-upgrade # This will run the actual package upgrade
```

Download and Install NodeJS:

```bash
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash - # get installer files for Node 10
sudo apt-get install -y nodejs # run the installer
node --version # Test the NodeJS version, should result in 10.10.0 or higher
npm --version  # Test NPM version, which comes with NodeJS, should be 5.6.0 or higher
npm version    # Will provide a more extensive version list of various tools
```

After successful installation, you should add Bluetooth permissions to NodeJS as described on https://github.com/noble/noble#running-without-rootsudo: 

```bash
sudo setcap cap_net_raw+eip $(eval readlink -f `which node`)
```

In case there is no `setcap` command on your system, you can install it by `sudo apt-get install libcap2-bin`.



### A longer description for RPi newbies

There is an excellent introduction (including a general RPi setup) and tutorial on w3schools. Please browse to https://www.w3schools.com/nodejs/nodejs_raspberrypi.asp and have fun.

After successful installation of NodeJS, you should add Bluetooth permissions to NodeJS as described on https://github.com/noble/noble#running-without-rootsudo: 

```bash
sudo setcap cap_net_raw+eip $(eval readlink -f `which node`)
```

In case there is no `setcap` command on your system, you can install it by `sudo apt-get install libcap2-bin`.

&nbsp;


## VSCode on RPi

### Installation

Installation can be done as secribed on https://code.headmelted.com/ with the following command:

```bash
. <( wget -O - https://code.headmelted.com/installers/apt.sh )
```

After successful installation, cd into your project folder and start vscode with `code-oss`.

If you are working via SSH on the RPi, use the SSH-Tool MobaXTerm on your (Windows-)PC. It comes with an X11 server and will automatically redirect the display of VSCode to your PC (see next chapter).

_Hint:_ In case you need to start VSCode as root (which should not be necessary unless you use it to modify system config files), you need to explicitely set a user data directory:

```bash
# as root or via sudo:
mkdir /root/.vscode-oss # run this only once
code-oss . --user-data-dir=/root/.vscode-oss # use this for every launch of vscode as root
```


### Run VSCode remotely via SSH and X11-Forwarding

1. Ensure SSH access to your RPi, e.g. as described on https://www.w3schools.com/nodejs/nodejs_raspberrypi.asp
1. Enable X11Forwarding on RPi:<br>
   On the RPi, open the `sshd_config` via `sudo nano /etc/ssh/sshd_config` and make sure that you have a line with `X11Forwarding yes`.
1. Install xorg and some test apps:
   ```bash
   sudo apt-get install xorg
   sudo apt-get install x11-apps
   ```
1. Install MobaXTerm on your Windows-PC:<br>
   See https://mobaxterm.mobatek.net/
1. Launch MobaXTerm and connect to your RPi via SSH. You should see:
   ```text
     ┌────────────────────────────────────────────────────────────────────┐
     │                        • MobaXterm 10.4 •                          │
     │            (SSH client, X-server and networking tools)             │
     │                                                                    │
     │ ➤ SSH session to root@bananapim2zero.fritz.box                     │
     │   • SSH compression : ✔                                            │
     │   • SSH-browser     : ✔                                            │
     │   • X11-forwarding  : ✔  (remote display is forwarded through SSH) │
     │   • DISPLAY         : ✔  (automatically set on remote server)      │
     │                                                                    │
     │ ➤ For more info, ctrl+click on help or visit our website           │
     └────────────────────────────────────────────────────────────────────┘
   ```
1. To test X11-Forwarding in the SSH-session, start `xeyes` or `xclock`. Their small windows should show up on your PC.
1. Launch VSCode: In the SSH session, change into your working directory on your RPi and launch `code-oss .` <br>
   The X11-Forwarding will display VSCode on your PC.

