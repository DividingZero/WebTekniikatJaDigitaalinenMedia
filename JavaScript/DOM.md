# DOM - Document Object Model
Document Object Model eli dokumenttioliomalli on puumainen kuvaus HTML dokumentistä.
![DOM](https://www.w3schools.com/js/pic_htmltree.gif) 
*w3schools.com*

HTML DOM on standardi, joka määrittelee kuinka HTML elementtejä valitaan, muokataan, lisätään ja poistetaan. Kaikkia elementtejä käsitellään olioina ja jokaista elementtiä, attribuuttia ja elementin sisältöä (esim. tekstiä) kutsutaan nimellä 'node'.
```html
<html>
    <head>
        <title>Esimerkki</title>
    </head>
    <body>
        <p>Tässä on yksi kappale</p>
        <script>
        const kappale = document.querySelector('p'); // valitsee dokumentistä ensimmäisen p-elementin
        console.log(kappale.innerText); // tulostaa p-elementin sisällä oleva tekstin konsoliin
        </script>
    </body>
</html>
```  
Yllä olevassa esimerkissä valittu p-elementti tallennetaan elementtioliona (tai elementtinodena) nimellä 'kappale'. Tämän jälkeen 'kappale'-oliota voidaan käsitellä [Document](https://developer.mozilla.org/en-US/docs/Web/API/Document)-rajapinnan ominaisuuksien ja metodien avulla.

## Parent/child
![DOM](https://www.w3schools.com/js/pic_htmltree.gif) 

Koska DOM kuvaa dokumentin puumaisena rakenteena, käytetään sen yhteydessä termejä vanhempi (tai äiti/isä), lapsi, ja sisar. Englanniksi parent, child ja sibling. Esim. ylläolevassa kuvassa h1-elementti on body-elementin lapsi ja a-elementin sisar. Vastaavasti body-elementti on sekä h1- ja a-elementtien vanhempi.

## [Document](https://developer.mozilla.org/en-US/docs/Web/API/Document)-rajapinta
`document`-rajapinta edustaa web-sivua, sen sisällä ovat kaikki muut dokumentin objektit. Kun haluat valita dokumentista minkä tahansa HTML-elementin, sinun tulee aloittaa document-rajapinnasta. Esim. `document.getElementByID('logo')`

### Tärkeimmät metodit ja ominaisuudet
```javascript
document.querySelector('#logo')        // hakee dokumentista yhden elementin css-valitsimen avulla. Tässä tapauksessa tietyllä id:llä
document.querySelectorAll('.nappi')    // hakee dokumentista elementtejä css-valitsimen avulla.
document.getElementById('logo')        // hakee dokumentista elementin tietyllä id:llä

// komennot voidaan kohidstaa myös valittuun nodeen:
solmu.getElementsByTagName("p")     // hakee solmu-nodesta kaikki p-elementit
solmu.appendChild(lapsi)            // lisää solmu-nodeen lapsinoden
solmu.removeChild(lapsi)            // poistaa solmu-nodesta lapsinoden
```
Koska document-rajapinta perii [Node](https://developer.mozilla.org/en-US/docs/Web/API/Node)- ja [Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)-rajapinnat, itse asiassa tärkeimmät ominaisuudet tulevat niistä sekä [ParnetNode](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode)-rajapinnasta:
```javascript
elem.innerHTML   // elem-noden sisältämä HTML-koodi
elem.innerText   // elem-noden sisältämä teksti
elem.nodeName    // elem-noden elementtityyppi
elem.nodeValue   // elem-noden arvo
elem.parentNode  // elem-noden parentnode
elem.childNodes  // elem-noden lapsinodet
elem.children    // elem-noden lapsielementit
elem.firstChild  // elem-noden ensimmäinen lapsinode 
elem.lastChild   // elem-noden viimeinen lapsinode
elem.attributes  // elem-noden attribuuttinodet
```
### Object collections
Dokumentista voidaan myös hakea elementtikokoelmia:
```javascript
document.forms      // hakee kaikki form-elementit
document.images     // hakee kaikki kuva-elementit
document.links      // hakee kaikki area- ja a-elementit, joilla on href-attribuutti
document.scripts    // hakee kaikki script-elementit
```

## Esimerkkejä

1. Valitse dokumentista elementti, jonka id on 'uutiset' ja tallenna elementtinode nimellä 'u'. Sen jälkeen valitse elementtinodesta 'u' kaikki p-elementit ja tallenna elementtilista nimellä 'p':
    ```javascript
    const u = document.getElementById('uutiset');
    const p = u.getElementsByTagName('p');
    
    // sama voidaan kirjoittaa myös ilman välimuuttujaa
    const p = document.getElementById('uutiset').getElementsByTagName("p");
 
    // tai yhdellä komennolla
    const p = document.querySelectorAll('#uutiset p');
    ```
1. Valitse listan `<ul>` toinen  nimike (item eli `<li>`):  
     ```html
        <ul>
           <li>Eka nimike</li>
           <li>Toka nimike</li>
           <li>Kolmas nimike</li>
        </ul>
    ```
    
    ```javascript
    const toka = document.getElementsByTagName('li')[1];  // getElementsByTagname palauttaa taulukon. Talukon järjestysnumerot alkavat nollasta, joten 1 tarkoittaa toista <li>-elementtiä.
    ```

1. Elementtilista kaikista "tiedote"-luokkaan kuuluvista p-elementeistä:   
    ```javascript
    const x = document.querySelectorAll('p.tiedote');
    ```
1. Elementin sisällön muuttaminen:
   ```html
   <p id="pvm"><span class="sininen">Maanantai</span></p>
   
   <script>
   document.getElementById('pvm').innerHTML = '<span class="punainen">Tiistai</span>';
   </script>
   ```
1. Attribuutin arvon muuttaminen:
   ```html
   <img id="logo" src="metropolia.png"  alt="Joku kuva">
   
   <script>
   document.getElementById('logo').src = 'laurea.png';                 // käytetään attribuutin nimeä ominaisuutena
   document.getElementById('logo').setAttribute('src', 'laurea.png');  // tai setAttribute()-metodia
   </script>
   ```
1. HTML:n lisääminen sivulle:
    1. innerHTML-ominaisuuden avulla:
       ```html
       <div id="esimerkki"></div>
       
       <script>
       const div = document.querySelector('#esimerkki');          // haetaan elementti, jonka id on esimerkki
       const html =                                               // tehdään monirivinen merkkijono, huomaa backtick merkkijonon ympärillä (gravis)
               `<p>
                   Tässä on kappale tekstiä, jossa on kuva.
                   <img src="http://placekitten.com/321/241" alt="Kissa">
                </p>`;
       div.innerHTML = html;                                      // asetetaan merkkijono 'html' valitun elementin HTML-sisällöksi
       </script>
       ```
    1. Sama DOM-metodien avulla
       ```html
           <div id="esimerkki"></div>
           
           <script>
           const div = document.querySelector('#esimerkki');       // haetaan elementti, jonka id on esimerkki
    
           const i = document.createElement('img');                // tehdään img elementti
           i.src = 'http://placekitten.com/321/241';               // asetetaan src-attribuutti
           i.alt = 'Kissa';                                        // asetetaan alt-attribuutti
           
           const t = document.createTextNode('Tässä on kappale tekstiä, jossa on kuva.');  // tehdään tekstinoodi
    
           const p = document.createElement('p');                  // tehdään p-elementti
           p.appendChild(t);                                       // lisätään teksti p-elementtin
           p.appendChild(i);                                       // lisätään kuva p-elementtiin
    
           div.appendChild(p);                                     // lisätään p-elementti HTML-dokumentista valittuun elementtiin
                                                                   // tässä vaiheessa luotu HTML ilmestyy dokumenttin.
           </script>
        ```
### CSS:n käsittely
JavaScriptillä voidaan myös muokata elementtien ulkoasua. Vaihtoehtoina tällöin on joko vaihtaa style-attribuutin tai class-attribuuttien arvoja aivan kuten HTML-dokumenteissa on normaalistikin tapana.

Inline eli style attribuutin muokkaaminen:

```html
<p style="background-color: #ccc; padding: 1rem;" id="kappale">Jotain tekstiä</p>

<script>
document.querySelector('#kappale').style = "color: #eee; background-color: #222; padding: 3rem;";
</script>
```
Class attribuutin muokkaaminen:
```css
/* ulkoinen css-tiedosto */
.punainen {
    color: #f00;
}

.sininen {
    color: #00f;
}
```

```html
<p class="punainen" id="kappale">Jotain tekstiä</p>

<script>
document.querySelector('#kappale').setAttribute('class', 'sininen');
// tai
document.querySelector('#kappale').classList.toggle('sininen');
</script>
```
[classList-dokumentaatio](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)

## Harjoitustehtävät
Lataa aloitustiedostot [tästä reposta](https://github.com/ilkkamtk/DOM-tehtavat).
1. teht1.html (4p)
   * Dokumentti sisältää html-taulukon, jossa on etunimi, sukunimi, nikki ja osoite.
   * Muokkaa teht1.js tiedostoa ja tee skripti joka korvaa listassa olevat tiedot omillasi.
   * Lisää JavaScriptillä listaan puhelinnumero
     * Voit lisätä myös otsikon `<th>` -elementillä
   * Poista JavaScriptillä nikki
     * Voit poistaa myös otsikon
1. teht2.html (2p)
   * Dokumentissä on kuva 1, joka on piilotettu CSS:n avulla
      * Muokkaa teht2.js tiedostoa ja tee skripti, joka tuo kuvan näkyviin style attribuuttia muokkaamalla
   * Dokumentissä on kuva 2, joka on piilotettu CSS:n avulla
      * Kirjoita käsin teht2.css tiedostoon luokka, joka tuo kuvan näkyviin
      * Muokkaa teht2.js tiedostoa ja tee skripti, joka muokkaa `<img>` elementin class attribuuttia siten, että kuva tulee näkyviin
1. teht3.html (3p)
   * teht3.js sisältää taulukon 'kuvat'
   * Tee for-silmukka, joka lisää innerHTML-ominaisuuden avulla listaan taulukossa olevat kuvat. Valmis HTML näyttää tältä: 
    ```html
    <ul>
      <li>
       <img src="lisää_osoite_tänne">
      </li>
      <li>....
    </ul>
    
    ```
    * tee for-silmukan sisällä `<li>` ja `<img>` elementit, jonka jälkeen valitse dokumentistä `<ul>` elementti ja sen sisään tulostat valmiin html-koodin innerHTML:n avulla  
1. teht4.html (3p)
   * Myös teht4.js sisältää taulukon 'kuvat'
   * Tee for-silmukka, joka lisää DOM-metodien avulla listaan taulukossa olevat kuvat. Valmis HTML näyttää tältä: 
    ```html
    <ul>
      <li>
       <img src="lisää_osoite_tänne">
      </li>
      <li>....
    </ul>
    
    ```
    * Tee for-silmukan sisällä createElement-metodilla `<li>` ja `<img>` elementit, jonka jälkeen valitse dokumentistä `<ul>` elementti ja sen sisään lisäät html elementit appendChild-metodin avulla
 1. tee tehtäviin 3 ja 4 CSS-tiedosto, joka poistaa listan edestä pallerot ([list-style-type](https://www.w3schools.com/cssref/pr_list-style-type.asp)), ja joka tekee joka toisen `<li>` elementin taustan harmaaksi ([pseudo-classes](https://www.w3schools.com/css/css_pseudo_classes.asp)) (2p)
 1. teht5.html (6p)
    * Tee skripti, joka tulostaa kellonajan `<p id=kello>` elementin sisälle sekunnin välein
        * Kellon tulee olla 24h kello ja sen tulee näyttää tunnit, minuutit ja sekunnit kussakin aina kaksi numeroa. Esim 09:34:03 tai 22:01:15.
        * Kellonaika saadaan [Date](https://www.w3schools.com/jsref/jsref_obj_date.asp)-olion avulla ja päivitetään [setInterval](BOM.md#setInterval-metodi)-metodilla

   
