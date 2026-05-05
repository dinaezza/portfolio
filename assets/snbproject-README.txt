# README — Alles-in-1.ps1

## Overzicht

"Alles-in-1.ps1" is een hoofdscript dat een volledige re-image WiFi & certificaat-remediatieflow automatiseert.
Het script zorgt ervoor dat een toestel:

1. tijdelijk verbinding maakt met het gastennetwerk,
2. het devicecertificaat controleert en herstelt indien nodig,
3. daarna automatisch opnieuw verbindt met het secure enterprise WiFi-netwerk.

Deze aanpak zorgt voor een betrouwbare netwerk- en certificaatconfiguratie na een re-image of bij verbindingsproblemen.


## Doel van het script

Het script is bedoeld om:

* netwerkproblemen na een re-image te voorkomen,
* verlopen of ontbrekende certificaten automatisch te herstellen,
* manuele tussenkomst te minimaliseren,
* en een consistente, herhaalbare workflow te bieden.


## Voor gebruik
De parameters moeten aangepast worden voor gebruik.

In de WiFi-scripts: 
Connect-GuestWifi.ps 
Connect-SecureWifi.ps1 
moeten de SSID’s van zowel het gastennetwerk als het secure enterprise netwerk correct ingesteld worden.

In het script CertificateCheck.ps1:
moeten de PacketFence-specifieke instellingen aangepast worden, 
waaronder de hostname of het IP-adres van de PacketFence server, 
de API-gebruikersnaam en het wachtwoord, 
en de naam van de Sub Certificate Authority die wordt gebruikt voor devicecertificaten. 



## Stap 1 — Verbinden met Guest WiFi

Script: Connect-GuestWifi.ps1

* Controleert noodzakelijke systeeminstellingen (o.a. Location Services)
* Verbindt met het gastennetwerk
* Verifieert WiFi- en internetconnectiviteit

Doel: stabiele internettoegang verkrijgen voor verdere acties.


## Stap 2 — CertificateCheck

Script: CertificateCheck.ps1

* Haalt het Intune / Azure AD Device ID op
* Controleert of een geldig clientcertificaat aanwezig is
* Zoekt het certificaat op in PacketFence
* Revoket het certificaat indien nodig
* Triggert een Intune synchronisatie
* Controleert opnieuw of een geldig certificaat aanwezig is

Doel: garanderen dat het toestel een correct en geldig certificaat heeft.


## Stap 3 — Verbinden met Secure WiFi

Script: Connect-SecureWifi.ps1

* Verbreekt eventueel bestaande WiFi-verbindingen
* Verbindt met het secure enterprise netwerk (EAP-TLS)
* Wacht op succesvolle authenticatie
* Verifieert internetconnectiviteit

Doel: het toestel terug in de juiste productie-WiFi brengen.



## Bestandsstructuur

C:\ProgramScripts\
 ├─ Alles-in-1.ps1
 ├─ Start-Alles-in-1.bat
 ├─ re-image\
 │   ├─ Connect-GuestWifi.ps1
 │   ├─ CertificateCheck.ps1
 │   └─ Connect-SecureWifi.ps1
 └─ Logs\
     └─ Alles-in-1_YYYY-MM-DD_HH-MM-SS.log



## Vereisten

* Windows 10 of Windows 11
* PowerShell 5.1 of hoger
* Administratorrechten
* Toestel is Intune enrolled
* Netwerktoegang tot PacketFence API


## Gebruik

Optie 1: Handmatig

1. Open PowerShell als Administrator
2. Ga naar de juiste map:

   cd C:\ProgramScripts

3. Start het script:

   .\Alles-in-1.ps1


Optie 2: Via batchbestand (aanbevolen)

Dubbelklik op:

Start-Alles-in-1.bat

Het batchbestand:

* vraagt automatisch adminrechten,
* past tijdelijk de execution policy aan,
* en start het PowerShell-script.



## Auteurs

* Script: Teamproject SNB
* Alles-in-1 & WiFiCleanup: Dina Ezzarfani
* CertificateCheck: Amal El Moussaoui
* Academiejaar: 2025–2026

## Dit script werd ontwikkeld in het kader van het SNB Project (Graduaat Systeem- en Netwerkbeheer).

