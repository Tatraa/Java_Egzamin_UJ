# Nie przerobione

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