# Network capture

Packets captured by TCPDUMP with command "sudo tcpdump -c 5 tcp"

    tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
    listening on enp0s1, link-type EN10MB (Ethernet), snapshot length 262144 bytes
    10:24:02.571867 IP 104.17.201.110.https > debian.53094: Flags [.], ack 2125596899, win 8, options           [nop,nop,TS val 2649390053 ecr 1366758042], length 0

10:24:02.573789 IP 104.17.201.110.https > debian.53094: Flags [F.], seq 0, ack 1, win 8, options [nop,nop,TS val 2649390055 ecr 1366758042], length 0
10:24:02.573804 IP debian.53094 > 104.17.201.110.https: Flags [.], ack 1, win 501, options [nop,nop,TS val 1366758073 ecr 2649390055], length 0
10:24:02.578661 IP 868.bm-nginx-loadbalancer.mgmt.fra1.adnexus.net.https > debian.46312: Flags [R.], seq 1389925576, ack 3413172315, win 83, options [nop,nop,TS val 2491301539 ecr 3894457195], length 0
10:24:02.580575 IP 868.bm-nginx-loadbalancer.mgmt.fra1.adnexus.net.https > debian.46312: Flags [R], seq 1389925576, win 0, length 0
5 packets captured
6 packets received by filter
0 packets dropped by kernel


    Vastaukseksi tcpdump antoi 5 TCP-pohjaista pakettia, joista löytää seuraavanlaista informaatiota:

    Kellonaika, Verkkoadapteri josta paketti napattiin, TCP-lipuke, eli TCP-yhteystila, jossa liput ".", "F.", "R." ja "R", tarkoittavat seuraavia asioita:

"." : Yhteys on huomattu (Acknowledgment)
"F." : Yhteys on päätetty ja huomattu (FIN-ACK)
"R" : Yhteys on nollattu
"R." : Yhteys on nollattu ja huomattu (RST-ACK)


Napatut paketit esittävät yhteyden kiertokulun loppuosan, koska pakettien lukumäärä on rajoitettu viiteen, pakettien määrästä esiintyy kommunikointi palvelimelta selaimelle

Connection acknowledged (.) --> Connection finished and acknowledged (F.) --> Connection reset and acknowledged (R.) --> Connection Reset (R)

Paketeista esiintyy myös pakettien lähde IP-osoite, eli miltä serveriltä paketti lähetettiin koneeseen, ja mistä koneelta se lähti takaisin serverille.

Paketeissa näkyy myös pakettien pituus (length), ikkuna-koko (window-size: esim. Paketti 3, jossa "win" on "83") ja paketin järjestysnumero (esim. paketin 4 järjestysnumero: "seq 1389925576").
    
    


