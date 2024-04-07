# The Art of Hacking:

- Aktiivisessa tiedustelussa tarkoituksena on kerätä mahdollisimman paljon tietoa kohdejärjestelmästä ja etsiä mahdollisia haavoittuvuuksia
- Voidaan käyttää työkaluja kuten Nmap jolla voidaan skannata avoimia portteja, joita voi hyväksikäyttää tunkeutumisessa

# Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains:

- Saa terminologiansa armeijassa käytetystä Kill Chain-termistä, jolla tarkoitetaan suunnitelmaa, jolla voidaan tuoda alas tai vallata kohde hyödyntämällä koko prosessin heikointa linkkiä, esimerkiksi Supply Chain-hyökkäyksellä


# PortSwigger SQL Injection: 
Mitä tehtävässa tuli tehdä, oli katsoa URL-palkin tekstiä ja huomata, että sen sisältävä 'category' lippu sisältää injektio-mahdollisuuden, sillä jos URL:n loppuosasta; '/filter?category=Clothing%2c+shoes+and+accessories' muuntaa kohdan category muotoon '/filter?category='+OR+1=1-- ' se palauttaa listan julkaisemattomia tuotteita, sillä kun URL ajaa komennon 'category', kyseinen tietokanta ei tarkista mahdollisen koodinsyötön varalta, jolloin käyttäjä voi lisätä oman muuttujansa, joka tässä tapauksessa on " '+OR+1=1-- " joka käytännössä vain hakee tietokannasta kategorian julkaisemattomista tuotteista ja tarjoilee sen käyttäjälle, vaikka käyttäjällä ei pitäisi olla pääsyä kyseiseen tietokantaan.



# Overthewire: 
ensimmäiset tasot olivat enimmäkseen SSH:n opettelua ja sen navigointia. tarkoitus oli kirjautua sisään serverille SSH:n avulla, löytää kirjautuneen koneen sisältä tietty tekstitiedosto, joka sisältää salasanan seuraavalle tasolle.

Ensimmäisen tehtävän tarkoitus oli vain kirjautua sisään käyttäen seuraavaa komentoa:

    $ ssh bandit.labs.overthewire.org -p 2220 -l bandit0

myöhemmin tajusin, että kirjautuakseen olisi voinut myös kirjoittaa komennon yksinkertaisemmin, eli;

    $ ssh bandit0@bandit.labs.overthewire.org -p 2220

Kuitenkin, tätä kautta pääsi tekemään ensimmäisen tason tehtävää, jonka tarkoituksena oli käyttää komentoa ls löytämään "readme" tiedosto aktiivisesta polusta ja lukea se:

    $ cat readme
    NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

Kyseinen tekstipätkä on salasana, jolla voi kirjautua seuraavalle tasolle. Salasana vaihtuu usein.

Seuraavat tehtävät seurasivat samanlaista kaavaa, toisessa piti käyttää cat ./- komentoa, jotta pystyi avaamaan tiedoston, jonka nimi oli vain yksinkertaisesti "-". Kolmannessa tehtävässä piti löytää tiedostonimi, joka sisälsi välilyöntejä seuraavalla komennolla:

    $ cat spaces\ in\ this\ filename

Joka palautti salasanan seuraavalle tasolle.


# WebGoat:
Asennuksen kanssa oli pieniä ongelmia, sillä aikaisempi WebGoat-asennukseni, jonka tein Lari Iso-Anttilan Tietoturvan Perusteet-kurssilla, on jostain syystä mennyt rikki, joten minun täytyi asentaa WebGoat uudestaan uudelle Kali Linux-asennukselle

![image](https://github.com/konetoivonen/laksyt/assets/164856618/c0f06572-b5bf-4ee0-8cc4-8f7dce2b501a)

# HTTP Basics ja Developer tools

HTTP Basics tehtävässä pyydettiin laittamaan oma nimi joka sitten palautti nimen väärinpäin:

![image](https://github.com/konetoivonen/laksyt/assets/164856618/5b985dcf-f328-4e30-8917-8fa8f6bafdf2)

Developer Tools-tehtävässä pyydettiin tunnistamaan, oliko HTTP-pyyntö POST vai GET pyyntö ja tunnistamaan ns. Taikanumero. Tehtävän suorittamiselle on luultavasti paljon elegantimpi ratkaisutapa mutta itse vain etsin inspect-elementillä elementtiä "magic" ja löysin arvon "magic_num" jonka arvo oli 70

![image](https://github.com/konetoivonen/laksyt/assets/164856618/3942fc01-f6b8-4655-8688-1d76ac617c34)





# Porttiskannaus:
Tehtävää varten asensin koneelleni Kali Linux-käyttöjärjestelmän ja aloin terminaalista testailemaan nmappia ja mitä se tekee. Tehtävän yhtenä tehtävänantona oli asentaa Apache tai SSH tai kumpikin ja verrata, miten erilaiselta porttiskannaus näytti ennen niiden asentamista, ja niiden jälkeen. Tässä on yksi ongelmistani, sillä Kali Linuxiin Apache ja SSH on jo valmiiksi asennettu, joten itselläni ei ole oikein ideaa, miten tulokset sitten eroaisivat muutenkaan. Anyways, ajoin muita komentoja, kuten 

    $ nmap -A

Joka palautti vastaukseksi seuraavan:

    $ sudo nmap -A localhost 
    Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-04-04 12:16 EDT
    Nmap scan report for localhost (127.0.0.1)
    Host is up (0.000013s latency).
    Other addresses for localhost (not scanned): ::1
    All 1000 scanned ports on localhost (127.0.0.1) are in ignored states.
    Not shown: 1000 closed tcp ports (reset)
    Too many fingerprints match this host to give specific OS details
    Network Distance: 0 hops

    OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
    Nmap done: 1 IP address (1 host up) scanned in 1.67 seconds

Ajoin myös huvin vuoksi komennon "nmap -A" kohteelle "scanme.nmap.org" joka on tapa testata Nmapin toimivuutta oikealla kohteella. Komennon ajo palautti seuraavan:

    nmap -A scanme.nmap.org
    Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-04-04 12:12 EDT
    Nmap scan report for scanme.nmap.org (45.33.32.156)
    Host is up (0.17s latency).
    Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
    Not shown: 996 filtered tcp ports (no-response)
    PORT      STATE SERVICE    VERSION
    22/tcp    open  ssh        OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
    | ssh-hostkey: 
    |   1024 ac:00:a0:1a:82:ff:cc:55:99:dc:67:2b:34:97:6b:75 (DSA)
    |   2048 20:3d:2d:44:62:2a:b0:5a:9d:b5:b3:05:14:c2:a6:b2 (RSA)
    |   256 96:02:bb:5e:57:54:1c:4e:45:2f:56:4c:4a:24:b2:57 (ECDSA)
    |_  256 33:fa:91:0f:e0:e1:7b:1f:6d:05:a2:b0:f1:54:41:56 (ED25519)
    80/tcp    open  http       Apache httpd 2.4.7 ((Ubuntu))
    |_http-title: Go ahead and ScanMe!
    |_http-server-header: Apache/2.4.7 (Ubuntu)
    |_http-favicon: Nmap Project
    9929/tcp  open  nping-echo Nping echo
    31337/tcp open  tcpwrapped
    Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
    
    Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
    Nmap done: 1 IP address (1 host up) scanned in 23.93 seconds

Mitä tulee komentojen eroavaisuuksiin, mitä nyt ymmärsin, niin tavallinen "nmap localhost" ajaa komennon perusasetuksilla, skannaten hyvin yksinkertaisesti vain portit ja niiden tilan, onko ne auki vai ei. Mutta nmap -A tarkoittaa "Aggressive" muotoa, jolloin nmap suorittaa erinlaisen, aggressiivisen skannauksen. Kyseinen skannaus eroaa huomattavasti sillä, että kohteen on paljon helpompi huomata skannaus, sillä porttien lisäksi, aggressiivinen skannaus skannaa myös käyttöjärjestelmän (-O), version (-sV), skriptiskannauksen (-sC) ja ajaa myös traceroute-komennon samalla (--traceroute).

Ajoin myös komennon "nmap -p- localhost", joka taas palauttaa kaikki kohteen portit, jolloin vastaukseksi sain tämän:

    sudo nmap -p- localhost 
    Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-04-04 12:09 EDT
    Nmap scan report for localhost (127.0.0.1)
    Host is up (0.0000040s latency).
    Other addresses for localhost (not scanned): ::1
    All 65535 scanned ports on localhost (127.0.0.1) are in ignored states.
    Not shown: 65535 closed tcp ports (reset)
    
    Nmap done: 1 IP address (1 host up) scanned in 0.71 seconds

Jos luen tuloksia oikein, omassa localhostissani ei ole avoinaisia portteja, joita voisi hyväksikäyttää tunkeutumiseen.


# Työkalu:

Tähän tehtävään en sen isommin löytänyt muuta kuin tuon työkalun jonka löytää läksyjen-tehtävänannon linkistä: https://inteltechniques.com/tools/Email.html. Laitoin tuohon oman sähköpostini jonka jälkeen painoin "Submit all" ja se avasi litanian verkkosivuja jotka ovat tarkoitettu sähköpostien etsimiseen erinäisistä vuoto-tietokannoista tai ihan vain hakukoneista. Alla vielä kuva sivusta:

![image](https://github.com/konetoivonen/laksyt/assets/164856618/3b7caae0-bbc9-475e-a968-81726e18b6e0)

# Lähteet:

https://terokarvinen.com/2024/eettinen-hakkerointi-2024/

https://inteltechniques.com/tools/index.html

https://nmap.org/

https://portswigger.net/

https://github.com/WebGoat/WebGoat/releases
