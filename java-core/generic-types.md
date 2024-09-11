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

### Metoda Generyczna

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

### Metoda Statyczna Generyczna

Metody statyczne również mogą być generyczne i wymagają takiej samej deklaracji typu przed typem zwracanym:

```java
public class Utils {
    public static <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.println(element);
        }
    }
}

// Przykład użycia:
Integer[] intArray = {1, 2, 3};
Utils.printArray(intArray);  // Wyświetli: 1 2 3
```

## Wielokrotne Typy Generyczne

W jednej klasie można używać wielu typów generycznych:

```java
public class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() { return key; }
    public V getValue() { return value; }
}
```

Użycie klasy `Pair`:

```java
Pair<Integer, String> pair = new Pair<>(1, "Jeden");
Integer key = pair.getKey();
String value = pair.getValue();
```

## Generyki w Interfejsach Funkcyjnych

Interfejs funkcyjny `Function<T, R>` z pakietu `java.util.function` to jeden z przykładów zastosowania generyków:

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