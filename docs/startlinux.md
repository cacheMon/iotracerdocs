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

3) Finally, install the Python dependencies. The simplest way is to install them all at once from `requirements.txt`

```bash
pip install -r requirements.txt
```

Or, if you prefer your distro's package manager:
```bash
# Ubuntu / Debian
sudo apt install python3-psutil python3-requests python3-zstandard

# Fedora
sudo dnf install python3-psutil python3-requests python3-zstandard

# Arch
sudo pacman -S python-psutil python-requests python-zstandard
```

4) You are all set.

## Basic Usages

Start tracing!

```bash
sudo iotrc
```

Tracing with [anonymization](./privacy.md)

```bash
sudo iotrc -a
```

To check your computer id

```bash
sudo iotrc --computer-id
```

### Command Options

```bash
usage: sudo iotrc [-h] [-v] [-a] [--cache] [--network] [--computer-id] [--reward] [--no-upload] {dev} ...

Trace IO syscalls

options:
  -h, --help       show this help message and exit
  -v, --verbose    Print verbose output
  -a, --anonimize  Enable anonymization of process and file names
  --computer-id    Print this machine ID and exit
  --reward         Show your reward code (unlocked after uploading traces)
  --no-upload      Disable automatic upload of traces (for testing)

subcommands:
  {dev}            Run in developer mode with extra logs and checks
                   (supports --trace-bucket NAME to override the upload bucket)
```

### Use our tool as a service!

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

## Uninstall

Run the uninstaller from your local repo:

```bash
sudo bash ~/io-tracer/uninstall.sh
```

This will:

- Remove the `iotrc` binary from `/usr/local/bin`
- Optionally delete the cloned repo at `~/io-tracer` (you'll be prompted)