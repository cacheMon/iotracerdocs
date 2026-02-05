# Quick Start Guide | Linux

## Prerequisites

- Linux system with kernel headers
- Python 3.x
- sudo privileges (required for BPF operations)
- BPF Compiler Collection / BCC

## Install

### One-line Installation

Execute the following command to install IO-Tracer on your device:

```bash
curl -sSL https://raw.githubusercontent.com/cacheMon/io-tracer/refs/heads/main/install.sh | sudo bash
```

If the command fails, you can try installing it manually in [Manual Installation](#manual-installation)

### Manual Installation

1) Clone the IO Tracer [repository](https://github.com/cacheMon/io-tracer)

```bash
git clone https://github.com/cacheMon/io-tracer.git
cd io-tracer
```

2) Install BCC:

```bash
# Debian
echo deb [http://cloudfront.debian.net/debian](http://cloudfront.debian.net/debian) sid main >> /etc/apt/sources.list
sudo apt-get install -y bpfcc-tools libbpfcc libbpfcc-dev linux-headers-$(uname -r)

# Ubuntu
sudo apt-get install bpfcc-tools linux-headers-$(uname -r)

# Fedora
sudo dnf install bcc

# Arch
pacman -S bcc bcc-tools python-bcc
```

> _For more distros, visit the official BCC's_ [installation guide](https://github.com/iovisor/bcc/blob/master/INSTALL.md)

3) Finally, install these last two libraries!

```bash
# ubuntu
sudo apt install python3-psutil
sudo apt install python3-requests

# ... (adjust the package manager for other distros)
```

4) You are all set.

## Basic Usages

Start tracing

```bash
sudo python3 iotrc.py
```

Tracing with [anonymization](./privacy.md)

```bash
sudo python3 iotrc.py -a
```

To check your computer id

```bash
sudo ./iotrc.py --computer-id
```

## Command Options

```bash
usage: iotrc.py [-h] [-o OUTPUT] [-v VERBOSE] [-a] [--dev] [--computer-id] [--reward]

Trace IO syscalls

options:
  -h, --help            show this help message and exit
  -o OUTPUT, --output OUTPUT
                        Output Directory for logging
  -v VERBOSE, --verbose VERBOSE
                        Print verbose output
  -a, --anonimize       Enable anonymization of process and file names
  --dev                 Developer mode with extra logs and checks
  --computer-id         Print this machine ID and exit
  --reward              Show your reward code (unlocked after uploading traces)
```

## Use our tool as a service!

We provided a simple bash script that installs and enable IO Traces as a service. This will allow you to **use the tool in the background** and **automatically run the script** everytime you boot your device.

```bash
Usage: sudo bash ./scripts/install_service.sh {install|uninstall|status|start|stop|restart|logs}

Options:
  install      Install and enable the service
  uninstall    Stop and remove the service
  status       Show service status
  start        Start the service now
  stop         Stop the service
  restart      Restart the service
  logs         View live service logs
```
