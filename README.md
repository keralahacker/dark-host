# dark-host

# Youtube: https://youtu.be/c/HackwithVyshu

sudo apt update && upgrade

# Step 1: Install Apache Server
sudo apt install apache2
systemctl start apache2
systemctl enable apache2

# Step 2: Host your application/website for example Wordpress/vTigerCrm etc
# in my case I have hosted my application on localhost http://127.0.0.1:3001/
# our goal is access that application on onion network

# Step3: Create Hidden Service
sudo apt install tor

# Start Tor
sudo tor
# NB: if fail to start, error; Could not bind to 127.0.0.1:9050: Address already in use
# then execute sudo killall tor

# Installed location
whereis tor

sudo nano /etc/tor/torrc

# un-comment two lines.
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 80 127.0.0.1:80

# Next, we'll want to correct the port on which Tor looks for our server. 
# in our case our application running on http://127.0.0.1:3001 port 3001, 
# we'll want to correct the line from port 80 to port 3001. 
# We will change the original seen below to the correct port number.
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 80 127.0.0.1:30001



# Start/Stop/Status tor
sudo systemctl start tor.service
sudo systemctl stop tor.service
sudo systemctl status tor.service
sudo systemctl restart tor.service

# Public key, private key, and onion url are located here
cd /var/lib/tor/hidden_service
ls
# Onion url
cat hostname

# COPY THAT URL AND VISIT WITH TOR BROWSER 


################### REMOVE TOR ###################
# To remove just tor package itself from Ubuntu 16.04 (Xenial Xerus) execute on terminal:
sudo apt-get remove tor

#Uninstall tor and it's dependent packages
sudo apt-get remove --auto-remove tor

# Purging tor, If you also want to delete configuration and/or data files of tor from Ubuntu then this will work:
sudo apt-get purge tor

#To delete configuration and/or data files of tor and it's dependencies from Ubuntu then execute:
sudo apt-get purge --auto-remove tor

################### NB ###################
# after configuration if it does not work, then restart pc and run "sudo tor"

