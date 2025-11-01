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
  
### Important software
To install software, run `dietpi-software` on after logged in on dietpi;
Then, go to search software, find and select the items below:
* Docker - To run containers
* Docker Compose - To handle your containers all at once
* LXDE - Lightweight GUI
* Chromium - To access the dashboard on kisk mode (visulization only)
* Git - To download confi files from this repo.

### Configure autostart
Run `dietpi-autostart`
Then go to option: `17: Custom script (foreground, with autologin) and paste the following autostart script:
```sh
#!/bin/bash
# DietPi-AutoStart custom script
# Location: /var/lib/dietpi/dietpi-autostart/custom.sh

# Aguarda a sessão X iniciar (sem isso, a rotação do monitor pode não funcionar)
sleep 5

# Define display
export DISPLAY=:0

# Rotaciona a tela HDMI-1
xrandr --output HDMI-1 --rotate right

# Oculta o cursor
unclutter -idle 1 -root &

# Inicia Chromium em kiosk
# localhost:3000 é onde o dashboard está localizado
chromium --kiosk http://localhost:3000 --force-device-scale-factor=0.9 --noerrdialogs --disable-infobars
```
Don't forget to enable auto log in with `dietpi` user.

PS: You should exit without selecting any other option, otherwise it will override your autostart configuration.
PS2: You can also pick other autostart config for testing, such as bootstraping LXDE or the root terminal; You can have a custom script as well.

### Setting manually the display size
I'm still not able to set it automatically; The only way I found was:
open `/boot/dietpi.txt` and set the following properties:

```
SOFTWARE_CHROMIUM_RES_X=1080
SOFTWARE_CHROMIUM_RES_Y=2560
```

### Running the dashboard and dependencies

Download docker compose files under monitoring files and docker up

dietpi-autostart -> set localhost:3000 as chromium kiosk entry.

At `/var/lib/dietpi/dietpi-software/installed/chromium-autostart.sh`:
 - Add `/home/dietpi/monitoring/docker compose up --wait` to ensure grafana runs and gets healthy before executing chromium on kiosk mode. Ps: Add it before exec command
 - 

