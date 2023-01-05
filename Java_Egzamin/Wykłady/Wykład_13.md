# Java Native Interface

### Co umożliwia?

- korzystanie z bibliotek systemowych (npisanych np. z C/C++) wewnątrz programu w Javie </br>

- korzystanie z obiektów Javy wewnątrz programów w innych językach programowania (C/C++)

Najczęściej JNI wykorzystuje się do realizacji niskopoziomowych komunikacji IO, która nie może być zrealizowana przez JVM, gdyż nie ma ona bezpośredniego dostępu do sprzętu.

### Wady:

- brak przenośności kodu pomiędzy różnymi platformami
- utrudnione debugowanie - drobne błędy JNI mogą "niedetermistycznie" destabilizować pracę JVM.
- brak garbage collectora
- problemy z konwersją danych (kodowanie stringów)

### Stworzenie aplikacji, kroki:

- napisanie programu w Javie 
- skompilowanie programu i wygenerowanie plików nagłówkowych dla metod natywnych
- implementacja metod natywnych (C/C++)
- kompilacja metod natywnych do biblioteki
- uruchomienie programu

### Program w Javie:

```
public class JNIHello {
    static {
        System.loadLibrary("hello"); // nazwa biblioteki z kodem
            // natywnym, moze zalezec od systemu operacyjnego
    }

    // deklaracja metody natywnej (ktora znajduje się w bibliotece)
    private native void sayHello();
    public static void main(String[] args) {
        JNIHello h = new JNIHello();
        h.sayHello(); // wywolanie metody natywnej
    }
}
```

Kompilacja: `javac JNIHello.java`

Generowanie plików nagłówkowych dla metod natywnych: `javah JNIHello`

Do generowania uużywamy skompilowanego pliku z rozszerzeniem `class`

#### Implementacja
```
#include “JNIHello.h”
#include <stdio.h>
JNIEXPORT void JNICALL Java_JNIHello_sayHello(JNIEnv *env, jobject obj){
    printf("Hello World!\n");
    return;
}
```
#### Kompilacja Biblioteki: 

Linux: ```gcc -I /etc-java-config-2/current-system-vm/include
-I /etc-java-config-2/current-system-vm/include/linux -fPIC
-shared -o libhello.so hello.c```

#### Kompilacja biblioteki:
Linux: ```java -Djava.library.path=. JNIHello```

### Podstawy JNI:

JNI definijue następujące typy natywne:

- jint, jbyte, jshort, jlong, jfloat, jdouble, jchar. jboolean
- jobject, jclass, jstring, jthrowable
- jarray (jintArray, jbyteArray ...)

