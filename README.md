# piager-installer
Ansible playbook to install Pi-Ager

## What
The German commuinity Grillsportverein created a commuinity project "Pi-Ager" - a Rasperry Pi controlled Dry-Ager (and much more).
More details to be found at https://github.com/Tronje-the-Falconer/Pi-Ager or http://pi-ager.org

## Why
Either you went for the ready-made images which are based on Debian Strech (or older) or you follow a cumbersome and error-prone manual installation instruction (e.g. http://pi-ager.org/installation/standalone_installation).
As this is much more reproducable with ansible and also easier for non-IT guys I tried to create this playbook.

## How
### Prerequisites
Please use an untouched Rasbian Buster Lite image - available at https://www.raspberrypi.org/downloads/raspbian/ 
Configure networking and log on to the machine via ssh as user `pi` (and password `raspberry`)
Install ansible and git to the image

	sudo apt update
	sudo apt upgrade -y
	sudo apt install ansible git -y

### Clone the repository
Clone the repository to your local raspberry

	git clone https://github.com/MelmanBrown/piager-installer.git
	cd pi-ager

### Check the config
You may want to set a custom password for the admin area of the web interface in the config under `group_vars/pi-ager`. Look for the ## CHANGEME ## comment.

### Create a ssh-key so that ansible can do it's magic
	ssh-keygen -b 2048 -t rsa -f /home/pi/.ssh/ansible -q -N ""
	cat /home/pi/.ssh/ansible.pub >> /home/pi/.ssh/authorized_keys
	chmod 600 /home/pi/.ssh/authorized_keys

### Run the playbook
Now let's see if it works

	ansible-playbook -i hosts site.yml

If you want som fun, run `sudo apt install cowsay -y` before executing the playbook

## What else
The webcam stuff is still missing. May come later..
