# KESKEN

### **HUOM** Railsin versio 5.0 on jo ilmestynyt, kurssimateriaali on tehty version 4.2 pohjalta. 

**:exclamation: Asennuksessa kestää erityisesti laitoksen koneilla pitkään :exclamation:**

**:exclamation: HUOM sudoa ei tule käyttää rbenv:iä tai muita rubyn versiomanagereja käyttäessä (poislukien kirjastojen asentaminen):exclamation:** 
Asennus tehdään käyttäjän omaan kotihakemistoon.


Varaa asennukseen kunnolla aikaa ja tee se mieluusti joskus kun levypalvelinten käyttö on muutoin vähäistä. Älä jätä asennusta ohjauksen alkuun, jos haluat tehdä muutakin kuin pyöritellä peukaloita.
 
--

Asennamme tässä Rubyn version 2.3.1 ja Railsin version 4.2.7 viimeaikoina suosioon nousseella [rbenv-versiomanagerilla] (https://github.com/sstephenson/rbenv)

Voit halutessasi käyttää myös [RVM:ää](https://rvm.io/rvm/install)  eli rbenvin hieman vanhempaa lähisukulaista.

**Älä kuitenkaan missään tapauksessa asenna Rubyä/Railsia Linuxin paketinhallintajärjestelmän kautta!**

**Huom:** seuraavassa on ohjeet ainoastaan Linuxille ja OSX:lle. 

## Rails Windowsille

Ruby on Railsin asentaminen Windowsiin onnistuu (ehkä) sivun [http://railsinstaller.org/en](http://railsinstaller.org/en) ohjeilla, saatat tosin joutua tekemään sivulla  [https://gist.github.com/luislavena/f064211759ee0f806c88](https://gist.github.com/luislavena/f064211759ee0f806c88) kerrotut toimenpiteet (step1, ..., step4)

Kurssilla ei tarjota mitään tukea tai apua Windows-asennuksen tekemiseen. Jos asennus em. ohjeilla ei onnistu, Windows-käyttäjille on tarjolla [Virtual Box -image](https://github.com/mluukkai/WebPalvelinohjelmointi2017/wiki/railsin-asennus#virtualbox), johon on esiasennettu Linux sekä Rails-kehitysympäristö. 

Jos haluat välttämättä käyttää Windowsia ja et suostu virtuaaliympäristön käyttöön, tapahtuu kurssille osallistuminen omalla vastuulla.

## rbenv Linuxille

Allaolevat on testattu laitoksen koneissa ja Ubuntun uusimman LTS version kanssa. Seuraavassa luvussa ohjeet OSX:lle. Windowsiin asentaminen ainoastaan omalla vastuulla! 

**Huom:** koneella tulee olla muutamia kirjastoja, joiden asennus onnistuu Ubuntussa komennolla <code>sudo apt-get install build-essential zlib1g-dev libpq-dev git sqlite3 libsqlite3-dev</code>. Laitoksen koneilla kirjastot ovat valmiina.

**Huom2:** __fuksiläppärille__ ja ehkä muillekin koneille on [asennettava kirjasto libffi-dev](https://github.com/sstephenson/ruby-build/wiki#build-failure-of-fiddle-with-ruby-220) seuraavasti:

```shell
sudo apt-get install libffi-dev
```

Seuraa sivun [https://github.com/rbenv/rbenv#installation](https://github.com/rbenv/rbenv#installation) kohtaa Installation, Basic GitHub Checkout.
* HUOM1: kohdissa 2 ja 3 joudut (ainakin) laitoksen koneissa muuttamaan tiedostoa <code>.bashrc</code>
* HUOM2: muista asentaa myös ruby-build (yllä linkatun ohjeen 5. kohta eli https://github.com/rbenv/ruby-build#readme) ohjeen "Installing as an rbenv plugin" mukaan
* HUOM3: joudut lisäämään tiedostoon _.bashrc_ tai _.bash_profile_ myös rivin <code>eval "$(rbenv init -)"</code>

Siirry kohtaan [Rubyn ja railsin asennus](https://github.com/mluukkai/WebPalvelinohjelmointi2017/wiki/railsin-asennus#rubyn-ja-railsin-asennus)

## rbenv OSXlle

Rbenvin asennus onnistuu helpoiten homebrew:in avulla. Ohjeet homebrewin asennukseen löydät osoitteesta http://brew.sh/

**HUOM**: jos kohta suoritettavien komentojen yhteydessä tulee valitusta liittyen _clock_gettime-symbol_iin, voi [tämä korjaus](http://miuku.net/tmp/ruby-mac-asennus.txt) auttaa.

Homebrewin asennuksen jälkeen 

    brew update
    brew install rbenv
    brew install ruby-build

Lisää myös rivit  

    export PATH="$HOME/.rbenv/bin:$PATH"  
    eval "$(rbenv init -)"

Tiedostoon `.bash_profile`  kotihakemistoosi. Voit mahdollisesti joutua luomaan sen. .-alkuiset tiedostot eivät oletuksena näy Finderissä. 

Tiedoston luominen tapahtuu terminaalista käsin esim. seuraavasti 

    cd
    nano .bash_profile

kopioi rivit tiedoston, tallenna tiedosto painamalla _control_ ja _o_, sulje se komennolla  _control_ ja _x_.

Käynnistä tässä vaiheessa terminaali uudelleen. 

**Huom:** joissain vanhoissa OSX:issä saattaa olla tarve tehdä em. rivien lisäys kotihakemistossa olevaan tiedostoon `.bashrc`

## Rubyn ja Railsin asennus

Tämän jälkeen asennetaan ja määritellään käytettävä Ruby:n versio komennoilla

    rbenv install 2.3.1
    rbenv global 2.3.1

Komento asentaa Rubyn version 2.3.1, joka on Rubyn uusin versio. Voit tarkistaa asennettavissa olevat versiot komennolla <code>rbenv install --list</code>

Varmista, että komennon <code>which ruby</code> tulos on suunnilleen seuraava:

    /Users/kayttajatunnus/.rbenv/shims/ruby

Asennetaan sitten Rails antamalla komentoriviltä seuraavat komennot (vastaa mahdollisiin __Overwrite the executable?__ -kyselyihin Y):

    echo 'gem: --no-ri --no-rdoc' >> ~/.gemrc
    gem install bundler
    gem install rspec
    gem install rake 
    rbenv rehash
    gem install rails -v 4.2.7
    rbenv rehash

**Huom:** Jos saat seuraavan virheen käynnistäessäsi palvelinta: 
<code> bin/rails:6: warning: already initialized constant APP_PATH
/home/user/myProject/bin/rails:6: warning: previous 
                     definition of APP_PATH was here
</code>

Tulee sinun lisätä projektin Gemfileen seuraava rivi:
<code> gem 'rb-readline' </code>

ja ajaa:

<code> bundle install </code>


## VirtualBox

Virtual Box https://www.virtualbox.org/ on mm. Windowsilla toimiva ilmainen [virtualisointiympäristö](https://www.virtualbox.org/wiki/Virtualization), joka mahdollistaa esim. Linuxin suorittamisen Windows-koneen sovelluksena. 

### alkutoimet

Jos haluat virtuaalikoneen käyttöösi, asenna ensin [VirtualBox](https://www.virtualbox.org/wiki/Downloads), lataa [virtuaalikoneimagen](http://www.cs.helsinki.fi/u/mluukkai/wadror/wadror-linux.zip) sisältävä zip-paketti ja pura se. Virtuaalikoneeseen on asennettu valmiiksi Ruby 2.3 ja Rails 4.2.4. Jos koneesi on käyttöjärjestelmä on [32-bittinen](http://windows.microsoft.com/fi-fi/windows7/find-out-32-or-64-bit), lataa 
[32-bittinen versio](http://www.cs.helsinki.fi/u/mluukkai/wadror/wadror-linux-32bit.zip) virtuaalikoneesta.

Hae koneellesi myös [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)

Varmista virtuaalikoneesi asetuksista (settings/network), että verkkoadapteri on tyyppiä  __bridged adapter__:

![](https://raw.githubusercontent.com/mluukkai/WebPalvelinohjelmointi2017/master/images/kuva1.png)

Käynnistä virtuaalikone. Käyttäjätunnus on `wadror` ja salasana  `wadror`. Kirjauduttuasi selvitä koneen _ip-osoite_ komennolla <code>ifconfig</code>. Tulostus näyttää seuraavalta:

![](https://raw.githubusercontent.com/mluukkai/WebPalvelinohjelmointi2017/master/images/kuva2a.png)

Esimerkin tapauksessa ip-osoite on `192.168.10.112`

### työskentely

Virtuaalikoneeseen kannattaa ottaa yhteys PuTTY:llä. Eli avaa ohjela, ja laita _server_:iksi virtuaalikoneen ip-osoite. Kaikki terminaalista annettavat komennot kannattaa antaa PuTTY:n kautta.

Virtuaalikoneella olevia tiedostoja on ehkä parasta editoida windowsista käsin. Se taas onnistuu liittämällä virtuaalikoneen kotihakemisto Windowsiin. Avaa file explorer, klikkaa oikeaa hiiren nappia _computer:in_ kohdalla ja valitse _map network drive_:

![](https://raw.githubusercontent.com/mluukkai/WebPalvelinohjelmointi2017/master/images/kuva3.png)

Anna osoitteeksi `\\virtuaalikoneenip-osoite\wadror`. Käyttäjätunnuksen ja salasanan syöttämisen jälkeen virtuaalikoneen kotihakemisto näkyy windowsissa omana levynään. 

Käynnistä virtuaalikoneella oleva Rails-sovellus aina komennolla `rails s -b 0.0.0.0`. Näin pystyt käyttämään sovellusta Windowsin selaimella. Kun avaat selaimen, pääset sovellukseen kirjoittamalla osoitteeksi <code>virtuaalikoneenip-osoite:3000/breweries</code>

### virtuaalikoneen sammutus

Kone sammuu komennolla <code>sudo shutdown -h now</code>
