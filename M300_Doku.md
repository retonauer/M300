# Modul 300

## MultiVM Infrastruktur in Betrieb nehmen
Nach dem Befehl _vagrant up_ die virtuellen Maschinen mmdb_data und mmdb_web gestartet

![Apache](https://www.retonauer.ch/M300/Apache.jpg)


## Bestehende VM aus Vagrant Cloud zum laufen bringen
Ich habe mich für ein einfaches Windwos entschieden
### Windows Box herunterladen
Ich habe die Box vom [internen Server](http://10.1.66.1.1) heruntergeladen.
#### Vagrantfile
Mein Vagrantfile sieht sehr einfach aus:
> Vagrant.configure(2) do |config| </br>
  config.vm.box = "windows" </br>
config.vm.provider "virtualbox" do |vb| </br>
  vb.memory = "1024"  </br>
end </br>
end </br>
>
## LB01
Als Projekt für LB01 haben wir uns für owncloud entschieden.
### Server
Wir werden einen owncloud-Server einetzen (LAMP-Server) und einen Datenbank-Server.
Der owncloud-Server ist ein Ubuntu 16.04 Server. Der Datenbankserver ebenfalls.

### Installation owncloud
Bei der installation sind wir nach diesem [Link](https://gridscale.io/community/tutorials/owncloud-ubuntu-installieren/) vorgegangen. Wir haben die VM zuerst von Hand aufgesetzt, damit wir wissen, welche Befehle ausgeführt werden müssen.

## Vagrant Box
Für die Web-Vagrant-Box haben wir uns für einen LAMP-Server (bigdeal/lamp-server) entschieden.
Bei der Datenbank haben wir uns für das Beispiel vom Lehrer (ubuntu/xenial64) entschieden.

## Installation
Da wir eine Owncloud aufsetzen werden, benötigen wir einen Webserver und eine Datenbank. Der Webserver ist Apache und die Datenbank MySQL.
### Web
Nach der Installation von Apache wird noch PHP7 installiert und das Packet von Owncloud. Nachdem man den Webbenutzer berichtigt hat, ist Webseite unter http://localhost:8080/owncloud erreichbar.
### Datenbank
Da bei der Installation von MySQL eine User-Interaktion gefordert wird, haben wir _debconf-set-selections_ eingesetzt. </br>
>sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password admin' </br>
      sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password admin' </br>
>
### MultiVM
Bei VMs (Web und DB) werden durch das selbe Vagrantfile installiert und konfiguriert. Dies spart Zeit. Wir haben dies mit folgender Codezeile umgesetzt:
>config.vm.define "web" do |web|
>
Danach muss bei jedem weiteren Befehl bei dem die VM konfiguriert wird web oder db mitgegeben werden.
### Netzwerk
Damit die beiden Server untereinander kommunizieren können, haben wir ein VM-Netzwerk erstellt. </br>
  * Web-Server 192.168.1.4
  * Datenbank-Server 192.168.1.5
### Firewall
Wir haben ebenfalls eine Firewall in Betrieb genommen. Dazu haben wir folgende Befehler eingesetzt um die benötigten Ports zu öffnen und SSH freizugeben:
>ufw --force enable </br>
udo ufw allow 3306/tcp </br>
sudo ufw allow ssh
>


### Konfigurationen nach der Installation
Nach der Installation muss man den Mysql-Server noch konfigurieren:
>mysql -u root -p </br>
CREATE USER 'owncloud'@'%' IDENTIFIED BY '1234'; </br>
CREATE DATABASE IF NOT EXISTS owncloud; </br>
GRANT ALL PRIVILEGES ON owncloud.* TO 'owncloud'@'%'; </br>
quit </br>
sudo reboot
>


## Problem
Unser erstes Problem lag darin, dass wir nach einer Anleitung gearbeitet haben, welche nicht funktioniert hat. Dank der Hilfe eines Schulkollegen konnten wir dieses Problem lösen. </br>
Das nächste Problem lag im Zugriff auf die Datenbank. Da Web und Datenbank nicht auf demselben Server liegen, muss der Remotezugriff freigegeben werden. Dies muss man mit einem Eintrag in einem Config-File machen. Alle Anleitungen im Internet haben uns auf ein falsches File geschickt. Nach langem suchen haben wir das richtige gefunden und es hat funktioniert

## Erweiterung
Man könnte unser Projekt noch erweitern, indem man die MySQL befehler um den Bnutzer anzulegen ebenfalls ins Vagrantfile nimmt. Dies haben wir leider nicht geschafft.
## Fazit
Ich habe Vagrant bis anhin noch nicht gekannt und habe in diesem Modul viel dazugelernt. Auch in diesem Projekt ist nicht alles nach Plan gelaufen, jedoch konnten wir alles Probleme beheben. Unser Endprodukt ist nicht nicht Perfekt und könnte erweitert werden. Allgemein kann man aber sagen, dass wir mit unserem Projekt zufrieden sind.
