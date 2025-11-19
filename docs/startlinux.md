# Quick Start Guide | Linux

## Prerequisites
- Linux system with kernel headers
- Python 3.x
- sudo privileges (required for BPF operations)
- BPF Compiler Collection / BCC

Clone the IO Tracer [repository](https://github.com/cacheMon/io-tracer)
```bash
git clone https://github.com/cacheMon/io-tracer.git
```

Instal BCC:
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

Finally, install these last two libraries!
```
sudo apt install python3-psutil
sudo apt install python3-requests
```

You are all set.

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
usage: iotrc.py [-h] [-o OUTPUT] [-v VERBOSE] [-a] [-au] [-s]

Trace IO syscalls

options:
  -h, --help            show this help message and exit
  -o OUTPUT, --output OUTPUT
                        Output Directory for logging, must be new!
  -v VERBOSE, --verbose VERBOSE
                        Print verbose output
  -a, --anonimize       Enable anonymization of process and file names
  -au, --auto-upload    Enable automatic upload of logs
  -s, --server-mode     Optimized for higher throughput in server environments
```