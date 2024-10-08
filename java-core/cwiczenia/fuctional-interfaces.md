**Zadanie 1: Podstawy interfejsów funkcyjnych**

Napisz własny interfejs funkcyjny `StringOperation`, który zawiera metodę abstrakcyjną:

```java
String apply(String s);
```

Następnie utwórz klasę `StringProcessor`, która w konstruktorze przyjmuje obiekt `StringOperation`. Klasa powinna posiadać metodę:

```java
String process(String s);
```

Metoda `process` powinna zastosować przekazaną w konstruktorze operację `StringOperation` do podanego ciągu znaków `s` i zwrócić wynik. Przetestuj działanie, tworząc różne instancje `StringProcessor` z różnymi implementacjami `StringOperation` (np. zamiana na wielkie litery, odwracanie ciągu znaków).

---

**Zadanie 2: Generyczne interfejsy funkcyjne**

Zdefiniuj generyczny interfejs funkcyjny `Converter<F, T>` z metodą:

```java
T convert(F from);
```

Następnie utwórz klasę `GenericConverter<F, T>`, która w konstruktorze przyjmuje obiekt `Converter<F, T>`. Klasa powinna posiadać metodę:

```java
T convert(F from);
```

Metoda `convert` powinna używać przekazanego w konstruktorze konwertera do przekształcenia obiektu typu `F` na obiekt typu `T`. Przetestuj działanie, tworząc różne instancje `GenericConverter` z różnymi implementacjami `Converter<F, T>`, przekształcając:

- `String` na `Integer`.
- `Integer` na `String`.
- `Double` na `String`.

---

**Zadanie 3: Łączenie interfejsów funkcyjnych z klasami generycznymi**

Stwórz generyczną klasę `Calculator<T>`, która w konstruktorze przyjmuje obiekt `Operation<T>`, gdzie `Operation` to generyczny interfejs funkcyjny z metodą:

```java
T apply(T a, T b);
```

Klasa `Calculator<T>` powinna posiadać metodę:

```java
T calculate(T a, T b);
```

Metoda `calculate` powinna używać przekazanej w konstruktorze operacji `Operation<T>` do przetworzenia wartości `a` i `b`. Zaimplementuj różne operacje arytmetyczne jako różne instancje `Calculator<T>` z odpowiednimi implementacjami `Operation<T>`:

- Dodawanie.
- Odejmowanie.
- Mnożenie.
- Dzielenie.

Przetestuj działanie klasy `Calculator` dla typów `Integer` i `Double`.

---

**Zadanie 4: Generyczne filtry z użyciem predykatów**

Utwórz generyczny interfejs funkcyjny `Predicate<T>` z metodą:

```java
boolean test(T t);
```

Następnie zaimplementuj klasę `Filter<T>`, która w konstruktorze przyjmuje obiekt `Predicate<T>`. Klasa powinna posiadać metodę:

```java
List<T> filter(List<T> items);
```

Metoda `filter` powinna zwrócić listę elementów z `items`, które spełniają warunek określony przez przekazany w konstruktorze `Predicate<T>`. Przetestuj działanie, tworząc różne instancje `Filter<T>` z różnymi implementacjami `Predicate<T>`, filtrując listy:

- Liczb całkowitych (np. tylko liczby parzyste).
- Ciągów znaków (np. tylko ciągi o długości większej niż 3).

---

**Zadanie 5: Pipeline z użyciem generycznych funkcji**

Zaimplementuj generyczną klasę `Pipeline<T>`, która umożliwia łańcuchowe przetwarzanie danych. Klasa powinna:

- Przechowywać listę funkcji `Function<T, T>`.
- Posiadać metodę `Pipeline<T> addFunction(Function<T, T> function)`, która dodaje funkcję do pipeline'u.
- Posiadać metodę `T execute(T input)`, która stosuje wszystkie dodane funkcje do wejścia `input` w kolejności ich dodawania.

Generyczny interfejs funkcyjny `Function<T, R>` powinien zawierać metodę:

```java
R apply(T t);
```

Przetestuj działanie `Pipeline`, tworząc łańcuch funkcji przetwarzających liczby lub ciągi znaków, np.:

- Dla liczb: pomnożenie przez 2, dodanie 3, podniesienie do kwadratu.
- Dla ciągów znaków: przycięcie spacji, zamiana na wielkie litery, dodanie prefixu.

