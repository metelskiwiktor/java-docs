
# Klasa Optional w Javie

## Wprowadzenie do klasy Optional

Klasa `Optional` została wprowadzona w Javie 8 jako część pakietu `java.util`. Jest to kontener, który może przechowywać jedną wartość typu obiektowego lub być pusty. Głównym celem użycia `Optional` jest unikanie problemów związanych z wartością `null` i uniknięcie `NullPointerException`. Klasa `Optional` pozwala na bardziej bezpieczne i czytelne zarządzanie brakiem wartości w programie.

## Funkcjonalność klasy Optional

1. **Tworzenie Optional:**
    - `Optional.of(value)` - tworzy Optional z wartością, wartość nie może być `null`.
    - `Optional.ofNullable(value)` - tworzy Optional, który może być pusty, jeżeli wartość jest `null`.
    - `Optional.empty()` - tworzy pusty Optional.

2. **Sprawdzanie zawartości:**
    - `isPresent()` - sprawdza, czy Optional zawiera wartość.
    - `isEmpty()` - sprawdza, czy Optional jest pusty (od Javy 11).

3. **Pobieranie wartości:**
    - `get()` - zwraca wartość, jeżeli jest obecna, lub rzuca wyjątek `NoSuchElementException` jeśli jest pusta.
    - `orElse(defaultValue)` - zwraca wartość, jeżeli jest obecna, w przeciwnym razie zwraca `defaultValue`.
    - `orElseGet(Supplier)` - zwraca wartość lub wykonuje dostarczony Supplier, aby uzyskać wartość domyślną.
    - `orElseThrow(Supplier)` - zwraca wartość lub rzuca wyjątek, jeżeli Optional jest pusty.

4. **Transformacja wartości:**
    - `map(Function)` - przekształca wartość, jeżeli jest obecna.
    - `flatMap(Function)` - podobne do `map`, ale pozwala na pracę z Optional w środku transformacji.
    - `filter(Predicate)` - zwraca Optional z wartością, jeśli spełnia podany warunek.

## Przykłady użycia

### Przykład 1: Tworzenie Optional i sprawdzanie zawartości

```java
Optional<String> name = Optional.of("Jan");
Optional<String> emptyName = Optional.empty();

System.out.println(name.isPresent());  // true
System.out.println(emptyName.isPresent());  // false
```

### Przykład 2: Użycie orElse

```java
String result = emptyName.orElse("Domyślna wartość");
System.out.println(result);  // "Domyślna wartość"
```

### Przykład 3: Użycie map i orElse

```java
Optional<String> optionalName = Optional.of("Anna");
String upperCaseName = optionalName.map(String::toUpperCase).orElse("Brak imienia");
System.out.println(upperCaseName);  // "ANNA"
```

## Zadania praktyczne

### Zadanie 1: Tworzenie Optional
Stwórz metodę, która przyjmuje obiekt typu `String` i zwraca `Optional<String>`. Jeżeli przekazana wartość jest `null`, zwróć pusty Optional.

### Zadanie 2: Bezpieczne pobieranie wartości
Napisz metodę, która przyjmuje `Optional<Integer>` i zwraca wartość pomnożoną przez 2, jeżeli Optional nie jest pusty. W przeciwnym razie zwróć `0`.

### Zadanie 3: Użycie map i filter
Przerób poniższy kod, by korzystał z Optional map i filter; ma zwracać Optional z wielkimi literami, ale tylko jeśli długość tekstu jest większa niż 3 znaki.

```java
Optional<String> toUpperCaseIfLongerThanThree(Optional<String> input) {
    if (input.isPresent()) {
        String value = input.get();
        if (value.length() > 3) {
            return Optional.of(value.toUpperCase());  
        }
    }
    return Optional.empty();
}
```

### Zadanie 4: Unikanie NullPointerException
Przerób poniższy kod, aby korzystał z Optional zamiast sprawdzać `null`:
```java
String value = getSomeValue();
if (value != null) {
    System.out.println(value.toUpperCase());
}
```

# FAQ
## Dlaczego istnieje `of` oraz `ofNullable`? Czy `of` nie wystarczy?

Metoda `of(T value)` nie akceptuje `null` jako argumentu i rzuca `NullPointerException`, jeśli `null` zostanie przekazany. Dzięki temu wymusza pewność, że nie pracujemy z `null`. Natomiast `ofNullable(T value)` pozwala na używanie `null`, co jest przydatne, gdy wartość może być nieokreślona. Użycie obu metod daje programiście pełną kontrolę nad tym, jak `Optional` będzie zarządzać potencjalnym brakiem wartości.

---

## Dlaczego możemy użyć `Supplier` zamiast bezpośredniego `T`?

`Supplier` w metodach takich jak `orElseGet` i `orElseThrow` pełni kluczową rolę, która różni się od zwykłego przekazania wartości typu `T`.

1. **Opóźnione obliczenia (`Lazy Evaluation`)**:
    - `Supplier` jest interfejsem funkcyjnym, który dostarcza wartość w momencie jej użycia, a nie od razu podczas wywołania metody.
    - Kod wewnątrz `Supplier` nie jest wykonywany, jeśli `Optional` zawiera wartość. Jest wywoływany dopiero wtedy, gdy jest potrzebny – na przykład, gdy `Optional` jest pusty.

2. **Efektywność**:
    - `Supplier` jest bardziej efektywny, gdy obliczenie wartości jest kosztowne lub skomplikowane, a jego wynik jest potrzebny tylko wtedy, gdy `Optional` jest pusty.
    - Dzięki `Supplier`, obliczenia są opóźnione, co może zapobiec niepotrzebnym operacjom i poprawić wydajność programu.

3. **Obsługa błędów i wyjątków**:
    - W przypadku `orElseThrow`, `Supplier` dostarcza wyjątek tylko wtedy, gdy jest potrzebny. Użycie `Supplier` pozwala na bardziej dynamiczne podejście do generowania wyjątków, np. z komunikatami zależnymi od bieżącego stanu.

---

## Czym jest `get()` klasy Optional?

Metoda `get()` w klasie `Optional` jest jedną z podstawowych metod do uzyskiwania wartości, ale powinna być używana ostrożnie lub całkowicie unikać jej w nowoczesnym kodzie. Klasa `Optional` została zaprojektowana, aby zapobiegać problemom związanym z `null`, jednak używanie `get()` może te problemy przywrócić.

### Powody, dla których warto unikać `get()`

1. **Rzucanie wyjątku `NoSuchElementException`**:
   Metoda `get()` rzuca wyjątek `NoSuchElementException`, gdy `Optional` jest pusty. To sprawia, że kod staje się równie niebezpieczny jak tradycyjne sprawdzanie `null`, narażając na nieoczekiwane wyjątki.

2. **Zmniejszona czytelność i bezpieczeństwo**:
   Użycie `get()` nie jest semantycznie bezpieczne, ponieważ nie wymusza na programiście uprzedniego sprawdzenia, czy wartość faktycznie istnieje. Lepszym podejściem jest użycie metod takich jak `orElse()`, `orElseGet()`, czy `ifPresent()`, które jasno określają, co się stanie, gdy wartość nie istnieje.

3. **Zaprzeczenie idei Optional**:
   Klasa `Optional` została stworzona w celu unikania bezpośredniego operowania na `null` i związanych z tym błędów. Używając `get()`, ignoruje się główny cel Optional, przywracając problemy, które ta klasa miała rozwiązywać.

> **_Informacja:_**  Używaj `get()` dopiero po ówczesnym sprawdzeniu wartości pola `Optional`, na przykład za pomocą `isPresent()`.

---

## Różnica między `map` a `flatMap` w klasie Optional

`map` i `flatMap` to dwie metody klasy `Optional`, które służą do przekształcania wartości przechowywanych w `Optional`. Obie są często używane, ale mają różne zastosowania i działanie.

### `map()`

- **Działanie**: Przekształca wartość przechowywaną w `Optional`, jeśli jest obecna, stosując do niej funkcję. Zwraca nowy `Optional` z wynikiem tej transformacji.
- **Zastosowanie**: Stosowane, gdy funkcja przekształcająca zwraca typ prosty (np. `String`, `Integer`), a nie `Optional`.
- **Przykład**:

```java
Optional<String> name = Optional.of("Anna");
Optional<String> upperCaseName = name.map(String::toUpperCase); // Zwraca Optional<String>
System.out.println(upperCaseName); // Output: Optional[ANNA]
```

### `flatMap()`

- **Działanie**: Działa podobnie jak `map`, ale zakłada, że funkcja przekształcająca zwraca `Optional`. Dzięki temu unikamy zagnieżdżonych `Optional<Optional<T>>`.
- **Zastosowanie**: Używane, gdy funkcja przekształcająca zwraca już `Optional`, co pozwala na "spłaszczenie" wyniku.
- **Przykład**:

```java
Optional<String> name = Optional.of("Anna");
Optional<Integer> nameLength = name.flatMap(n -> Optional.of(n.length())); // Zwraca Optional<Integer>
System.out.println(nameLength); // Output: Optional[4]
```

### Główna różnica

- **`map`** przekształca wartość i zwraca `Optional` z nową wartością.
- **`flatMap`** przekształca wartość i spłaszcza wynik, jeśli jest on `Optional`, zapobiegając zagnieżdżeniom `Optional` w `Optional`.
