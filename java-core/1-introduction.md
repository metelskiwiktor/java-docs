# 1.1. Historia i cechy języka Java

## Historia i filozofia języka Java

### Powstanie języka w firmie Sun Microsystems

Java to jeden z najpopularniejszych języków programowania na świecie, stworzony w firmie Sun Microsystems w 1991 roku
przez zespół kierowany przez Jamesa Goslinga. Początkowo język ten nazywał się Oak, a jego celem było opracowanie
przenośnego oprogramowania dla urządzeń elektronicznych takich jak dekodery telewizji kablowej. Projekt szybko
ewoluował, a w 1995 roku język został przemianowany na Java, kiedy to Sun Microsystems oficjalnie go przedstawił jako
platformę do tworzenia oprogramowania działającego niezależnie od systemu operacyjnego.

### Główne założenia i cele twórców

Celem twórców Javy było stworzenie języka, który będzie:

- **Prosty i znajomy** – Java czerpie wiele koncepcji z C++ i innych języków, ale eliminuje ich skomplikowane aspekty,
  co czyni ją łatwiejszą do nauczenia.
- **Niezależny od platformy** – Java została zaprojektowana z myślą o zasadzie "Write Once, Run Anywhere" (WORA), co
  oznacza, że raz napisany kod może być uruchamiany na dowolnej platformie posiadającej maszynę wirtualną Java (JVM).
- **Bezpieczny** – Dzięki wbudowanym mechanizmom bezpieczeństwa, takim jak kontrola dostępu i weryfikacja kodu
  bajtowego, Java chroni przed nieautoryzowanym dostępem i szkodliwym oprogramowaniem.
- **Wydajny** – Java korzysta z technologii Just-In-Time (JIT) compilation, która optymalizuje wykonywanie kodu na
  bieżąco.
- **Wielowątkowy i dynamiczny** – Obsługa wielu wątków pozwala na wykonywanie kilku procesów jednocześnie, a dynamiczne
  ładowanie klas umożliwia płynne rozszerzanie funkcjonalności.

### Ewolucja języka na przestrzeni lat

Java przeszła wiele istotnych zmian:

- **Java 1.0 (1996)**: Pierwsza oficjalna wersja, skupiona na appletach internetowych.
- **Java 2 (1998)**: Wprowadzenie trzech edycji: SE (Standard Edition), EE (Enterprise Edition), ME (Micro Edition).
- **Java 5 (2004)**: Wprowadzenie takich funkcji jak generics, pętle for-each, autoboxing/unboxing.
- **Java 8 (2014)**: Wprowadzenie wyrażeń lambda, Stream API, nowe API do obsługi dat i czasu.
- **Java 9-17**: Nowe funkcje językowe i optymalizacje, w tym modułowość (Java 9), API do zarządzania procesami,
  ulepszony Garbage Collector, wyrażenia switch, rekordy i pattern matching.
- **Java 18-21**: Nowe funkcje w wersjach preview, takie jak wirtualne wątki (Project Loom), Foreign Function & Memory
  API, kontynuacja rozwoju pattern matching

#### LTS i wersje preview

W ramach rozwoju Javy wprowadzane są różne typy wydań:

- **LTS (Long-Term Support)**: Wersje Javy oznaczone jako LTS (np. Java 8, 11, 17, 21) otrzymują długoterminowe wsparcie
  techniczne, co oznacza, że są regularnie aktualizowane o poprawki bezpieczeństwa i błędy przez wiele lat. Są
  preferowane w środowiskach produkcyjnych, gdzie stabilność i bezpieczeństwo są kluczowe.

- **Wersje preview**: Niektóre nowe funkcje Javy są wprowadzane jako "preview" w pierwszych wydaniach, co oznacza, że są
  dostępne do testowania, ale nie są jeszcze finalnie zatwierdzone. Funkcje te mogą ulec zmianie w przyszłych wersjach.
  Wersje preview umożliwiają programistom eksperymentowanie z nowymi funkcjami, zanim zostaną one oficjalnie włączone do
  standardu Javy. Przykładami takich funkcji są wirtualne wątki (Project Loom) i Foreign Function & Memory API.

### Java Community Process

Java Community Process (JCP) to formalny mechanizm wprowadzania zmian i rozwijania technologii związanych z językiem
Java. Umożliwia on społeczności programistów uczestniczenie w tworzeniu nowych specyfikacji i standardów Javy. Dzięki
temu Java rozwija się w sposób otwarty i zgodny z oczekiwaniami społeczności, co zapewnia jej stałą popularność i
szerokie wsparcie.

## Cechy języka Java

### Niezależność od platformy (Write Once, Run Anywhere)

Jedną z kluczowych cech Javy jest jej niezależność od platformy. Kod źródłowy napisany w Javie jest kompilowany do kodu
bajtowego, który może być uruchamiany na dowolnej maszynie wirtualnej Java (JVM). Dzięki temu programiści mogą pisać kod
raz i uruchamiać go na różnych systemach operacyjnych, takich jak Windows, MacOS czy Linux, bez konieczności
wprowadzania jakichkolwiek zmian.

### Bezpieczeństwo i kontrola dostępu

Java zapewnia wbudowane mechanizmy bezpieczeństwa, które chronią przed potencjalnymi zagrożeniami. Są to między innymi:

- **Kontrola dostępu** – Mechanizmy pozwalające na ograniczenie dostępu do określonych części kodu lub danych.
- **Sandboxing**: Izolacja kodu w tzw. piaskownicy, co ogranicza jego dostęp do zasobów systemowych.
- **Weryfikacja kodu bajtowego** – JVM sprawdza kod bajtowy przed jego wykonaniem, aby upewnić się, że nie jest on
  uszkodzony ani nie zawiera złośliwych elementów.

### Programowanie obiektowe

Java jest językiem w pełni obiektowym, co oznacza, że wszystkie struktury danych w Javie są reprezentowane jako obiekty.
Umożliwia to tworzenie modularnych i wielokrotnego użytku komponentów, co zwiększa przejrzystość i zrozumiałość kodu
oraz ułatwia jego konserwację.

### Automatyczne zarządzanie pamięcią (wprowadzenie do Garbage Collectora)

Java automatycznie zarządza pamięcią za pomocą Garbage Collectora, który odpowiedzialny jest za usuwanie nieużywanych
obiektów z pamięci. Pozwala to programistom skupić się na logice aplikacji, zamiast martwić się o ręczne zarządzanie
pamięcią i uniknąć problemów takich jak wycieki pamięci.

### Bogata biblioteka standardowa

Java posiada rozbudowaną bibliotekę standardową, która oferuje szeroki zakres gotowych do użycia klas i metod. Obejmuje
ona między innymi: operacje na plikach, zarządzanie sieciami, obsługę baz danych, narzędzia kryptograficzne i wiele
innych. Dzięki temu programiści mają dostęp do licznych funkcji i narzędzi, które ułatwiają tworzenie różnorodnych
aplikacji.

### Wielowątkowość

Java oferuje wsparcie dla programowania wielowątkowego, co pozwala na wykonywanie wielu zadań jednocześnie. Jest to
szczególnie przydatne w aplikacjach wymagających dużej wydajności, takich jak gry komputerowe, aplikacje serwerowe, czy
systemy operacyjne.

### Wsparcie dla sieci i aplikacji rozproszonych

Java została zaprojektowana z myślą o wsparciu dla aplikacji sieciowych i rozproszonych. Dzięki bibliotekom takim jak
`java.net` oraz serwletom, programiści mogą łatwo tworzyć aplikacje działające w środowiskach sieciowych, od prostych
serwerów HTTP po złożone systemy rozproszone.

# 1.2. Podstawowe komponenty Javy: JVM, JRE, JDK

## Czym są JVM, JRE, JDK?

Java składa się z trzech podstawowych komponentów: JVM (Java Virtual Machine), JRE (Java Runtime Environment) i JDK (
Java Development Kit). Każdy z tych komponentów odgrywa istotną rolę w cyklu życia aplikacji Java – od napisania kodu po
jego uruchomienie.

## Java Virtual Machine (JVM)

### Rola JVM w uruchamianiu aplikacji Java

JVM jest odpowiedzialna za:

- **Interpretację i wykonanie bajtkodu**: Zapewniając niezależność od platformy.
- **Zarządzanie pamięcią**: Poprzez Garbage Collector.
- **Zapewnienie bezpieczeństwa**: Poprzez weryfikację bajtkodu i izolację aplikacji.

### Ogólny przegląd architektury JVM

- **Class Loader**: Ładuje klasy do pamięci podczas uruchamiania aplikacji.
- **Execution Engine**: Wykonuje instrukcje bajtkodu.
- **Runtime Data Areas**: Obszary pamięci używane podczas wykonywania programu (stos, sterta, rejestry).
- **Garbage Collector**: Zarządza automatycznym zwalnianiem nieużywanej pamięci.

## Java Runtime Environment (JRE)

### Składniki JRE

JRE to środowisko uruchomieniowe Javy, które składa się z JVM oraz zestawu bibliotek klas podstawowych, niezbędnych do
uruchamiania aplikacji napisanych w Javie. JRE zawiera także inne komponenty, takie jak biblioteki dla interfejsu
użytkownika (Swing, AWT) oraz narzędzia do zarządzania aplikacjami.

## Java Development Kit (JDK)

### Składniki JDK

JDK jest kompletnym zestawem narzędzi programistycznych, które umożliwiają tworzenie, kompilowanie i uruchamianie
aplikacji Java. W skład JDK wchodzą:

- **Kompilator (javac)**: Kompiluje kod źródłowy (.java) do bajtkodu (.class).
- **Debugger (jdb)**: Umożliwia debugowanie aplikacji.
- **Narzędzia pomocnicze**:
    - `jar`: Tworzenie i zarządzanie archiwami JAR.
    - `javadoc`: Generowanie dokumentacji z kodu źródłowego.
    - `javap`: Disassembler do analizy bajtkodu.
- **JRE**: Do uruchamiania i testowania aplikacji.

### Różnice między JDK a JRE

JRE zawiera jedynie komponenty potrzebne do uruchamiania aplikacji Java, podczas gdy JDK zawiera wszystkie narzędzia
potrzebne do tworzenia, kompilowania i uruchamiania aplikacji. Dlatego JDK jest niezbędne dla programistów, a JRE
wystarczy użytkownikom końcowym.

### OpenJDK oraz inni dostawcy

Java Development Kit (JDK) jest dostępny w różnych wersjach dostarczanych przez społeczność open-source oraz firmy
komercyjne. Główne opcje to:

- **OpenJDK**: Otwarta implementacja platformy Java SE, rozwijana przez społeczność oraz firmy takie jak Oracle. OpenJDK
  jest darmowe i stanowi podstawę dla wielu innych dystrybucji JDK, co czyni je powszechnie używanym w środowiskach
  deweloperskich i produkcyjnych.

- **Inni dostawcy**:
    - **Oracle JDK**: Komercyjna wersja JDK oparta na OpenJDK, oferująca dodatkowe narzędzia, optymalizacje i wsparcie
      techniczne.
    - **Amazon Corretto**: Darmowa dystrybucja JDK oparta na OpenJDK, rozwijana przez Amazon, dostosowana do użytku w
      chmurze i na serwerach.
    - **Azul Zulu**: Dystrybucja JDK oferowana przez Azul Systems, dostępna zarówno w wersjach darmowych, jak i
      komercyjnych, z dodatkowymi opcjami wsparcia.
    - **Adoptium (dawniej AdoptOpenJDK)**: Projekt rozwijany przez społeczność, oferujący darmowe, wysokiej jakości
      binaria JDK kompatybilne z OpenJDK.

Te dystrybucje oferują różne opcje wsparcia, funkcje dodatkowe oraz optymalizacje, które mogą być przydatne w różnych
kontekstach użycia.
