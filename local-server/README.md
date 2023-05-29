# Local server setup
Below are the steps used to setup a local server within the Hackspace. Currently this is a Raspberry Pi 4.

## Installing the OS
Using the Raspberry Pi imager, install the Raspberry Pi OS Lite onto an external hard drive/SSD. The following advanced options should also be set:

* Hostname. Set to something unique. There will often be other Raspberry Pis in the hackspace.
* Enable SSH. Recommended public-key authentication only.
* Set username and password. Create an admin account for yourself. Don't share this with other members, instead create more accounts as needed.
* Configure wireless LAN. If not using ethernet then make sure this is setup to use the non-member network.

## Securing the server
Ensure the OS is update with `sudo apt update && sudo apt upgrade`.

Setup the firewall to only allow SSH and HTTP/S:
```
sudo apt install ufw
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw limit ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw logging on
sudo ufw enable
```

TODO: Fail2Ban setup.

## Web proxy setup
Install Nginx with `sudo apt install nginx`. You should be able to see a default page if you visit the server in your browser.

Once happy the default configuration symlink can be deleted from `/etc/nginx/sites-enabled/default`.

## Database setup
Install PostgreSQL with `sudo apt install postgresql`. Ensure it is set to run on boot with SystemD.

Create a new superuser account to make management a little easier `sudo -u postgres createuser -s <your_username>`. There's no need to set a password as it will trust your current login.

