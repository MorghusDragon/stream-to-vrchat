# Stream to VRChat
A set of files to create a server that can stream your desktop to VRChat video players with low latency.

## Setup

### Windows

#### Prerequisites

 * [MediaMTX Standalone](https://github.com/bluenviron/mediamtx/releases) (Scroll down to "Assets" and then pick the file "mediamtx_vX.X.X_windows_amd64.zip")

#### Starting

* Unzip the downloaded Zip file to a new directory, it should contain the file "mediamtx.exe".
* Copy the file [mediamtx.yml](/mediamtx.yml) into the same directory.
* Double click "mediamtx.exe"
* If a red warning screen pops up (Smart Screen), click "Run Anyway"

### Linux

#### Prerequisites

 * [Docker](https://docs.docker.com/engine/install/)

On a fresh Ubuntu 22.04 system, run this:

```
sudo apt install docker.io docker-compose
```

#### Starting

 * Use `git clone` or download the Zip file of this repository and unzip it into a new directory
 * Edit the `.env` file and set 
 * Run `docker-compose up -d` to start the service
