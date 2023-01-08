# Współbieżność

### Procesy

Program w Javie uruchamiany jest w ramach pojedynczego procesu JVM. Z tego powodu implementacja współbieżności koncentruje się głównie na obsłudze wątków.
Niemniej Java udostępnia także mechanizmy umożliwiające uruchamianie procesów systemu operacyjnego.

Proces można stworzyć korzystając z metody `Runtime.exec()` lub klasy `ProcessBuilder` z pakietu `java.lang`

```javascript
String s;
 Process ps = Runtime.getRuntime().exec("ls -l");
 BufferedReader bri = new BufferedReader(new InputStreamReader(
 ps.getInputStream()));
 BufferedReader bre = new BufferedReader(new InputStreamReader(
 ps.getErrorStream()));
 while ((s = bri.readLine()) != null)
    System.out.println(s);
 bri.close();
 while ((s = bre.readLine()) != null)
    System.out.println(s);
```

Klasa `ProcessBuilder` pozwala precyzyjniej określić środowisko, w którym działa proces:

```javascript
ProcessBuilder builder = new ProcessBuilder("ls", "-l");
builder.directory(new File("."));
builder.redirectErrorStream(true);
builder.redirectOutput(Redirect.INHERIT);
Process ps;
try {
    ps = builder.start();
    ps.waitFor();
} catch (IOException | InterruptedException e) {
    e.printStackTrace();
}
```

### Wątki

Istnieją dwa podstawowe sposoby tworzenia wątków. Pierwszy polega na rozszerzeniu klasy `java.lang.Thread`

```javascript
public class HelloThread extends Thread {
    public void run() {
        System.out.println("Witam z wątku");
    }
    public static void main(String args[]) {
        Thread t = new HelloThread();
        t.start();
        System.out.println("Witam z programu");
        //OUTPUT:
        //Witam z programu
        //Witam z wątku
    }
}
```

Drugi opiera się na skonstruowaniu wątku w oparciu o klasę implementującą interfejs `java.lang.Runnable`

```javascript
public class HelloRunnable implements Runnable {
    public void run() {
        System.out.println("Witam z watku");
    }
    public static void main(String args[]) {
        Thread t = new Thread(new HelloRunnable());
        t.start();
        System.out.println("Witam z programu");
        // OUTPUT taki sam jak wyżej
    }
}
```
Ten przypadek jest ogólniejszy i zalecany ponieważ klasa implementująca wątek może rozszeżać inną klasę.

Inne przykłady:

```javascript
Runnable task = new Runnable(){
 public void run() {
 System.out.println("Witam z watku");
 }
}
Thread t = new Thread(task);
t.start();
-------------------------------------------------------------------------
Thread t = new Thread(new Runnable(){
 public void run() {
 System.out.println("Witam z watku");
 }
});
t.start();
-------------------------------------------------------------------------
Thread t = new Thread(() -> { System.out.println("Witam z watku");} );
t.start();
```

### Klasa Thread

Wątki mogą być wstrzymywane oraz wybudzane/przerywane:

```javascript
public class HelloThread implements Runnable{
    public void run() {
        try {
            Thread.sleep(10000); // wstrzymanie na 10 sek.
        } catch (InterruptedException e) {
        System.out.println("interupted");
    }
    }
    public static void main(String[] args) throws InterruptedException{
        Thread t = new Thread(new HelloThread());
        t.start();
        Thread.sleep(5000);
        System.out.println("budzenie");
        t.interrupt();
        //OUTPUT:
        //budzenie
        //interupted
    }
}
```
```javascript
public class HelloThread implements Runnable{
    public void run() {
        try {
            Thread.sleep(5000);
        } catch (InterruptedException e) {
            return;
        }
        System.out.println("watek");
    }
    public static void main(String[] args) throws InterruptedException{
        Thread t = new Thread(new HelloThread());
        t.start();
        t.join(); // czekamy na zakonczenie t
        System.out.println("teraz ja");
        //OUTPUT
        //watek
        //teraz ja
    }
}
```

### Synchronizacja

Wątki mogą się komunikować przez dowolne współużytkowane zasoby (np. Referencje do obiektów). Jest to bardzo efektywne, jednak może powodować problemy, gdy kilka wątków korzysta z jednego zasobu.

Problem ten rozwiązuje się używając synchronizacji. Oznaczenie metod słowem `synchronized` powoduje, że w danej chwili może być wykonana tylko jedna z nich:

```javascript
class SynchronizedCounter {
    private int c = 0;
    public synchronized void increment() {
        c++;
    }
    public synchronized void decrement() {
        c--;
    }
    public synchronized int value() {
        return c;
    }
}
```

### Blokada wewnętrzna

Każdy obiekt posiada powiązaną z nim blokadę wewnętrzną. Jeśli wątek chce uzyskać wyłączny dostęp do obiektu może skorzystać z tej blokady.
```javascript
public void addName(String s) {
    synchronized(this) {
        name = s;
        counter++;
    }
    nameList.add(name);
}
```
Wątek musi jednoznacznie wskazywać obiekt, z którym jest związana używana przez niego blokada. Taki typ blokad nazywamy synchronizacją na poziomie instrukcji (synchronized statements)

### Blokada drobnoziarnista

Dostęp do c1 i c2 musi być synchronizowany niezależnie - nie chcemy blokować na raz obu liczników
```javascript
public class FineGrainedLockEx {
    private long c1 = 0, c2 = 0;
    private Object lock1 = new Object();
    private Object lock2 = new Object();
    public void inc1() {
        sychronized(lock1) {
            c1++;
        }
    }
    public void inc2() {
        sychronized(lock2) {
            c2++;
        }
    }
}
```

### Operacje atomowe (xD)

Typowo dostęp do zmiennej/referencji nie jest zrealizowany jako pojedyncza operacja. Aby takie operacje były atomowe należy oznaczyć ją słowem `volatile`
```javascript
private volatile long c1 = 0;

public void inc1() {     
    c1 += 5; // nie jest atomowa bo atomowy jest odczyt i zapis
             // wartosci a nie jej zwiekszanie
    }
}
```

### Typowe problemy wątków:

W programach wielowątkowych występuje kilka rodzajów problemów, które mogą powodować niewłaściwe działanie programów:

- zakleszczenia (deadlock) - wątki blokują wzajemnie zasoby potrzebne im do dalszego działania (pięciu filozofów)
- zagłodzenia (starvation) - jeden wątek blokuje zasób potrzebny innym wątkom
- livelock - 'odwrotność' deadlocka - wątek reaguje na zachowanie drugiego wątku, które jest reakcją na zachowanie pierwszego wątku

```javascript
public class Deadlock {

    static class Worker {
        public String name;
        public Worker(String name) {
            this.name = name;
    }
    public synchronized void doWork(Worker w){
        System.out.println(this.name + " pracuje z " + w.name);
        try {
            Thread.sleep(1000); // pracujemy
        } catch (InterruptedException e) { }
        w.release();
    }
    public synchronized void release() {
        System.out.println(this.name + " jest znowu gotowy");
    }
    public static void main(String[] args) {
        final Worker w1 = new Worker("w1");
        final Worker w2 = new Worker("w2");
        new Thread(new Runnable() {
        public void run() { w1.doWork(w2); }
        }).start();
       
        new Thread(new Runnable() {
        public void run() { w2.doWork(w1); }
        }).start();
        }
        //workerzy zaczynają pracować i blokada następuje
        //na metodzie `release()` w obu obiektach
    }
}
```

### Wait/Notify

Często jest tak, że ątek musi poczekać, aż inny wątek wykona określoną część swoich zadań, np jeden wątek oblicza wyniki, a drugi je wypisuje na ekranie

### Executors

Egzekutory oddzielają wątek od zarządzania nim

```javascript
Executor exec = ...;
executor.execute(new RunnableTask1());
executor.execute(new RunnableTask2());
```

Executor jest rozszerzany przez ExecutorService, który dodatkowo umożliwia uruchomienie wątków Callable, które mogą zwracać wynik działania. (`java.util.concurrent.ExecutorService`)

Kolejnym rodzajem egzekutorów są tzw. Thread Pools - zbiory, wspólnie zarządzanych wątków. W JRE 7.0 wprowadzono ForkJoinPool, przeznaczony do wielo procesorowych obliczeń równoległych. 

