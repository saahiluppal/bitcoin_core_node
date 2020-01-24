# Installing Bitcoin Core Node
This repo do installation of bitcoin core node on your linux system.
## Usage
<strong>Directory:</strong> install_bitcoin_core_node
```
bash install
```
OR
```
./install.sh
```
Script will automatically detect System requirements and do installation.

### Distros associated with RedHat may encounter package problems. Hence package list is provided.
if on terminal, download using
```
wget -i btc_pkgs.txt
```

## Docker Files
<strong>Directory:</strong> docker

For Ubuntu as Base OS. Build docker file as 
```
docker build -t <custom image name> .
```
OR provide <-f> to hardcore path

Upcoming Dockerfiles:
 - Fedora as Base OS
 - CentOS as Base OS

