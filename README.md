# transmission-telegram
Telegram chat bot to control Transmission.  
Sorry, only magnet links are supported now.

Install as daemon under Linux using systemd:

1. Register new Telegram bot as described at https://core.telegram.org/bots#botfather
   Save it's token.
2. Install Python 3 and pip.
3. Install Telegram and Transmission libraries using pip:  
    `pip3 install transmissionrpc`  
    `pip3 install python-telegram-bot`
4. Create directory for bot and copy it's source to it:  
    `mkdir /opt/transmission-telegram`  
    `cd /opt/transmission-telegram`  
    `git clone https://github.com/Chudsaviet/transmission-telegram.git`
5. Create symlink and data directory:  
    `ln -s /opt/transmission-telegram/transmission-telegram.py /usr/sbin/transmission-telegram`  
    `mkdir /var/lib/transmission-telegram`
6. Create directory in /etc and copy config in it:  
    `mkdir /etc/transmission-telegram`  
    `cp config.ini.example /etc/transmission-telegram/config.ini`  
7. Generate secret:  
    `dd if=/dev/urandom bs=4096 cnt=1 | sha256sum`
8. Edit config to set Transmission and Telegram credentials, and secret:  
    `editor /etc/transmission-telegram/config.ini`
9. Copy systemd service definition to systemd directory:  
    `cp scripts/transmission-telegram.service /etc/systemd/system/`
10. If you are running bot at the same machine as Transmission, it would be better to start bot after Transmission.
    Just edit `/etc/systemd/system/transmission-telegram.service` and add transmission-daemon.service to `after` section.
11. Reload systemd daemons, enable and run transmission-telegram:  
    `systemctl daemon-reload`  
    `systemctl enable transmission-telegram.service`  
    `systemctl start transmission-telegram`  
12. Check status of the daemon:  
    `systemctl status transmission-telegram`
