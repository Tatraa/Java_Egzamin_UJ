# Java i XML

### Czym jest plik XML?

XML, czyli Extensible Markup Language to język znaczników, który jest podobny do HTML-a. Za jego pomocą można zaprezentować, jak również przechowywać oraz rekonstruować różne dane. XML stanowi zestaw reguł kodowania dokumentów, które są czytelne zarówno dla człowieka, jak i dla komputera.

```javascript
<?xml version="1.0" encoding="UTF-8"?>
<rss xmlns:dc="http://purl.org/dc/elements/1.1/" version="2.0"> // root element, korzen, pod nim jest wszystko
    <channel>
        <title>Aktualności</title>
            <link>http://www.uj.edu.pl/uniwersytet/aktualnosci/...</link>
            <description>Aktualności Uniwersytetu Jagiellońskiego</description>
            <item>
            <title>Lista Pamięci - Stanisław Szczur</title>
            <link>http://www.uj.edu.pl/uniwersytet/aktualnosci/...</link>
            <description />
            <pubDate>Thu, 20 Dec 2012 07:44:00 GMT</pubDate>
            <dc:creator>Jolanta Herian-Ślusarska</dc:creator>
            <dc:date>2012-12-20T07:44:00Z</dc:date>
        </item>
        <item>...</item>
        ...
    </channel>
</rss>
```

Parsery DOM jak i SAX służą do odczytywania i zapisywania dokumentu XML.

### Dom

Parsery DOM tworzą drzewo reprezentujące dane zawarte w dokumencie XML. Po zbudowaniu DOM przetwarzanie odbywa się na modelu w pamięci operacyjnej.

```javascript
import java.io.IOException;
import java.net.URL;

import javax.xml.parsers;
import org.w3c.dom.*;
import org.xml.sax.SAXException;

public class DOMExample {
    public static void main() throws ParserConfigurationException,SAXException,IOException{
        UEL url = new URL(//jakiś RSS)
    
        DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
        
        DocumentBuilder dBuilder = dbFactory.newDocumentBuilder();
        
        Document doc = dBuilder.parse(url.openStream());
        
        sout("Root element:" + doc.getDocumentElement().getNodeName());
        
        NodeList nList = doc.getElementByTagName("item");
        for(int i = 0; i < nList.getLength(); i++){
            Node n = nList.item(i)
    
            if(n.getNodeType() == Node.ELEMENT_NODE) {
                Element e = (Element) n;
                System.out.println("Tytul : "
                                    + getTagValue("title", e));
                System.out.println("Link : "
                                    + getTagValue("link", e));
                System.out.println("dodane przez : "
                                    + getTagValue("dc:creator", e));
            }
        }
    }
    private static String getTagValue(String s, Element e) {
        NodeList nl = e.getElementByTagName(s).item(0).getChildNodes();
        Node n = (Node) nl.item(0);
        return n.getNodeValue();
    }
}
```
#### Modyfikacja DOM

Możliwa jest także modyfikacja zawartości DOM utworzonego w wyniku parsowania dokumentu XML.:

```javascript
// pobieramy element title i zmieniamy go
if ("title".equals(node.getNodeName())) {
node.setTextContent("Nowy tytul");
}
// kasujemy link
if ("link".equals(node.getNodeName())) {
itemElement.removeChild(node);
}
// tworzenie nowego dokumentu
Document doc = docBuilder.newDocument();
Element e = doc.createElement("root");
doc.appendChild(e);
```
#### Zapis DOM

Zapisać można przy użyciu Transformatorów:

```javascript
// domyslna fabryka transformatorow
TransformerFactory transformerFactory = TransformerFactory.newInstance();
// nowy tranformator
Transformer transformer = transformerFactory.newTransformer();
// wejscie transformatora (skad transformator bierze dane)
DOMSource source = new DOMSource(doc);
// wyjscie transformatora (gdzie “zmienione” dane zostana zapisane)
StreamResult result = new StreamResult(new File("file.xml"));
// uruchomienie transformatora – zapis DOM do pliku w formacie XML
transformer.transform(source, result);
```

### SAX

### JAXB

__Java Architecture for XML Binding__ - Jest to specyfikacja wchodząca w skład Javy SE pozwalająca na manipulację dokumentami XML. JAXB definiuje zestaw adnotacji, które pozwalają na konfigurację mapowania obiektów Javy. Dzięki takiemu podejściu jest to specyfikacja nieinwazyjna i mogąca być zastosowana do już istniejących, zwykłych klas POJO bez ingenerncji w ich kod.

- `@XmlRootElement` - definiuje, że dana klasa może być mapowana na dokument XML
- `@XmlAccessorType` - określa, czy dostęp do składowych klasy będzie odbywał się bezpośrednio, czy poprzez metody dostępowe
- `@XmlTransient` - wyłącza dane pole z mapowania dokumentu

Przykładowy kod do sparsowania:
```javascript
import java.io.File;
import javax.xml.bind.*;
import javax.xml.bind.annotation.*;
@XmlRootElement
class Person {
    String name;
    int age;
    public String getName() {
       return name;
    }
        @XmlElement
        public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    @XmlElement
    public void setAge(int age) {
        this.age = age;
    }
    public String toString() {
        return this.name + " (" + this.age + ")";
    }
}
````
````javascript
public class JAXBExample{
    public static void main(String[] args) throws JAXBException {
        Person p = new Person();
        p.setName("Barnaba");
        p.setAge(33);
        File f = new File("person.xml");
        JAXBContext ctx = JAXBContext.newInstance(Person.class); // fabryka parserów JAXB
        Marshaller marshaller = ctx.createMarshaller();
        marshaller.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
        marshaller.marshal(p, System.out);  //ładnie sformatowane bedzie z wycięciami
        marshaller.marshal(p, f);
        p = null;                           // jak mając plik zrobić z niego obiekt
        Unmarshaller unmarshaller = ctx.createUnmarshaller();
        p = (Person)unmarshaller.unmarshal(f);
        System.out.println(p);
    }

````
`Marshaller` to klasa która służy do serializacji obiektów Java do takich formatów jak XML. Natomiast słowo `marshall` oznacza proces serializacji obiektów

### Serializacja i XML
Inną metodą serializacji niektrórych obiektów do plików tekstowych w formacie XML:

#### XMLEncoder 
XMLEncoder umożliwia zapisanie stanu obiektu do pliku XML
#### XMLDecoder
XMLDecoder umożliwia odczytanie tego stanu z pliku XML i utworzenie obiektu z tego stanu

```javascript
XMLEncoder e = new XMLEncoder(new FileOutputStream("jbutton.xml"));
e.writeObject(new JButton("Hello world"));
e.close();
```
```javascript
XMLDecoder d = new XMLDecoder(new FileInputStream("jbutton.xml"));
obj = d.readObject();
d.close();
```

### Ant

Ant jest narzędziem umożliwiającym automatyzację procesów związanych z budowaniem programów. Podstawowe cechy Anta to.:

- konfiguracja zadań zapisana w formacie XML
- wieloplatformowość
- rozszerzalność w oparciu o klasy napisane w Javie

Aby wykonać 'Anta' należy wpisać w konsoli polecenie `ant`

Różnica między C++owym Make'iem jest taka, że `Make` dotyczy opisywania zależności między plikami i sposobu budowania plików. `Ant` dotyczy zależności mięzy 'zadaniami' i jest bardziej sposobem na sklejanie ze sobą skryptów budujących