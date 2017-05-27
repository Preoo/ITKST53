# ITKST53
Säilö ITKST53-kurssin palautuksille
## Luento 1
Turvallisuus määriteltiin seuraavasti: jonkin tehtävän tai tavoitteen saavuttaminen huolimatta mahdollisista uhkatekijöistä. Mielesäni uhka voi olla muutakin kuin hyökkääjä, mutta tällä kurssilla keskitytään lähinnä ns "bad actor" tilanteeseen. Luennolla esiteltiin tapa ajatella turvallisuutta seuraavista näkökulmista:

* **policy:** tavoite, tarkoitus, toiminnan määrittely. Näitä voi olla vaikka tiedon luotettavuus tai pääsyoikeuksien määrääminen. Policy määrää mitä mekanismi pyrkii saamaan aikaan, eli mekanismi siis toteuttaa policyä. Hyökkääjä voi pyrkiä hyväksikäyttämään tai rikkomaan tätä policyä, jota yritetään mallintaa uhkamallin avulla.
* **uhkamalli:** malli tai kuvitelma mitä uhka/hyökkääjä voi tehdä tai pyrkii tekemään. Vaikea luoda täydellistä uhkamallia, etenkin jos järjestelmä ei toimi tyhjiössä, kuten näytettiin esimerkkinä luonnolla salasanan nollaamisesta ja ukloisten järjestelmien hyväksikäytöstä. Uhkamalli ovat lähinnä olettamuksia.
* **mekanismi:** järjestelmä tai ohjelmisto, jolla valittu policy taataan. Mekanismeja voivat olla pääsynhallinta, salaus, tilit ja niiden käyttöoikeuksien erottaminen. Mekanismeissa voi olla aukkoja, joita ei huomioitu uhkamallissa. Mekanismin ei välttämättä tarvitse olla vedenpitävä, kunhan voidaan väsyttää hyökkääjä. Ei taida toimia hyvin varustautunutta/valtion tukemaan hyökkääjää vastaan. Yleisesti on hyvä pyrkiä käyttämään mekanismeja pienentämään tai kuristamaan hyökkäyspinta-alaa.

Vaikeus syntyy uhkamallien laajuudesta ja voidaanko ennustaa tai arvioida hyökkääjän käyttäytymistä? Policy voi sallia hyökkääjän toimia, joten sitä suunnitellessa pitäisi hahmottaa tietoturvallinen malli. Esimerksi salasanajärjestelmässä jäähyjen käyttä arvausyrityksiä vastaan on hyvä keino parantaa turvallisuutta laajamittaista useiden tilien murtautumista vastaan. Tosin tästä voi olla vähemmän hyötyä, jos hyökkäys on kohdistettu. Muiden järjestelmien kanssa toimittaessa pitäisi omat systeemit/politiikat kehittää siten, että kriittisessä toiminnassa, kuten tilinhallinassa ei olla riippuvaisia muiden järjestelmien paljastamista tiedoista. (esim. jos tilin palautukseen riittää tieto, joka on saatavilla muista järjestelmistä, voi politiikan uudelleen miettiminen olla paikallaan. Luentoesimerkeissä ei ilmeisesti aina kyetty asettamaan hyökkääjän asemaan).

Hyviä esimerkkejä uhkamallin ongelmista olivat esitellyt heikkoudet salauksen vahvuudessa/ sertifikaattien luotettavuudessa jotka yhdistyivät nätisti mekanismeihin. Käyttäjän toimet osana uhkamallia ovat myös kiinnostava näkökulma. Kuinka järjestelmän toiminta pitäisi suunnitella, jos käyttäjä voidaan huijata toimimaan sitä vastaan? Nähtävsti varmin tapa on määritellä oikeudet siten, että käyttäjä ei kykene yksin sabotoimaan järjestlemää. Uhkamallien pitäisi myös huomioida, että hyökkääjä hallitsee laitteen, jolla palvelun kanssa kommunkoidaan. Eli uhkamalli on suunniteltava siten, että palvelupyynnöt eivät ole ain oikein muotoiltuja. Uhkamalli jossa hyökkääj toimii käyttäjän välineillä ei ole realistinen.

Mekanismien ongelmat esiintyvät virhetilanteina tai bugeina. Luentoesimerkki applen icloud salananan arvausrajapinnasta, joka ei toteuttanut muiden rajapintojen tavoin salananan arvaukseen liittyvää policyä, tai citigroup palvelu, jossa ei tarkistettu sessiota ovat esimerkkejä räikeistä ja helposti ymmärrettävistä virheistä.

Mielestäni tämä merkitsee, että usein ei voida rakentaa täysin vedenpitävää järjestelmää. Hyökkääjän käyttämät menetelmät eivät aina vastaan oletusta ja käytetyillä työkaluilla(tarkistus, auditointi, ohjelmointikieli missä ei voida suoraan käsitellä muistiosoitteita/pinoa) voidaan karsia joitain riskitekijöitä. Kuitenkin pelikenttä on silti usein liian laaja ja nojautuminen yhteen mekanismiin on huono idea. Tekninen velka ja kolmannen osapuolen järjestelmät jo itsessään kehottavat rajoittamaan yhden järjestelmän murtumisen vaikutusta(mekanismit tässä: service accounts, eri kerrokset, järjestelmän eristäminen). Tällä kerralla hieman avattu ideaa, jonka mukaan ohjelmointikielen hallitseminen itsessään ei riitä, vaan on tunnettava sen erityspiirteitä. Keinoja näiden varalle voivat olla paremmat työkalut, parempi tietotaito tai kattavempi testaus. Työkaluilla tarkoitan siis kääntäjän tai kehitysympäristön tarjoamia varoituksia tunnetuista epäturvallista tavoista. Tietotaidon parantaminen on itsestäänselvyys mutta käytännössä hyökkääjien mekanismit ovat niin syvällä, että vähemmän kokenut ohjelmoija tulee tekemään virheitä. Sen lisäksi esimerkit ja (vanhentuneet?) oppaat saattavat ohjata aloittelijan väärälle tielle, josta palaaminen on vaikeampaa. 

## Luento 2
Ylivuodot (c/c++) ovat ohjelmointikielen ominaisuuksia, jossa muistiosoitteet ovat ohjelmoijan käsiteltävissä (huonon koodin kautta täten myös hyökkääjän). Perusesimerkki ylivuodosta on bufferin, tai array:n täyttäminen yli sille varatun rajan. Hyväksikäyttö hyödyntää x86-arkkitehtuurin tuntemusta ja laitteistopinon manipulointia. Aikasemmassa luennossa(luentoäiväkirjamerkinnässä) mainittiin ylivuotoja vastaan suojautuminen käyttämällä ohjelmointikieltä, joka ei palajasta raajoja muistiosoitteita. Tämä helpottaa ohjelmoijan työtä, mutta samalla siirtää vastuun kielen runtime-ympäristön päälle ja jos tarvitaan kirjastoja, jotka eivät käytä mem-safe kieltä, voidaan vain luottaa että ylivuotoja ei voi tapahtuma kolmannen osapuolen koodissa.
 
Ylivuotoja varten päätin kerrata(ja usein syventyä uuteen asiaan) miten ylivuodot tapahtuvat ja mitä mekanismeja siinä käytetään. Pino ja sen kehykset kyllä muistuivat mutta (myöhemmille luennoilla käytävät) rekisterit ja järjestelmäkutsut vaativat pidemmän hetken. Tämä oli tärkeä sillä os labran tehtävistä (joita en siis palauta kurssin suoritusta varten mutta teen ja katselen omaan tahtiin, riippuen ajasta ja mielenkiinnosta) vaativat syvällistä tietoa rekistereistä. Aikamoinen hyppäys, jos eniten ohjelmointikokemusta on muistiturvallisista kielistä :-/. 
 
Ylivuotojen välttämiseen ehdotettiin bugien välttämistä. Erinomainen ehdotus, onnistunee mahdollisesti pienempien sovelluksien kanssa mutta kuten luennolla 1 mainittiin, niin nykyiset järjestelmät ovat entistä monimutkaisiempia. Ja kuten on tullut esille, hyökkääjän hyväksikäyttämät bugit ovat syvällä ohjelmointikielen yksityiskohdissa. Tämä on jo yksi syy, miksi bugiton ohjelmointi on haave, kaunis uni. Myös materiaali, jonka pohjalta on kukin opiskellut voi osaltaan vaikuttaa(vaikeuttaa) bugien välttämistä. Toinen tapa (pyrkiä) estämään ylivuotoja mahdollistavat bugit on analysoida ohjelmallisesti kirjoitettu lähdekoodi ja käyttää saatuaj tietoja testauksen alustamiseen tai ohjelmoidan varoittamiseen. Hyvä muistutus on pyrkiä ulottamaan testaus ohjelman suorituspuun jokaiselle "oksalle". Viimeinen esitelty tapa on käyttää ohjelmointikiletä ja ympäristö missä ylivuotoja ei tapahtudu, koska kirjoitettuohjelma ei käsittele suoraan muistia tai sen osoittimia.
 
Baggy bounds oli uusi asia ja tuotti kyllä hieman vaikeuksia hahmottaa sen toimintaperiaatetta kokonaisuudessaan julkaisua lukemalla (kuten luennoitisija mainitisi). Perusperiaate on varata muistia 2^x lohkoissa ja osoitin operaation kohdalla tarksitetaan onko osoitin sille varatulla alueella. Tämä varattu alue tod. on isompi, kuin itse objekti. Baggy bounds rajojen ulkopuolelle jäävät osoittimet merkitään siten, että niitä ei käsitellä. Tämän metodin ongelma on, että se vaatii kääntäjän tuen. Uskoakseni NX-mem ja erinäiset muistiavaruuden hajautusmenetelmät ovat yleisempiä. Syy on todennäköisesti, että vaikka baggy bounds aiheuttaa muihin vastaviin menetelmiin nähden vähemmän hävikkiä, on kehittäjille silti helpompi käyttää muita menetelmiä (kuten: DEP, aslr).  Luennolla 3 käytiin sen periaatetta tarkemmin läpi, joten säästän sinne tarkemman kirjoittelun. Tosin tässä on huomattavaa, että missä NX-muisti (non-exec) suojaa injektoidulta, hyökkääjä voi silti hyödyntää ohjelman muistissa sijaitsevia (tai ladattujen kirjastojen muistissa) olevia palasia (myöhemillä kerroilla kutsuttiin gadget:ksi, suomeksi vehje?), eli ROP.
 
Kuitenkin canaries periaate on looginen ja aikaisemmin tuttu wiki-artikkelien pohjalta. Myöskin sen ongelmat, eli jos canaryn arvo on staattinen tai ennaltaarvattava (kiinnostava idea oli käyttää jotain signaalia esimerksi istunnon tai socketin sulkemista signaalina staattisen canaryn etsimisessä. Myös pinon tilasta vuotavat menetelmät olivat uusia tuttavuuksia minulle, joku string-format metodi. Tarvittiin tarkempi tarkastelu OWASP-wikissä idean selvittämiseksi. Muistan lapsuudesta erään verkkopelin, jossa serveri saatiin kaadettua kirjoittamalla yleiseen chattiin %n%n%n%n%n%n, joka taitaa liittyä juurin tähän string format menetelmään). Muita keinoja, joissa tallennetaan muistin varauksen yhteydessä varatun muistin koko erilliseen tietueeseen on esitetty mutta niillä on oma suorituskyky/muistin tarpeensa (tarpeeksi iso, jotta tekniikkaa ei voida käyttää tuotannossa tai kriittisissä sovelluksissa).
