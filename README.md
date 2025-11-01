# personal-dashboard
This is my personal dashboard

It runs on top of a raspbery pi 5, allowing me to create a dashboard to follow up with important stuff.

The goal of this repo is to reproduce the steps to get it up and running again in the future.

### Details:

* RaspberryPi 5 - 4Gb of RAM
* MicroSD 64GB
* [DietPI](https://dietpi.com/#downloadinfo)

### Configuration

1. Burn DietPI image on microSD with [RaspberyPi Imager](https://www.raspberrypi.com/software/)
2. Boot up with the microSD and configure all the way.
3. Once you are in the terminal, you can configure DietPi
  

Install:
Docker
Docker Compose
LXDE
Chromium
Git


Configure:
kiosk mode on chromium target.
display size;

Download docker compose files under monitoring files and docker up

dietpi-autostart -> set localhost:3000 as chromium kiosk entry.

At `/var/lib/dietpi/dietpi-software/installed/chromium-autostart.sh`:
 - Add `/home/dietpi/monitoring/docker compose up --wait` to ensure grafana runs and gets healthy before executing chromium on kiosk mode. Ps: Add it before exec command
 - 

