# Quick Start Guide | Linux

## Prerequisites
- Linux system with kernel headers
- Python 3.x
- sudo privileges (required for BPF operations)
- BPF Compiler Collection / BCC

You can execute these commands for BCC installation:
```bash
# Debian
echo deb http://cloudfront.debian.net/debian sid main >> /etc/apt/sources.list
sudo apt-get install -y bpfcc-tools libbpfcc libbpfcc-dev linux-headers-$(uname -r)

# Ubuntu
sudo apt-get install bpfcc-tools linux-headers-$(uname -r)

# Fedora
sudo dnf install bcc

# Arch
pacman -S bcc bcc-tools python-bcc
```

For more distros, visit the official BCC's [installation guide](https://github.com/iovisor/bcc/blob/master/INSTALL.md)

Finally, install process monitor
```
sudo apt install python3-psutil
```

## Basic Usages

Start tracing
```bash
sudo python3 iotrc.py 
```

Tracing with [anonymization](./privacy.md)
```bash
sudo python3 iotrc.py -a
```

Tracing with automatic upload
```bash
sudo python3 iotrc.py -au
```


## Command Options
```
usage: iotrc.py [-h] [-o OUTPUT] [-v VERBOSE] [-a] [-au]

Trace IO syscalls

options:
  -h, --help            show this help message and exit
  -o OUTPUT, --output OUTPUT
                        Output Directory for logging, must be new!
  -v VERBOSE, --verbose VERBOSE
                        Print verbose output
  -a, --anonimize       Enable anonymization of process and file names
  -au, --auto-upload    Enable anonymization of process and file names
```