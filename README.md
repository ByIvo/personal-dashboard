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

#### Configure which appliation will autostart
1. Run `dietpi-autostart`
2. Then go to option: `11 : Chromium - Dedicated use without desktop` and hit enter.
3. Set `http://localhost:3000`, which is the Grafana UI, and hit enter.
4. select `dietpi` user.

Don't forget to enable auto log in with `dietpi` user.

PS: You should exit autostart menu without selecting any other option, otherwise it will override your autostart configuration.

#### Make UI wait untill dashboard and dependencies are healthy
1. Open the chromium autostart file in edit mode:
```sh
sudo nano /var/lib/dietpi/dietpi-software/installed/chromium-autostart.sh
```
2. Before the last command (the one that starts chromium), append the following command:
```sh
cd /home/dietpi/monitoring && docker compose up -d --wait
```

### Setting manually the display size
I'm still not able to set it automatically; The only way I found was:
open `/boot/dietpi.txt` and set the following properties:

```
SOFTWARE_CHROMIUM_RES_X=1080  
SOFTWARE_CHROMIUM_RES_Y=2560   
```

