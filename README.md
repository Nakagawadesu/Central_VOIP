# Central_VOIP :calling:

# Prerequisites
- An Ubuntu 22 server in a VM or remote server () Oracle Virtual Box recomended 
- Root or sudo privileges
- Internet connection (if in a VM set the Network to Bridge Adapter)

### Installing Dependencies
Before installing Asterisk, you need to update your package lists and install the necessary dependencies. Open your terminal and execute the following commands:
```
sudo apt update
sudo apt upgrade
sudo apt install -y wget build-essential subversion
```

### Downloading and Installing Asterisk
With the dependencies in place, you can now download and compile Asterisk:
```
cd /usr/src
sudo wget http://downloads.asterisk.org/pub/telephony/asterisk/asterisk-18-current.tar.gz
sudo tar xvf asterisk-18-current.tar.gz
```

Change into the extracted directory and install additional required packages:
```
cd asterisk-18*
sudo contrib/scripts/install_prereq install
```
Now, proceed to compile and install Asterisk:
```
sudo ./configure
sudo make menuselect
sudo make
sudo make install
sudo make samples
sudo make config
sudo ldconfig
```

With Asterisk installed, you can now set up its user and group permissions:
```
sudo adduser --system --group --no-create-home asterisk
sudo chown -R asterisk
/etc/asterisk
sudo chown -R asterisk
/var/{lib,log,spool}/asterisk
sudo chown -R asterisk
/usr/lib/asterisk
```

### Configuring Asterisk
Editing the main configuration file is the next step. Open it using your favorite text editor:
```
sudo nano /etc/asterisk/asterisk.conf
```

Make the necessary changes according to your setup, then start and enable Asterisk at boot:
```
sudo systemctl start asterisk
sudo systemctl enable asterisk
```

Ensure that Asterisk is running without issues:
```
sudo asterisk -vvvr
```

### Setting Up SIP Accounts
To handle VoIP calls, you need to set up SIP accounts. Edit the `sip.conf` and `extensions.conf` files:
```
sudo nano /etc/asterisk/sip.conf
sudo nano /etc/asterisk/extensions.conf
sudo nano /etc/asterisk/voicemail.conf
```

Add your SIP users in `sip.conf` and dial plan in `extensions.conf`.

### :pushpin: How to use 
- In the configuration file in this repo 5 Ramals where configured
- To test the VOIP central download Zoiper5
- login with <Ramal_Number>@<your_VM_IP> and Ramal_Number as passwword
- To use the URA dial 800 and then the last digit of the ramal you wnat to contact
- To dial a Specific Ramal dial the Ramal_Number
- To record a voice audio DIal 5500 , start talking after the beep sound and then after tou are done type # to end it, it should be played back, the audio will be stored in the /tmp/prompt<msg<number>> in your VM



