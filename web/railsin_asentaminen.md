**HUOM** sudoa ei tule käyttää rbenv:iä tai muita rubyn versiomanagereja käyttäessä (poislukien kirjastojen asentaminen), sillä asennus tehdään käyttäjän omaan kotihakemistoon. 

Varaa asennukseen kunnolla aikaa ja tee se mieluusti joskus kun levypalvelinten käyttö on muutoin vähäistä. Älä jätä asennusta ohjauksen alkuun, jos haluat tehdä muutakin kuin pyöritellä peukaloita.
 
--

Asennamme tässä Rubyn version 2.5.1 ja Railsin version 5.2.1 viimeaikoina suosioon nousseella [rbenv-versiomanagerilla] (https://github.com/sstephenson/rbenv)

Voit halutessasi käyttää myös [RVM:ää](https://rvm.io/rvm/install)  eli rbenvin hieman vanhempaa lähisukulaista.

**Älä kuitenkaan missään tapauksessa asenna Rubyä/Railsia Linuxin paketinhallintajärjestelmän kautta!**

**Huom:** seuraavassa on ohjeet ainoastaan Linuxille ja OSX:lle. 

## Rails Windowsille

Ruby on Railsin asentaminen Windowsiin onnistuu (ehkä) sivun [http://railsinstaller.org/en](http://railsinstaller.org/en) ohjeilla.

Jos haluat välttämättä käyttää Windowsia ja et suostu käyttämään laitoksen konetta, tapahtuu kurssille osallistuminen omalla vastuulla.

## rbenv Linuxille

Allaolevat on testattu laitoksen koneissa ja Ubuntun uusimman LTS version kanssa. Seuraavassa luvussa ohjeet OSX:lle. Windowsiin asentaminen ainoastaan omalla vastuulla! 

**Huom:** koneella tulee olla muutamia kirjastoja, joiden asennus onnistuu Ubuntussa komennolla <code>sudo apt-get install build-essential zlib1g-dev libpq-dev git sqlite3 libsqlite3-dev</code>. Laitoksen koneilla kirjastot ovat valmiina.

**Huom2:** __fuksiläppärille__ ja ehkä muillekin koneille on [asennettava kirjasto libffi-dev](https://github.com/sstephenson/ruby-build/wiki#build-failure-of-fiddle-with-ruby-220) seuraavasti:

```shell
sudo apt-get install libffi-dev
```

Toimitaan sivun [https://github.com/rbenv/rbenv#installation](https://github.com/rbenv/rbenv#installation) kohdan _Installation, Basic GitHub Checkout_ mukaan, eli annetaan terminaalissa seuraavat komennot:

* _git clone https://github.com/rbenv/rbenv.git ~/.rbenv_
* _echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile_
* _echo 'eval "$(rbenv init -)"' >> ~/.bash_profile_
* _echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc_
* _echo 'eval "$(rbenv init -)"' >> ~/.bashrc_
* _mkdir -p "$(rbenv root)"/plugins_
* _git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build_

Käynnistä terminaali ja varmista seuraavan komennon avulla, että kaikki on kunnossa

* curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash

Komennon tulostuksen pitäisi näyttää suunilleen seuraavalta:

```
Checking for `rbenv' in PATH: /usr/local/bin/rbenv
Checking for rbenv shims in PATH: OK
Checking `rbenv install' support: /usr/local/bin/rbenv-install (ruby-build 20170523)
Counting installed Ruby versions: none
  There aren't any Ruby versions installed under `~/.rbenv/versions'.
  You can install Ruby versions like so: rbenv install 2.2.4
Checking RubyGems settings: OK
Auditing installed plugins: OK
```

Siirry kohtaan [Rubyn ja railsin asennus](https://github.com/mluukkai/WebPalvelinohjelmointi2017/wiki/railsin-asennus#rubyn-ja-railsin-asennus)

## rbenv OSXlle

Rbenvin asennus onnistuu helpoiten homebrew:in avulla. Ohjeet homebrewin asennukseen löydät osoitteesta http://brew.sh/

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

Kun _rbenv_ on asennettu, asennetaan ja määritellään käytettävä Ruby:n versio komennoilla

    rbenv install 2.5.1
    rbenv global 2.5.1

Komento asentaa Rubyn version 2.5.1, joka on Rubyn uusin versio. Voit tarkistaa asennettavissa olevat versiot komennolla <code>rbenv install --list</code>

Varmista, että komennon <code>which ruby</code> tulos on suunnilleen seuraava:

    /Users/kayttajatunnus/.rbenv/shims/ruby

Asennetaan sitten Rails antamalla komentoriviltä seuraavat komennot (vastaa mahdollisiin __Overwrite the executable?__ -kyselyihin Y):

    echo 'gem: --no-ri --no-rdoc' >> ~/.gemrc
    gem install bundler
    gem install rspec
    gem install rake 
    rbenv rehash
    gem install rails -v 5.2.1
    rbenv rehash

