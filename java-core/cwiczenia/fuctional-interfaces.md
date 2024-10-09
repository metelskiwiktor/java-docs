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

**Zadanie 2: Obsługa zdarzeń za pomocą interfejsów funkcyjnych**

Napisz interfejs funkcyjny `EventListener`, który zawiera metodę:

```java
void onEvent(String eventType, Object data);
```

Następnie utwórz klasę `EventManager`, która pozwala na rejestrowanie i wywoływanie zdarzeń. Klasa powinna posiadać metody:

```java
void registerListener(EventListener listener);
void triggerEvent(String eventType, Object data);
```

- Metoda `registerListener` pozwala na dodanie nowego słuchacza zdarzeń.
- Metoda `triggerEvent` powinna powiadamiać wszystkich zarejestrowanych słuchaczy o wystąpieniu zdarzenia, przekazując im typ zdarzenia i powiązane dane.

Przetestuj działanie, tworząc różne implementacje `EventListener`, które reagują na różne typy zdarzeń, na przykład:

- Logowanie zdarzeń do konsoli.
- Aktualizowanie interfejsu użytkownika.
- Zapis zdarzeń do pliku.

---

**Zadanie 3: Generyczne filtry z użyciem predykatów**

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

**Zadanie 4: Operacje na kolekcjach z użyciem interfejsów funkcyjnych**

Zdefiniuj interfejs funkcyjny `Transformer<T, R>` z metodą:

```java
R transform(T input);
```

Następnie utwórz klasę `CollectionUtils`, która zawiera statyczną metodę:

```java
public static <T, R> List<R> map(List<T> list, Transformer<T, R> transformer);
```

Metoda `map` powinna przekształcać listę `list`, stosując do każdego jej elementu funkcję `transformer`, i zwracać nową listę wyników.

Przetestuj działanie, tworząc różne transformacje:

- Zamiana listy liczb na ich reprezentacje tekstowe.
- Podniesienie każdej liczby w liście do kwadratu.
- Konwersja listy ciągów znaków na ich długości.

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

