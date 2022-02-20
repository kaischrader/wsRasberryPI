# Rasberry PI

## Installation

Unter Windows:

Software **Raspberry Pi Imager** für das passende Betriebssystem von <https://www.raspberrypi.com/software/> herunterladen. 

In der Software sind zwei Optionen zu wählen:

- Das Betriebssystem, das installiert werden soll
- Die SD-Karte, auf die geschrieben werden soll

Für den headless Betrieb reicht das Image **Rasberry Pi OS Lite (64-Bit)** aus.

Nach Auswahl der beiden Optionen kann das Schreiben gestartet werden.

## Raspberry PI OS

Nun die Software `sudo raspi-config` starten.

#### System Options:

- S1 Wireless LAN: SSID: **Entenhausen1**, Schlüssel: **Entenhausen_01**
- S3 Password: **tuongvy01**
- S4 Hostname: **dagobert**

#### Interface Options:

- I2 SSH: enable

#### Localisation Options

- L1 Locale: de_DE.UTF-8 UTF-8, en_GB.UTF-8 UTF-8
- L2 Timezone: Europa, Berlin
- L3 Keyboard: PC-Tastatur mit 105 Tasten (intl)
- L4 WLAN Country: DE Germany

## Absicherung des Systems

Eine ausführliche Beschreibung ist hier zu finden: <https://raspberrytips.com/security-tips-raspberry-pi/>

- Neuen Nutzer anlegen: **kai**, **tuongvy01**

  ```sh
  sudo adduser `<username>`

  // sudo Privilegien zuweisen
  sudo adduser `<username>` sudo

  // pi-Benutzer löschen
  sudo pkill -u pi
  sudo deluser -remove-home pi
  ```  

- Regelmäßig das System aktualisieren:
  
  ```sh
  sudo apt update
  sudo apt upgrade
  ```
  
  Automatisierung der Aktualisierung:

  ```sh
  sudo apt install unattended-upgrades

  // Konfiguration:
  sudo nano /etc/apt/apt.conf.d/50unattended-upgrades

  // Folgende Zeile aktivieren:
  Unattended-Upgrade::Mail "kai";

  // Konfiguration Aktualisierungsintervall:
  sudo nano /etc/apt/apt.conf.d/02periodic

  // Dort einfügen:
  APT::Periodic::Enable "1";
  APT::Periodic::Update-Package-Lists "1";
  APT::Periodic::Download-Upgradeable-Packages "1";
  APT::Periodic::Unattended-Upgrade "1";
  APT::Periodic::AutocleanInterval "1";
  APT::Periodic::Verbose "2";

  // Test:
  sudo unattended-upgrades -d
  ```

- Kennwort für sudo

  ```sh
  // Konfiguration über folgende Datei:
  sudo nano /etc/sudoers.d/010_pi-nopasswd

  // Folgende Zeile für jeden Benutzer aktivieren:
  kai ALL=(ALL) PASSWD: ALL
  ```

- SSH-port ändern
  > 1288

## Installation von Software

### git

Webseite: <https://git-scm.com/>

``` bash
sudo apt-get install git

// Test
git --version
```  

### Node

Webseite: <https://nodejs.org/en/>

Die Installation ist hier beschrieben: <https://github.com/nodesource/distributions>

```bash
curl -fsSL https://deb.nodesource.com/setup_17.x | sudo -E bash -

sudo apt-get install -y nodejs

// Test
node --version
npm --version
```

### PM2 Process Management

Webseite: <https://pm2.keymetrics.io/>

```bash
sudo npm i pm2 -g

// Test
pm2 --version
```

### UFW firewall

Webseite: --

```bash
sudo apt install ufw

// Test
ufw --version

sudo ufw enable
sudo ufw status
sudo ufw allow ssh (Port 22)
sudo ufw allow http (Port 80)
sudo ufw allow https (Port 443)
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



## FRITZ!Box 6591 Cable

IP-Adresse: 77.21.162.122

Aktivierte Portfreigaben:
Freigabe Port (IPv4)
nodeserver 3000
HTTP-Server 80
HTTPS-Server 443

## SSH-Port

Geändert von 22 auf 1111.
