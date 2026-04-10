# Powershell komentoja

Tämä on vain pieni listaus koskien powershell hyödyllisiä komentoja, mitä tekee testinsä windows työasemalla ja serverissä normaalisti. Näitä ei tapahdu joka päivä, mutta pieni listuas hyvänsä

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

























