# Pierwszy program w Javie i struktura projektu

Rozpoczęcie przygody z Javą zaczyna się od napisania i uruchomienia pierwszego programu. W tym segmencie przeprowadzimy
Cię przez proces tworzenia prostego programu, wyjaśnimy, jak działa kompilacja i uruchamianie kodu w Javie, oraz omówimy
organizację kodu w projektach. Dowiesz się również, czym są pakiety, pliki JAR i jak z nich korzystać.

## Tworzenie pierwszego programu w Javie

### Pisanie programu "Hello, World!"

Najlepszym sposobem na rozpoczęcie nauki jest napisanie programu, który wyświetla na ekranie prosty komunikat. W
przypadku Javy tradycyjnie jest to "Hello, World!".

**Przykładowy kod:**

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

**Omówienie kodu:**

- **Deklaracja klasy:** `public class HelloWorld` tworzy publiczną klasę o nazwie `HelloWorld`. W Javie każda aplikacja
  jest zbiorem klas.
- **Metoda `main`:** `public static void main(String[] args)` to punkt startowy programu. JVM (Java Virtual Machine)
  zaczyna wykonywanie kodu właśnie od tej metody.
- **Wyświetlanie tekstu:** `System.out.println("Hello, World!");` powoduje wyświetlenie tekstu na konsoli i przejście do
  nowej linii.

### Zrozumienie elementów programu

#### Metoda `main`

Metoda `main` jest niezbędna w każdej aplikacji konsolowej w Javie. Jej sygnatura musi dokładnie odpowiadać:

```java
public static void main(String[] args)
```

- **`public`:** Metoda jest dostępna dla JVM z dowolnego miejsca.
- **`static`:** Należy do klasy, a nie do instancji obiektu.
- **`void`:** Nie zwraca żadnej wartości.
- **`String[] args`:** Tablica argumentów przekazywanych z linii poleceń.

#### Użycie `System.out.println` i `System.out.print`

- **`System.out.println()`** – wyświetla podany tekst i dodaje na końcu znak nowej linii.
- **`System.out.print()`** – wyświetla tekst bez dodawania nowej linii.

**Przykład:**

```java
System.out.print("To jest ");
System.out.println("przykład.");
```

**Wynik na konsoli:**

```
To jest przykład.
```

### Komentarze w Javie

Komentarze służą do opisywania kodu i są ignorowane przez kompilator.

- **Komentarz jednoliniowy:** Zaczyna się od `//`.

  ```java
  // To jest komentarz jednoliniowy
  ```

- **Komentarz wieloliniowy:** Zaczyna się od `/*`, a kończy na `*/`.

  ```java
  /*
   * To jest komentarz
   * wieloliniowy.
   */
  ```

- **Komentarz dokumentacyjny:** Używany z narzędziem `javadoc` do generowania dokumentacji.

  ```java
  /**
   * To jest komentarz dokumentacyjny.
   */
  ```

## Kompilacja i uruchamianie programu

### Czym jest kompilator?

Kompilator to program, który tłumaczy kod źródłowy napisany w języku programowania (np. Java) na kod maszynowy lub inny
format pośredni. W Javie kompilator `javac` tłumaczy kod źródłowy na **kod bajtowy** – niezależny od platformy kod
wykonywany przez JVM.

### Kompilacja kodu źródłowego

1. **Zapisz kod źródłowy** w pliku z rozszerzeniem `.java`. Nazwa pliku powinna odpowiadać nazwie klasy publicznej w nim
   zawartej.

   **Przykład:** `HelloWorld.java`

2. **Kompilacja za pomocą `javac`:**

   W linii poleceń przejdź do katalogu z plikiem źródłowym i wykonaj:

   ```bash
   javac HelloWorld.java
   ```

   Po kompilacji powstanie plik `HelloWorld.class` zawierający kod bajtowy.

### Uruchamianie programu za pomocą `java`

Komenda `java` uruchamia JVM, która interpretuje kod bajtowy zawarty w plikach `.class`.

**Uruchomienie programu:**

```bash
java HelloWorld
```

**Wynik:**

```
Hello, World!
```

### Struktura katalogów w projekcie Java

Dla lepszej organizacji kodu w projektach Java zaleca się stosowanie poniższej struktury katalogów:

- **`src/`** – katalog z kodem źródłowym (`.java`). Tutaj umieszczane są wszystkie pliki źródłowe projektu. Organizacja
  katalogów wewnątrz `src` powinna odzwierciedlać strukturę pakietów, np. `src/com/example/app`.

- **`bin/`** – katalog z plikami wynikowymi (`.class`). Katalog `bin` jest często używany do przechowywania
  skompilowanych plików kodu bajtowego generowanych przez kompilator `javac`.

- **`target/`** – katalog z wynikami budowania projektu, używany zazwyczaj przez narzędzia do automatyzacji budowania,
  takie jak **Maven**. Oprócz skompilowanych plików `.class`, `target` może zawierać pliki JAR/WAR, raporty z testów,
  dokumentację, itp. Jest to miejsce, gdzie narzędzia budujące zapisują wszystkie pliki i zasoby związane z procesem
  budowy.

- **`out/`** – katalog z plikami wynikowymi, podobny do `bin/`, używany głównie przez IDE (np. IntelliJ IDEA). W `out`
  znajdziesz skompilowane pliki `.class` i inne pliki wynikowe związane z budowaniem projektu za pomocą narzędzi
  wbudowanych w IDE.

Każdy z tych katalogów ma swoje specyficzne zastosowanie w zależności od używanych narzędzi i preferencji projektu.

**Przykład struktury:**

```
projekt/
├── src/
│   └── HelloWorld.java
└── bin/
```

### Kompilacja z określeniem katalogu docelowego

Aby skompilować kod i umieścić pliki `.class` w określonym katalogu (np. `bin/`), użyj:

```bash
javac -d bin/ src/HelloWorld.java
```

- **`-d bin/`** – wskazuje katalog docelowy dla plików wynikowych.

## Głębsze spojrzenie na kompilację i uruchamianie

### Rola kodu bajtowego i JVM

- **Kod bajtowy:** Skompilowany kod pośredni, który jest niezależny od platformy. Pliki `.class` zawierają kod bajtowy.
- **JVM:** Maszyna wirtualna Javy interpretuje kod bajtowy i wykonuje go na konkretnej platformie.

Dzięki temu podejściu programy Java są przenośne między różnymi systemami operacyjnymi bez konieczności rekompilacji.

### Co się dzieje podczas kompilacji?

- **Kompilator `javac`** analizuje kod źródłowy pod kątem błędów składniowych.
- Jeśli nie ma błędów, generuje pliki `.class` z kodem bajtowym.
- Kod bajtowy jest zoptymalizowany pod kątem wydajności i gotowy do interpretacji przez JVM.

### Komenda `java`

Komenda `java` uruchamia JVM i wskazuje, którą klasę z metodą `main` ma wykonać.

**Składnia:**

```bash
java [opcje] nazwa_klasy
```

- **`[opcje]`** – opcjonalne parametry dla JVM.
- **`nazwa_klasy`** – nazwa klasy bez rozszerzenia `.class`.

## Organizacja kodu i struktura projektu

### Pakiety w Javie

Pakiety służą do grupowania powiązanych klas i interfejsów oraz pomagają uniknąć konfliktów nazw.

#### Definiowanie pakietu

Na początku pliku źródłowego deklaruje się pakiet:

```java
package com.moje.przykladowe.pakiety;
```

#### Organizacja plików zgodnie z pakietami

Struktura katalogów powinna odzwierciedlać hierarchię pakietów.

**Przykład:**

- **Deklaracja pakietu:**

  ```java
  package com.example.app;
  ```

- **Struktura katalogów:**

  ```
  projekt/
  ├── src/
  │   └── com/
  │       └── example/
  │           └── app/
  │               └── Main.java
  ```

#### Importowanie klas z innych pakietów

Aby użyć klasy z innego pakietu, należy ją zaimportować, na przykład:

```java
import com.example.utils.Helper;

public class Main {
    // kod klasy
}
```

Jeśli chcesz zaimportować wszystkie klasy z pakietu, wystarczy dodać gwiazdkę (*):

```java
import com.example.utils.*;
```

> [!WARNING]
> W niektórych organizacjach pracy zabronione jest importowanie wszystkich klas z pakietu w kodzie produkcyjnym.

### Tworzenie i korzystanie z plików JAR

#### Czym jest plik JAR?

Plik **JAR** (Java ARchive) to skompresowane archiwum (podobne do ZIP) zawierające skompilowane klasy, zasoby i metadane
potrzebne do uruchomienia aplikacji Java.

Aby plik JAR mógł być uruchamialny, **wymaga pliku manifestu** (`MANIFEST.MF`). Plik manifestu powinien określać kluczowe
informacje o zawartości archiwum JAR.

#### Czym jest plik manifestu?

Plik manifestu (`MANIFEST.MF`) jest specjalnym plikiem tekstowym, który znajduje się wewnątrz archiwum JAR w katalogu
`META-INF/`. Plik manifestu zawiera metadane o zawartości archiwum JAR i może określać różne informacje, takie jak:

- **`Main-Class`**: Nazwa klasy zawierającej metodę `main()`, która jest punktem wejścia do aplikacji. Dzięki tej
  informacji, JVM wie, którą klasę uruchomić po wykonaniu komendy `java -jar`.

- **`Class-Path`**: Ścieżki do dodatkowych bibliotek lub innych plików JAR, które są wymagane do uruchomienia aplikacji.

- **Inne opcje**: Własne metadane, wersje bibliotek, autora, itp.

#### Po co używa się plików JAR?

- **Dystrybucja:** Ułatwiają rozpowszechnianie aplikacji jako pojedynczego pliku.
- **Modularność:** Pozwalają na organizację kodu w moduły i łatwe zarządzanie zależnościami.
- **Wydajność:** JVM może efektywniej ładować klasy z jednego skompresowanego pliku.

#### Tworzenie pliku JAR

1. **Skopiuj wszystkie skompilowane klasy do jednego katalogu** (np. `bin/`).

2. **Utwórz plik manifestu `manifest.mf`:**

   **Przykład zawartości:**

   ```
   Manifest-Version: 1.0
   Main-Class: com.example.app.Main
   ```

3. **Utwórz plik JAR za pomocą narzędzia `jar`:**

   ```bash
   jar cfm app.jar manifest.mf -C bin/ .
   ```

    - **`c`** – tworzy nowe archiwum.
    - **`f`** – określa nazwę pliku JAR.
    - **`m`** – dołącza manifest.
    - **`-C bin/ .`** – wskazuje katalog z plikami do dodania.

#### Uruchamianie aplikacji z pliku JAR

```bash
java -jar app.jar
```

#### Dodatkowe zastosowania plików JAR

- **Biblioteki:** Pakowanie klas pomocniczych, które mogą być wykorzystywane w innych projektach.
- **Aplikacje webowe:** W środowisku Java EE pliki JAR są używane w archiwach WAR i EAR.

## Podsumowanie

W tym segmencie zapoznaliśmy się z podstawami tworzenia i uruchamiania aplikacji w Javie. Omówiliśmy strukturę prostego
programu, proces kompilacji i uruchamiania kodu oraz organizację projektu.

**Kluczowe punkty:**

- **Pierwszy program:** Napisanie i zrozumienie działania programu "Hello, World!".
- **Kompilacja:** Proces tłumaczenia kodu źródłowego na kod bajtowy za pomocą kompilatora `javac`.
- **Uruchamianie programu:** Wykonywanie skompilowanego kodu przez JVM za pomocą komendy `java`.
- **Struktura projektu:** Organizacja kodu w katalogach `src/` i `bin/` lub `target/`.
- **Pakiety:** Grupowanie klas w pakiety dla lepszej organizacji i unikania konfliktów nazw.
- **Pliki JAR:** Tworzenie archiwów zawierających skompilowane klasy i zasoby, ułatwiające dystrybucję i uruchamianie
  aplikacji.

## Przydatne wskazówki

- **Uważaj na wielkość liter:** Java jest językiem czułym na wielkość liter, więc `Main` i `main` to dwie różne rzeczy.
- **Sprawdzaj ścieżki dostępu:** Przy organizacji kodu w pakietach upewnij się, że struktura katalogów odpowiada
  deklaracjom pakietów.

# Zadania praktyczne

## Zadania podstawowe

1. **Napisz swój pierwszy program w Javie:**
    - Stwórz nowy plik Java o nazwie `HelloWorld.java`.
    - Napisz program, który wypisuje "Hello, World!" na konsoli.
    - Skompiluj i uruchom program, aby upewnić się, że działa poprawnie.

2. **Zmień wyjście w programie:**
    - Zmodyfikuj program `HelloWorld.java`, aby zamiast "Hello, World!" wypisywał "Witaj, Java!".
    - Skompiluj i uruchom zmieniony program.

3. **Dodaj nową metodę:**
    - Dodaj do klasy `HelloWorld` nową metodę `printCustomMessage`, która przyjmuje parametr typu `String` i wypisuje ten tekst na konsoli.
    - Zmień metodę `main`, aby wywoływała `printCustomMessage` z własnym tekstem.

## Zadania zaawansowane

1. **Tworzenie i użycie pakietu:**
    - Stwórz nowy pakiet o nazwie `com.example.helloworld`.
    - Przenieś klasę `HelloWorld` do nowo utworzonego pakietu.
    - Zmodyfikuj kod, aby poprawnie importować i używać klasy z pakietu, a następnie skompiluj i uruchom program.

2. **Utwórz plik JAR i uruchom go:**
    - Skompiluj swój program i utwórz z niego plik JAR (Java Archive).
    - Upewnij się, że plik JAR jest samodzielny i można go uruchomić za pomocą polecenia `java -jar`.
    - Przetestuj działanie pliku JAR, uruchamiając go z konsoli.

