# Refleksje

Polega na dynamicznym korzystaniu ze struktur języka programowania, które nie muysały być zdeterminowane w momencie tworzenia oprogramowania.

Najważniejsze klasy języka Java, które umożliwiają programowanie refleksyjne to `Class`, `Field`, `Method`, `Arrat`, `Constructor`. Znajdują się one w pakietach `java.lang` i `java.lang.reflect`

Każdy obiekt w Javie jest instancją klasy `Object`. Każdy typ (obiektowy, prymitywny, tablicowy itp) jest reprezentowany przez instancję klasy `Class`, którą uzyskujemy za pomocą `getClass()`

```javascript
import java.util.HashSet;
import java.util.Set;
enum Day {
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY,
    THURSDAY, FRIDAY, SATURDAY
}
public class ReflectionExample {
    public static void main(String[] args){
        Class c;
        c = "foo".getClass();
        System.out.println(c.getName()); // wypisuje java.lang.String
        c = "foo".getClass();
        System.out.println(c.getName()); // wypisuje java.lang.String
        c = System.out.getClass();
        System.out.println(c.getName()); // wypisuje java.io.PrintStream
        c = Day.SUNDAY.getClass();
        System.out.println(c.getName()); // wypisuje Day
        byte[] bytes = new byte[1024];
        c = bytes.getClass();
        System.out.println(c.getName()); // wypisuje [B
        Set<String> s = new HashSet<String>();
        c = s.getClass();
        System.out.println(c.getName()); // wypisuje java.util.HashSet
    }
}
```

Jeśli nie mamy obiektu (instancji klasy) możemy użyć atrybutu `class`.

`c = java.io.PrintStream.class; // java.io.PrintStream`

`c = int[][][].class; // [[[I`

Ten sposób jest szczególnie użyteczny w przypadku typów prymitywnych:

```javascript
boolean b;
Class c = b.getClass(); // compile-time error
```

### Klasy:

Wybrane metody klasy Class:
```javascript
static Class<?> forName(String className)
Constructor<T> getConstructor(Class<?>... parameterTypes)
Constructor<?>[] getConstructors()
Field getField(String name)
Field[] getFields()
Class<?>[] getInterfaces()
Method getMethod(String name, Class<?>... parameterTypes)
Method[] getMethods()
int getModifiers()
Class<? super T> getSuperclass()
TypeVariable<Class<T>>[] getTypeParameters()
boolean isArray()
boolean isInterface()
boolean isPrimitive()
T newInstance()
```

Ciekawa rzecz:

```javascript
class C1{}
class C2 extends C1{}
...
C1 o1 = new C1(); // równoważne C1.class.newInstance()
C2 o2 = new C2();

o1.getClass().isAssignableFrom(o2.getClass()); //true
o2.getClass().isAssignableFrom(o1.getClass()); //false
o1.getClass().isInstance(o2);                  //true
o2.getClass().isInstance(o1);                  //false
```


