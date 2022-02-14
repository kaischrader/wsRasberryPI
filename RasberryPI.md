# Rasberry PI

## Installation

Betriebssystem **Rasbian** von <https://www.raspberrypi.org/downloads/raspbian/> herunterladen. Für den headless Betrieb reicht das Image **Rasbian Buster Lite** aus.

Zum Schreiben des Images auf die SD Karte kann die Software **Etcher** benutzt werden, die hier <https://www.balena.io/etcher/> zu finden ist.

Nach dem Flashen SD Karte in den Raspberry Pi einsetzen und den Computer booten. Initial muss zum Anmelden auf dem Pi der Benutzer **pi** mit dem Kennwort **raspberry** verwendet werden.

Nun die Software `sudo raspi-config` starten.

- SSH aktivieren
- Hostname setzen: **entenhausen**

## Absicherung

- Neuen Nutzer anlegen: **dagobert** **tuongvy01**
  > sudo adduser `<username>`
- sudo Privilegien einrichten

  > sudo adduser `<username>` sudo

- pi-Benutzer löschen

  > sudo pkill -u pi

  > sudo deluser -remove-home pi

- Kennwort für sudo

  > sudo nano /etc/sudoers.d/010_pi-nopasswd

  > dagobert ALL=(ALL) NOPASSWD: ALL

  > dagobert ALL=(ALL) PASSWD: ALL

- SSH-port ändern
  > 1288

## Node.js

## 3. Install Node/NPM

```sh
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs
node --version
npm --version
```

- Git

  > sudo apt-get install git

  ```sh
  git clone yourproject.git
  ```

````

- Setup PM2 process manager to keep your app running

```sh
sudo npm i pm2 -g
pm2 start app (or whatever your file name)
# Other pm2 commands
pm2 show app
pm2 status
pm2 restart app
pm2 stop app
pm2 logs (Show log stream)
pm2 flush (Clear logs)
# To make sure app starts when reboot
pm2 startup ubuntu
````

System logs

/var/log/syslog: main log file for all services
/var/log/message: whole systems log file
/var/log/auth.log: all authentication attempts are logged here
/var/log/mail.log: if you have a mail server, you’ll find a trace of recent emails sent here
Any critical application log file, for example /var/log/apache2/error.log or /var/log/mysql/error.log

## Basics

Adressen im Heimnetz:

```script
LAN:  192.168.178.42
WLAN: 192.168.178.44
```

Hostnamen setzen:

Unter `C:\Windows\System32\drivers\etc` die Datei `hosts` editieren und für die o.g. Adressen lesbare Namen eintragen, also z.B.:

```hosts
192.168.178.42  rasberrypi
```

Anmeldung

Remote-Login, z.B. aus **cmder**:

`ssh pi@rasberrypi`

```login
Benutzer: pi
Kennwort: isegal;7
Benutzer: imhotep
Kennwort: tuongvy01
```

## Nützliche Befehle

```script
sudo                  // Befehl als Superuser ausführen
sudo shutdown -r now  // Linux Neustart
ip a                  // Informationen zum Netzwerk.
```

### Paketverwaltung

```script
sudo apt-get update
sudo apt-get upgrade
sudo apt-get remove “package-name”
sudo apt-get purge “package-name”
sudo apt-get autoremove
```

### Prozesse

- `ps -e` Laufende Prozesse anzeigen.
- `killall 'programmname'` Alle laufenden Prozesse für 'programmname' killen.
- `kill 'PID'` Prozess über id killen.

## Prozessmanager **PM2**

```script
sudo npm i pm2 -g
pm2 start app (or whatever your file name)

# Other pm2 commands
pm2 show app
pm2 status
pm2 restart app
pm2 stop app
pm2 logs (Show log stream)
pm2 flush (Clear logs)

# To make sure app starts when reboot
pm2 startup ubuntu
```

## Firewall **ufw**

```script
sudo ufw enable
sudo ufw status
sudo ufw allow ssh (Port 22)
sudo ufw allow http (Port 80)
sudo ufw allow https (Port 443)
```

## FRITZ!Box 6591 Cable

IP-Adresse: 77.21.162.122

Aktivierte Portfreigaben:
Freigabe Port (IPv4)
nodeserver 3000
HTTP-Server 80
HTTPS-Server 443

## SSH-Port

Geändert von 22 auf 1111.