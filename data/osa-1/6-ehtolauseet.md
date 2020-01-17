---
path: "/osa-1/6-ehtolauseet"
title: "Ehtolauseet ja vaihtoehtoinen toiminta"
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

- Tunnet käsitteen ehtolause ja osaat luoda ohjelmaan vaihtoehtoista toimintaa ehtolauseen avulla.
- Tunnet ehtolauseissa tyypillisesti käytettävät vertailuoperaattorit ja loogiset operaatiot.
- Osaat vertailla sekä lukuja että merkkijonoja, muistaen merkkijonoihin liittyvän equals-komennon.
- Tunnet ehtolauseen suoritusjärjestyksen ja tiedät, että ehtolauseiden läpikäynti lopetetaan ensimmäiseen ehtoon, jonka lauseke evaluoituu todeksi.

</text-box>


Ohjelmamme ovat tähän mennessä olleet lineaarisia eli ohjelmien suoritus on tapahtunut ylhäältä alaspäin ilman suuria yllätyksiä tai vaihtoehtoja. Ohjelmiin halutaan kuitenkin usein vaihtoehtoista toiminnallisuutta, eli toiminnallisuutta joka riippuu tavalla tai toisella ohjelmassa olevien muuttujien tilasta.

Jotta ohjelman suoritus voisi _haarautua_ esimerkiksi käyttäjän antaman syötteen perusteella, tarvitsemme käyttöömme **ehtolauseen**. Yksinkertaisin ehtolause on seuraavanlainen.

```java
System.out.println("Hei maailma!");
if (true) {
    System.out.println("Et voi välttää tätä koodia!");
}
```

<sample-output>

Hei maailma!
Et voi välttää tätä koodia!

</sample-output>

Ehtolause alkaa avainsanalla `if`, jota seuraa sulut. Sulkujen sisälle asetetaan lauseke, joka evaluoidaan kun ehtolause saavutetaan. Evaluoinnin tulos on totuusarvo, yllä evaluointia ei tehty, vaan ehtolauseessa käytettiin suoraan totuusarvoa.

Sulkuja seuraa lohko, joka määritellään avaavan aaltosulun `{` ja sulkevan aaltosulun `}` sisään. Lohkon sisällä oleva lähdekoodi mikäli sulkujen sisälle asetettu lauseke evaluoidaan todeksi (true).

Tarkastellaan esimerkkiä, missä ehtolauseen lausekkeessa vertaillaan lukuja.

```java
int luku = 11;
if (luku > 10) {
    System.out.println("Luku oli suurempi kuin 10");
}
```

Jos ehtolauseen lauseke evaluoidaan todeksi, yllä "jos muuttujassa luku oleva arvo on suurempi kuin 10", ohjelman suoritus siirtyy ehtolauseen määrittelemään lohkoon. Jos taas lauseke on epätotta, ohjelman suoritus siirtyy ehtolauseeseen liittyvän lohkon päättävän aaltosulun jälkeiseen lauseeseen.

Huomaa, että `if` -lauseen perään ei tule puolipistettä, sillä lause ei lopu ehto-osan jälkeen.

<programming-exercise name="Ylinopeussakko" tmcname='osa01-Osa01_24.Ylinopeussakko'>

Tee ohjelma, joka kysyy käyttäjältä kokonaisluvun ja tulostaa merkkijonon "Ylinopeussakko!" jos luku on suurempi kuin 120.

<sample-output>

Kerro nopeus:
**15**

</sample-output>

<sample-output>

Kerro nopeus:
**135**
Ylinopeussakko!

</sample-output>

</programming-exercise>


## Ohjelmakoodin sisennyksestä ja lohkoista

Lohkolla tarkoitetaan aaltosulkujen rajaamaa aluetta. Ohjelman sisältävä lähdekooditiedosto sisältää merkkijonon `public class`, jota seuraa ohjelman nimi ja lohkon avaava aaltosulku. Lohko päättyy sulkevaan aaltosulkuun. Alla olevassa kuvassa on näytettynä värjättynä ohjelman lohko.

![Esimerkki lohkoista](../img/lohkoesimerkki-1.png)

Ohjelmissa toistuva rimpsu `public static void main(String[] args)` aloittaa oman lohkon, jonka sisällä oleva lähdekoodi suoritetaan kun ohjelma käynnistetään -- rimpsu on oikeastaan jokaisen ohjelman aloituskohta. Yllä olevassa esimerkissä on todellisuudessa kaksi lohkoa, kuten alla olevasta kuvasta huomaamme.

![](../img/lohkoesimerkki-2.png)

Lohkot määrittelevät ohjelman rakennetta ja rajaavat ohjelmaa. Aaltosuluille tulee aina löytyä pari: koodi, josta josta puuttuu lohkon päättävä (tai aloittava) aaltosulku, on virheellinen.

Myös ehtolause aloittaa lohkon.

Lohkoihin liittyy ohjelman rakenteen ja toiminnan määrittelyn lisäksi luettavuuteen liittyvä seikka. Lohkojen sisällä oleva koodi sisennetään. Esimerkiksi ehtolauseeseen liittyvän lohkon sisältämä lähdekoodi sisennetään neljä välilyöntiä sisemmälle kuin ehtolauseen aloittava `if`-komento. Neljä merkkiä saa myös tabulaattorimerkillä (q:n vasemmalla puolella oleva näppäin). Kun lohko sulkeutuu, eli tulee `}`-merkki, sisennys loppuu. `}`-merkki on samalla tasolla kuin ehtolauseen aloittanut `if`-komento.

Alla oleva esimerkki on sisennetty väärin.

```java
if (luku > 10) {
luku = 9;
}
```

Alla oleva esimerkki on sisennetty oikein.

```java
if (luku > 10) {
    luku = 9;
}
```

<text-box variant="hint" name="Automaattinen ohjelmakoodin sisentäminen">

Javassa koodia sisennetään neljän välilyönnin tai yhden tabulaattorin verran jokaisen lohkon kohdalla. Käytä sisentämiseen joko välilyöntejä tai tabulaattoreita. Joissakin tapauksissa sisennys saattaa hajota mikäli käytät molempia. NetBeans auttaa tässä kun painat kirjainyhdistelmää "alt + shift + f" (macOS "control + shift + f").

Jatkossa ohjelmakoodi tulee sisentää oikein myös tehtävissä. Jos sisennys on väärin, ei ohjelmointiympäristö hyväksy tehtävää. Näät sisennysvirheet testien tuloksissa keltaisena.

![Esimerkki virheviestistä](sisennysvirhe.png "Esimerkki virheviestistä")

Yllä olevassa virheviestissä sanotaan että rivin 8 alussa olisi pitänyt olla 8 välilyöntiä sisennystä, mutta siellä olikin vain 2 välilyöntiä. Tässä tapauksessa sisennyksen saa korjattua oikeaksi lisäämällä rivin alkuun 6 välilyöntiä lisää.

</text-box>

<programming-exercise name="Sisennys kuntoon" tmcname='osa01-Osa01_25.SisennysKuntoon'>

Tehtäväpohjassa on ehtolauseen käyttöä demonstroiva ohjelma. Ohjelma on kuitenkin sisennetty väärin.

Kokeile ajaa testit ennen kuin teet mitään. TMC näyttää sisennysvirheet eri lailla kuin ohjelmalogiikassa olevat virheet.

Kun huomaat, miten sisennysvirheet merkitään, korjaa virheet. Opettele käyttämään automaattista ohjelmakoodin sisentämistä jo nyt.


</programming-exercise>


## Vertailuoperaattorit

Vertailuoperaattoreita ovat seuraavat:

* `>`suurempi kuin
* `>=`suurempi tai yhtä suuri kuin
* `<`pienempi kuin
* `<=` pienempi tai yhtä suuri kuin
* `==` yhtä suuri kuin
* `!=` erisuuri kuin

```java
int luku = 55;

if (luku != 0) {
    System.out.println("Luku oli erisuuri kuin 0");
}

if (luku >= 1000) {
    System.out.println("Luku oli vähintään 1000");
}
```

<sample-output>

Luku oli erisuuri kuin 0

</sample-output>

<programming-exercise name="Orwell" tmcname='osa01-Osa01_26.Orwell'>

Tee ohjelma, joka kysyy käyttäjältä kokonaisluvun ja tulostaa merkkijonon "Orwell" jos luku on täsmälleen 1984.

<sample-output>

Anna luku:
**1983**

</sample-output>

<sample-output>

Anna luku:
**1984**
Orwell

</sample-output>

</programming-exercise>


<programming-exercise name="Wanha" tmcname='osa01-Osa01_27.Wanha'>

Tee ohjelma, joka kysyy käyttäjältä vuosilukua. Jos käyttäjä syöttää luvun, joka on pienempi kuin 2015, ohjelma tulostaa merkkijonon "Wanha!".

<sample-output>

Anna vuosiluku:
**2017**

</sample-output>

<sample-output>

Anna vuosiluku:
**2013**
Wanha!

</sample-output>

</programming-exercise>


## Muulloin eli else

Jos ehtolauseen sulkujen sisällä oleva lauseke evaluoituu epätodeksi, ohjelmakoodin suoritus siirtyy ehtolauseen lohkon lopettavan aaltosulun seuraavaan lauseeseen. Tämä ei aina ole toivottua, vaan usein halutaan luoda vaihtoehtoinen toiminta tilanteeseen, missä ehtolauseen lauseke on epätotta.

Tämä onnistuu `if`-komennon yhteydessä käytettävän `else`-komennon avulla.

```java
int luku = 4;

if (luku > 5) {
    System.out.println("Lukusi on suurempi kuin viisi!");
} else {
    System.out.println("Lukusi on viisi tai alle!");
}
```

<sample-output>

Lukusi on viisi tai alle!

</sample-output>

Jos ehtolauseeseen on määritelty `else`-haara, suoritetaan else-haaran määrittelemä lohko jos ehtolauseen ehto ei ole totta. Komento `else` tulee samalle riville `if`-komennon määrittelemän lohkon lopettavan aaltosulun kanssa.


<programming-exercise name="Positiivinen luku" tmcname='osa01-Osa01_28.PositiivinenLuku'>

Tee ohjelma, joka kysyy käyttäjältä kokonaisluvun ja kertoo, onko se positiivinen (eli suurempi kuin nolla) vai ei.

<sample-output>

Anna luku:
**5**
Luku on positiivinen.

</sample-output>

<sample-output>

Anna luku:
**-2**
Luku ei ole positiivinen.

</sample-output>

</programming-exercise>


<programming-exercise name="Täysi-ikäisyys" tmcname='osa01-Osa01_29.TaysiIkaisyys'>

Tee ohjelma, joka kysyy käyttäjän ikää ja kertoo, onko tämä täysi-ikäinen (eli 18-vuotias tai vanhempi).

<sample-output>

Kuinka vanha olet?
**12**
Et ole täysi-ikäinen!

</sample-output>

<sample-output>

Kuinka vanha olet?
**32**
Olet täysi-ikäinen!

</sample-output>

</programming-exercise>


## Lisää vaihtoehtoja: else if

Jos vaihtoehtoja on useampia käytetään `else if`-komentoa. Komento `else if` on kuin `else`, mutta lisäehdolla. `else if` tulee `if`-ehdon jälkeen, ja niitä voi olla useita.

```java
int luku = 3;

if (luku == 1) {
    System.out.println("Luku on yksi");
} else if (luku == 2) {
    System.out.println("Lukuna on kaksi");
} else if (luku == 3) {
    System.out.println("Kolme lienee lukuna!");
} else {
    System.out.println("Jotain muuta!");
}
```

<sample-output>

Kolme lienee lukuna!

</sample-output>

Luetaan yllä oleva esimerkki: 'Jos luku on yksi, tulosta "Luku on yksi", muuten jos luku on kaksi, tulosta "Lukuna on kaksi", muuten jos lukuna on kolme, tulosta "Kolme lienee lukuna!". Muulloin, tulosta "Jotain muuta!"'.

Yllä olevan ohjelman askeleittainen visualisointi:

<code-states-visualizer input='{"code":"public class Esimerkki {\n  public static void main(String[] args) {\n    int luku = 3;\n    \n    if (luku == 1) {\n      System.out.println(\"Luku on yksi\");\n    } else if (luku == 2) {\n      System.out.println(\"Lukuna on kaksi\");\n    } else if (luku == 3) {\n      System.out.println(\"Kolme lienee lukuna!\");\n    } else {\n      System.out.println(\"Jotain muuta!\");\n    }\n  }\n}","stdin":"","trace":[{"stdout":"","event":"call","line":3,"stack_to_render":[{"func_name":"main:3","encoded_locals":{},"ordered_varnames":[],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"1","frame_id":1}],"globals":{},"ordered_globals":[],"func_name":"main","heap":{}},{"stdout":"","event":"step_line","line":3,"stack_to_render":[{"func_name":"main:3","encoded_locals":{},"ordered_varnames":[],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"2","frame_id":2}],"globals":{},"ordered_globals":[],"func_name":"main","heap":{}},{"stdout":"","event":"step_line","line":5,"stack_to_render":[{"func_name":"main:5","encoded_locals":{"luku":3},"ordered_varnames":["luku"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"4","frame_id":4}],"globals":{},"ordered_globals":[],"func_name":"main","heap":{}},{"stdout":"","event":"step_line","line":7,"stack_to_render":[{"func_name":"main:7","encoded_locals":{"luku":3},"ordered_varnames":["luku"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"8","frame_id":8}],"globals":{},"ordered_globals":[],"func_name":"main","heap":{}},{"stdout":"","event":"step_line","line":9,"stack_to_render":[{"func_name":"main:9","encoded_locals":{"luku":3},"ordered_varnames":["luku"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"12","frame_id":12}],"globals":{},"ordered_globals":[],"func_name":"main","heap":{}},{"stdout":"","event":"step_line","line":10,"stack_to_render":[{"func_name":"main:10","encoded_locals":{"luku":3},"ordered_varnames":["luku"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"16","frame_id":16}],"globals":{},"ordered_globals":[],"func_name":"main","heap":{}},{"stdout":"Kolme lienee lukuna!\n","event":"step_line","line":14,"stack_to_render":[{"func_name":"main:14","encoded_locals":{"luku":3},"ordered_varnames":["luku"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"20","frame_id":20}],"globals":{},"ordered_globals":[],"func_name":"main","heap":{}},{"stdout":"Kolme lienee lukuna!\n","event":"return","line":14,"stack_to_render":[{"func_name":"main:14","encoded_locals":{"luku":3,"__return__":["VOID"]},"ordered_varnames":["luku","__return__"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"21","frame_id":21}],"globals":{},"ordered_globals":[],"func_name":"main","heap":{}}],"userlog":"Debugger VM maxMemory: 455M\n"}'></code-states-visualizer>


<programming-exercise name="Suurempi tai yhtäsuuri" tmcname='osa01-Osa01_30.SuurempiTaiYhtasuuri'>

Tee ohjelma, joka kysyy käyttäjältä kaksi kokonaislukua ja tulostaa niistä suuremman. Jos luvut ovat yhtä suuret, ohjelma huomaa myös tämän.

Esimerkkitulostuksia:

<sample-output>

Anna ensimmäinen luku:
**5**
Anna toinen luku:
**3**
Suurempi luku: 5

</sample-output>

<sample-output>

Anna ensimmäinen luku:
**5**
Anna toinen luku:
**8**
Suurempi luku: 8

</sample-output>

<sample-output>

Anna ensimmäinen luku: **5**
Anna toinen luku: **5**
Luvut ovat yhtä suuret!

</sample-output>

</programming-exercise>


## Vertailujen suoritusjärjestys

Vertailut suoritetaan järjestyksessä ylhäältä alaspäin. Kun suorituksessa päästään ehtolauseeseen, jonka ehto on totta, suoritetaan lohko ja lopetetaan vertailu.

```java
int luku = 5;

if (luku == 0) {
    System.out.println("Luku on nolla.");
} else if (luku > 0) {
    System.out.println("Luku on suurempi kuin nolla.");
} else if (luku > 2) {
    System.out.println("Luku on suurempi kuin kaksi.");
} else {
    System.out.println("Luku on pienempi kuin nolla.");
}
```

<sample-output>

Luku on suurempi kuin nolla.

</sample-output>

Yllä oleva esimerkki tulostaa merkkijonon "Luku on suurempi kuin nolla." vaikka myös ehto `luku > 2` on totta. Vertailu lopetetaan ensimmäiseen valintakäskyyn, jonka ehto on totta.


<programming-exercise name="Arvosanat ja pisteet" tmcname='osa01-Osa01_31.ArvosanatJaPisteet'>

Alla oleva taulukko kuvaa erään kurssin arvosanan muodostumista. Tee ohjelma, joka ilmoittaa kurssiarvosanan annetun taulukon mukaisesti.

| pistemäärä   | arvosana     |
| ------------ | --------     |
| < 0          | mahdotonta!  |
| 0-49         | hylätty      |
| 50-59        | 1            |
| 60-69        | 2            |
| 70-79        | 3            |
| 80-89        | 4            |
| 90-100       | 5            |
| > 100        | uskomatonta! |

Esimerkkitulostuksia:

<sample-output>

Anna pisteet [0-100]:
**37**
Arvosana: hylätty

</sample-output>

<sample-output>

Anna pisteet [0-100]:
**76**
Arvosana: 3

</sample-output>

<sample-output>

Anna pisteet [0-100]:
**95**
Arvosana: 5

</sample-output>

<sample-output>

Anna pisteet [0-100]:
**-3**
Arvosana: mahdotonta!

</sample-output>

</programming-exercise>



## Ehtolauseen lauseke ja totuusarvomuuttuja

Ehtolauseen sulkuihin asetettavan arvon tulee olla lausekkeen evaluoinnin jälkeen totuusarvotyyppinen. Totuusarvomuuttujan tyyppi on `boolean` ja arvo _true_ tai _false_.

```java
boolean onkoTotta = true;
System.out.println("Totuusarvomuuttujan arvo on " + onkoTotta);
```

<sample-output>

Totuusarvomuuttujan arvo on true

</sample-output>

Ehtolauseen voi suorittaa myös seuraavasti:

```java
boolean onkoTotta = true;
if (onkoTotta) {
    System.out.println("Aika vinhaa!");
}
```

<sample-output>

Aika vinhaa!

</sample-output>

Vertailuoperaattoreita voi käyttää myös ehtojen ulkopuolella. Tällöin vertailun tuloksena saatu totuusarvo asetetaan talteen totuusarvomuuttujaan myöhempää käyttöä varten.

```java
int eka = 1;
int toka = 3;
boolean onkoSuurempi = eka > toka;
```

Yllä olevassa esimerkissä totuusarvomuuttuja `onkoSuurempi` sisältää nyt totuusarvon _false_. Yllä olevaa esimerkkiä voi myös jatkaa ja ottaa siihen mukaan ehtolauseen.

```java
int eka = 1;
int toka = 3;
boolean onkoPienempi = eka < toka;

if (onkoPienempi) {
    System.out.println("1 on pienempi kuin 3!");
}
```

![](../img/drawings/boolean-muuttuja.png)

Yllä olevassa kuvassa ohjelmakoodia on suoritettu niin pitkään, että ohjelman muuttujat on luotu ja niihin on asetettu arvot. Muuttujassa `onkoPienempi` on arvona `true`. Seuraavana suoritetaan vertailu `if (onkoPienempi)` -- muuttujaan `onkoPienempi` liittyvä arvo löytyy sen lokerosta, ja lopulta ohjelma tulostaa:

<sample-output>

1 on pienempi kuin 3!

</sample-output>


<text-box variant='hint' name='Jakojäännös'>

Jakojäännös on hieman harvemmin käytetty operaatio, joka on kuitenkin varsin näppärä kun halutaan tarkistaa esimerkiksi luvun jaollisuutta. Jakojäännösoperaation merkki on `%`.

```java
int jakojaannos = 7 % 2;
System.out.println(jakojaannos); // tulostaa 1
System.out.println(5 % 3); // tulostaa 2
System.out.println(7 % 4); // tulostaa 3
System.out.println(8 % 4); // tulostaa 0
System.out.println(1 % 2); // tulostaa 1
```

Jos haluamme tietää onko käyttäjän syöttämä luku jaollinen neljälläsadalla, tarkastamme onko syötetyn luvun jakojäännös neljänsadan suhteen nolla.

```java
Scanner lukija = new Scanner(System.in);

int luku = Integer.valueOf(lukija.nextLine());
int jakojaannos = luku % 400;

if (jakojaannos == 0) {
    System.out.println("Luku " + luku + " on jaollinen neljälläsadalla.");
} else {
    System.out.println("Luku " + luku + " ei ole jaollinen neljälläsadalla.");
}
```

Koska jakojäännös on samanlainen operaatio kuin muutkin laskut, voi sen asettaa osaksi valintakäskyä.

```java
Scanner lukija = new Scanner(System.in);

int luku = Integer.valueOf(lukija.nextLine());

if (luku % 400 == 0) {
    System.out.println("Luku " + luku + " on jaollinen neljälläsadalla.");
} else {
    System.out.println("Luku " + luku + " ei ole jaollinen neljälläsadalla.");
}
```

</text-box>


<programming-exercise name="Pariton vai parillinen" tmcname='osa01-Osa01_32.ParitonVaiParillinen'>

Tee ohjelma, joka kysyy käyttäjältä luvun ja ilmoittaa, onko syötetty luku parillinen vai pariton.

<sample-output>

Anna luku:
**2**
Luku 2 on parillinen.

</sample-output>

<sample-output>

Anna luku:
**7**
Luku 7 on pariton.

</sample-output>

Vihje: Luvun jakojäännös 2:lla kertoo, onko luku parillinen vai pariton. Jakojäännös taas saadaan `%`-operaattorilla, tehtäväpohjassa on lisää ohjeita miten parittomuustarkastus hoituu jakojäännöksen avulla.

</programming-exercise>

## Ehtolauseet ja merkkijonojen vertailu

Siinä missä kokonaislukujen, liukulukujen, ja totuusarvojen samuutta voi verrata kahdella yhtäsuuruusmerkillä (`muuttuja1 == muuttuja2`), ei merkkijonojen samuuden vertailu kahdella yhtäsuuruusmerkillä onnistu.

Voit kokeilla tätä seuraavalla ohjelmalla:

```java
Scanner lukija = new Scanner(System.in);

System.out.println("Syötä ensimmäinen merkkijono");
String eka = lukija.nextLine();
System.out.println("Syötä toinen merkkijono");
String toka = lukija.nextLine();

if (eka == toka) {
    System.out.println("Merkkijonot olivat samat!");
} else {
    System.out.println("Merkkijonot olivat eri!");
}
```

<sample-output>

Syötä ensimmäinen merkkijono
**sama**
Syötä toinen merkkijono
**sama**
Merkkijonot olivat eri!

</sample-output>

<sample-output>

Syötä ensimmäinen merkkijono
**sama**
Syötä toinen merkkijono
**eri**
Merkkijonot olivat eri!

</sample-output>

Tämä liittyy merkkijonojen sisäiseen toimintaan sekä siihen, miten muuttujien vertailu on Javassa toteutettu. Käytännössä vertailun toimintaan vaikuttaa se, kuinka paljon tietoa muuttuja voi sisältää -- merkkijonot voivat sisältää äärettömän määrän merkkejä, kun taas kokonaisluvut, liukuluvut ja totuusarvot sisältävät aina yhden luvun tai arvon. Muuttujia, jotka sisältävät aina vain yhden luvun tai arvon voi verrata yhtäsuuruusmerkillä, kun taas enemmän tietoa sisältävillä muuttujille tällainen vertailu ei toimi. Palaamme tähän tarkemmin myöhemmin tällä kurssilla.

Merkkijonojen vertailussa käytetään merkkijonomuuttujiin liittyvää `equals`-komentoa. Komento toimii seuraavalla tavalla:

```java
Scanner lukija = new Scanner(System.in);

System.out.println("Syötä merkkijono");
String syote = lukija.nextLine();

if (syote.equals("merkkijono")) {
    System.out.println("Luit ohjeet oikein, hyvä!");
} else {
    System.out.println("Metsään meni!");
}
```

<sample-output>

Syötä merkkijono
**ok!**
Metsään meni!

</sample-output>

<sample-output>

Syötä merkkijono
**merkkijono**
Luit ohjeet oikein, hyvä!

</sample-output>

Komento equals kirjoitetaan merkkijonomuuttujan jälkeen siten, että se kiinnitetään pisteellä vertailtavaan muuttujaan. Komennolle annetaan parametrina merkkijono, johon muuttujaa vertaillaan. Mikäli merkkijonomuuttujaa vertaillaan suoraan merkkijonoon, voi merkkijonon asettaa hipsuilla merkittynä equals-komennon sulkujen sisään. Muulloin sulkujen sisään asetetaan sen merkkijonomuuttujan nimi, johon merkkijonomuuttujan sisältämää merkkijonoa verrataan.

Alla olevassa esimerkissä luetaan käyttäjältä kaksi merkkijonoa. Ensin tarkastetaan ovatko syötetyt merkkijonot samat, jonka jälkeen tarkastetaan onko syötettyjen merkkijonojen arvo "kaksi merkkijonoa".

```java
Scanner lukija = new Scanner(System.in);

System.out.println("Syötä kaksi merkkijonoa");
String eka = lukija.nextLine();
String toka = lukija.nextLine();

if (eka.equals(toka)) {
    System.out.println("Merkkijonot olivat samat!");
} else {
    System.out.println("Merkkijonot olivat eri!");
}

if (eka.equals("kaksi merkkijonoa")) {
    System.out.println("Nokkelaa!");
}

if (toka.equals("kaksi merkkijonoa")) {
    System.out.println("Ovelaa!");
}
```

<sample-output>

Syötä kaksi merkkijonoa
**hei**
**maailma**
Merkkijonot olivat eri!

</sample-output>

<sample-output>

Syötä kaksi merkkijonoa
**kaksi merkkijonoa**
**maailma**
Merkkijonot olivat eri!
Nokkelaa!

</sample-output>

<sample-output>

Syötä kaksi merkkijonoa
**samat**
**samat**
Merkkijonot olivat samat!

</sample-output>


<programming-exercise name="Tunnussana" tmcname='osa01-Osa01_33.Tunnussana'>

Tee ohjelma, joka kysyy käyttäjältä tunnussanaa. Mikäli tunnussana on "Caput Draconis", ohjelma tulostaa "Tervetuloa!". Muulloin ohjelman tulostus on "Hus siitä!".

<sample-output>

Tunnussana?
**Wattlebird**
Hus siitä!

</sample-output>

<sample-output>

Tunnussana?
**Caput Draconis**
Tervetuloa!

</sample-output>

</programming-exercise>


<programming-exercise name="Samat sanat" tmcname='osa01-Osa01_34.SamatSanat'>

Tee ohjelma, joka kysyy käyttäjältä kahta merkkijonoa. Mikäli merkkijonot ovat samat, ohjelma tulostaa "Samat sanat", muulloin ohjelma tulostaa "Ei sitten".

<sample-output>

Syötä ensimmäinen merkkijono:
**hei**
Syötä toinen merkkijono:
**hei**
Samat sanat

</sample-output>

<sample-output>

Syötä ensimmäinen merkkijono:
**hei**
Syötä toinen merkkijono:
**maailma**
Ei sitten

</sample-output>

</programming-exercise>


## Loogiset operaatiot


Ehtolauseen lauseke voi koostua useammasta osasta, joissa käytetään loogisia operaatioita **ja** `&&`, **tai** `||`, sekä **ei** `!`.

* Kahdesta lausekkeesta koostuva lauseke, joka yhdistetään ja-operaatiolla, on totta jos ja vain jos yhdistettävistä lausekkeista molemmat evaluoituvat todeksi.
* Kahdesta lausekkeesta koostuva lauseke, joka yhdistetään tai-operaatiolla, on totta jos jompikumpi tai molemmat yhdistettävistä lausekkeista evaluoituvat todeksi.
* Loogista operaatiota ei käytetään totuusarvon muuntamiseen truesta falseksi tai falsesta trueksi.

Seuraavassa yhdistetään `&&`:lla eli ja-operaatiolla kaksi yksittäistä ehtoa. Koodilla tarkistetaan, onko muuttujassa oleva luku suurempi kuin 4 ja pienempi kuin 11, eli siis välillä 5-10:


```java
System.out.println("Onkohan luku väliltä 5-10: ");
int luku = 7;

if (luku >= 5 && luku <= 10) {
    System.out.println("On! :)");
} else {
    System.out.println("Ei ollut :(");
}
```

<sample-output>

Onkohan luku väliltä 5-10:
On! :)

</sample-output>

Seuraavassa annetaan `||`:n eli tai-operaation avulla kaksi vaihtoehtoa, onko luku pienempi kuin 0 tai suurempi kuin 100. Ehto toteutuu jos luku täyttää jommankumman ehdon:

```java
System.out.println("Onkohan luku pienempi kuin 0 tai suurempi kuin 100");
int luku = 145;

if (luku < 0 || luku > 100) {
    System.out.println("On! :)");
} else {
    System.out.println("Ei ollut :(");
}
```

<sample-output>

Onkohan luku pienempi kuin 0 tai suurempi kuin 100
On! :)

</sample-output>


Seuraavassa käännetään `!` ei-operaatiolla lausekkeen `luku > 4` tulos. Ei-operaatio merkitään lauseketta ennen niin, että käännettävä lauseke rajataan suluilla, ja ei-operaatio lisätään sulkuja ennen.

```java
int luku = 7;

if (!(luku > 4)) {
    System.out.println("Luku ei ole suurempi kuin 4.");
} else {
    System.out.println("Luku on suurempi tai yhtäsuuri kuin 4.");
}
```

<sample-output>

Luku on suurempi tai yhtäsuuri kuin 4.

</sample-output>

Alla on kuvattuna lausekkeiden toimintaa kun lausekkeissa on loogisia operaatioita.


| luku  | luku > 0  | luku < 10  | luku > 0 && luku < 10  | !(luku > 0 && luku < 10)  | luku > 0 \|\| luku < 10  |
| ----- | --------- | ---------- | ---------------------- | ------------------------- | ---------------------- |
| -1    | false     | true       | false                  | true                      | true                   |
| 0     | false     | true       | false                  | true                      | true                   |
| 1     | true      | true       | true                   | false                     | true                   |
| 9     | true      | true       | true                   | false                     | true                   |
| 10    | true      | false      | false                  | true                      | true                   |


<programming-exercise name='Iän tarkistus' tmcname='osa01-Osa01_35.IanTarkistus'>

Tee ohjelma, joka kysyy käyttäjän iän ja tarkistaa, että se on mahdollinen (ainakin 0 ja korkeintaan 120). Käytä ohjelmassa vain yhtä `if`-komentoa.

<sample-output>

Kuinka vanha olet? **10**
OK

</sample-output>

<sample-output>

Kuinka vanha olet? **55**
OK

</sample-output>

<sample-output>

Kuinka vanha olet? **-3**
Mahdotonta!

</sample-output>

<sample-output>

Kuinka vanha olet? **150**
Mahdotonta!

</sample-output>

</programming-exercise>


## Ehtolauseiden suoritusjärjestys

Tutustutaan ehtolauseiden suoritusjärjestykseen klassisen ohjelmointiongelman kautta.

_'Kirjoita ohjelma, joka kysyy käyttäjältä lukua yhden ja sadan väliltä ja tulostaa luvun. Jos luku on kolmella jaollinen, luvun sijaan tulostetaan "Fizz". Jos luku on viidellä jaollinen, luvun sijaan tulostetaan "Buzz". Jos luku on sekä kolmella että viidellä jaollinen, luvun sijaan tulostetaan "FizzBuzz"'._

Ohjelmoija lähtee ratkaisemaan tehtävää lukemalla ongelmakuvauksen, ja luomalla ohjelmakoodia ongelmakuvausta seuraten. Koska ohjelman suoritusehdot esitellään ongelmassa annetussa järjestyksessä, muodostuu ohjelman rakenne järjestyksen perusteella. Ohjelman rakenne muodostuu seuraavien askelten perusteella:

* Tee ohjelma, joka lukee luvun käyttäjältä ja tulostaa sen.
* Jos luku on jaollinen kolmella, tulosta luvun sijaan merkkijono "Fizz".
* Jos luku on jaollinen viidellä, tulosta luvun sijaan merkkijono "Buzz".
* Jos luku on jaollinen kolmella ja viidellä, tulosta luvun sijan merkkijono "FizzBuzz".

Jos-tyyppiset ehdot on helppo toteuttaa `if - else if - else` -valintakäskyjen avulla. Alla oleva koodi on toteutettu yllä olevien askelten perusteella, mutta se ei kuitenkaan toimi oikein, kuten alla olevista esimerkeistä huomataan.

```java
Scanner lukija = new Scanner(System.in);

int luku = Integer.valueOf(lukija.nextLine());

if (luku % 3 == 0) {
    System.out.println("Fizz");
} else if (luku % 5 == 0) {
    System.out.println("Buzz");
} else if (luku % 3 == 0 && luku % 5 == 0) {
    System.out.println("FizzBuzz");
} else {
    System.out.println(luku);
}
```

<sample-output>

**3**
Fizz

</sample-output>


<sample-output>

**4**
4

</sample-output>

<sample-output>

**5**
Buzz

</sample-output>

<sample-output>

**15**
Fizz

</sample-output>

Edellisessä lähestymistavassa ongelmana on se, että **ehtolauseiden läpikäynti lopetetaan ensimmäiseen ehtoon, jonka arvo on totta**. Esimerkiksi luvulla 15 tulostetaan merkkijono "Fizz", sillä luku on kolmella jaollinen (15 % 3 == 0).

Yksi lähestymistapa yllä olevan ajatusketjun kehittämiseen on ensin etsiä **vaativin ehto** ja toteuttaa se. Tämän jälkeen toteutettaisiin muut ehdot. Yllä olevassa esimerkissä ehto "jos luku on jaollinen kolmella **ja** viidellä" vaatii kahden tapauksen toteutumista. Nyt ajatusketju olisi muotoa.

1. Tee ohjelma, joka lukee luvun käyttäjältä.
2. Jos luku on jaollinen kolmella ja viidellä, tulosta luvun sijan merkkijono "FizzBuzz".
3. Jos luku on jaollinen kolmella, tulosta luvun sijaan merkkijono "Fizz".
4. Jos luku on jaollinen viidellä, tulosta luvun sijaan merkkijono "Buzz".
5. Muulloin ohjelma tulostaa käyttäjältä luetun luvun.


Nyt ongelmakin tuntuu ratkeavan.

```java
Scanner lukija = new Scanner(System.in);

int luku = Integer.valueOf(lukija.nextLine());

if (luku % 3 == 0 && luku % 5 == 0) {
    System.out.println("FizzBuzz");
} else if (luku % 3 == 0) {
    System.out.println("Fizz");
} else if (luku % 5 == 0) {
    System.out.println("Buzz");
} else {
    System.out.println(luku);
}
```

<sample-output>

**2**
2

</sample-output>

<sample-output>

**5**
Buzz

</sample-output>

<sample-output>

**30**
FizzBuzz

</sample-output>


<programming-exercise name='Karkausvuosi' tmcname='osa01-Osa01_36.Karkausvuosi'>

Vuosi on karkausvuosi, jos se on jaollinen 4:llä. Kuitenkin jos vuosi on jaollinen 100:lla, se on karkausvuosi vain silloin, kun se on jaollinen myös 400:lla.

Tee ohjelma, joka lukee käyttäjältä vuosiluvun, ja tarkistaa, onko vuosi karkausvuosi.

<sample-output>

Anna vuosi: **2011**
Vuosi ei ole karkausvuosi.

</sample-output>

<sample-output>

Anna vuosi: **2012**
Vuosi on karkausvuosi.

</sample-output>

<sample-output>

Anna vuosi: **1800**
Vuosi ei ole karkausvuosi.

</sample-output>

<sample-output>

Anna vuosi: **2000**
Vuosi on karkausvuosi.

</sample-output>

Vihje 1: Jollain luvulla jaollisuuden voi tarkastaa jakojäännösoperaation `%` avulla seuraavasti.

```java
int luku = 5;

if (luku % 5 == 0) {
    System.out.println("Luku on viidellä jaollinen!");
}

if (luku % 6 != 0) {
    System.out.println("Luku ei ole kuudella jaollinen!")
}
```

<sample-output>

Luku on viidellä jaollinen!
Luku ei ole kuudella jaollinen!

</sample-output>

Vihje 2: mieti ongelmaa if, else if, else if, ... -vertailujen ketjuna ja aloita ohjelman rakentaminen tilanteesta, missä voit olla varma, että ohjelma ei ole karkausvuosi.


```java
Scanner lukija = new Scanner(System.in);
int luku = Integer.valueOf(lukija.nextLine());

if (luku % 4 != 0) {
    System.out.println("Vuosi ei ole karkausvuosi.");
} else if (...) {
    ...
} ...
```

</programming-exercise>


<programming-exercise name='Lahjaverolaskuri' tmcname='osa01-Osa01_37.Lahjaverolaskuri'>

[https://www.vero.fi/henkiloasiakkaat/omaisuus/lahja/](https://www.vero.fi/henkiloasiakkaat/omaisuus/lahja/): *Lahja tarkoittaa sitä, että omaisuus siirtyy toiselle henkilölle ilman korvausta. Lahjasta pitää maksaa lahjaveroa, jos samalta lahjanantajalta saatujen lahjojen arvo on kolmen vuoden aikana 5 000 euroa tai enemmän.*

Kun lahja tulee lähimmiltä sukulaisilta, lahjaveron määrä määräytyy seuraavan taulukon mukaan (lähde [vero.fi](https://www.vero.fi/henkiloasiakkaat/omaisuus/lahja/lahjaverolaskuri/#lahjaverotaulukot)):

| Lahja                 | Vero alarajalla  | Veroprosentti ylimenevästä  |
|-----------------------|------------------|-----------------------------|
| 5 000 -- 25 000       | 100              | 8                           |
| 25 000 -- 55 000      | 1 700            | 10                          |
| 55 000 -- 200 000     | 4 700            | 12                          |
| 200 000 -- 1 000 000  | 22 100           | 15                          |
| 1 000 000 --          | 142 100          | 17                          |

Esimerkiksi 6000 euron lahjasta tulee maksaa veroa 180 euroa (100 + (6000-5000) * 0.08), ja 75000 euron lahjasta tulee maksaa veroa 7100 euroa (4700 + (75000-55000) * 0.12).

Tee ohjelma, joka laskee lahjaveron lähimmiltä sukulaisilta annetulle lahjalle. Alla on muutama esimerkki ohjelman toiminnasta.

<sample-output>

Lahjan suuruus?
**3500**
Ei veroa!

</sample-output>


<sample-output>

Lahjan suuruus?
**5000**
Vero: 100.0

</sample-output>

<sample-output>

Lahjan suuruus?
**27500**
Vero: 1950.0

</sample-output>


</programming-exercise>
