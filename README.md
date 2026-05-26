# HomeLab-Projekt

## Inhaltsverzeichnis
1. Projektübersicht / Ziel
2. Techstack
3. Netzwerkarchitektur
4. Fehlerbehebung (AMD-V BIOS Error)
5. Schritt-für-Schritt-Anleitung

## Ziel 
* Einrichtung einer Active Directory Testumgebung zur Simulation von IT Support Szenarien / Benutzerverwaltung

## Verwendete Technologien
* VMware Workstation Pro
* Windows Server 2022 Standard (Evaluation, Desktopdarstellung)
* Windows 10 Enterprise

## Fehlerbehebung (Troubleshooting): AMD-V BIOS Error
**Problem:** 

Beim ersten Startversuch der virtuellen Maschine trat ein Virtualisierungsfehler auf, der den Systemstart blockierte. 

![AMD-V BIOS Error Bild](/screenshots/AMD_V_Error.png "AMD-V BIOS Error")

## Ursachenanalyse
Die Hardware-Visualisierungserweiterung (AMD-V) des physischen AMD-Prozessors auf dem Host-Mainboard war im UEFI/BIOS deaktiviert. Der Typ-2-Hypervisor (VMware Workstation Pro) benötigt jedoch direkten Hardwarezugriff auf diese Befehlssätze.

## Lösungsschritte
1. **Host-System herunterfahren:** Der Computer wurde komplett neu gestartet.
2. **UEFI/BIOS aufrufen:** Während des Boot-Vorgangs wurde wiederholt die `F2` Taste (abhängig vom Mainboard-Hersteller) gedrückt, um die Firmware-Oberfläche zu öffnen.
3. **Advanced Mode aktivieren:** Über die `F7` Taste wurde zu den erweiterten Einstellungen gewechselt.
4. **SVM-Mode lokalisieren:** Mithilfe der Suchleiste, wurde die Option SVM Mode (Secure Virtual Machine) gefunden.
5. **Aktivierung:** Der Status wurde von `Disabled` auf `Enabled` geändert.
6. **Speichern & Booten:** Mithilfe von `F10` wurden die Einstellungen gespeichert. Nach dem Booten in das Host-Windows startete die VM in VMware Workstation Pro einwandfrei.

