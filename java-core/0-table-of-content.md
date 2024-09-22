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
- Zasady nazewnictwa i konwencja nazewnictwa (klasa, metoda, pole)
- Typy zmiennych
- Zasięg zmiennych
    - Zmienne lokalne
    - Słowo kluczowe `static` - pola statyczne
- Słowo kluczowe `final`
    - Definiowanie stałych
    - Niezmienność referencji
- Operacje wejścia
    - Wyjaśnienie czym jest klasa `System` 
    - Użycie klasy `Scanner`, `BufferedReader` i `InputStreamReader` do odczytu danych od użytkownika

# Segment 4: Operatory, instrukcje sterujące i kontrola przepływu

## 4.1. Operatory

- Operatory arytmetyczne
- Operatory porównania
- Operatory przypisania
- Operatory logiczne
- Operatory bitowe
- Operator ternarny (odnośnik do operatora w `Instrukcje warunkowe`)
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
