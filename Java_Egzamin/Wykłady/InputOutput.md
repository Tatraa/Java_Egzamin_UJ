# I/O (Strumienie, pliki)

### Strumienie bajtowe
Większość operacji We/Wy znajduje się w pakiecie `java.io`

Strumienie bajtowe traktują dane jak zbiór ośmiobitowych bajtów. Wszystkie strumienie bajtowe rozszerzają klasy `InputStream` lub `OutputStream`

Przykładowy program Wypisujący dane z pliku do pliku:

```javascript
public class CopyBytes {
    public static void main(String[] args) throws IOException {

        FileInputStream in = null;
        FileOutputStream out = null;
        try {
            in = new FileInputStream("input.txt");
            out = new FileOutputStream("output.txt");
            int c;

            while ((c = in.read()) != -1) {
                out.write(c);
            }
        } finally {                     // to co jest w finally wykona się teoretycznie zawsze
            if (in != null) {
                in.close();             // każdy strumień trzeba po sobie zamykać
            }
            if (out != null) {
                out.close();
            }
        }
    }
}
```
Strumienie bajtowe reprezentują 'niskopoziomowy' dostęp do danych. Dlatego w konkretnych sytuacjach warto je zastąpić przez bardziej specjalistyczne rodzaje strumieni.

### Strumienie znakowe

Strumienie znakowe automatycznie konwertują dane tekstowe do formatu Unicode. Konwersja jest dokonywana w oparciu o ustawienia regionalne komputera, na którym uruchomiono JVM, lub jest sterowana przez programistę.

Strumienie znakowe rozszerzają klasy `Reader` lub `Writer`

Przykładowy wygląda praktycznie tak samo tylko zamiast `FileInputStream` i `FileOutputStream` używa się `FileReader` oraz `FileWriter`:
```javascript
in = new FileReader("input.txt");
out = new FileWriter("output.txt");
```
Strumienie znakowe wykorzystują do komunikacji strumienie bajtowe, a same zajmują się konwersją danych

### Strumienie buforowane

Umożliwiają odczytywanie tekstu linia po lini

```javascript
in = new BufferedReader(new FileReader("input.txt"));
out = new PrintWriter(new FileWriter("output.txt"));
```
Istnieją cztery klasy buforowanych strumieni:

- `BufferedInputStream` i `BufferedOutputStream` - strumienie bajtowe
- `BufferedReader` i `BufferedWriter` - przesył znaków

Aby wymusić zapis danych poprzez wyjściowy, buforowany strumień, można użyć metody `flush()`

### Skanowanie

Pozwala na przetwarzanie słów (domyślnie rozdzielonych przez `Character.isWhiteSpace(char c)`)

```javascript
s = new Scanner(new BufferedReader(
new FileReader("input.txt")));
while (s.hasNext()) {
System.out.println(s.next());
```

Aby zmienić zachowanie obiektu `Scanner`, można skorzystać z metody: `useDelimeter()`. Przykładowo `s.useDelimeter(",\\s*")`;
zmienia znakrozdzielający na przecinek po którym następuje dowolna liczba "białych spacji", gdzie:
`\s` - biały znak, `*` - dowolna ilość, `\\` - żeby eskejpować bo samo `\s` oznaczałoby unikać

### Formatowanie

Wyjściowe strumienie znakowe umożliwiają podstawowe formatowanie dancyh za pomocą kilku odmian metody `print()` i `format()`.

Format uwzględnia czy jesteśmy w Polsce i ustawia dla nas np. `2,0` zamiast `2.0`. Format wypisuje domyślnie z 6 cyframi po przecinku.

### Metody wieloargumentowe

```javascript
public static void multiint(int... ints){
    for (int i=0; i<ints.length; i++)
        System.out.println(ints[i]);
    System.out.println();
    for(int i: ints)
        System.out.println(i);
}

public static void main(String[] args){
    multiint(123,34,65,76,44,11,0);
    multiint();
    multiint(12, 28);
}
```
`(int... ints)` to tak jakby tu była tablica intów, multiargument zawsze deklaruje się jako ostatni.

### ClassLoader

### Strumienie binarne

Strumienie binarne pozwalają efektywniej zarządzać zasobami. Istnieją dwa podstawowe rodzaje strumieni.

- strumienie danych: `DataInputStream` i `DataOutputStream`:
```javascript
DataOutputStream dos = new DataOutputStream(System.out);
dos.writeDouble(123.12);
dos.writeUTF("Grzegrz\u00f3\u0142ka");
dos.writeInt(12345);
dos.close();
```
- strumienie obiektowe: `ObjectInputStream` i `ObjectOutputStream`:
```javascript
ObjectOutputStream oos = new ObjectOutputStream(System.out);
oos.writeObject("Grzegrz\u00f3\u0142ka");
oos.close();
```

### Serializacja

Serializacja to wbudowany mechanizm zapisywania obiektów, który pozwala na binarny zapis całego drzewa obiektów. Oznacza to tyle, że jeśli mamy obiekt X, który posiada referencję do obiektu Y to serializując X również Y zostanie automatycznie zapisany w strumieniu wyjściowym.

Tak zapisany obiekt możesz później otworzyć przy kolejnym uruchomieniu programu. Jednak serializacja ma więcej zastosowań.

Dzięki temu mechanizmowi można na przykład przesyłać obiekty przez sieć. Obiekt, który stworzyliśmy na jednym komputerze (wewnątrz pamięci jednej wirtualnej maszyny Java) może być zserializowany, przesłany przez sieć i zdeserializowany na drugim komputerze tworząc nową instancję obiektu (wewnątrz pamięci drugiej wirtualnej maszyny Javy). Na obu tych komputerach wirtualna maszyna Javy musi mieć dostęp do skompilowanej wersji klasy.

Dla obiektów typu JavaBeans istnieje także możliwość serializacji tekstowej (do plików w formacie XML) z wyukorzystaniem klas `XMLEncoder` i `XMLDecoder`

### Strumienie kompresujące

#### Gzip

Służą do obsługi formatów gzip, zip, jar.
```javascript
Scanner sc = new Scanner(System.in);
GZIPOutputStream gos = new GZIPOutputStream(
    new FileOutputStream(args[0]));

while(sc.hasNext()){
    String s = sc.nextLine() + "\n";
    gos.write(s.getBytes());
}
sc.close();
gos.close();
```
`GZIPoutputStream` nie zapisuje danych do pliku tylko je przetwarza. Do zapisuj wykorzystuje on strumień, którego instancje dostaje w konstruktorze (w przykładzie `FileOutputStream`)

#### Zip

Format ZIP obsługuje archiwa złożone z wielu plików, ZipEntry to znacznik informujący, że następujące po nim dane należą do wskazanego pliku.

### Archiwa JAR

Java wyróżnia takżę szczególny rodzaj archiwum ZIP: JAR (`JarOutputStream`, `JarInputStream`). Archiwa JAR zawierają pliki klas wraz z dodatkowymi zasobami potrzebnymi do działania aplikacji.

Podstawowe zalety dystrybucji programów w postaci plików jar to:

- bezpieczeństwo: archiwa mogą być cyfrowo podpisywane
- kompresja: skrócenie czasu ładowania apletu lub aplikacji
- zarządzanie zawartością archiwów z poziomu języka Java
- zarządzanie wersjami na poziomie pakietów oraz archiwów
- przenośność

Archiwum jar tworzy się używając komendy jar, np:

`jar cf archiwum.jar klasa1.class klasa2.class ...`

c - tworzenie pliku, f - zawartość archiwum zostanie zapisana do pliku archiwum.jar zamiast standardowego wyjścia.

### Manifest

W archiwum jar znajduje się katalog `META-INF` a w nim plik `MANIFEST.MF` wierający dodatkowe informacje o archiwum. np:

```javascript
Manifest-Version: 1.0
Created-By: 1.5.0-b64 (Sun Microsystems Inc.)
Ant-Version: Apache Ant 1.6.5
Main-Class: pl.edu.uj.if.wyklady.java.Wyklad06
```
która mówi że po uruchomieniu archiwum wykona się metoda `main` zawarta w klasie Wykład6 znajdująccej sie w pakiecie `pl.edu.uj.if.wyklady.java`

Uruchomienie pliku jar:
`java -jar archiwum.jar`
