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