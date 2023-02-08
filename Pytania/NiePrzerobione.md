# Nie przerobione

-  Certyfikat SSH
-  co decyduje o sposobie
   parsowania, można wywołać na nim
   takie metody
-  Co to są Refleksja opisz Field
-  Dziedziczenie Typów
   Generycznych hierarchia
- Porównać wydajność Kolekcji
-  Omówić Wait() Notify() notify()
-  Napisz kod który wypisze źródło
   HTML Strony
-  Co to jest Jar po co i gdzie sie go
   używa, co to jest manifest i o co w
   nim chodzi jaka jest jego struktura
- Refleksje
-  Wszystko o Properties gdzie
   oprócz wykładu o kolekcjach sie
   pojawiło (przy ResourceBundle)
-  Krótko o instrukcjach
   warunkowych
- Typy Proste w Java
-  Co robi metoda t.join() dla t
   będącego instancją klasy Thread
-  Jak utworzyć nową instancję
   klasy bez używania słówka new
-  Przykłady strumieni binarnych
-  Co to interfejs
-  Co wiesz o klasie abstrakcyjnej
-  Co to jest ConstantPool
- Do czego służy blok finally
-  Skróty JDK,JRE,JVM
-  Jak skopiować zawartość obiektu
-  Opisz klasę Vector
-  Połączenie z bazą danych
- słowo kluczowe static, czy można w niestatycznych metodach skorzystać ze statycznych zmiennych/metod?
- wait(), notify(), notifyAll(), co dokładnie robi notifyAll, skąd notifyAll wie które wątki wybudzić (tutaj trochę się zagmatwałem więc warto faktycznie wiedzieć co dokładnie robi)
- jak w bazie danych otrzymać dany wynik, rezultat? (ResultSet)

- generyki vs wildcard
-  jfilechooser
-  sax (default handler)

- opisać działanie i różnice 'throw' i 'throws'. Czy 'throw' będzie działać w metodzie bez 'throws' (nie). Dodatkowo opowiedzieć o Runtime Exception i czy możemy obsługiwać takie wyjątki jak nullPointerException. (tak)
- blokada wewnętrzna oraz drobnoziarnista. Pokazał kod, gdzie uruchamiał 4 wątki na tą samą metodę i trzeba było podać sposób, by były odpowiednio zsynchronizowane niezależnie.
- opisać JWS oraz JNLP. W jakim formacie są pliki JNLP, co się w nich znajduje i jak działają.

- czym się różni ArrayList od Vectora, gdzie przechowują elementy, co jest szybsze
- t.join, co robi gdzie się używa, jak  popierdolilem mu trochę to spytał się jeszcze o metody tworzenia wątków
- napisać klienta ssl

- czym jest klasa abstrakcyjna, czym jest interfejs, czy mogą być przekazane jako argumenty funkcji
- URLconnection, jak się tworzy, do czego służy, czy może służyć do przesyłania danych
- ResultSet

- wszystkie metody iteracji przez tablicę/listę rozpisać -  czyli iteratory, enumeratory, lambda, różne pętlę for
- serializacja, jakich strumieni się używa; interfejs serializable, czy ma jakieś metody w sobie (nie ma)
- ANT - co to, co ma w sobie (dokładny opis tego slajdu z wykładu o tym)

- HashTable i HashMap , jak działają, co implementują / rozszerzają, i czym się różnią (trzeba wspomnieć że jedno może trzymać nulle drugie nie)
- Pola Tekstowe w Swingu, wymienić wszystkie i podać różnice między nimi + jak dodawać scrolla
- Napisać Parser DOM + jak dostać się do roota + jak dostać się do innych elementów

- Opisać Executory jak działają, po co są, później  podał mi taska i pytał jakbym go zrównoleglił za pomocą executora ( dokładne metody)
- Wszystko o ResourceBundle( dokładne metody) odrazu opisać Properties i Locale
- typy połączenia z baza danych napisać kod który łaczy z baza danych

- symbole wieloznaczne, gdzie w kodzie jest błąd (wykład 4, slajd 20)
- generowanie klucza, jakie argumenty się podaje w komendzie keytool, jak użyć certyfikatu w serwerze i kliencie
- JAXB, w sumie wszystko o nim
- zmienne statyczne
- JOptionPane (powiedzialem ze sa tam 4 metody przykladowe np showMessageDialog, showInoutDialog i potem na kartce mi kazal napisac showInoutDialog)
- HSQLDB

- properties
- jak uruchomic proces
- Dal kod i trzeba bylo to napisac za pomoca refleksji (jedna klasa)

- miałeś klasę A z atrybutem value i za pomocą refleksji stworzyć instancję A i przypisać jej atrybutowi wartość.
- jak odczytać dane z Gzipa
- stworzyć Server Echo

- Javadoc (komenda, co to i jakie komentarze uznaje)
- Jar (komendę + co to jest + manifest)
- InvocationHandler + proxy

- Interfejs Cloneable, metoda clone (co robi, kiedy obiekt musi ją nadpisać)
- JFileChooser (jak stworzyć, co dostaje sie na wyniku, jak dostać sie do plików które wybrał użytkownik, czy można wybrać więcej niż jeden, co w JPanelu zmienia podanie go jako argument w showOpenDialog, czy można null)
- Proxy (do czego służy, jak stworzyć, czego potrzebuje)

- modyfikatory dostępu, wszedł na refleksyjne i dynamiczne - czy można dostać wartość prywatnej zmiennej? (Tak, zmieniając modyfikator dostępu albo parsując do XML i sobie stamtąd odczytać 🙃)
- wait i notify, czy można zawsze wywołać (nie) + kod, jak wywołać nowy wątek nie rozszerzając klasy i nie implementując żadnego interfejsu
- XML i SAX, default handler i napisać kod na kartce jak się parsuje saxem

- Co to Scanner i jak napisać
- URL i URLConnection, metody łączenia się po URL i do czego można się łączyć
- napisać klasę i metodę refleksyjnie. Do metody przekazać argument "Hello"

- LayoutManager
- throws
- JDBC, omówić sposoby połączenia z bazą danych
- Resource Bundle, 
- JFileChooser,

- jak uzyskać referencje do obiektu Class (Class c = (...))

- HashTable
- Socket i ServerSocket, co je używa, co przyjmują, .connect(), co się dzieje jak nic się nie połączy i close()
- jak uzyskać referencje do obiektu Class

- Typy generyczne, typ surowe
- Notify i wait
- Wszystko o Ant

- ResourceBundle + kod
- porównać i opisać JTextArea i JEditorPane
- jak uzyskać referencje do obiektu Class

- wszystko o HashTable, jakie ma metody, jak pozyskać element
- Socket i ServerSocket jak działa, w jaki sposób nawiązują połączenie, co mają w środku, w jaki sposób przekazują dane
- sax i defaulthandler, co to defaulthandler, w jaki sposób obsłużyć konkretną rzecz z XML za pomocą defaulthandlera
- (dodatkowe na zdanie)napisał kod z użyciem wildcarda i zapytał czy lista.put(0, obj) się wykona i dlaczego nie

-  Collection, przykłady interfejsów rozszerzających. Vector opis metod. Metody wspólne w collection. 
- Tworzenie procesów. Co zwraca Runtime.getRuntime().exec, co pobiera w argumencie.
- ClassLoader, struktura pliku .class XD
- Napisać kod dla przepisania danych z jednego pliku w inny
- Contenery, Componenty  
- Programowanie Funkcyjne
- Klasy abstrakcyjne, co to jest, do czego służy, przykład
- Java Web Start, co robi i jak
- Pytanie dot. wypisania tablicy za pomocą przetwarzania strumieni i funkcji, czym jest java.util.Function, co zawiera, jakie ma metody
- Serializable, jak użyć
- Execute, jak zainicjować, jak uruchomić wątek
-  Bajtkod, jak uruchomić metode
- stworzyc serwer echo
- roznice miedzy vector i hashtable
- resultset
- EchoServer
- ResultSet
- Proces
- metody wieloargumentowe
- JTextArea
-  (x, y) -> x * y; co to jest  (samo stwierdzenie że Function nie wystarczyło, albowiem chodziło o Bifunction)
- prosze napisac serwer ktory po nawiazaniu polaczenia z klientem napisze mu hello i sie zamknie
- sposoby nawiązywania polaczenia z baza danych i konkretnie jak to zrobic za pomoca drivermanagera
- czym sa interfejsy, wszystko co o nich wiesz i wymień tyle ile ich pamietasz
- napisać program który gzipem ztaruje plik tekstowy
- layout manager - co to, rodzaje, czy jframe ma defaultowego mangera
- co to statement (to interfejs a nie klasa), skąd go pobieramy, jak go używać (np. executeQuery)
- Serializable, co to i kazał jakoś użyć jak nie byłem pewien ale na dobrej drodze
- Co robi join, później dopytał czym się to różni od tego jakbym normalnie zakończył wątek returnem
   jak nie wiedziałem to kazał czytać dokumentację xdd
- nie wiedziałem i nawet nie pamiętam czego XDD
- Program napisz JButton i wyświetl w okienku
- Jar
- Zapis dokumentu w DOM
- Napisz JFileChooser, który wyświetli zawartość pliku, który wybierze użytkownik 
- JavaDoc 
- XmlEncoder i XmlDecoder
- (ratunkowe) Napisać w jednej linijce JOptionPane, który wyświetli Hello i będzie miał przycisk OK
- Opisac jak wyglada proces serializacji
- Tworzenie procesu*
- Co oznaczają 4 pierwsze bajty w kazdej z klas w javie
- Napisać metodę która korzysta z typu generycznego w klasie, która z niego nie korzysta 
- Słówko volatile, gdzie się używa + czy można używać poza wątkiem
- Wszystko o strumieniach bajtowych i znakowych, ich klasy itp.
- cloneable. Jak działa, kiedy trzeba napisać swój - przykład
- Struktura pliku class i co się w tym pliku znajduje
- Napisz program, który stworzy 5 wątków, każdy z nich wypisze inną literę -mamy 2 wektory:
   Vector vecraw=new Vector
   Vector<Object> vecobj = new Vector
   porównaj, opisz jak działają 
- napisz w jednej linijce program, który wypisze za pomocą strumieni wszystkie elementy vecobj z poprzedniego pytania
- Volatile - czym jest, gdzie się używa, co robi
- Napisz program wysyłający na serwer wiadomość "hello" (Socket)
- Predykat - czym jest itp itd, potem przeszedł na temat Function i kazał napisać przykładową funkcję
- strumienie bajtowe i znakowe (opisać i porównać)
- wszystko co wiesz o ANT
- porównać i opisać vector i hashtable (generalnie powiedzieć wszystko co się wie na ich temat)
- Posortować wektor po długości stringów, z uzyciem comparable 
- Jak działa metoda accept w klasie Socket(nie ma jej)
- Co to jest supplier i consumer w programowaniu funkcyjnym 
- (pomocnicze).co znajduje się w java. util.funtion
- Posortować wektor po długości stringów, z uzyciem comparable
- Co robi accept w Socket (w socket nie ma accept)
- Czym są Supplier i Consumer
- Napisac clonable klase
- Classloader
- ResultSet
- Wypisać Properties do pliku
- ExecutorService i co zwraca metoda submit
- Invocation handler
- Napisać klasę z int i Vector potem sklonować
- ResultSet
- ClassLoader
- Napisać program który jako pierwszy argument wywołania programu podaje nazwę pliku
     a następne argumenty to dane które chcemy zapisać do tego pliku
- Czy jest możliwe by utworzony w javie proces czekał? Jeśli tak to jak to zrobić.
   Jak stworzyć proces w javie.
- HSQLDB
- Jak możemy pobierać dane użytkownika z klawiatury.
- Co to jest ANT i budowa pliku XML
- Wypisać refleksyjnie metody klasy Object
- program taki ze pobiera dane z klawiatury i zapisuje do pliku
- synchronized w wątkach, co to, jak uzywac
- SAX Parser- co to, opisać po kolei parsowanie + czym jest DefaultHadler i jak się z niego korzysta
- czym się różni throw od throws
- napisać aplikacje okienkową z dwoma JButtonami które reagują na kliknięcia
- co to unary operator
- Jak możemy pobierać dane użytkownika z klawiatury.
- Co to jest ANT i budowa pliku XML
- Wypisać refleksyjnie metody klasy Object
- Wypisać Properties do pliku
- ExecutorService i co zwraca metoda submit
- Invocation handler
-  Napisać program, który czyta tekst ze standardowego wejścia i wyświetla go w polu tekstowym w nowym okienku (czyli Swing).
- Serializacja - po co (jakich metod używamy jak chcemy użyć własnej implementacji). Jak potem zapisujemy klasę, która spełnia wymagania?
- Co to jest HSQLD? Czym się różni od innych? Jaki tryb jest użyteczny (chodziło oczywiście o Stand Alone)?
- Interfejs Comparable
- URL, URLConnection; różnice i jak odbierac dane z serwera.
- Bytecode, plik .class
- Interfejs Serializable
- JTextArea i JEditorPane (różnice, podobieństwa)
- Czym jest tryb stand-alone w bazach HSQLDB
- JAXB mocno dopytywał o marshaller
- Zrobić przycisk i pole tekstowe swing
- Kolekcje, opisać wektor
- Swing, pole do wpisywania tekstu i pod nim przycisk. Gdy klikniemy w przycisk to wypisuje w konsoli ten tekst.
- JAXB, marshaller, metody, inicjalizacja kontekstu
- Kolekcje z naciskiem na te z wykładu, kazał mi opisać TreeMap, złożoności, co jest lepsze w porównaniu z ArrayList a co gorsze
-  Napisać serwer, który wysyła "Hello" do klienta
-  Co znaczy (x,y)->x+y; i co tam trzeba dopisać, żeby się skomplikowało
- Napisać serwer TCP
- Czym są metody pomostowe 
- Jak załadować klasę z tablicy bajtów (ClassLoader::defineClass)
- Napisać jakąś kolekcje np. hashmape i posortować klucze alfabetycznie
- ExecutorService na czym polega.
- DOM jak używać i coś o Sax
  (Pomocnicze) napisać metodę Main() refleksyjnie
- Cloneable
- Co robi metoda pack()
- Predicate 