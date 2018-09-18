# Installing NodeJS and VSCode on RPi

This page describes how to install and use NodeJS and VSCode on RPi

## NodeJS on RPi

### A short description for RPi dudes

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
```

### A longer description for RPi newbees

There is an excellent introduction (including a general RPi setup) and tutorial on w3schools. Please browse to https://www.w3schools.com/nodejs/nodejs_raspberrypi.asp and have fun.

&nbsp;


## VSCode on RPi

Installation can be done as secribed on https://code.headmelted.com/

```bash
. <( wget -O - https://code.headmelted.com/installers/apt.sh )
```

After successful installation, cd into your project folder and start vscode with `code-oss .`

If you are working via SSH on the RPi, use the SSH-Tool MobaXTerm on your (Windows-)PC. It comes with an X11 server and will automatically redirect the display of VSCode to your PC.

In case you need to start VSCode as root (e.g. for accessing BLE devices via noble), you need to explicitely set a user data directory:

```bash
# as root or via sudo:
mkdir /root/.vscode-oss # run this only once
code-oss . --user-data-dir=/root/.vscode-oss # use this for every launch of vscode as root
```
