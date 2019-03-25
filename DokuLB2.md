#  Dokumentation LB2

# K1 / K2

## Persönlicher Stand

Ich habe aus dem Betrieb schon einige Erfahrungen mit Virtualisierung gemacht, 
da wir aber so gut wie nur Microsoft Produkte verwenden, habe ich was die Virualisierung
mit Linux angeht nur Erfahrungen aus dem ÜK 340 welchen ich Momentan absolviere. 
Ich werde diesen am 15.3.2019 abschliessen. Mit Vagrant habe ich bisher noch keine Erfahrungen gemacht.
Virtualisierung und die Automatisierung davon ist für mich aber ein sehr spannendes Thema und ich 
freue mich mehr darüber zu lernen. Auch Markdown und Github habe ich bis anhin noch nie verwendet.

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
    
##   Beschreibung

 * Web Server mit Apache und MySQL
 * DB Server mit MySQL
 * Die Verbindung zu den VM's wird über den Internen Netzwerk Adapter hergestellt.
 * Der HTTP Port (80) ist von ausssen freigegeben.
 * Für den Zugriff per ssh muss in dem Vagrantfile der Name definiert werden
 
     $ vagrant ssh web
     $ vagrant ssh database
     
### Konfiguration Vagrant Umgebung


Als erstes wird mit

$ vagrant add box ubuntu/xenial 

eine Box installiert, hier wird das Betreibssystem bereitgestellt. Anschliessend wird mit:

$ vagrant init ubuntu/xenial64 

ein Vagrant file erstellt, welches aber noch bearbeitet werden muss. Die Grundkonfiguration wird ohne änderungen am Vagrantfile installiert, die Softwareinstallation, benötigt aber zusätzliche änderungen. Dafür verwende ich ein Shell Skript welches im Vagrant file als provisionierung angegeben wird. 

 $ db.vm.provision "shell", path: "db.sh"
 
#### Testing

Die beiden VM's können dann durch das starten des Vagrant file's mit:

$ vagrant up

aufgesetzt werden. Der Vorgang war erfolgreich, wenn die Datenbank im Webbrowser unter (http://127.0.0.1:8080/adminer.php) erreichbar ist. Das Login fenster erscheint und es kann mit (admin / 1234) eingeloggt werden.



# K4


## Firewall und Reverse Proxy

   Für die Firewall wird ufw verwendet, diese kann ganz eifach per Command Line installiert werden.
   
    $ sudo apt-get install ufw
    $ sudo ufw enable
    
### Firewall Rules

#### Webserver

Auf dem Webserver müssen die Ports 80 und 22 geöffnet werden (HTTP und SSH)

    $ sudo ufw allow 80/tcp
    $ sudo ufw allow from "Host-IP" to any port 22
    
#### DB Server

Auf dem DB Server muss der Webserver freigegeben werden und der Zugriff via ssh vom Hostsystem

   $ sudo ufw allow "IP Webserver" to any port 3306
   $ sudo ufw allow from "IP Host" to any port 22
   
### Reverse Proxy

Auf dem Webserver werden die folgenden Module installiert:

  $ sudo apt-get install libapache2-mod-proxy-html
  $ sudo apt-get install libxm12-dev
  
Danach kann der Proxy mit folgenden Befehlen aktiviert werden:

  $ sudo a2enmod proxy
  $ sudo a2enmod proxy_html
  $ sudo a2enmod proxy_http

Danach muss noch die Datei im Verzeichniss /etc/apache2/apache2.conf bearbeitet werden:

 Servername localhost
 
Webserver neu starten:

$ sudo service apache2 restart
    
# K5

# Wissenszuwachs

Ich kann nun mit Vagrant einzelne und auch mehrere VM's mit sehr wenig Aufwand aufsetzen kann. Ausserdem verstehe ich wie ein Vagrant file mit einem Shell Skript bearbeiten, und so automatisch Packages installieren kann. Was Github angeht, ich habe gelernt wie Projekte erstellt und bearbeitet werden können. Ausserdem habe ich mich mit der Community etwas auseinandergesetzt. Mit Markdown hatte ich anfangs einige Schwierigkeiten, mittlerweile finde ich mich aber auch hier recht gut zurecht. Die Linux befehle welche im "Git bash" verwendet wurden kannte ich schon, da habe ich also nichts neues gelernt. Auch mit Web- und Datenbankservern habe ich schon gearbeitet.

# Reflexion

Mir hat die Aufgabenstellung anfangs nicht so spass gemacht, weil ich recht viele Probleme mit Vagrant hatte. Ich habe mir dann im Betrieb noch Zeit genommen um weiter daran zu arbeiten und bin dann auf den richtigen Weg gekommen. Als es dann funktioniert hat, hatte ich mehr spass und bin auch gut vorangekommen. Ich habe vor in der Freien Zeit im Betrieb noch andere Automatisierungsprodukte anzuschauen und dass am besten passende für mich zu finden.
