Scripting Project 2de zit
Auteur: Dina Ezzarfani


Beschrijving:
Mijn script voert automatisch de installatie en configuratie van een Windows Server als domeincontroller uit
en maakt het beheer eenvoudiger via een menu die je handmatig kunt gebruiken. 


Automatische stappen:
Bij het starten van scriptingDEZ.ps1 worden deze dingen automatisch uitgevoerd:

1. Netwerkconfiguratie aanpassen volgens computer.settings.xml  
   Let op: je moet het MAC-adres van de netwerkadapters in het XML-bestand zetten.
2. Domain Controller installeren of lid maken van een bestaand domein.
3. Organizational Units aanmaken uit ou.txt.
4. Security Groups aanmaken uit securitygroups.csv.
5. Domeingebruikers aanmaken uit users.json.
6. Users toevoegen aan groepen volgens users.json.
7. Mappen en shares aanmaken uit mappen.txt en shares.csv.
8. NTFS-rechten toekennen aan mappen/shares volgens rechten.csv.

Als de server herstart na de DC-installatie wordt het script automatisch hervat bij de volgende stap.


Handmatige opties:
Na de automatische uitvoering verschijnt een menu om:
- OU's toe te voegen
- Security Groups aan te maken
- Domain Users aan te maken
- Mappen/shares toe te voegen
- Users toe te voegen aan groepen
- NTFS-rechten in te stellen


Bestanden:
- scriptingDEZ.ps1 → Hoofdscript en menu
- modules\algemeenDEZ.psm1 → Algemene functies (loggen, serverconfig)
- modules\domainsettingsDEZ.psm1 → Domein- en AD-functies
- settings\ → Configuratiebestanden (XML, JSON, CSV, TXT)
- logs\InstallatieLogDEZ.txt → Logbestand met alle acties



Gebruik:
1. Plaats alle bestanden (bijv. `C:\scripting`).
2. Pas de configuratiebestanden in settings\ aan naar wens.
3. Voeg het juiste MAC-adres van je netwerkadapters toe in computer.settings.xml.
4. Start PowerShell als Administrator.
5. Voer uit:
cd C:\scripting
.\scriptingDEZ.ps1

