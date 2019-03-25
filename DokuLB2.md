#  Dokumentation LB2

# K1 / K2

## Persönlicher Stand

Ich habe aus dem Betrieb schon einige Erfahrungen mit Virtualisierung gemacht, 
da wir aber so gut wie nur Microsoft Produkte verwenden, habe ich was die Virualisierung
mit Linux angeht nur Erfahrungen aus dem ÜK 340 welchen ich Momentan absolviere. 
Ich werde diesen am 15.3.2019 abschliessen. Mit Vagrant habe ich bisher noch keine Erfahrungen gemacht.
Virtualisierung und die Automatisierung davon ist für mich aber ein sehr spannendes Thema und ich 
freue mich mehr darüber zu lernen.

### Einrichten

## Git bash

1. Git bash herunterladen 
2. Git bash installieren

Anschliessend wird noch das Repository auf den lokalen Computer kopiert.

$ git clone https://github.com/mc-b/M300      #Repository klonen
 
  
## GitHub Account

1. GitHub Account erstellen
2. Mit Git bash SSH Key erstellen
 $ ssh-keygen -t rsa 4096 -C "lucas.gamper@edu.tbz.ch"
3. SSH Key dem Agent hinzufügen
4. SSH Key dem GitHub Konto hinzufügen

## Virtualbox

1. Virtualbox herunterladen
2. Virtualbox installieren

## Visual Studio Code

1. Visual Studio Code herunterladen
2. Visual Studio Code installieren
3. Extensions installieren
4. Einstellungen anpassen

## Vagrant

1. Vagrant herunterladen
2. Vagrant installieren
3. Vagrant VM erstellen

# K3

Eine VM kann mit Vagrant wie folgt erstellt werden:
    
    $ mkdir vagrantvm                                                                       #Ordner für die VM erstellen
    $ cd vagrantvm                                                                          #In verzeichniss wechseln
    $ vagrant box add http://10.1.66.11/vagrant/ubuntu/xenial64.box --name ubuntu/xenial64  #Vagrant-Box vom Repository in den Ordner kopiert
    $ vagrant init ubuntu/xenial64                                                          #Vagrantfile erstellen
    $ vagrant up --provider virtualbox                                                      #Virtuelle Maschine erstellen & starten
    
Danach ist die VM in Virtualbox ersichtlich und kann benützt werden. Dazu wird der folgende Befehl verwendet.

$ vagrant ssh 


# Vagrant Befehle

Hier sind die wichtigsten Vagrant Befehle aufgelistet:

| Befehl           |Beschreibung                                                                             |
| -----------------|:---------------------------------------------------------------------------------------:|
| Vagrant init     |Initialisiert die Vagrant Umgebung im aktuellen Verzeichnis und erstellt ein Vagrantfile |
| Vagrant up       |Erzeugt und Konfiguriert eine Virtuelle Maschine basierend auf dem Vagrantfile           |
| Vagrant ssh      |Verbindung zur VM per SSH wird hergestellt                                               | 
| Vagrant status   |Zeigt den aktuellen Status der VM an                                                     | 
| Vagrant port     |Zeigt die Weitergeleiteten Ports der VM an                                               | 
| Vagrant halt     |VM wird gestoppt                                                                         | 
| Vagrant destroy  |VM wird gestoppt und gelöscht                                                            | 

# Vagrant Umgebung

    +---------------------------------------------------------------+
    ! Notebook - Schulnetz 10.x.x.x und Privates Netz 192.168.2.100 !                 
    ! Port: 8080 (192.158.2.100:80)                                 !	
    !                                                               !	
    !    +--------------------+          +---------------------+    !
    !    ! Web Server         !          ! DB Server           !    !       
    !    ! Host: m330-web     !          ! Host: m300-db       !    !
    !    ! IP: 192.168.2.123  ! <------> ! IP: 192.168.2.145   !    !
    !    ! Port: 80           !          ! Port 3306           !    !
    !    ! Nat: 8080          !          ! Nat: -              !    !
    !    +--------------------+          +---------------------+    !
    !                                                               !	
    +---------------------------------------------------------------+

## Webserver

Der Webserver kann anschliessend auf der VM installiert werden. Dazu wird folgender Befehl verwendet.

   $ sudo apt-get install apache2
  
Da wir dies aber automatisieren wollen, können wir den schnelleren, einfacheren Weg über Vagrant benützen.

   $  cd m300/vagrant/web
   
   $  vagrant up
  
Anschliessend ist der Webserver installiert und kann auf der VM im Webbrowser unter http://127.0.0.1 erreicht werden.



## Firewall und Reverse Proxy

   Für die Firewall wird ufw verwendet, diese kann ganz eifach per Command Line installiert werden.
   
    $ sudo apt-get install ufw
    
   
