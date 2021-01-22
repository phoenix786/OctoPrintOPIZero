Note: the following procedures are what worked for my setup, taken advantage of these two toutorials. 
https://community.octoprint.org/t/setting-up-octoprint-on-a-raspberry-pi-running-raspbian-or-raspberry-pi-os/2337
https://sudomod.com/forum/viewtopic.php?t=10262

# OctoPrintOPIZero
Install OctoPrint on Orange Pi Zero

1. Download a stable version of Armbian in https://www.armbian.com/orange-pi-zero/.

2. Download balena Etcher and etch the img file to sd card https://www.balena.io/etcher/.

3. Connect to Orange Pi zero via SSH create a new user as "octopi".

4. update the system.
```
sudo apt-get update
sudo apt-get upgrade
```

5. Logout as root then log back in as the user you made previously. "octopi"

6. 
```
sudo apt install python3-pip python3-dev python3-setuptools python3-venv git libyaml-dev build-essential
mkdir OctoPrint && cd OctoPrint
python3 -m venv venv
source venv/bin/activate
```

7. Install octoprint into virtual environment.
```
pip install pip --upgrade
pip install octoprint
```

8. You may need to add the pi user to the dialout group and tty so that the user can access the serial ports, before starting OctoPrint.
```
sudo usermod -a -G tty octopi
sudo usermod -a -G dialout octopi
```

9. Starting the server for the first time.
```
~/OctoPrint/venv/bin/octoprint serve
```

10. Now if you type in a web browser <octoprintIP>:5000 (where <octoprintIP> is Orange Pi IP address)



AUTO START OCTOPRINT ON SYSTEM START

1. Open an edditor and change the following lines.
```
sudo nano /etc/systemd/system/octoprint.service
```
change these two lines like so: 
User:octopi
ExecStart=/home/pi/OctoPrint/venv/bin/octoprint

2. Then add the script to autostart using: 
```
sudo systemctl enable octoprint.service
```



