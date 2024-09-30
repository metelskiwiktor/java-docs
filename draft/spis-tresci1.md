# Spis treści Java Core

## Segment 1: Wprowadzenie do Javy

### 1.1. Wstęp do Javy

- **Czym są JVM, JRE, JDK?**
    - **Java Virtual Machine (JVM)**
        - Rola JVM w uruchamianiu aplikacji Java
        - Architektura JVM (Class Loader, Execution Engine, pamięć)
    - **Java Runtime Environment (JRE)**
        - Składniki JRE (JVM, biblioteki klas podstawowych)
    - **Java Development Kit (JDK)**
        - Składniki JDK (kompilator `javac`, debugger, narzędzia)
        - Różnice między JDK a JRE
- **Historia i filozofia języka Java**
    - Powstanie języka w firmie Sun Microsystems
    - Główne założenia i cele twórców
    - Ewolucja języka na przestrzeni lat
- **Cechy języka Java**
    - Niezależność od platformy (Write Once, Run Anywhere)
    - Bezpieczeństwo i kontrola dostępu
    - Programowanie obiektowe
    - Automatyczne zarządzanie pamięcią (Garbage Collector)
    - Bogata biblioteka standardowa
    - Wielowątkowość
    - Wsparcie dla sieci i aplikacji rozproszonych

### 1.2. Ekosystem Javy

- **Kompilator i interpretator**
    - Proces kompilacji kodu źródłowego do kodu bajtowego
    - Interpretacja kodu bajtowego przez JVM
- **Just-In-Time Compiler (JIT)**
    - Optymalizacja wydajności aplikacji podczas wykonania

### 1.3. Struktura programu w Javie

- **Nazwa klasy a nazwa pliku**
    - Konwencje nazewnictwa
    - Wpływ na kompilację i uruchamianie programu
- **Metoda `main`**
    - Punkt wejścia do aplikacji
    - Argumenty wiersza poleceń
- **Komentarze**
    - Jednoliniowe (`//`), wieloliniowe (`/* ... */`), dokumentacyjne (`/** ... */`)
- **Operacje wejścia/wyjścia**
    - **Operacje wyjścia**
        - Użycie `System.out.println` i `System.out.print`
    - **Operacje wejścia**
        - Użycie klasy `Scanner` do odczytu danych
- **Przykładowy program**
    - Analiza krok po kroku prostego programu

---

## Segment 2: Podstawy składni Javy

### 2.1. Typy danych prymitywne i referencyjne

- **Co to jest referencja?**
    - Przechowywanie adresów obiektów w pamięci
- **Typy prymitywne**
    - Liczbowe (`byte`, `short`, `int`, `long`, `float`, `double`)
    - Znakowe (`char`)
    - Logiczne (`boolean`)
- **Typy referencyjne**
    - Klasa `String`
    - Obiektowe odpowiedniki typów prymitywnych (`Integer`, `Double`, itp.)

### 2.2. Autoboxing i unboxing

- **Automatyczna konwersja typów**
    - Konwersja między typami prymitywnymi a ich obiektowymi odpowiednikami
- **Pułapki i dobre praktyki**
    - Unikanie niepotrzebnego autoboxingu
    - Wydajność aplikacji

### 2.3. Zmienne i stałe

- **Deklaracja i inicjalizacja**
    - Zasady nazewnictwa
    - Typy zmiennych
- **Zasięg zmiennych**
    - Zmienne lokalne, pola klasy
- **Słowo kluczowe `final`**
    - Definiowanie stałych
    - Niezmienność referencji

### 2.4. Operatory i rzutowanie typów

- **Operatory**
    - Arytmetyczne, porównania, logiczne, bitowe, ternarny
- **Rzutowanie typów**
    - Rzutowanie jawne i niejawne
    - Konwersje między typami prymitywnymi
- **Rzutowanie obiektów**
    - Upcasting i downcasting
    - `ClassCastException`
- **Pułapki związane z rzutowaniem**
    - Utrata precyzji
    - Bezpieczeństwo typów

### 2.5. Instrukcje sterujące

- **Instrukcje warunkowe**
    - `if`, `else if`, `else`
    - `switch` (w tym nowości w Java 14+)
- **Pętle**
    - `for`, `enhanced for` (`foreach`), `while`, `do-while`
- **Instrukcje skoku**
    - `break`, `continue`, `return`
- **Operacje na warunkach i tablicach**
    - Iterowanie po tablicach i kolekcjach
    - Zagnieżdżone pętle

### 2.6. Tablice

- **Definicja i inicjalizacja**
    - Tablice typów prymitywnych
    - Tablice obiektów (`String`, inne klasy)
- **Jednowymiarowe i wielowymiarowe**
    - Tablice dwuwymiarowe (macierze)
    - Tablice nieregularne (tablice tablic)
- **Operacje na tablicach**
    - Iterowanie, modyfikacja elementów
    - Metody pomocnicze (`Arrays.sort`, `Arrays.fill`)

### 2.7. Klasa `String` i String Pool

- **Czym jest String Pool?**
    - Mechanizm przechowywania literałów `String`
    - Optymalizacja pamięci
- **Wskaż, czemu `String` jest immutable oraz wyjaśnij jego znaczenie**
    - Immutability klasy `String`
        - Dlaczego `String` jest niemutowalny?
        - Znaczenie i konsekwencje
- **W jaki sposób do `String` można dodać kolejne ciągi znaków, skoro jest immutable?**
    - Tworzenie nowych obiektów `String`
    - Wpływ na pamięć i wydajność
- **Wskaż, czemu konkatenacja `String` w pętli jest niewydajna. Jakie rozwiązanie jest w stanie je poprawić?**
    - Problem z tworzeniem wielu obiektów `String`
    - Zastosowanie `StringBuilder` i `StringBuffer`
- **Do jakich zastosowań nadają się: `String`, `StringBuffer`, `StringBuilder`?**
    - Różnice między nimi
    - Scenariusze zastosowań
- **Tworzenie i porównywanie `String`**
    - **Czemu obiekty powinno porównywać się za pomocą metody `equals` a nie `==`?**
        - Różnice między `equals()` a `==`
    - **Metoda `intern()`**
        - Jak działa i kiedy jej używać

---

## Segment 3: Kompilacja kodu i struktura projektu

### 3.1. Kompilacja kodu

- **Proces kompilacji**
    - Użycie kompilatora `javac`
    - Generowanie plików `.class`
- **Błędy kompilacji**
    - Typowe błędy i sposoby ich rozwiązywania

### 3.2. Struktura projektu

- **Pakiety**
    - Organizacja kodu w pakietach
    - Konwencje nazewnictwa
- **Katalogi źródłowe i binarne**
    - Organizacja plików w projekcie
- **Pliki manifestu**
    - Zastosowanie w tworzeniu plików JAR

---

## Segment 4: Uruchamianie programów i szczegóły działania JVM

### 4.1. Uruchamianie programów

- **Użycie polecenia `java`**
    - Opcje uruchamiania
    - Przekazywanie argumentów
- **Klasa główna**
    - Znaczenie i wybór klasy z metodą `main`

### 4.2. Szczegóły działania JVM

- **Ładowanie klas**
    - Mechanizm Class Loader
- **Zarządzanie pamięcią**
    - Stos (Stack) i sterta (Heap)
- **Garbage Collector**
    - Co to jest Garbage Collector? Kiedy się włącza?
        - Mechanizmy zbierania śmieci
        - Automatyczne zarządzanie pamięcią

---

## Segment 5: Algorytmy i struktury danych

### 5.1. Podstawowe algorytmy

- **Sortowanie**
    - Bubble sort, selection sort, quicksort
- **Wyszukiwanie**
    - Linear search, binary search

### 5.2. Struktury danych

- **Listy**
    - Listy jednokierunkowe, dwukierunkowe
- **Stosy i kolejki**
    - Zasady działania
- **Drzewa**
    - Drzewa binarne, drzewa poszukiwań
- **Grafy**
    - Reprezentacja i podstawowe algorytmy

---

## Segment 6: Pakiety, moduły i organizacja kodu

### 6.1. Pakiety

- **Definiowanie pakietów**
    - Słowo kluczowe `package`
- **Importowanie klas**
    - Słowo kluczowe `import`
- **Modyfikatory dostępu a pakiety**
    - Publiczny, domyślny, chroniony, prywatny

### 6.2. Moduły (Java 9+)

- **System modułów**
    - Plik `module-info.java`
- **Definiowanie modułów**
    - Słowa kluczowe `module`, `requires`, `exports`

---

## Segment 7: Programowanie obiektowe w Javie - Podstawy

### 7.1. Klasy i obiekty

- **Definiowanie klas**
    - Konwencje nazewnictwa
    - Składowe klasy (pola, metody)
- **Tworzenie obiektów**
    - Operator `new`
    - Referencje do obiektów
- **Pola klasy**
    - Stan obiektu
    - Modyfikatory dostępu pól
    - Słowa kluczowe `final`, `static`
    - Klasa `Object` jako baza wszystkich klas

### 7.2. Metody

- **Definiowanie metod**
    - Sygnatura metody (typ zwracany, nazwa, parametry)
    - Modyfikatory dostępu metod
- **Metody statyczne**
    - Słowo kluczowe `static`
    - Zastosowanie i ograniczenia
- **Przeciążanie metod**
    - Definicja i zastosowanie
    - Wymagania dotyczące sygnatur
- **Enkapsulacja**
    - Ukrywanie szczegółów implementacji
    - Gettery i settery
- **Nadpisanie metod**
    - Anotacja `@Override`
    - Polimorfizm w działaniu
- **Metody specjalne**
    - `toString()`, `equals()`, `hashCode()`
    - **Co należy zrobić, aby porównanie obiektów za pomocą metody `equals` zwróciło nam oczekiwany efekt?**
        - Implementacja `equals()` i `hashCode()`
        - Kontrakt między `equals()` a `hashCode()`

### 7.3. Konstruktorzy

- **Konstruktor domyślny**
    - Automatyczne generowanie
- **Przeciążanie konstruktorów**
    - Wiele konstruktorów w jednej klasie
- **Inicjalizacja obiektów**
    - Bloki inicjalizacyjne
    - Inicjalizacja pól w miejscu deklaracji

---

## Segment 8: Wyjątki i obsługa błędów

### 8.1. Mechanizm wyjątków w Javie

- **Opisz hierarchię wyjątków. Czym różni się checked od unchecked?**
    - Klasy `Throwable`, `Exception`, `Error`
    - Różnice między wyjątkami sprawdzanymi i niesprawdzanymi
- **Czym są `final`, `finally` i `finalize`?**
    - Słowo kluczowe `finally`
        - Wykonywanie kodu niezależnie od wystąpienia wyjątku
    - Metoda `finalize()`
        - Sprzątanie przed usunięciem obiektu przez Garbage Collector
        - Dlaczego jest odradzana na rzecz innych mechanizmów?

### 8.2. Obsługa wyjątków

- **Bloki `try`, `catch`, `finally`**
    - Struktura i zasady działania
- **Rzucanie wyjątków**
    - Słowa kluczowe `throw` i `throws`
    - Propagacja wyjątków
- **`try-with-resources` (Java 7+)**
    - Automatyczne zarządzanie zasobami
    - Interfejs `AutoCloseable`

### 8.3. Dobre praktyki w obsłudze wyjątków

- **Unikanie pustych bloków `catch`**
- **Specyficzność obsługi wyjątków**
- **Dokumentowanie wyjątków**
    - Anotacja `@throws` w JavaDoc

---

## Segment 9: Serializacja danych

### 9.1. Serializacja w Javie

- **Czym jest serializacja danych w Javie?**
    - Interfejs `Serializable`
- **Proces serializacji i deserializacji**
    - Zapisywanie obiektów do strumienia bajtów
    - Odczytywanie obiektów ze strumienia bajtów
- **Klasy `ObjectOutputStream` i `ObjectInputStream`**
    - Przykłady użycia
- **Pole `serialVersionUID`**
    - Znaczenie i zastosowanie
    - Wpływ na kompatybilność wersji klasy
- **Dobre praktyki**
    - Bezpieczeństwo podczas serializacji
    - Unikanie problemów z kompatybilnością

---

## Segment 10: Testowanie jednostkowe

### 10.1. Wprowadzenie do testowania

- **Znaczenie testów jednostkowych**
- **Frameworki do testowania**
    - JUnit, TestNG

### 10.2. Pisanie testów

- **Anotacje testowe**
    - `@Test`, `@Before`, `@After`
- **Assercje**
    - `assertEquals`, `assertTrue`, `assertFalse`, itp.
- **Mockowanie zależności**
    - Wprowadzenie do mocków
    - Frameworki takie jak Mockito

---

## Segment 11: Narzędzia do budowania projektów

### 11.1. Maven

- **Struktura projektu Maven**
- **Plik `pom.xml`**
    - Zarządzanie zależnościami
- **Budowanie i uruchamianie projektu**

### 11.2. Gradle

- **Konfiguracja projektu**
    - Pliki `build.gradle`
- **Zarządzanie zależnościami**
- **Budowanie i uruchamianie projektu**

---

## Segment 12: Dziedziczenie i polimorfizm

### 12.1. Dziedziczenie

- **Słowo kluczowe `extends`**
    - Definiowanie relacji między klasami
- **Klasa bazowa i pochodna**
    - Dostęp do składowych klasy bazowej
    - Słowo kluczowe `super`
- **Klasa `final`**
    - Ograniczenie dziedziczenia
    - Zastosowania

### 12.2. Polimorfizm

- **Przesłanianie metod (`@Override`)**
    - Zasady i ograniczenia
- **Polimorfizm referencyjny**
    - Typ referencji a typ obiektu
- **Rzutowanie obiektów**
    - Rzutowanie w górę i w dół hierarchii
    - Operator `instanceof`

### 12.3. Klasy wewnętrzne (Inner Classes)

- **Klasy wewnętrzne niestatyczne**
    - Definicja i zastosowanie
    - Dostęp do składowych zewnętrznej klasy
- **Klasy wewnętrzne statyczne**
    - Słowo kluczowe `static`
    - Różnice w dostępie do składowych
- **Klasy anonimowe**
    - Tworzenie jednorazowych implementacji
    - Zastosowanie w wyrażeniach lambda

---

## Segment 13: Interfejsy i klasy abstrakcyjne

### 13.1. Klasy abstrakcyjne

- **Jakie są różnice między interfejsem a klasą abstrakcyjną?**
    - Definicja i zastosowanie
    - Metody abstrakcyjne i konkretne
- **Dziedziczenie po klasach abstrakcyjnych**
    - Ograniczenia i możliwości

### 13.2. Interfejsy

- **Definiowanie interfejsów**
    - Metody abstrakcyjne
    - Pola w interfejsach
        - Domyślnie `public`, `static`, `final`
- **Implementacja interfejsów (`implements`)**
    - Wielokrotna implementacja
- **Nowości w interfejsach (Java 8+)**
    - Domyślne metody
    - Metody statyczne
    - Prywatne metody (Java 9+)

### 13.3. Różnice między klasą abstrakcyjną a interfejsem

- **Dziedziczenie**
    - Klasa może dziedziczyć po jednej klasie abstrakcyjnej, ale implementować wiele interfejsów
- **Pola i metody**
    - Różnice w deklaracji i implementacji
- **Wyrażenia lambda**
    - **Interfejsy funkcyjne**
        - Możliwość użycia jako cel wyrażenia lambda
    - **Klasy abstrakcyjne**
        - Nie mogą być użyte jako cel wyrażenia lambda
- **Zastosowania praktyczne**
    - Kiedy używać którego mechanizmu

---

## Segment 14: Typy generyczne (Generics)

### 14.1. Wprowadzenie do generyków

- **Dlaczego warto używać generyków?**
    - Bezpieczeństwo typów
    - Unikanie rzutowań

### 14.2. Definiowanie typów generycznych

- **Klasy generyczne**
- **Metody generyczne**
- **Ograniczenia generyczne**
    - Ograniczenia typu (`extends`, `super`)

### 14.3. Typy surowe i wymazywanie typów

- **Typy surowe (raw types)**
- **Wymazywanie typów (type erasure)**

---

## Segment 15: Java Collections Framework (JCF) - Wprowadzenie

### 15.1. Opisz Java Collections Framework – przydatne interfejsy oraz ich implementacje i różnice

- **Hierarchia interfejsów i klas**
    - Przegląd podstawowych interfejsów (`Collection`, `List`, `Set`, `Map`, `Queue`)
- **Ogólny przegląd kolekcji**
    - Zalety użycia kolekcji
    - Różnice między kolekcjami a tablicami

### 15.2. Czym się różni `Comparable` od `Comparator`?

- **Interfejs `Comparable`**
    - Naturalne porządkowanie obiektów
    - Implementacja metody `compareTo()`
- **Interfejs `Comparator`**
    - Niestandardowe porządkowanie obiektów
    - Implementacja metody `compare()`
- **Porównanie obu interfejsów**
    - Zastosowania i różnice
- **Przykłady praktyczne**
    - Sortowanie kolekcji

### 15.3. Opisz `hashCode()`, jego działanie oraz wykorzystanie w kolekcjach

- **Implementacja metod `hashCode()` i `equals()`**
    - Kontrakt między tymi metodami
- **Wykorzystanie w kolekcjach**
    - Działanie `HashMap`, `HashSet`
    - Znaczenie dla poprawności i wydajności

### 15.4. Przegląd ważnych kolekcji

- **Listy**
    - `ArrayList`, `LinkedList`
    - Różnice w wydajności i zastosowania
- **Zbiory (`Set`)**
    - `HashSet`, `LinkedHashSet`, `TreeSet`
    - Właściwości i zastosowania
- **Mapy**
    - `HashMap`, `LinkedHashMap`, `TreeMap`
    - Różnice i scenariusze użycia
- **Kolejki i stosy**
    - `Queue`, `Deque`, `PriorityQueue`
    - Operacje FIFO i LIFO

---

## Segment 16: Biblioteki standardowe

### 16.1. Pakiet `java.lang`

- **Klasa `Math`**
- **Klasa `System`**
- **Klasa `Object`**

### 16.2. Pakiet `java.util`

- **Kolekcje**
- **Klasa `Date` i `Calendar`**
- **Klasa `Random`**

### 16.3. Pakiet `java.io`

- **Strumienie wejścia/wyjścia**
- **Obsługa plików**

---

## Segment 17: Listy w Javie

### 17.1. Interfejs `List`

- **Metody interfejsu `List`**
    - `add()`, `get()`, `remove()`, `size()`, itp.
- **Implementacje list**
    - `ArrayList`
    - `LinkedList`

### 17.2. Porównanie `ArrayList` i `LinkedList`

- **Wydajność operacji**
    - Dostęp losowy vs. wstawianie/usuwanie
- **Zastosowania praktyczne**

---

## Segment 18: Zbiory (`Set`) w Javie

### 18.1. Interfejs `Set`

- **Właściwości zbiorów**
    - Brak duplikatów
- **Implementacje zbiorów**
    - `HashSet`
    - `LinkedHashSet`
    - `TreeSet`

### 18.2. Porównanie implementacji `Set`

- **Sposób przechowywania danych**
- **Porządek elementów**
- **Wydajność operacji**

---

## Segment 19: Mapy w Javie

### 19.1. Interfejs `Map`

- **Przechowywanie par klucz-wartość**
- **Metody interfejsu `Map`**
    - `put()`, `get()`, `remove()`, `containsKey()`, itp.

### 19.2. Implementacje map

- **`HashMap`**
    - Szybki dostęp
- **`LinkedHashMap`**
    - Zachowanie kolejności wstawiania
- **`TreeMap`**
    - Przechowywanie w porządku naturalnym lub według `Comparator`

---

## Segment 20: Kolejki i stosy

### 20.1. Interfejs `Queue`

- **Operacje kolejki**
    - `add()`, `offer()`, `poll()`, `peek()`

### 20.2. Implementacje kolejek

- **`LinkedList` jako kolejka**
- **`PriorityQueue`**

### 20.3. Stosy w Javie

- **Klasa `Stack`**
- **Interfejs `Deque`**
    - Implementacja stosu za pomocą `ArrayDeque`

---

## Segment 21: Iteratory i przetwarzanie kolekcji

### 21.1. Interfejs `Iterator`

- **Metody `hasNext()`, `next()`, `remove()`**
- **Użycie iteratora w pętli**

### 21.2. Pętle `foreach` i wyrażenia lambda

- **Pętla `foreach`**
- **Metoda `forEach()` w kolekcjach**

### 21.3. Modyfikacja kolekcji podczas iteracji

- **Unikanie `ConcurrentModificationException`**
- **Iterator usuwający elementy**

---

## Segment 22: Wielowątkowość i synchronizacja

### 22.1. Co to jest wątek w Javie?

- **Wątki i procesy**
    - Różnice i zastosowania
- **Tworzenie wątków**
    - Klasa `Thread`
    - Interfejs `Runnable`
    - Jakie są sposoby tworzenia wątku w Javie?
        - Dziedziczenie po `Thread`
        - Implementacja `Runnable`
        - Wyrażenia lambda

### 22.2. Cykl życia wątku

- **Stany wątku**
    - Nowy, gotowy, działający, zablokowany, zakończony
- **Metody kontroli wątków**
    - `start()`, `run()`, `sleep()`, `join()`

### 22.3. Dlaczego nieprzemyślana implementacja wątków jest niebezpieczna?

- **Warunki wyścigu (Race conditions)**
- **Zakleszczenia (Deadlocks)**
- **Wpływ na bezpieczeństwo i stabilność aplikacji**

### 22.4. Jakie znasz sposoby synchronizacji wątków, aby nie doszło do kolizji? Czym jest sekcja krytyczna wątku?

- **Słowo kluczowe `synchronized`**
    - Metody i bloki synchronizowane
- **Blokady**
    - Interfejs `Lock`
    - Klasa `ReentrantLock`
- **Sekcja krytyczna wątku**
    - Definicja i znaczenie
    - Unikanie kolizji danych

### 22.5. Problemy współbieżności

- **Warunki wyścigu**
- **Zakleszczenia**
- **Bezpieczeństwo wątkowe**
    - Dobre praktyki programowania

### 22.6. Pakiet `java.util.concurrent`

- **Executors**
    - Tworzenie pul wątków
    - Interfejs `ExecutorService`
- **Kolekcje współbieżne**
    - `ConcurrentHashMap`
    - `CopyOnWriteArrayList`
- **Synchronizatory**
    - `Semaphore`
    - `CountDownLatch`
    - `CyclicBarrier`
- **Klasa `CompletableFuture`**
    - Programowanie asynchroniczne
    - Łączenie i kompozycja zadań asynchronicznych

---

## Segment 23: Strumienie (Streams) w Javie

### 23.1. Wprowadzenie do strumieni

- **Czym są strumienie?**
    - Przetwarzanie danych w sposób deklaratywny
- **Budowanie strumieni**
    - Ze zbiorów, tablic, plików

### 23.2. Operacje na strumieniach

- **Operacje pośrednie (intermediate)**
    - `filter()`, `map()`, `sorted()`, `limit()`, `distinct()`
- **Operacje końcowe (terminal)**
    - `collect()`, `forEach()`, `reduce()`, `count()`

### 23.3. Przetwarzanie równoległe

- **Strumienie równoległe**
    - `parallelStream()`
- **Zagadnienia związane z synchronizacją**

---

## Segment 24: Funkcjonalności języka w Javie 8+

### 24.1. Wyrażenia lambda

- **Składnia wyrażeń lambda**
- **Interfejsy funkcyjne**
    - `Function`, `Consumer`, `Supplier`, `Predicate`

### 24.2. Metody domyślne i statyczne w interfejsach

- **Definiowanie metod domyślnych**
- **Zastosowania**

### 24.3. Nowe API daty i czasu

- **Pakiet `java.time`**
    - `LocalDate`, `LocalTime`, `LocalDateTime`, `ZonedDateTime`
- **Formatowanie i parsowanie dat**

---

## Segment 25: Interfejsy funkcyjne i programowanie funkcyjne

### 25.1. Interfejsy funkcyjne

- **Definicja**
    - Interfejs z jedną metodą abstrakcyjną
- **Anotacja `@FunctionalInterface`**

### 25.2. Programowanie funkcyjne w Javie

- **Czyste funkcje**
- **Niezmienność danych**
- **Strumienie jako narzędzie programowania funkcyjnego**

---

## Segment 26: Refleksja i anotacje

### 26.1. Refleksja

- **Pakiet `java.lang.reflect`**
- **Uzyskiwanie informacji o klasach, metodach, polach**
- **Tworzenie obiektów w czasie wykonania**

### 26.2. Anotacje

- **Definiowanie własnych anotacji**
- **Anotacje wbudowane**
    - `@Override`, `@Deprecated`, `@SuppressWarnings`
- **Przetwarzanie anotacji w czasie kompilacji i wykonania**

---

## Segment 27: Garbage Collector

- **Co to jest Garbage Collector? Kiedy się włącza?**
    - Mechanizmy zbierania śmieci
    - Kryteria uruchamiania GC
- **Generacje pamięci**
    - Młoda i stara generacja
    - `Survivor Spaces`
- **Profilowanie i diagnostyka**
    - Narzędzia (`jconsole`, `jvisualvm`, `jstat`)
    - Analiza zrzutów pamięci (heap dump)
- **Optymalizacja aplikacji**
    - Ustawienia JVM
    - Dobre praktyki zarządzania pamięcią

---

## Segment 28: JVM i zarządzanie pamięcią

### 28.1. Architektura JVM

- **Class Loader**
- **Execution Engine**
- **Pamięć JVM**

### 28.2. Zarządzanie pamięcią

- **Stos (Stack)**
- **Sterta (Heap)**
- **Metaspace**

### 28.3. Monitorowanie i tunelowanie JVM

- **Parametry startowe JVM**
- **Narzędzia monitorujące**

---

## Segment 29: Bezpieczeństwo w Javie

### 29.1. Model bezpieczeństwa

- **Polityki bezpieczeństwa**
- **Manager bezpieczeństwa**

### 29.2. Szyfrowanie i podpisy cyfrowe

- **Pakiet `java.security`**
- **Algorytmy kryptograficzne**

---

## Segment 30: Wzorce projektowe w Javie

### 30.1. Wzorce kreacyjne

- **Singleton**
- **Builder**
- **Factory Method**

### 30.2. Wzorce strukturalne

- **Adapter**
- **Decorator**
- **Facade**

### 30.3. Wzorce behawioralne

- **Observer**
- **Strategy**
- **Command**

---

## Segment 31: Jakie są główne nowe funkcjonalności w poszczególnych wersjach Javy?

### 31.1. Java 8

- **Wyrażenia lambda**
- **Stream API**
- **Metody domyślne w interfejsach**
- **Nowe API daty i czasu**

### 31.2. Java 9

- **System modułów (Project Jigsaw)**
- **Metody prywatne w interfejsach**
- **Fabryczne metody kolekcji**
    - `List.of()`, `Set.of()`, `Map.of()`

### 31.3. Java 10

- **Inferred Type (`var`)**
    - Lokalna inferencja typów

### 31.4. Java 11

- **Nowe metody w klasie `String`**
    - `isBlank()`, `lines()`, `strip()`, `repeat()`
- **Uruchamianie plików źródłowych bez kompilacji**
    - `java MyClass.java`

### 31.5. Java 14

- **Wyrażenia `switch`**
    - Nowa składnia i możliwości
- **Bloki tekstowe**
    - Wielolinijkowe literały tekstowe

### 31.6. Java 16

- **Klasy rekordowe (`record`)**
    - Zwięzła deklaracja klas danych

### 31.7. Java 17

- **Klasy zapieczętowane (`sealed`)**
    - Kontrola dziedziczenia po klasach

---
