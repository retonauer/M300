# Dokumentation LB2
## Installation Docker
Docker haben wir nicht direkt auf dem Laptop installiert, sondern in einer VM. Diese haben wir vom Lehrer erhalten.
## Bestehender Container in Betrieb nehmen
Danach habe ich einen bestehenden Container in Betrieb genommen. Dazu musste ich zuerst das Image erstellen. Die habe ich mit folgendem Befehl gemacht: </br>
> docker build -t apache . </br>
>
Dazu muss man natürlich im Ordner des Containers sein. </br>
Danach kann man den Conainer starten: </br>
>docker run apache:latest
>
## Container als Backend, Desktop-App als Frontend
Um dieses Ziel zu erreichen habe ich das Beispiel vom Lehrer genommen (OSTicket). </br>
### Probleme
Mein Problem bestand darin, dass ich nicht auf die Weboberfläche zugreiffen konnte. Das Problem bestand darin, dass der Port nicht korrekt weitergeleitet wurde, da dieser bereits besetzt war. Ich habe dann andere Ports benutzt und es hat funktioniert.
### Endprodukt
Das Endprodukt funktioniert:
![Ticket](https://www.retonauer.ch/M300/Ticket.jpg)
### Eigene Lösung erstellen
Als eigene Lösung habe ich eine Wordpress-Seite erstellt. Dazu habe ich ein Container mit einer MariadDB und einen Container mit der Wordpress-Installation. Dazu bin ich nach folgender Anleitung vorgegangen: [Anleitung](https://www.techrepublic.com/article/how-to-install-wordpress-with-docker/) </br>
Die folgenden zwei Befehle sind die wichtigsten: </br>
#### Datenbank
>docker run -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_USER=wpuser -e MYSQL_PASSWORD=1234 -e MYSQL_DATABASE=wordpress_db -v /opt/wordpress/database:/var/lib/mysql --name wordpressdb -d mariadb
> </br>
#### Wordpress
>docker run -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD=1234 -e WORDPRESS_DB_NAME=wordpress_db -p 8081:80 -v /opt/wordpress/html:/var/www/html --link wordpressdb:mysql --name wpcontainer -d wordpress
> </br>
#### Netzwerk
Die Wordpress-Installation ist über den Port 8081 erreichbar. Dieser wird direkt auf das Host-System genatet. Somit kann man die Installations-Oberfläche mit dem Link http://localhost:8081 erreicht werden:
![Wordpress](https://www.retonauer.ch/M300/wordpress.JPG) </br>
Nach der Dateneingabe gelangt man auf das Dashboard und die Webseite wird angezeigt:
![Dashboard](https://www.retonauer.ch/M300/dashboard.JPG)
![Webseite](https://www.retonauer.ch/M300/Webseite.jpg)
