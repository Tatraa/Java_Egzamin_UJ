# Java i Sieci

### URL

Inifed Resource Locator jest podstawową klasą identyfikującą zasoby w internecie:
```javascript
URL url = new URL("http://www.google.pl/");
BufferedReader in = new BufferedReader(new InputStreamReader(
                                                url.openStream()));
```

### URLConnection

Zawiera on metody umożliwiające nawiązanie połączenia z zasobem reprezentowanym przez URL:
```javascript
URL url = new URL("http://www.google.pl/");
URLConnection con = url.openConnection();
BufferedReader in = new BufferedReader(new InputStreamReader(
                                                con.getInputStream()));
```
URLConnection umożliwia również zapis do wskazanego zasobu przez obiekt URL:
```javascript
URL url = new URL(args[0]);
URLConnection con = url.openConnection();
con.setDoOutput(true);
OutputStreamWriter out = new OutputStreamWriter(
                                        con.getOutputStream());
```

Zarówno jak w przypadku URL i URLConnection komunikacja odbywa się z wykorzystaniem odpowiedniego protokołu. Dokumentacja Javy gwarantuje standardowo obsługę następujących protokołów:

- http
- https
- ftp
- file
- jar

### Interfejs gniazd

Standardowa obsługa sieci w Javie opiera się o tzw. interfejs gniazd. Najważniejsze klasy, umożliwiające komunikację poprzez sieć to:

- __Socket__ - klasa reprezentująca gniazdo służące do nawiązywania połączenia, wysyłania i odbierania danych.
- __ServerSocket__ - klasa reprezentująca gniazdo oczekujące na przychodzące żądania połączeń.

Istnieją jeszcze gniazda SSLSocket i SSLServerSocket obsługujące komunikację szyfrowaną protokołem SSL/TLS

### SSL W Javie

Protokół SSL umożliwia bezpieczną (szyfrowaną) transmisję danych
poprzez niezabezpieczoną sieć. Dodatkowo SSL umożliwia autoryzację
stron komunikacji. W tym celu wykorzystywany jest mechanizm
certyfikatów. Za transmisję z użyciem protokołu SSL odpowiedzialne są
klasy zgrupowane w pakiecie javax.net.SSL.

### Java Web Start

Technologia Java Web Start jest stosowana do lokalnego uruchamiania programów w Javie umieszczonych w sieci.

- jest w peło niezależna od używanych przeglądarek internetowych
- umożliwia automatycznie pobranie właściwej wersji środowiska JRE
- pobierane są tylko pliki, które zostały zmienione
- obsługuje prawa dostępu do zasobów lokalnego komputera
- do opisu zadania do uruchomienia wykorzystuje pliki jnlp (Java Network Launch Protocol)

````javascript
<?xml version="1.0" encoding="utf-8"?>
<jnlp
    spec="1.0+"
    codebase="http://www.serwer.w.sieci.pl/katalog"
    href="plik_jws.jnlp">
    <information>
        <title>Nazwa programu</title>
        <vendor>Producent programu</vendor>
        <homepage href="http://www.strona.programu.pl"/>
        <description kind="short">Krotki opis programu</description>
        <icon kind="splash" href="kat/splashscreen.gif"/>
        <icon href="kat/ikona.gif"/>
        <offline-allowed/>
    </information>
    <security>
        <all-permissions/>
</security>
    <resources>
        <j2se version="1.4+"/>
        <jar href="kat/archiwum1.jar"/>
        <jar href=" kat2/lib/biblioteka.jar"/>
    </resources>
    <application-desc main-class="pl.edu.uj.if.ExampleClass"/>
</jnlp>
````
Plik jnlp umieszczany na serwerze www.