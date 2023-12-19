# Stream to VRChat
A set of files to create a server that can stream your desktop to VRChat video players with low latency.

## Setup

This guide works for Windows with your home internet connection, which is totally free. However,
your home internet connection needs to be sufficiently fast, and you need to know how to configure
your router to forward a port to your PC.

Alternatively, if your home internet connection isn't fast enough or you just want it always available,
there's a rough guide on how to set up a Virtual Private Server (VPS) with Linux, which come for as low as $4/month.

### Windows (Local PC, Home internet connection)

#### Prerequisites

 * [MediaMTX Standalone](https://github.com/bluenviron/mediamtx/releases) (Scroll down to "Assets" and then pick the file "mediamtx_vX.X.X_windows_amd64.zip")
 * Port forward port `8554 (TCP)` from your home router to your PC
 * Your home IP address (find out by googling "what is my IP")
 * Sufficient upload speed with your home internet connection

#### Starting

* Unzip the downloaded Zip file to a new directory, it should contain the file "mediamtx.exe".
* Copy the file [mediamtx.yml](/mediamtx.yml) into the same directory.
* Double click "mediamtx.exe"
* If a red warning screen pops up (Smart Screen), click "Run Anyway"

### Linux (On VPS, paid)

#### Prerequisites

 * [Docker](https://docs.docker.com/engine/install/)
 * Your own VPS or machine where ports 443, 1936 and 8554 are available via IPv4
   I recommend [Hetzner](https://www.hetzner.com/) for the most bang for your buck, but
   any other VPS hosting provider will do as well, like [DigitalOcean](https://www.digitalocean.com),
   [OVH](https://www.ovh.com) or [Vultr](https://www.vultr.com)
 * A DNS name for your server IP. If you have your own domain name, great! If not, you can get one for
   free at [FreeDNS](https://freedns.afraid.org).

On a fresh Ubuntu 22.04 system, run this:

```
# Install Docker packages
sudo apt install docker.io docker-compose
# (Optional) Enable Firewall for security
ufw allow OpenSSH
ufw allow 443/tcp
ufw allow 1936/tcp
ufw allow 8554/tcp
ufw enable
```

#### Starting

 * Use `git clone` or download the Zip file of this repository and unzip it into a new directory
 * Edit the `.env` file and set the `HOSTNAME` and `ACME_EMAIL` variables
 * (Optional) Edit the `mediamtx.yml` file and change the `publishUser` and `publishPass` values for 
   added security
 * Run `docker-compose up -d` to start the service


## Streaming

Using [OBS](https://obsproject.com/), change your Stream Service to "Custom" and enter the following URL: 

* Windows from your PC:

    rtmp://localhost/

* Linux with VPS:

    rtmps://your-dns-name.com:1936/

Replace `your-dns-name.com` with the `HOSTNAME` you set in your `.env` file. 

Set your Stream Key to `stream`. If you set a username and password in your `mediamtx.yml` file, change
the Stream Key to `stream?user=myusername&pass=mypassword`.

That's it! Now you can click "Start Stream" in OBS.

## In VRChat

Go to any video player in VRChat and enter the following stream URL:

* Windows from your PC:

      rtspt://your-home-ip:8554/stream

  You can find your home IP by googling "what is my IP".

* Linux with VPS:

      rtspt://your-dns-name.com:8554/stream

If it doesn't work on first try, try once more or click the Sync button.