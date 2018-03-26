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

