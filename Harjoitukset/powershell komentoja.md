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



























