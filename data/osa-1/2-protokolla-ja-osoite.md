---
path: '/osa-1/2-protokolla-ja-osoite'
title: 'Protokolla ja osoite'
---

<div>
<lead>Tietokoneet kommunikoivat keskenään noudattamalla jotain yhdessä sovittua yhteyskäytäntöä eli protokollaa. Muuten ne eivät voisi ymmärtää toisiaan. Toinen kone tunnistetaan sen verkkotunnuksesta tai osoitteesta. Koneella voi olla useita erilaisia osoitteita ja niitä käytetään eri tarkoituksiin.</lead>
</div>


## Lähettäjä ja vastaanottaja

Tietoverkossa kulkevia viestejä kutsutaan usein sanomiksi. Niillä on aina lähettäjä ja vähintään yksi vastaanottaja. Usein sanomia verrataan postin välitettäväksi annettuihin kirjeisiin. Lähettäjä vain antaa sanoman tietoverkon välitettäväksi ja vastaanottaja saa viestin tietoverkosta, mutta kummankaan ei tarvitse tietää miten sanoma verkossa liikkui lähettäjän ja vastaanottajan välillä.

Lähettäjän täytyy vain määritellä sanoman sisältö ja vastaanottajan osoite. Sitten lähettäjä vain laittaa viestin verkon kuljetettavaksi ja luottaa siihen, että tietoverkko osaa siirtää viestin vastaanottajalle.

Internet-verkossa toimittaessa vastaanottajan pitää olla valmiina vastaanottamaan sanoma heti kun se on saapumassa. Internet ei jätä viestiä odottelemaan, josko vastaanottaja suostuisi ottamaan viestin vastaan. Jos vastaanottajaa ei tavoiteta, niin sanoma katoaa.

Asiakkaan ja palvelimen välisessä kommunikoinnissa tämä tarkoittaa sitä, että palvelimen pitää olla koko ajan verkossa ja valmiina vastaanottamaan viestejä. Asiakkaan sen sijaan ei tarvitse olla verkossa ennen kuin se haluaa ottaa yhteyttä palvelimeen.

Asiakkaan ja palvelimen välisessä viestien vaihdossa kumpikin osapuoli on vuorollaan lähettäjänä ja vastaanottajana, joten asiakkaankin pitää pysyä kiinni tietoverkossa kunnes se on vastaanottanut kaikki sanomat, joita se odotti palvelimen lähettävän.


## Protokolla eli yhteyskäytäntö

Jotta tietokoneiden välinen kommunikointi ja sanomien vaihto olisi mahdollista, niin niiden täytyy noudattaa yhteistä käytäntöä sekä sanomien lähettämisessä että sanomien sisällössä ja rakenteessa.

Valtaosa IETF:n standardeista onkin erilaisia internet-verkon protokollien määrittelyjä. Näiden avulla eri ohjelmoijien tekemät ohjelmat voivat kommunikoida toistensa kanssa onnistuneesti. Myös laitevalmistajien toteuttamien laitteiden pitää noudattaa standardoituja protokollia, jolla kommunikointi laitteiden välillä on mahdollista.

Esimerkiksi www-sivujen kanssa käytettävä HTTP on standardoitu IETF:n toimesta. Se on kuvattu useammassakin RFC standardissa. Uusin protokollan viestejä kuvaava standardi on [RFC7230](https://tools.ietf.org/html/rfc7230) vuodelta 2014. Sitä edellinen RFC2616 oli vuodelta 1999, joten ihan hirvittävän usein näitä vakiintuneita protokollia ei muokata. Itse asiassa myös standardisarjan numerot 7231-7235 käsittelevät HTTP-protokollaa ja sen eri piirteitä.


## Internetin protokollapino

Vaikka voimme helposti sanoa, että lähettäjä ja vastaanottaja kommunikoivat keskenään, niin todellisuudessa kommunikointi tietoverkon välityksellä on paljon monimutkaisempaa ja vaatii yhteistyötä eri laitteilta ja ohjelmistoilta. Toisaalta kuitenkin lähettäjä ja vastaanottaja kommunikoivat keskenään jonkun viestinvälityspalvelun avulla. Niiden ei tarvitse tietää, miten välityspalvelu tarkemmin toimii, kunhan se tarjoaa niille palvelun, jonka avulla viestit kulkevat lähettäjältä vastaanottajalle. Näin ne piilottavat tai abstrahoivat tarpeettomat yksityiskohdat pois omasta viestienvaihdostaan.
Vastaavasti lähettäjälle ja vastaanottajalle tällaista välityspalvelua tarjoava järjestelmä käyttää omassa toiminnassaan jotain palveluja, joiden toteutuksen yksityiskohtia sen ei tarvitse tietää.

Näistä palveluista muodostuu kerrosrakenne. Internetin sanomien välitykseen liittyvää kerrosrakennetta kutsutaan protokollapinoksi. Siinä on viisi kerrosta (sovellus, kuljetus, verkko, linkki ja fyysinen kerros). Kullakin kerroksella on määritelty tiettyjä palveluja, joita se tarjoaa yläpuolellaan olevalle kerrokselle. Vastaavasti kukin kerros käyttää alapuolellaan olevan kerroksen palveluja. Wikipediassa on kuvattu nelikerroksinen [TCP/IP-viitemalli](https://fi.wikipedia.org/wiki/TCP/IP-viitemalli), jossa linkkikerros ja fyysinen kerros on yhdistetty yhdeksi peruskerrokseksi. Internetin kannalta keskeiset kerrokset ovat kuljetus- ja verkkokerros, jotka määrittelevät internetin keskeiset protokollat TCP:n ja IP:n. Prokollapinolle on myös määritelty teoreettisempi [OSI-viitemalli](https://fi.wikipedia.org/wiki/OSI-malli), jossa on 7 kerrosta. 

![viesti kulkee sovelluskerrokselta muiden kerrosten läpi fyysiselle kerrokselle ja sieltä vastaanottajan fyysiselle kerrokselle ja käänteisessä järjestyksessä kerrosten läpi sovelluskerrokselle](../img/kerrokset.svg)

Lähettäjä ja vastaanottaja, joka kommunikoivat keskenään käyttäen HTTP-protokollaa, sijoitetaan tässä protokollapinossa sovelluskerrokselle. Tällä kerroksella ovat siis kaikki ohjelmat, joilla on jokin yhteiseen tavoitteeseen liittyvä tarve kommunikoida keskenään. Näitä ovat tyypillisesti esimerkiksi www-selain ja -palvelin, sähköpostiohjelma, pikaviestinpalvelua toteuttava ohjelma (esim. Whatsapp, Telegram, Jabber). Ne käyttävät omaan ohjelman sisäiseen kommunikointiin jotain sovellustason protokollaa, kuten HTTP tai XMPP. Sovellukset voivat ottaa käyttöön jonkun jo standardoidun sovellustason protokollan (esim. HTTP, XMPP) tai määritellä ihan oman protokollan, jota ne käyttävät. Tyypillisesti käyttäjän ohjelmat on sijoitettu sovelluskerrokselle, eivätkä käyttäjät voi suoraan käyttää alempien kerrosten protokollia.

Tietoliikenteessä puhutaan usein päästä-päähän -yhteydestä, jolla tarkoitetaan sitä, että sovellusten ei tarvitse tietää, miten viesti alemmilla kerroksilla liikkuu, vaan ne voivat luottaa siihen, että lähettäjän lähettämä viesti päätyy vastaanottajalleen toiseen päähän.

Kuljetuskerroksen tehtävä on nimenomaan tarjota sovelluskerrokselle tällainen yhteys lähettäjän ja vastaanottajan välille. Lähettäjä voi siis antaa viestinsä kuljetuskerrokselle toimitettavaksi ja olettaa, että vastaanottaja saa viestin oman tietokoneensa kuljetuskerrokselta. Kuljetuskerroksen toiminnalle voidaan asettaa myös erilaisia laatukriteerejä, esim. viestiä ei saa muuttua, kadota tai kahdentua. Toisaalta ihan yhtä hyvin voidaan kuljetuskerrokselle antaa lupa tarjota huonompilaatuista palvelua, esim. sallia viestin katoaminen. Internetin kuljetuskerroksen kaksi tärkeintä protokollaa ovat TCP ja UDP. Tutustutaan niihin tarkemmin myöhemmin tällä kurssilla.

Verkkokerros tarjoaa palveluna kuljetuskerrokselle sanoman siirron verkossa lähtöpisteestä A kohteeseen B. Verkkokerros siis tietää missä päin verkkoa eri laitteet ovat ja mitä reittiä viestit niille pitää kuljettaa. Verkkokerroksen tärkein tehtävä on siis huolehtia viestien reitittämisestä verkossa siten, että ne päätyvät oikeille vastaanottajille. Tämän kerroksen tärkein sanomien siirtoon liittyvä protokolla on IP, joka on lyhenne englanninkielen sanoista Internet Protocol eli suomennettuna Internet-verkon protokolla.

Verkkokerros on liima, joka liittää erilaiset sovellukset ja niiden kuljetustarpeet sekä erilaiset verkkoteknologiat ja niiden tarjoamat kuljetuspalvelut yhteen. Kaikkien internet-verkossa palvelua tarjoavien laitteiden täytyy osata IP-protokollaa. Tämä koskee sekä käyttäjien laitteita että verkon reitittimiä.

Linkkikerros tarjoaa verkkokerrokselle sanoman siirtopalvelun kahden vierekkäisen laitteen välillä. Laitteet ovat vierekkäisiä, jos niiden välissä ei ole muita verkkokerroksen palveluja tarjoavia laitteita. Nämä laitteet voivat olla fyysisesti lähellä toisiaan kuten kotiverkon ADSL-modeemi ja kotona olevat tietokoneet. Ne voivat yhtä hyvin olla fyysisesti hyvinkin kaukana toisistaan, kuten Hollannissa ja Yhdysvalloissa olevat reitittimet, jotka on yhdistetty toisiinsa yhdellä yhtenäisellä tuhansia kilometrejä pitkällä merikaapelilla. (Jos merikaapelin sijainnit kiinnostavat, niin verkkosivu https://www.submarinecablemap.com/ näyttää ne kartalla.)

Laitteet on voitu yhdistää toisiin erilaisilla verkkoteknologioilla. Kullakin niistä on omat protokollansa, joiden avulla linkkikerros pystyy palvelun tarjoamaan. Ethernet-verkko ja langaton WLAN-verkko ovat ehkä tunnetuimpia Internetissa käytettyjä verkkoteknologioita, mutta niitä on muitakin.

Internetin protokollapinon alin, fyysinen, kerros huolehtii bittien siirtämisestä linkkikerroksen laitteiden välillä. Tälläkin kerroksella bittien siirtoon voidaan käyttää erilaisia tekniikoita. Ne voidaan koodata valoksi valokuituun, sähköpulsseiksi koaksiaalikaapeliin tai radioaalloiksi langattoman verkon yhteyksillä. Näitä koodaustapoja emme tällä kurssilla käsittele.


<div><quiz id="ec2be8d8-89c1-5ed3-828e-314af1991f69"></quiz></div>


## Verkkotunnus eli laitteen osoite

Me olemme tottuneet käyttämään erilaisista Internet-verkon palveluista ihmiselle luettavia nimiä kuten mooc.fi, www.helsinki.fi tai vaikkapa eecs.berkeley.edu. Koska tietokoneet toimivat biteillä ja numerot on helpompi esittää bitteinä kuin kirjaimet (katso Tietokoneen toiminta -kurssin materiaaleista lisää biteistä ja numeroiden esitysmuodoista), on internet-verkon toimijoiden kesken sovittu, että kaikilla IP-protokollaa käyttävillä laitteilla pitää olla IP-numero, jolla ko. laite internet-verkossa tunnistetaan ja jonka avulla se voidaan myös löytää. Tästä käytetään myös nimeä IP-osoite. IP-numero nimitys korostaa siis tunnisteen olevan numero ja IP-osoite korostaa tunnisteen merkitystä laitteen tunnistamisessa. Molemmat nimitykset tarkoittavat samaa asiaa.

Käymme myöhemmin läpi Internet-verkon nimipalvelun (Domain Name Service, DNS) toimintaa. Nimipalvelun tehtävänä on huolehtia näiden ihmiselle luettavien nimien ja IP-numeroiden vastaavuuksista. Huomaa kuitenkin jo nyt, että yhdellä nimellä voi olla monta IP-numeroa ja yhdellä IP-numerolla voi olla monta nimeä. Jos jo nyt kiinnostaa kokeilla millaista tietoa osoitteista löytyy, niin whois-tietokannassa on tietoa nimien ja osoitteiden omistajista (tai oikeastaan tahoista, joille ko. nimet / osoitteet on rekisteröity). Nimipalvelusta tietoja taas voi kysellä vaikkapa nslookup -komennolla. Komento toimii suoraan tietokoneen komentoriviltä, mutta verkosta löytyy myös useita palveluja, jotka sallivat käyttäjiensä tehdä näitä kyselyjä www-selaimella.

IP-numero liittyy siis protokollapinon verkkokerroksen toimintaan. Muillakin kerroksilla on tarvetta tunnistaa vastapuoli, mutta niillä kerroksilla käytetään erilaisia kyseiseen toimintaan paremmin sopivia osoitteita.

IP-numeroita on kahta tyyppiä. Meillä on käytössä IP-protokollasta sekä versio 4 että versio 6. Näillä versioilla on käytössään erilainen IP-osoite. Se perinteisempi osoite [IPv4](https://fi.wikipedia.org/wiki/IP-osoite) on muodoltaan 128.214.189.90  eli siinä on neljä ryhmää numeroita erotettuna pisteillä toisistaan. Kussakin ryhmässä voi olla numerot 0-255. Eli kukin numero esittää yhden tavun (=8 bittiä) arvon. Näin IPv4:n mukaisessa osoitteessa on kaikkiaan 32 bittiä. [IPv6:n](https://fi.wikipedia.org/wiki/IPv6) mukaisia osoitteita on vasta alettu vähitellen käyttää, kun IPv4-osoitteet ovat loppuneet. IPv6:n mukainen osite on huomattavasti IPv4-osoitetta pidempi. Siinä on peräti 128 bittiä, jotta osoitteet eivät loppuisi kesken. Esimerkiksi verkkonimeä eecs.berkeley.edu vastaava IPv4 osoite on 23.185.0.1 ja IPv6 osoite on 2620:12a:8001::1.

Koska IP-osoite on laitteen tunniste maailmanlaajuisesti, sen pitää olla globaalisti ainutlaatuinen, ja siksi IP-osoitteita (katso Wikipedian [artikkeli](https://fi.wikipedia.org/wiki/IP-osoite)) hallinnoi [IANA (Internet Assigned Numbers Authority)](https://www.iana.org/). Joitakin IP-osoitteista on varattu yksityiseen käyttöön. Nämä osoitteet voi ottaa käyttöön koska tahansa, mutta niille ei voi eikä saa liikennöidä julkisessa internetissä. Palataan osoitteiden tarkempaan rakenteeseen myöhemmin.

Monet tietokoneen käyttäjät ovat törmänneet myös [MAC-osoitteeseen](https://fi.wikipedia.org/wiki/MAC-osoite). Minun käyttämässäni kannettavassa tietokoneessa koneen MAC-osoite on laitteen pohjassa olevassa tarrassa. Protokollapinon kannalta MAC-osoite liittyy linkkikerrokseen, koska se on mm. Ethernet-verkossa käytettävä laitteen tunniste. MAC-osoitteella pyritään yksilöimään laitteet siten, että millään kahdella laitteella ei ole maailmanlaajuisesti samaa tunnistetta. Aiemmin MAC-osoite oli laitevalmistajan laitteelle antama osoite, jota ei voinut vaihtaa, mutta nykyään se on ainakin joissakin tilanteissa vaihdettavissa. Protokollapinon kannalta tätä osoitetta käyttävät ne verkon osat, jotka toimivat linkkikerroksella. Linkkikerroksella ei verkkokerroksen IP-osoite ole käytettävissä, kun se on ylemmän kerroksen osoite ja piilossa linkkikerroksen oman kirjekuoren sisällä eikä siis näy linkkikerroksen toimijoille.

MAC-osoite on 48-bittiä eli 6 tavua. Koska osoite on maailmanlaajuisesti yksilöivä, niin laitevalmistajille osoitteita jakaa standardointiorganisaatio IEEE. Laitevalmistaja saa aika käyttöönsä yhden (tai useamman) osoitesarjan, jossa ensimmäiset 24 bittiä ovat samat kaikille sarjan laitteille. Niillä tunnistetaan siis kyseistä osoitesarjaa hallinnoiva laitevalmistaja. Loput 24 bittiä laitevalmistaja jakaa itse valmistamiensa laitteiden verkkoliitännöille. Laitteessa, jossa on useita verkkoliitäntöjä, on myös useita MAC-osoitteita, koska niitä tarvitaan yksi per liitäntä. Minun kannettavalla tietokoneellani on kaksi MAC-osoitetta. Toinen langalliselle ethernet-yhteydelle ja toinen langattomallalle WLAN-yhteydelle.

Verkkokerroksella käytetty IP-osoite on tarkoitettu tietyn tietokoneen tai muun internet-verkkoon liitetyn verkkolaitteen tunnistamiseen mutta se ei riitä yhdessä tietokoneessa toimivien useiden sovellusten ja niitä edustavien prosessien tunnistamiseen kyseisssä laitteessa. Siksi verkkokerroksen yläpuolella oleva kuljetuskerros käyttää [porttinumeroa](https://fi.wikipedia.org/wiki/Portti_(tietoliikenne)) tietyn sovelluskerroksen kommunikointiyhteyden tai sovelluksen tunnistamiseen. Porttinumeroita käsitellään hiukan enemmän myöhemmin kun tutustutaan tarkemmin kuljetuskerroksen toimintaan. Sovellukset liitetään tiettyyn porttinumeroon pistokkeilla (socket). Pistokkeet ovat tarpeen ohjelmoijille, jotka tekevät tietoliikennesovelluksia. Koska emme kurssilla opettele tekemään verkkosovelluksia, niin emme tutustu myöskään pistokkeisiin. Eri protokollien kohdalla kerrotaan, jos niihin liittyy sovittuja, standardoituja porttinumeroita, jotka ovat aina ko. sovelluksen käytössä.


<div><quiz id="096f0a47-e840-5331-842f-fe2605f12fac"></quiz></div>
