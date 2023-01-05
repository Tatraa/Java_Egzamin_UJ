# Java i Bazy Danych

O SQLu nie będę nic tutaj pisał

### JDBC

Java Database Conectivity to specyfikacja określająca zbiór klas i interfejsów napisanych w Javie, które mogą być wykorzystane przez programistów tworzących oprogramowanie korzystające z baz danych. Implementacja JDBC jest dostarczana przez producentów baz danych.

Jedną z ważniejszych zalet takiego rozwiązania jest ukrycie przed programistą kwestii technicznych dotyczących komunukacji z bazą danych. Dzięki temu ten sam program napisany w Javie może współpracować z róznymi systemami baz danych.
Wystarczy podmienić odpowiednie biblioteki implementujące JDBC.

#### Przykład:
```javascript
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class TestDriver {
    public static void main(String[] args) {
        Statement stmt = null;
        ResultSet rs = null;
        try {
            Class.forName("com.mysql.jdbc.Driver").newInstance();
            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost/test?user=monty&password=");
            stmt = con.createStatement();
            rs = stmt.executeQuery("SELECT * FROM Tabela");
            while (rs.next()) {
                System.out.println(rs.getString("Imie"));
            }
        }
        catch (Exception ex) { // obsluga bledow
        } finally { // zwalnianie zasobow
            if (rs != null) {
                try {
                    rs.close();
                } catch (SQLException sqlEx) { // ignorujemy
                }
                rs = null;
            }
            if (stmt != null) {
                try {
                    stmt.close();
                } catch (SQLException sqlEx) { // ignorujemy
                }
                stmt = null;
            }
            // analogicznie con.close();
        }
    }
}
```

### Nawiązywanie połączenia:

Istnieją dwie metody nawiązywania połączenia z bazą danych:

- Za pomocą `DriverManager`
```javascript
String url = "jdbc:odbc:bazadanych";
Connection con = DriverManager.getConnection(url, "login", "haslo");
```
- za pomocą klasy `DataSource` i usługi JNDI
```javascript
Context ctx = new InitialContext();
DataSource ds = (DataSource)ctx.lookup("jdbc/MojaDB");
Connection con = ds.getConnection("myLogin", "myPassword");
```

### Driver Manager:

To tradycyjna warstwa zarządzająca JDBC pomiędzy użytkownikiem a sterownikiem. Aktualną listę dostępnych sterowników można uzyskać za pomocą metody: `Enumaration`
```
DriverManager.getDrivers()
```
Aby załadować dodatkowy sterownik należy skorzystać z metody:`Class Class.forName(String)` podając jako argument klasę ze sterownikiem np:
```javascript
Class.forName("jdbc.odbc.JdbcObdcDriver"); // protokół:odbc
Class.forName("com.mysql.jdbc.Driver");    // protokół jdbc:mysql
```

## DataSource:
DataSource reprezentuje źródło danych. Zawiera informacje identyfikujące i opisujące dane. Obiekt DataSource współpracuje z technologią __Java Naming and Directory Interface__, jest tworzony i zarządzany niezależnie od używającej go aplikacji.

Korzystanie ze źródła danych zarejestrowanego w JNDI zapewnia:

- brak bezpośredniego odwołania do sterownika przez aplikacje
- umożliwoa implementację grupowania połączeń oraz rozproszonych transakcji

Te cechy sprawiają, że korzystanie z klasy DataSource jest zalecaną metodą tworzenia połączenia z bazą danych, szczególnie w przypadku dużych aplikacji rozproszonych.

### Przesyłanie zapytań

Do przesyłania zapytań do bazy danych służą obiekty klasy:

- `Statement` - typowe pytania (bezparametrowe)
- `PreparedStatement` - prekompilowane pytania zawierające parametry wejściowe
- `CallableStatement` - procedury zapisane w bazie danych

Obiekt `Statement` tworzy się w ramach nawiązanego wcześniej połączenia:
```javascript
Connection con = DriverManager.getConnection(url, login, pass);
Statement stmt = con.createStatement();
stmt.executeUpdate("INSERT INTO table(name, price) VALUE 'ser', 2.0");
```

Do przesyłania zapytań służą metody:

- `executeQuery` - pytania zwracające dane: SELECT
- `executeUpdate` - pytania zmieniające dane: INSERT, UPDATE, CREATE TABLE, ...
- execute - dowolne zapytania. Dzięki tej instrukcji można wykonać sekwencje pytań, przekazać i odebrać dodatkowe parametry.

W ramach jednego obiektu Statement można wykonać sekwencyjnie kilka zapytań. Po zakończeniu używania obiektu zaleca się wywołanie metody `close()`.
### Odbieranie wyników:

Wyniki zwrócone w wyniku wykonania zapytania są dostępne poprzez obiekt typu `ResultSet`:

```javascript
Statement stmt = con.createStatement();
ResultSet rs = stmt.executeQuery("SELECT a, b, c FROM table");
while (rs.next()) {
// odebranie i wypisanie wyników w bieżącym rekordzie
int i = rs.getInt("a");
String s = rs.getString("b");
float f = rs.getFloat("c");
System.out.println("Rekord = " + i + " " + s + " " + f);
}
```
### HSQLDB

__Hyper SQL Database__ to system zarządzania relacyjnymi bazami danych w całości napisany w Javie (open source).

Do niektórych własności HSQLDB należą:
- obsługa SQL'a
- obsługa transakcji (COMMIT, ROLLBACK, SAVEPOINT), zdalnych procedur i funkcji, triggerów itp.
- możliwość dołączania do programów i appletów. Działanie w trybie read-only
- rozmiar tekstowych i binarnych danych ograniczony przez rozmiar pamięci.

### Serwer HSQLDB

- Taki podstawowy to HyperSQL Server - `org.hsqldb.server.Server`
- HyperSQL WebServer - używan, jeśli serwer może używać tylko protokołu HTTP lub HTTPS `org.hsqldb.server.WebServer`
- HyperSQL Servlet - te same protokoły co WebServer
- Stand-alone - 'serwer' uruchamiany w ramach procesu, w którym nawiązujemy połączeni z bazą.

Wszystkie tryby pracy serwera umożliwiają korzystanie z JDBC

### Połączenie HSQLDB

```javascript
try {
    Class.forName("org.hsqldb.jdbc.JDBCDriver" );
} catch (Exception e) {
    System.err.println("ERROR: failed to load HSQLDB JDBC driver.");
    e.printStackTrace();
    return;
}
Connection c =
DriverManager.getConnection("jdbc:hsqldb:hsql://localhost/xdb", "SA", "");

Connection c =
DriverManager.getConnection("jdbc:hsqldb:http://localhost/xdb", "SA", "");

Connection c =
DriverManager.getConnection("jdbc:hsqldb:file:/opt/db/testdb;shutdown=true
", "SA", ""); // ścieżka do pliku, gdzie będzie zapisywane; shutdown musi być przed rozłączeniem"
```

### stand-alone HSQLDB

W trybie stand-alone 'serwer' bazy danych działa w ramach tej samej wirtualnej maszyny Javy, co korzystający z niego program "kliencki".
```javascript
Connection c = DriverManager.getConnection("jdbc:hsqldb:file:/opt/db/testdb", "sa", "");
```
Niewielkie bazy danych mogą być uruchamiane do pracy w pamięci operacyjnej komputera:
```javascript
Connection c = DriverManager.getConnection("jdbc:hsqldb:mem:testdb", "sa", "");
```
W obecnej wersji HSQLDB istnieje możliwość jednoczesnego używania wieli 'serwerów' baz danych w trybie stand-alone

W Javie za BD odpowiada JDBC, deweloperzy muszą zaimplementować metody ukryte pod tym interfejsem niezależnie jakiej DB sie używa:

1. załadować sterownik </br>
2. połączyć się </br>
__Lub inaczej </br>__
1. uzyskać połączenie </br>
2. stworzyć statement i zamknąć go dopiero wtedy jak odbierze się co się chce