# Wprowadzenie do Testów Jednostkowych w Javie z użyciem JUnit 5

Testowanie jest kluczowym elementem procesu tworzenia oprogramowania. Pozwala na wykrycie błędów na wczesnym etapie oraz zapewnia, że kod działa zgodnie z oczekiwaniami. W tym artykule skupimy się na testach jednostkowych w Javie, korzystając z frameworka JUnit 5.

## 1. Skąd się bierze nazwa testu jednostkowego?

Termin **test jednostkowy** (ang. *unit test*) pochodzi od słowa "jednostka", które w kontekście programowania odnosi się do najmniejszej części kodu, którą można przetestować w izolacji. W języku Java taką jednostką może być pojedyncza metoda lub klasa.

## 2. Czym jest test jednostkowy?

Test jednostkowy to niewielki fragment kodu, który sprawdza poprawność działania pojedynczej jednostki kodu źródłowego. Celem jest upewnienie się, że dana metoda zwraca oczekiwane wyniki dla różnych zestawów danych wejściowych. Testy jednostkowe pomagają w:

- Wykrywaniu błędów na wczesnym etapie.
- Ułatwieniu refaktoryzacji kodu.
- Dokumentowaniu zachowania kodu.

## 3. Nazewnictwo testów jednostkowych

Dobre praktyki sugerują, aby nazwy testów były:

- **Opisowe**: Nazwa powinna jasno wskazywać, co jest testowane i jakie są oczekiwane rezultaty.
- **Konsekwentne**: Stosowanie jednolitego schematu nazewnictwa ułatwia nawigację i zrozumienie kodu.

Przykładowe konwencje nazewnictwa:

- **`methodName_StateUnderTest_ExpectedBehavior()`**: Ta konwencja opisuje nazwę metody, stan testowany oraz oczekiwane zachowanie. Na przykład `add_TwoPositiveNumbers_ReturnsSum()`.
- **`shouldDoSomething_WhenCondition()`**: Ta konwencja zaczyna się od "should" (powinien) i opisuje, co metoda powinna zrobić w określonych warunkach. Na przykład `shouldThrowException_WhenDivideByZero()`.
- **`testMethodName()`**: Prostszą konwencją jest nazywanie testów po prostu `testAdd()`, choć jest to mniej opisowe.

## 4. Jakie przypadki powinny testy sprawdzać?

Testy powinny obejmować:

- **Przypadki pozytywne**: Sprawdzanie, czy metoda działa poprawnie dla prawidłowych danych wejściowych.
- **Przypadki negatywne**: Testowanie zachowania metody dla nieprawidłowych lub skrajnych danych wejściowych.
- **Przypadki brzegowe**: Sprawdzanie działania metody na granicach zakresu danych (np. maksymalne i minimalne wartości).

## 5. Struktura testu

Istnieje kilka popularnych struktur pisania testów:

### Given/When/Then (najczęściej stosowana)

- **Given** (Stan początkowy): Przygotowanie danych i środowiska.
- **When** (Działanie): Wykonanie testowanej metody.
- **Then** (Oczekiwany wynik): Sprawdzenie rezultatów za pomocą asercji.

### Arrange/Act/Assert

- **Arrange**: Przygotowanie danych i obiektów potrzebnych do testu.
- **Act**: Wykonanie testowanej akcji lub metody.
- **Assert**: Weryfikacja wyników za pomocą asercji.

### Setup/Exercise/Verify/Teardown

- **Setup**: Inicjalizacja obiektów i stanu przed testem.
- **Exercise**: Wykonanie testowanej metody.
- **Verify**: Sprawdzenie wyników.
- **Teardown**: Czyszczenie po teście (nie zawsze potrzebne w testach jednostkowych).

Wybór struktury zależy od preferencji zespołu i konwencji stosowanych w projekcie.

## 6. Informacje o JUnit

### JUnit 3, 4 i 5

- **JUnit 3**: Wprowadził podstawy testowania jednostkowego w Javie, używając dziedziczenia i metod zaczynających się od `test`.
- **JUnit 4**: Wprowadził adnotacje, takie jak `@Test`, co uprościło pisanie testów i wyeliminowało potrzebę dziedziczenia.
- **JUnit 5**: Najnowsza wersja, która wprowadza modularną architekturę i nowe funkcje.

#### Moduły JUnit 5

- **JUnit Platform**: Podstawa dla uruchamiania testów na różnych platformach i silnikach testowych.
- **JUnit Jupiter**: Nowe API i adnotacje do pisania testów (zastępuje JUnit 4).
- **JUnit Vintage**: Umożliwia uruchamianie testów napisanych w JUnit 3 i 4 w środowisku JUnit 5.

### Klasa Assertions

Klasa **Assertions** w JUnit Jupiter zawiera statyczne metody służące do weryfikacji oczekiwanych wyników w testach. Są one kluczowe dla sprawdzania, czy testowane metody działają poprawnie. Przykładowe metody asercji:

- `Assertions.assertEquals(expected, actual)`: Sprawdza, czy dwie wartości są równe.
- `Assertions.assertTrue(condition)`: Sprawdza, czy warunek jest prawdziwy.
- `Assertions.assertThrows(exceptionClass, executable)`: Sprawdza, czy wykonanie kodu rzuca oczekiwany wyjątek.

### Adnotacje @BeforeEach, @AfterEach, @BeforeAll, @AfterAll

- `@BeforeEach`: Metoda oznaczona tą adnotacją jest wykonywana przed każdym testem. Używana do przygotowania stanu przed testem.
- `@AfterEach`: Metoda wykonywana po każdym teście. Służy do czyszczenia stanu po teście.
- `@BeforeAll`: Metoda wykonywana raz przed wszystkimi testami. Musi być statyczna.
- `@AfterAll`: Metoda wykonywana raz po wszystkich testach. Musi być statyczna.

Te adnotacje pomagają w zarządzaniu stanem testów i unikaniu powtarzającego się kodu.

### Dodawanie JUnit 5 jako zależności w Maven

Aby dodać JUnit 5 do projektu Maven, należy umieścić w pliku `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.9.3</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

## 7. Tworzenie prostego kalkulatora

### Struktura projektu

Przy tworzeniu testów jednostkowych ważne jest zachowanie odpowiedniej struktury katalogów w projekcie Maven:

```
projekt/
├── src/
│   ├── main/
│   │   └── java/
│   │       └── Calculator.java
│   └── test/
│       └── java/
│           └── CalculatorTest.java
```

- **Kod źródłowy** znajduje się w `src/main/java`.
- **Testy jednostkowe** umieszczamy w `src/test/java`.
- Dzięki takiej strukturze narzędzia budujące (np. Maven) automatycznie wykryją testy.
- Ważne jest by struktura katalogu `test` odzwierciedlała strukturę katalogu `main` w celu zachowania widoczności
  modyfikatór dostępu typu `package`.

### Adnotacja @Test

Każda metoda testowa powinna być oznaczona adnotacją `@Test` z pakietu `org.junit.jupiter.api.Test`:

```java
import org.junit.jupiter.api.Test;
```

## 7.1. Opis klasy `Calculator`

Stworzymy klasę `Calculator`, która będzie zawierała podstawowe operacje arytmetyczne:

- **Dodawanie** (`add`)
- **Odejmowanie** (`subtract`)
- **Mnożenie** (`multiply`)
- **Dzielenie** (`divide`)

Poniżej znajduje się implementacja klasy `Calculator`:

```java
public class Calculator {

    public int add(int a, int b) {
        return a + b;
    }

    public int subtract(int a, int b) {
        return a - b;
    }

    public int multiply(int a, int b) {
        return a * b;
    }

    public double divide(int a, int b) {
        if (b == 0) {
            throw new ArithmeticException("Nie można dzielić przez zero");
        }
        return (double) a / b;
    }
}
```

### Testowanie metod klasy `Calculator`

Poniżej omówimy każdą metodę z osobna, przedstawimy możliwe przypadki testowe i zaprezentujemy przykładowe metody testowe.

### 7.2. Metoda `add`

**Opis**: Dodaje dwie liczby całkowite.

**Możliwe przypadki testowe**:

1. Dodawanie dwóch liczb dodatnich.
2. Dodawanie liczby dodatniej i ujemnej.
3. Dodawanie dwóch liczb ujemnych.
4. Dodawanie z zerem.

#### Przykładowe metody testowe

##### Test 1: Dodawanie dwóch liczb dodatnich

```java
@Test
void shouldReturnSum_WhenAddingTwoPositiveNumbers() {
    // Given
    Calculator calculator = new Calculator();
    int a = 5;
    int b = 10;

    // When
    int result = calculator.add(a, b);

    // Then
    Assertions.assertEquals(15, result);
}
```

**Opis**: Test sprawdza, czy metoda `add` poprawnie dodaje dwie liczby dodatnie.

##### Test 2: Dodawanie liczby dodatniej i ujemnej

```java
@Test
void shouldReturnSum_WhenAddingPositiveAndNegativeNumber() {
    // Given
    Calculator calculator = new Calculator();
    int a = 5;
    int b = -3;

    // When
    int result = calculator.add(a, b);

    // Then
    Assertions.assertEquals(2, result);
}
```

**Opis**: Test weryfikuje działanie metody `add` przy dodawaniu liczby dodatniej i ujemnej.

##### Test 3: Dodawanie z zerem

```java
@Test
void shouldReturnSameNumber_WhenAddingZero() {
    // Given
    Calculator calculator = new Calculator();
    int a = 7;
    int b = 0;

    // When
    int result = calculator.add(a, b);

    // Then
    Assertions.assertEquals(7, result);
}
```

**Opis**: Test sprawdza, czy dodawanie z zerem zwraca tę samą liczbę.

### 7.3. Metoda `subtract`

**Opis**: Odejmuje drugą liczbę od pierwszej.

**Możliwe przypadki testowe**:

1. Odejmowanie dwóch liczb dodatnich.
2. Odejmowanie liczby ujemnej od dodatniej.
3. Odejmowanie z zerem.

#### Przykładowa metoda testowa

##### Test: Odejmowanie dwóch liczb

```java
@Test
void shouldReturnDifference_WhenSubtractingTwoNumbers() {
    // Given
    Calculator calculator = new Calculator();
    int a = 10;
    int b = 5;

    // When
    int result = calculator.subtract(a, b);

    // Then
    Assertions.assertEquals(5, result);
}
```

**Opis**: Test sprawdza, czy metoda `subtract` poprawnie odejmuje dwie liczby.

### 7.4. Metoda `multiply`

**Opis**: Mnoży dwie liczby całkowite.

**Możliwe przypadki testowe**:

1. Mnożenie dwóch liczb dodatnich.
2. Mnożenie liczby dodatniej przez zero.
3. Mnożenie dwóch liczb ujemnych.

#### Przykładowe metody testowe

##### Test: Mnożenie przez zero

```java
@Test
void shouldReturnZero_WhenMultiplyingByZero() {
    // Given
    Calculator calculator = new Calculator();
    int a = 5;
    int b = 0;

    // When
    int result = calculator.multiply(a, b);

    // Then
    Assertions.assertEquals(0, result);
}
```

**Opis**: Test weryfikuje, czy mnożenie przez zero zwraca zero.

##### Test: Mnożenie dwóch liczb ujemnych

```java
@Test
void shouldReturnPositive_WhenMultiplyingTwoNegativeNumbers() {
    // Given
    Calculator calculator = new Calculator();
    int a = -4;
    int b = -5;

    // When
    int result = calculator.multiply(a, b);

    // Then
    Assertions.assertEquals(20, result);
}
```

**Opis**: Test sprawdza, czy mnożenie dwóch liczb ujemnych daje wynik dodatni.

### 7.5. Metoda `divide`

**Opis**: Dzieli pierwszą liczbę przez drugą.

**Możliwe przypadki testowe**:

1. Dzielenie dwóch liczb dodatnich.
2. Dzielenie przez zero (powinien być rzucony wyjątek).
3. Dzielenie liczby ujemnej przez dodatnią.
4. Dzielenie liczby przez samą siebie.

#### Przykładowe metody testowe

##### Test 1: Dzielenie dwóch liczb dodatnich

```java
@Test
void shouldReturnQuotient_WhenDividingTwoPositiveNumbers() {
    // Given
    Calculator calculator = new Calculator();
    int a = 10;
    int b = 2;

    // When
    double result = calculator.divide(a, b);

    // Then
    Assertions.assertEquals(5.0, result);
}
```

**Opis**: Test sprawdza, czy metoda `divide` poprawnie dzieli dwie liczby dodatnie.

##### Test 2: Dzielenie przez zero

```java
@Test
void shouldThrowException_WhenDividingByZero() {
    // Given
    Calculator calculator = new Calculator();
    int a = 10;
    int b = 0;

    // When & Then
    Assertions.assertThrows(ArithmeticException.class, () -> calculator.divide(a, b));
}
```

**Opis**: Test sprawdza, czy metoda `divide` rzuca wyjątek `ArithmeticException` przy próbie dzielenia przez zero.

##### Test 3: Dzielenie liczby ujemnej przez dodatnią

```java
@Test
void shouldReturnNegativeQuotient_WhenDividingNegativeByPositive() {
    // Given
    Calculator calculator = new Calculator();
    int a = -10;
    int b = 2;

    // When
    double result = calculator.divide(a, b);

    // Then
    Assertions.assertEquals(-5.0, result);
}
```

**Opis**: Test weryfikuje, czy dzielenie liczby ujemnej przez dodatnią daje wynik ujemny.

## 8. Pełna klasa testowa `CalculatorTest`

Poniżej przedstawiamy pełną klasę testową, która zawiera wszystkie opisane wyżej testy:

```java
import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.Test;

public class CalculatorTest {

    @Test
    void shouldReturnSum_WhenAddingTwoPositiveNumbers() {
        // Given
        Calculator calculator = new Calculator();
        int a = 5;
        int b = 10;

        // When
        int result = calculator.add(a, b);

        // Then
        Assertions.assertEquals(15, result);
    }

    @Test
    void shouldReturnSum_WhenAddingPositiveAndNegativeNumber() {
        // Given
        Calculator calculator = new Calculator();
        int a = 5;
        int b = -3;

        // When
        int result = calculator.add(a, b);

        // Then
        Assertions.assertEquals(2, result);
    }

    @Test
    void shouldReturnSameNumber_WhenAddingZero() {
        // Given
        Calculator calculator = new Calculator();
        int a = 7;
        int b = 0;

        // When
        int result = calculator.add(a, b);

        // Then
        Assertions.assertEquals(7, result);
    }

    @Test
    void shouldReturnDifference_WhenSubtractingTwoNumbers() {
        // Given
        Calculator calculator = new Calculator();
        int a = 10;
        int b = 5;

        // When
        int result = calculator.subtract(a, b);

        // Then
        Assertions.assertEquals(5, result);
    }

    @Test
    void shouldReturnZero_WhenMultiplyingByZero() {
        // Given
        Calculator calculator = new Calculator();
        int a = 5;
        int b = 0;

        // When
        int result = calculator.multiply(a, b);

        // Then
        Assertions.assertEquals(0, result);
    }

    @Test
    void shouldReturnPositive_WhenMultiplyingTwoNegativeNumbers() {
        // Given
        Calculator calculator = new Calculator();
        int a = -4;
        int b = -5;

        // When
        int result = calculator.multiply(a, b);

        // Then
        Assertions.assertEquals(20, result);
    }

    @Test
    void shouldReturnQuotient_WhenDividingTwoPositiveNumbers() {
        // Given
        Calculator calculator = new Calculator();
        int a = 10;
        int b = 2;

        // When
        double result = calculator.divide(a, b);

        // Then
        Assertions.assertEquals(5.0, result);
    }

    @Test
    void shouldThrowException_WhenDividingByZero() {
        // Given
        Calculator calculator = new Calculator();
        int a = 10;
        int b = 0;

        // When & Then
        Assertions.assertThrows(ArithmeticException.class, () -> calculator.divide(a, b));
    }

    @Test
    void shouldReturnNegativeQuotient_WhenDividingNegativeByPositive() {
        // Given
        Calculator calculator = new Calculator();
        int a = -10;
        int b = 2;

        // When
        double result = calculator.divide(a, b);

        // Then
        Assertions.assertEquals(-5.0, result);
    }
}
```

## 9. Dodatkowe informacje o klasie Assertions i adnotacjach cyklu życia testów

### Klasa Assertions

Klasa `Assertions` zawiera metody statyczne służące do weryfikacji wyników w testach.

Przykładowe metody:

- `Assertions.assertEquals(expected, actual)`: Sprawdza, czy oczekiwana wartość jest równa rzeczywistej.
- `Assertions.assertNotNull(object)`: Sprawdza, czy obiekt nie jest `null`.
- `Assertions.assertTrue(condition)`: Sprawdza, czy warunek jest prawdziwy.
- `Assertions.assertFalse(condition)`: Sprawdza, czy warunek jest fałszywy.
- `Assertions.assertThrows(exceptionClass, executable)`: Sprawdza, czy wykonanie kodu rzuca oczekiwany wyjątek.

### Adnotacje cyklu życia testów

- `@BeforeEach`: Metoda oznaczona tą adnotacją jest wykonywana przed każdym testem. Używana do inicjalizacji zasobów potrzebnych w testach.

    ```java
    @BeforeEach
    void setUp() {
        // Kod inicjalizacyjny
    }
    ```

- `@AfterEach`: Metoda wykonywana po każdym teście. Służy do zwalniania zasobów.

    ```java
    @AfterEach
    void tearDown() {
        // Kod czyszczący
    }
    ```

- `@BeforeAll`: Metoda wykonywana raz przed wszystkimi testami. Musi być statyczna. Używana do kosztownych operacji inicjalizacyjnych.

    ```java
    @BeforeAll
    static void initAll() {
        // Inicjalizacja przed wszystkimi testami
    }
    ```

- `@AfterAll`: Metoda wykonywana raz po wszystkich testach. Musi być statyczna. Służy do zwalniania zasobów używanych przez wszystkie testy.

    ```java
    @AfterAll
    static void tearDownAll() {
        // Czyszczenie po wszystkich testach
    }
    ```

Przykład zastosowania w klasie testowej:

```java
import org.junit.jupiter.api.*;

public class CalculatorTest {

    private Calculator calculator;

    @BeforeAll
    static void initAll() {
        System.out.println("Inicjalizacja przed wszystkimi testami");
    }

    @BeforeEach
    void setUp() {
        calculator = new Calculator();
    }

    @Test
    void testAddition() {
        // Testy
    }

    @AfterEach
    void tearDown() {
        // Czyszczenie po teście
    }

    @AfterAll
    static void tearDownAll() {
        System.out.println("Czyszczenie po wszystkich testach");
    }
}
```
