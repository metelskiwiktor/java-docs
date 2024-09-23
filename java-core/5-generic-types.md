# Typy generyczne w Javie

## Wprowadzenie do typów generycznych

Typy generyczne, wprowadzone w Javie 5, umożliwiają definiowanie klas, interfejsów i metod, które przyjmują typy jako
parametry. Generyki pozwalają na wielokrotne użycie kodu, bezpieczeństwo typów oraz czytelność, umożliwiając działanie
tego samego kodu na różnych typach danych bez potrzeby rzutowania.

## Korzyści z używania generyków

1. **Bezpieczeństwo Typów**: Generyki zapewniają sprawdzanie typów w czasie kompilacji, co zapobiega
   `ClassCastException` w czasie wykonania, upewniając się, że manipulowane dane są oczekiwanego typu.

2. **Wielokrotne użycie kodu**: Dzięki używaniu generyków, można napisać metodę lub klasę, która działa z różnymi typami
   danych, co redukuje powielanie kodu i ułatwia jego utrzymanie.

3. **Czytelność**: Generyki sprawiają, że kod jest bardziej czytelny, dzięki jednoznacznemu określeniu typu obiektów
   używanych w kodzie, co zmniejsza niejasności i poprawia samo-dokumentację kodu.

## Jak używać generyków

Generyki definiuje się za pomocą nawiasów kątowych (`<>`) i mogą być stosowane do klas, interfejsów oraz metod. Na
przykład:

### Klasa Generyczna

```java
public class Box<T> {
    private T item;

    public void setItem(T item) {
        this.item = item;
    }

    public T getItem() {
        return item;
    }
}
```

W tym przykładzie `T` to parametr typu, który można zastąpić dowolnym typem przy tworzeniu instancji klasy `Box`:

```java
Box<Integer> integerBox = new Box<>();
integerBox.setItem(123);

Box<String> stringBox = new Box<>();
stringBox.setItem("Witaj, Generyki!");
```

### Metoda generyczna

Metoda generyczna musi zadeklarować typ generyczny przed zwracanym typem lub przed słowem kluczowym `void`, aby mogła
operować na dowolnym typie danych. Może być zarówno statyczna, jak i niestatyczna. Oto przykład niestatycznej metody
generycznej:

```java
public class Printer {
    public <T> void print(T item) {
        System.out.println(item);
    }
}

// Przykład użycia:
Printer printer = new Printer();
printer.<String>print("Hello");
printer.print(123);  // Typ może być wnioskowany automatycznie
```

### Metoda statyczna generyczna

Metody statyczne również mogą być generyczne i wymagają takiej samej deklaracji typu przed typem zwracanym:

```java
public class Container<T> {

   private T value;

   public Container(T value) {
      this.value = value;
   }

   public T getValue() {
      return value;
   }

   public static <T> Container<T> create(T value) {
      return new Container<>(value);
   }
}

Container<String> stringContainer = Container.create("Hello World");
System.out.println(stringContainer.getValue()); //wyświetli: "Hello World"
```

## Wielokrotne typy generyczne

W jednej klasie można używać wielu typów generycznych:

```java
public class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() {
        return key;
    }

    public V getValue() {
        return value;
    }
}
```

Użycie klasy `Pair`:

```java
Pair<Integer, String> pair = new Pair<>(1, "Jeden");
Integer key = pair.getKey();
String value = pair.getValue();
```

## Generyki w interfejsach funkcyjnych

### Wprowadzenie do `Supplier`

Interfejs `Supplier<T>` z pakietu `java.util.function` jest częścią biblioteki funkcyjnej Javy i reprezentuje dostawcę
wyników. Nie przyjmuje żadnych argumentów i zwraca wynik określonego typu. `Supplier` jest generycznym interfejsem z
typem `T` określającym typ zwracany przez metodę `get()`.

```java
public interface Supplier<T> {
    T get();
}
```

### Przykład użycia `Supplier`

```java
import java.util.function.Supplier;

public class SupplierExample {
    public static void main(String[] args) {
        Supplier<String> stringSupplier = () -> "Hello, Supplier!";
        System.out.println(stringSupplier.get()); // Wyświetli: Hello, Supplier!

        Supplier<Double> randomSupplier = Math::random;
        System.out.println(randomSupplier.get()); // Wyświetli losową liczbę
    }
}
```

### Opis

1. **Deklaracja typu**: `Supplier<T>` jest interfejsem generycznym, gdzie `T` reprezentuje typ zwracany przez metodę
   `get()`.
2. **Użycie lambd**: `Supplier` często jest używany w połączeniu z wyrażeniami lambda lub metodami referencyjnymi, aby
   dostarczyć prosty sposób na zwracanie wyników.

---

### Wprowadzenie do `Function`

Możesz użyć następującego opisu, który lepiej wyjaśnia, czym jest interfejs Function w Javie:

`Function<T, R>` to interfejs funkcyjny z pakietu `java.util.function`, który reprezentuje funkcję przyjmującą jeden argument i
zwracającą wynik. Jest to generyczny interfejs, gdzie `T` jest typem wejściowego argumentu, a `R` jest typem zwracanego
wyniku. `Function` jest często używany do przekształcania wartości lub wykonywania operacji na danych wejściowych, takich
jak mapowanie, filtrowanie lub konwersja typów.

```java
public interface Function<T, R> {
    R apply(T t);
}

Function<String, Integer> stringLength = s -> s.length();
int length = stringLength.apply("Hello");
```

W tym przypadku `T` to typ wejściowy (`String`), a `R` to typ wyjściowy (`Integer`).

## Znak wieloznaczny w generykach

Java zapewnia ograniczone i nieograniczone znaki wieloznaczne do obsługi bardziej złożonych scenariuszy:

1. **Nieograniczony znak wieloznaczny (`<?>`)**: Używany, gdy typ jest nieznany.
2. **Górny ograniczony znak wieloznaczny (`<? extends T>`)**: Ogranicza nieznany typ do konkretnego typu lub jego
   podtypu.
3. **Dolny ograniczony znak wieloznaczny (`<? super T>`)**: Ogranicza nieznany typ do konkretnego typu lub jego nadtypu.

### Porównanie Wildcards i Generyków

- `<? extends T>` pozwala na odczytywanie danych z kolekcji, ale nie na ich modyfikację.
- `<? super T>` pozwala na modyfikację danych, ale nie na odczytywanie ich z pełną precyzją typu.

### Przykład użycia znaków wieloznacznych

```java
public static void processElements(List<? extends Number> numbers) {
    for (Number number : numbers) {
        System.out.println(number);
    }
}
```

W tym przykładzie `processElements` może akceptować listę dowolnych podtypów `Number` (takich jak `Integer`, `Double`,
itp.).

## Ograniczenia typów generycznych

Chociaż typy generyczne w Javie mają wiele zalet, istnieje kilka ograniczeń, o których należy pamiętać:

### 1. Tworzenie tablic typów generycznych
W Javie nie można bezpośrednio utworzyć tablicy typów generycznych. Na przykład próba utworzenia tablicy typu generycznego `T[]` w klasie generycznej spowoduje błąd kompilacji:

```java
public class MyClass<T> {
    T[] array = new T[10];  // Błąd kompilacji!
}
```

Jest to spowodowane mechanizmem wymazywania typów (**type erasure**), który usuwa informacje o typach generycznych podczas kompilacji. W efekcie, nie ma możliwości bezpośredniego tworzenia tablic z typami generycznymi.

Aby obejść to ograniczenie, można skorzystać z rzutowania lub metody `Array.newInstance`:
```java
import java.lang.reflect.Array;

public class MyClass<T> {
    private T[] array;

    public MyClass(Class<T> clazz, int size) {
        array = (T[]) Array.newInstance(clazz, size);
    }
}
```

Znacznie częstszym rozwiązaniem jest unikanie użycia typów generycznych w tablicach i zastąpienie ich tablicami `Object[]`, z rzutowaniem typów w odpowiednich miejscach:
```java
public class MyArrayList<T> {
    private Object[] elements;

    public MyArrayList(int size) {
        elements = new Object[size];
    }

    public void add(T element, int index) {
        elements[index] = element;  // Przechowywanie w Object[]
    }

    public T get(int index) {
        return (T) elements[index];  // Rzutowanie na T
    }
}
```


### 2. Typy prymitywne nie mogą być używane jako argumenty typów generycznych
Generics w Javie działają wyłącznie z typami referencyjnymi (np. `Integer`, `String`). Nie można używać typów prymitywnych (np. `int`, `char`) jako parametrów typu:

```java
List<int> intList = new ArrayList<>();  // Błąd kompilacji!
```

W takich przypadkach należy używać odpowiedników prymitywnych typów referencyjnych (np. `Integer` zamiast `int`).

### 3. Nie można utworzyć instancji typu generycznego
Nie można utworzyć bezpośrednio instancji typu generycznego z powodu wymazywania typów. Przykład:

```java
public class MyClass<T> {
    public MyClass() {
        T obj = new T();  // Błąd kompilacji!
    }
}
```

Aby obejść to ograniczenie, można przyjąć `Class<T>` jako parametr konstruktora, a następnie użyć metody `newInstance()`:

```java
public class MyClass<T> {
   private T obj;

   public MyClass(Class<T> clazz) throws InstantiationException, IllegalAccessException {
      obj = clazz.getDeclaredConstructor().newInstance();
   }
}
```

### 4. Brak wsparcia dla przeładowania metod na podstawie parametrów typu generycznego
Java nie obsługuje przeładowania metod w oparciu o różne typy parametrów generycznych. Na przykład:

```java
public class MyClass {
    public void print(List<String> list) { /* ... */ }
    public void print(List<Integer> list) { /* ... */ }  // Błąd kompilacji!
}
```

## Zadanie praktyczne

Twoim zadaniem jest zaimplementowanie uproszczonej wersji klasy `Optional` w Javie.

Klasa `Optional` została wprowadzona w Javie 8 jako część pakietu `java.util`. Jest to kontener, który może przechowywać
jedną wartość typu obiektowego lub być pusty. Głównym celem użycia `Optional` jest unikanie problemów związanych z
wartością `null` i uniknięcie `NullPointerException`. Klasa ta pozwala na bardziej bezpieczne i czytelne
zarządzanie brakiem wartości w programie.

Twoja implementacja klasy powinna umożliwiać przechowywanie obiektu dowolnego typu oraz operacje takie jak pobieranie wartości i
sprawdzanie, czy wartość jest obecna.

## Sekcja 1: Podstawowe operacje

### `ofNullable(T value)`

`ofNullable` to statyczna metoda, która zwraca instancję `Optional`. Jeśli przekazana wartość jest `null`, metoda zwraca pustą instancję `Optional`; w przeciwnym przypadku, zwraca instancję `Optional` z wartością.

```java
Optional<String> nullableValue = Optional.ofNullable("Hello");
System.out.println(nullableValue.get()); // Wyświetli: Hello

Optional<String> emptyNullableValue = Optional.ofNullable(null);
System.out.println(emptyNullableValue.isPresent()); // Wyświetli: false
```

### `empty()`

Metoda `empty` zwraca pustą instancję `Optional`, która nie przechowuje żadnej wartości.

```java
Optional<String> emptyValue = Optional.empty();
boolean isValuePresent = emptyValue.isPresent(); // Zwraca: false
```

### `isPresent()`

Metoda `isPresent` zwraca `true`, jeśli wartość jest obecna w `Optional`, oraz `false` w przeciwnym przypadku.

```java
Optional<String> optionalValue = Optional.ofNullable("Hello");
if (optionalValue.isPresent()) {
    System.out.println("Wartość jest obecna!");
}
```

### `get()`

Metoda `get` zwraca przechowywaną wartość, jeśli jest obecna. Jeśli wartość nie jest obecna, rzuca wyjątek `NoSuchElementException`.

```java
Optional<String> optionalValue = Optional.ofNullable("Hello");
String value = optionalValue.get(); // Zwraca: "Hello"
System.out.println(value); // Wyświetli: Hello
```

### `orElse(T other)`

Metoda `orElse` zwraca przechowywaną wartość, jeśli jest obecna, w przeciwnym przypadku zwraca wartość domyślną przekazaną jako argument.

```java
Optional<String> optionalValue = Optional.empty();
String value = optionalValue.orElse("Default Value");
System.out.println(value); // Wyświetli: Default Value
```

## Sekcja 2: Rozszerzone operacje

### `of(T value)`

Metoda `of` jest podobna do `ofNullable`, ale różni się tym, że nie akceptuje wartości `null`. Jeśli `null` zostanie przekazany do `of`, metoda rzuci wyjątek `NullPointerException`.

```java
try {
    Optional<String> nullValue = Optional.of(null); // Rzuci NullPointerException
} catch (NullPointerException e) {
    System.out.println("Nie można przekazać wartości null do metody of!");
}
```

### `isEmpty()`

Metoda `isEmpty` zwraca `true`, jeśli w `Optional` nie ma żadnej wartości (czyli jest pusty), oraz `false` w przeciwnym przypadku.

```java
Optional<String> emptyValue = Optional.empty();
if (emptyValue.isEmpty()) {
    System.out.println("Optional jest pusty!");
}
```

### `orElseGet(Supplier<? extends T> other)`

Metoda `orElseGet` zwraca wartość, jeśli jest obecna, w przeciwnym przypadku wywołuje dostarczony `Supplier` i zwraca jego wynik.

```java
Optional<String> emptyValue = Optional.empty();
String generatedValue = emptyValue.orElseGet(() -> "Generated Value");
System.out.println(generatedValue); // Wyświetli: Generated Value
```

### `orElseThrow(Supplier<? extends X> exceptionSupplier)`

Metoda `orElseThrow` zwraca wartość, jeśli jest obecna, w przeciwnym przypadku rzuca wyjątek dostarczony przez `Supplier`.

```java
Optional<String> emptyValue = Optional.empty();
emptyValue.orElseThrow(() -> new IllegalArgumentException("Brak wartości")); // Rzuci wyjątek IllegalArgumentException
```
