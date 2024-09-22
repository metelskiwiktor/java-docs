# Segment 1: Wprowadzenie do Javy i środowiska wykonawczego

## 1.1. Historia i cechy języka Java

- Historia i filozofia języka Java
    - Powstanie języka w firmie Sun Microsystems
    - Główne założenia i cele twórców
    - Ewolucja języka na przestrzeni lat
    - Java Community Process
- Cechy języka Java
    - Niezależność od platformy (Write Once, Run Anywhere)
    - Bezpieczeństwo i kontrola dostępu
    - Programowanie obiektowe (krótkie wspomnienie, bez szczegółów)
    - Automatyczne zarządzanie pamięcią (wprowadzenie do Garbage Collectora)
    - Bogata biblioteka standardowa
    - Wielowątkowość
    - Wsparcie dla sieci i aplikacji rozproszonych

## 1.2. Podstawowe komponenty Javy: JVM, JRE, JDK

- Czym są JVM, JRE, JDK?
- Java Virtual Machine (JVM)
    - Rola JVM w uruchamianiu aplikacji Java
    - Ogólny przegląd architektury JVM
- Java Runtime Environment (JRE)
    - Składniki JRE (JVM, biblioteki klas podstawowych)
- Java Development Kit (JDK)
    - Składniki JDK (kompilator javac, debugger, narzędzia)
    - Różnice między JDK a JRE
    - OpenJDK oraz inni dostawcy, LTS

# Segment 2: Pierwszy program w Javie i struktura projektu

## 2.1. Tworzenie i kompilacja prostego programu

- Metoda main
    - Punkt wejścia do aplikacji
    - Użycie `System.out.println` i `System.out.print`
- Struktura programu w Javie
    - Nazwa klasy a nazwa pliku
    - Konwencje nazewnictwa
- Komentarze
    - Jednoliniowe (`//`), wieloliniowe (`/* ... */`), dokumentacyjne (`/** ... */`)
- Kompilacja i uruchamianie programu
    - Użycie kompilatora `javac`
    - Generowanie plików `.class`
    - Katalogi źródłowe i binarne (`src/` i `bin/` lub `target/`)
    - Wyjaśnienie kodu binarnego i rola bitów w kompilacji
    - Uruchamianie programu za pomocą `java`

## 2.2. Struktura projektu i organizacja kodu

- Pakiety
    - Organizacja kodu w pakietach
    - Konwencje nazewnictwa pakietów
    - Importowanie klas z innych pakietów
- Pliki manifestu
    - Tworzenie plików JAR
    - Zastosowanie plików manifestu w definiowaniu punktu wejścia

# Segment 3: Podstawy składni Javy i typy danych

## 3.1. Typy danych prymitywne i referencyjne

- Typy prymitywne
    - Liczbowe (`byte`, `short`, `int`, `long`, `float`, `double`)
    - Znakowe (`char`)
    - Logiczne (`boolean`)
- Typy referencyjne
    - Klasa `String`
    - Obiektowe odpowiedniki typów prymitywnych (klasy opakowujące: `Integer`, `Double`, `Character`, `Boolean`, itp.)
    - Autoboxing i unboxing
    - Referencje
    - Przechowywanie adresów obiektów w pamięci
    - Porównanie typów prymitywnych i referencyjnych

## 3.2. Zmienne i stałe

- Deklaracja i inicjalizacja
- Zasady nazewnictwa
- Typy zmiennych
- Zasięg zmiennych
    - Zmienne lokalne
    - Słowo kluczowe `static` - pola statyczne
- Słowo kluczowe `final`
    - Definiowanie stałych
    - Niezmienność referencji
- Operacje wejścia
    - Użycie klasy `Scanner`, `BufferedReader` i `InputStreamReader` do odczytu danych od użytkownika

# Segment 4: Operatory, instrukcje sterujące i kontrola przepływu

## 4.1. Operatory

- Operatory arytmetyczne
- Operatory porównania
- Operatory przypisania
- Operatory logiczne
- Operatory bitowe
- Operator ternary (hiperłącze do jego wyjaśnienia w `Instrukcje sterujące`)
- Precedencja operatorów

## 4.2. Instrukcje sterujące

- Instrukcje warunkowe
    - `if`, `else if`, `else`
    - `switch`
    - Operator ternarny
- Pętle
    - `for`, `enhanced for` (foreach), `while`, `do-while`
- Instrukcje skoku
    - `break`, `continue`, `return`

# Segment 5: Tablice i klasy standardowe

## 5.1. Tablice

- Definicja i inicjalizacja
    - Tablice typów prymitywnych
    - Tablice obiektów
    - Jednowymiarowe i wielowymiarowe
    - Tablice dwuwymiarowe (macierze)
    - Tablice nieregularne (tablice tablic)
- Operacje na tablicach
    - Iterowanie, modyfikacja elementów

---

# Segment 6: Szczegóły działania JVM i proces kompilacji
## 6.1. Architektura JVM w szczegółach
- Class Loader
    - Mechanizm ładowania klas
    - Hierarchia Class Loaderów
- Execution Engine
    - Interpretacja i kompilacja JIT
    - Wykonywanie instrukcji
- Podział pamięci w JVM
    - Stos (Stack)
        - Przechowywanie ramek stosu
        - Zmienne lokalne i parametry metody
    - Sterta (Heap)
        - Przechowywanie obiektów
        - Alokacja i dealokacja pamięci
    - Metaspace
        - Przechowywanie metadanych klas

## 6.2. Proces kompilacji i uruchamiania aplikacji
- Od kodu źródłowego do kodu bajtowego
    - Rola kompilatora `javac`
- Uruchamianie aplikacji
    - Użycie polecenia `java`
- Ustawienia JVM: parametry startowe
    - Ustawianie pamięci JVM (`-Xms`, `-Xmx`)
        - Minimalna i maksymalna ilość pamięci
        - Wpływ na wydajność aplikacji
- Inne przydatne opcje
    - Ścieżki klas (`-classpath`)
    - Ustawienia dla Garbage Collectora

# Segment 7: Zarządzanie pamięcią i Garbage Collector
## 7.1. Mechanizmy Garbage Collectora
- Co to jest Garbage Collector? Kiedy się włącza?
- Mechanizmy zbierania nieużywanych obiektów
    - Kryteria uruchamiania GC
- Generacje pamięci
    - Młoda i stara generacja
    - Eden Space i Survivor Spaces
- Podstawowe algorytmy GC
    - Mark and Sweep
    - Copying
    - Mark-Compact

## 7.2. Znaczenie dla programisty
- Jak pisać kod przyjazny dla GC
    - Unikanie tworzenia zbędnych obiektów
    - Wzorce projektowe wspierające wydajność
- Unikanie wycieków pamięci
    - Typowe przyczyny
    - Narzędzia do wykrywania wycieków

# Segment 8: Optymalizacja aplikacji i tunelowanie JVM
## 8.1. Profilowanie i diagnostyka
- Narzędzia do profilowania
    - `jvisualvm`
    - Java Mission Control
    - Krótkie omówienie możliwości
- Analiza zużycia pamięci i CPU
    - Identyfikacja wąskich gardeł
    - Optymalizacja krytycznych fragmentów kodu

## 8.2. Ustawienia JVM i optymalizacja
- Parametry startowe JVM
    - Ustawianie rozmiaru sterty (`-Xms`, `-Xmx`)
    - Ustawienia dla Garbage Collectora
    - Wybór algorytmu GC (np. `-XX:+UseG1GC`)
    - Konfiguracja parametrów GC
- Monitorowanie aplikacji w środowisku produkcyjnym
    - Narzędzia monitorujące
        - Java Mission Control, YourKit
    - Praktyki monitorowania
        - Zbieranie metryk
        - Analiza logów

## 8.3. Zaawansowane mechanizmy Garbage Collectora
- Przegląd różnych GC w JVM
    - Serial GC
    - Parallel GC
    - G1 GC
    - ZGC
    - Kiedy stosować różne GC
- Tunelowanie GC
    - Ustawienia JVM wpływające na GC
    - Dostosowywanie parametrów do potrzeb aplikacji