# Powershell komentoja

Tämä on vain pieni listaus koskien powershell hyödyllisiä komentoja, mitä tekee testinsä windows työasemalla ja serverissä normaalisti. Näitä ei tapahdu joka päivä, mutta pieni listuas hyvänsä ja tässä on pientä dejavu toistoja.

ARP‑taulukko (Address Resolution Protocol) on tietokoneen ylläpitämä lista, joka kertoo, mikä IP‑osoite vastaa mitä MAC‑osoitetta paikallisessa verkossa. 
- selvittää, mitä laitteita on ollut lähiverkossa
- tarkistaa, onko jokin IP‑osoite sidottu tiettyyn MAC‑osoitteeseen
- diagnosoida verkko‑ongelmia (esim. IP‑konfliktit)
- havaita epäilyttäviä ARP‑spoofing‑tilanteita
```
$arp -a
```

Tyhjentäminen arp-välimuistit tapahtuu:
```
$arp -d *
```

Lisää staattinen ARP‑merkintä:
```
$arp -s <IP> <MAC>
```

---

Tämä komento on Windowsin komentorivin komento, joka näyttää kaikki verkko‑yhteydet, portit ja niitä käyttävät prosessit (PID‑tunnuksella).
- selvittää, mikä ohjelma käyttää tiettyä porttia
- nähdä avoimet TCP/UDP‑yhteydet
- tutkia epäilyttäviä yhteyksiä
- yhdistää portin → PID → prosessin nimi (Task Managerista tai tasklist‑komennolla)
```
$netstat -ano
```

---

Tämä on Windowsin komentorivikomento, joka näyttää kaikki käynnissä olevat prosessit, niiden PID‑tunnukset, muistinkäytön ja joskus myös kuvaustiedot. Se on komentoriviversio Tehtävienhallinnan Prosessit‑välilehdestä. Saat listan, jossa näkyy mm.:
- Image Name — prosessin nimi (esim. chrome.exe)
- PID — prosessin tunnus
- Session Name / Session# — istunto, jossa prosessi pyörii
- Mem Usage — muistinkäyttö
```
$tasklist
```

---

`sfc /scannow` - on Windowsin sisäänrakennettu järjestelmänkorjauskomento, joka tarkistaa ja korjaa vioittuneita tai puuttuvia järjestelmätiedostoja. Windows:
- skannaa kaikki suojatut järjestelmätiedostot
- vertaa niitä alkuperäisiin versioihin
- korvaa vioittuneet, muuttuneet tai puuttuvat tiedostot automaattisesti

```
sfc /scannow
```

Tarkistaa DNS-resoluution ja näyttää IP-osoitteet.
```
$Resolve-DnsName google.com
```

Näyttää käytössä olevat DNS-palvelimet.
```
$Get-DnsClientServerAddress
```

Tyhjentää DNS-välimuistin.
```
$Clear-DnsClientCache
```

Näyttää DNS-välimuistin sisällön.
```
$Get-DnsClientCache
```

Pingaa kohdetta PowerShellin Test-Connectionilla.
```
$Test-Connection 8.8.8.8 -Count 4
```

Testaa TCP-portin yhteyden (korvaa telnetin).
```
$Test-NetConnection -ComputerName google.com -Port 443
```

Suorittaa tracerouten PowerShellillä.
```
$Test-NetConnection -TraceRoute google.com
```

Näyttää kaikki verkkokortit ja niiden tilan.
```
$Get-NetAdapter
```

Näyttää IP-osoitteet, gatewayt ja DNS-palvelimet.
```
$Get-NetIPConfiguration
```

Näyttää ARP-taulukon (IP–MAC -parit).
```
$Get-NetNeighbor
```

Näyttää reititystaulun.
```
$Get-NetRoute
```

Listaa kaikki käynnissä olevat prosessit.
```
$Get-Process
```

Listaa Windows-palvelut ja niiden tilan.
```
$Get-Service
```

Näyttää käynnistysohjelmat.
```
$Get-CimInstance Win32_StartupCommand
```

Näyttää asemat ja levyjen tilan.
```
$Get-Volume
```

Näyttää fyysiset levyt ja niiden kunnon.
```
$Get-PhysicalDisk
```

Näyttää levyjen SMART-tiedot.
```
$Get-PhysicalDisk | Get-StorageReliabilityCounter
```

Näyttää viimeisimmät järjestelmälokit.
```
$Get-EventLog -LogName System -Newest 50
```

Testaa AD-domainin luottosuhteen.
```
$Test-ComputerSecureChannel
```

Listaa domain controllerit.
```
$Get-ADDomainController -Filter *
```

Näyttää AD-replikointitiedot.
```
$Get-ADReplicationPartnerMetadata -Target <DC>
```

Näyttää SMB-jaot.
```
$Get-SmbShare
```

Listaa Windowsin palomuurisäännöt.
```
$Get-NetFirewallRule
```

Näyttää avoimet TCP-yhteydet ja portit.
```
$Get-NetTCPConnection
```

Näyttää prosessin PID:n, joka käyttää porttia 80.
```
$Get-NetTCPConnection -LocalPort 80 | Select-Object -ExpandProperty OwningProcess
```

Näyttää prosessin nimen PID:n perusteella.
```
$Get-Process -Id <PID>
```

Korjaa Windowsin komponenttivaraston.
```
$DISM /Online /Cleanup-Image /RestoreHealth
```

Näyttää ajastetut tehtävät.
```
$Get-ScheduledTask
```

Näyttää verkkoasemien kytkennät.
```
$Get-SmbMapping
```

Näyttää tallennetut WiFi-profiilit.
```
$netsh wlan show profiles
```

Näyttää WiFi-verkon salasanan.
```
$netsh wlan show profile name="<SSID>" key=clear
```

---
---

# Windows Server / Active Directory ‑vianmääritykseen liittyvät PowerShell‑komennot

Tarkistaa, onko koneen AD‑luottosuhde kunnossa (secure channel).
```
$Test-ComputerSecureChannel
```

Listaa kaikki domain controllerit.
```
$Get-ADDomainController -Filter *
```

Näyttää yksityiskohtaiset tiedot tietystä domain controllerista.
```
$Get-ADDomainController -Identity <DCName>
```

Testaa yhteyden domain controlleriin (DNS, LDAP, Kerberos).
```
$Test-ADDomainController -Identity <DCName>
```

Näyttää AD‑metsän tiedot.
```
$Get-ADForest
```

Näyttää AD‑domainin tiedot.
```
$Get-ADDomain
```

Näyttää AD‑replikointipartnerit ja viimeisimmät replikoinnit.
```
$Get-ADReplicationPartnerMetadata -Target <DCName>
```

Näyttää AD‑replikointitilastot ja virheet.
```
$Get-ADReplicationFailure -Target <DCName>
```

Näyttää kaikki FSMO‑roolien haltijat.
```
$Get-ADDomain | Select-Object InfrastructureMaster, RIDMaster, PDCEmulator
$Get-ADForest | Select-Object SchemaMaster, DomainNamingMaster
```

Testaa AD‑replikoinnin tilan koko domainissa.
```
$Get-ADReplicationConnection -Filter *
```

Näyttää AD‑sivustot ja aliverkot.
```
$Get-ADReplicationSite -Filter *
$Get-ADReplicationSubnet -Filter *
```

Näyttää käyttäjän AD‑tiedot.
```
$Get-ADUser -Identity <username> -Properties *
```

Näyttää ryhmän AD‑tiedot.
```
$Get-ADGroup -Identity <groupname> -Properties *
```

Näyttää käyttäjän ryhmäjäsenyydet.
```
$Get-ADPrincipalGroupMembership <username>
```

Näyttää ryhmän jäsenet.
```
$Get-ADGroupMember -Identity <groupname>
```

Etsii käyttäjän, joka on lukittu ulos AD:stä.
```
$Search-ADAccount -LockedOut
```

Etsii käyttäjän, jonka salasana on vanhentunut.
```
$Search-ADAccount -PasswordExpired
```

Etsii käyttäjän, jonka tili on disabloitu.
```
$Search-ADAccount -AccountDisabled
```

Näyttää kaikki koneobjektit domainissa.
```
$Get-ADComputer -Filter * -Properties *
```

Näyttää tietyn koneen AD‑attribuutit.
```
$Get-ADComputer -Identity <hostname> -Properties *
```

Testaa Kerberos‑lipun saamisen (hyödyllinen DC‑ongelmiin).
```
$klist
```

Tyhjentää Kerberos‑liput.
```
$klist purge
```

Testaa DNS‑SRV‑tietueet domain controllerille.
```
$Resolve-DnsName -Type SRV _ldap._tcp.dc._msdcs.<domain>
```

Testaa AD‑sisäisen DNS‑palvelun toimivuuden.
```
$Resolve-DnsName <domain> -Server <DC-IP>
```

Näyttää kaikki GPO:t domainissa.
```
$Get-GPO -All
```

Näyttää GPO‑linkitykset OU:lle.
```
$Get-GPInheritance -Target <OU DN>
```

Päivittää ryhmäkäytännöt pakotetusti.
```
$gpupdate /force
```

Näyttää GPO‑tulokset (RSoP) koneelle tai käyttäjälle.
```
$gpresult /r
```

Näyttää AD‑terveystarkastuksen (DC‑diag PowerShell‑versio).
```
$Get-ADReplicationQueueOperation
```

Näyttää AD‑objektien replikointiviiveet.
```
$Get-ADReplicationUpToDatenessVectorTable -Target <DCName> -Partition * | Sort-Object -Property USN
```

Näyttää domain controllerin roolit ja tilan.
```
$Get-ADDomainController -Filter * | Select-Object Name,IPv4Address,IsGlobalCatalog,OperationMasterRoles,Site
```

Näyttää AD‑tietokannan koon ja polun.
```
$Get-Item "C:\Windows\NTDS\ntds.dit"
```

Näyttää AD‑lokit (Directory Service log).
```
$Get-EventLog -LogName "Directory Service" -Newest 50
```

Näyttää DNS‑palvelimen lokit (jos rooli asennettu).
```
$Get-EventLog -LogName "DNS Server" -Newest 50
```

Näyttää DHCP‑palvelimen tilan (jos rooli asennettu).
```
$Get-DhcpServerv4Scope
```

Näyttää Hyper‑V‑virtuaalikoneet (jos rooli asennettu).
```
$Get-VM
```

Näyttää AD‑sertifikaattipalvelimen CA‑tiedot (jos rooli asennettu).
```
$Get-CertificationAuthority
```

Näyttää AD‑objektien replikointiongelmat koko domainissa.
```
$repadmin /replsummary
```

Näyttää domain controllerin replikointivirheet.
```
$repadmin /showrepl <DCName>
```

Näyttää AD‑sivustot ja reititykset.
```
$repadmin /showutdvec <DCName> <NamingContext>
```









