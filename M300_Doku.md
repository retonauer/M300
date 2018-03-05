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
> Vagrant.configure(2) do |config|
  config.vm.box = "windows"
config.vm.provider "virtualbox" do |vb|
  vb.memory = "1024"  
end
end 



