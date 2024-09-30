# Wprowadzenie

W dzisiejszych aplikacjach opartych na języku Java, mapowanie obiektowo-relacyjne (ORM) odgrywa kluczową rolę w zarządzaniu danymi. Technologia JPA (Java Persistence API) oraz implementacje takie jak Hibernate umożliwiają programistom efektywne łączenie obiektów Java z bazami danych. W tym dokumencie skupimy się na omówieniu kluczowych adnotacji JPA, które są niezbędne do prawidłowego mapowania klas na tabele w bazie danych. Przeanalizujemy ich zastosowanie, atrybuty, wymagania, ograniczenia oraz przedstawimy praktyczne przykłady kodu. Dodatkowo, podzielimy się wskazówkami przy projektowaniu oraz zaprezentujemy przykłady praktyczne. Na koniec przygotowaliśmy zestaw pytań rekrutacyjnych wraz z odpowiedziami, które pomogą w utrwaleniu wiedzy.

# Adnotacje

## @Entity

**Opis:** Adnotacja `@Entity` służy do oznaczania klasy jako encji, czyli jednostki trwałej, która będzie mapowana na tabelę w bazie danych.

**Atrybuty:**

- `name` (opcjonalny): nazwa encji; domyślnie jest to nazwa klasy.

**Wymagania:**

- Klasa oznaczona jako `@Entity` musi mieć konstruktor bezargumentowy (może być prywatny lub publiczny).
- Musi posiadać unikalny identyfikator oznaczony adnotacją `@Id`.

**Ograniczenia:**

- Nie można oznaczyć jako `@Entity` klasy abstrakcyjnej bez strategii dziedziczenia.

**Przykład kodu:**

```java
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class Uzytkownik {
    @Id
    private Long id;
    private String imie;
    private String nazwisko;

    // Konstruktor, gettery i settery
}
```

---

## @Table

**Opis:** Adnotacja `@Table` służy do mapowania encji na konkretną tabelę w bazie danych.

**Atrybuty:**

- `name` (opcjonalny): nazwa tabeli w bazie danych; domyślnie nazwa klasy.
- `schema` (opcjonalny): schemat bazy danych.
- `catalog` (opcjonalny): katalog bazy danych.

**Wymagania:**

- Musi być użyta w klasie oznaczonej `@Entity`.

**Ograniczenia:**

- Nazwa tabeli musi być unikalna w ramach schematu/katalogu.

**Przykład kodu:**

```java
import javax.persistence.Entity;
import javax.persistence.Table;
import javax.persistence.Id;

@Entity
@Table(name = "uzytkownicy")
public class Uzytkownik {
    @Id
    private Long id;
    private String imie;
    private String nazwisko;

    // Konstruktor, gettery i settery
}
```

---

## @Id

**Opis:** Adnotacja `@Id` oznacza pole jako klucz główny encji.

**Atrybuty:** Brak.

**Wymagania:**

- Każda encja musi mieć dokładnie jedno pole oznaczone `@Id`.
- Typ pola powinien być wspierany przez dostawcę JPA.

**Ograniczenia:**

- Klucz główny nie może być `null`.

**Przykład kodu:**

```java
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class Produkt {
    @Id
    private Long id;
    private String nazwa;

    // Konstruktor, gettery i settery
}
```

---

## @GeneratedValue

**Opis:** Adnotacja `@GeneratedValue` wskazuje, że wartość klucza głównego będzie generowana automatycznie.

**Atrybuty:**

- `strategy` (opcjonalny): strategia generowania wartości (`AUTO`, `IDENTITY`, `SEQUENCE`, `TABLE`).
- `generator` (opcjonalny): nazwa generatora.

**Wymagania:**

- Musi być użyta w polu oznaczonym `@Id`.

**Ograniczenia:**

- Strategia generowania musi być wspierana przez bazę danych.

**Przykład kodu:**

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;

@Entity
public class Zamowienie {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private Date data;

    // Konstruktor, gettery i settery
}
```

---

## @Column

**Opis:** Adnotacja `@Column` służy do mapowania pola klasy na kolumnę w tabeli bazy danych.

**Atrybuty:**

- `name` (opcjonalny): nazwa kolumny; domyślnie nazwa pola.
- `nullable` (opcjonalny): czy kolumna może przyjmować wartość `null`.
- `length` (opcjonalny): długość kolumny dla typów znakowych.
- `unique` (opcjonalny): czy wartość w kolumnie musi być unikalna.

**Wymagania:** Brak.

**Ograniczenia:** Typ pola musi być zgodny z typem kolumny w bazie danych.

**Przykład kodu:**

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.Column;

@Entity
public class Klient {
    @Id
    private Long id;

    @Column(name = "email_klienta", nullable = false, unique = true)
    private String email;

    // Konstruktor, gettery i settery
}
```

---

## @Transient

**Opis:** Adnotacja `@Transient` wskazuje, że pole nie będzie mapowane na kolumnę w bazie danych.

**Atrybuty:** Brak.

**Wymagania:** Brak.

**Ograniczenia:** Pola oznaczone `@Transient` nie są utrwalane w bazie danych.

**Przykład kodu:**

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.Transient;

@Entity
public class Sesja {
    @Id
    private Long id;

    @Transient
    private String tymczasowyToken;

    // Konstruktor, gettery i settery
}
```

---

## @Version

**Opis:** Adnotacja `@Version` służy do zarządzania wersjonowaniem encji, co umożliwia kontrolę współbieżności optymistycznej.

**Atrybuty:** Brak.

**Wymagania:**

- Pole oznaczone `@Version` powinno być typu `int`, `Integer`, `long`, `Long`, `short`, `Short`, `Timestamp`.

**Ograniczenia:** Tylko jedno pole w encji może być oznaczone `@Version`.

**Przykład kodu:**

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.Version;

@Entity
public class Dokument {
    @Id
    private Long id;

    @Version
    private int wersja;

    private String tresc;

    // Konstruktor, gettery i settery
}
```

# Wskazówki przy projektowaniu

- **Starannie planuj strukturę encji:** Przemyśl relacje między encjami oraz ich mapowanie na tabele, aby uniknąć problemów z integralnością danych.
- **Używaj odpowiednich typów danych:** Dopasuj typy pól w encji do typów kolumn w bazie danych, aby zapewnić spójność.
- **Kontroluj dostęp do pól:** Stosuj enkapsulację, korzystając z prywatnych pól i publicznych getterów oraz setterów.
- **Wykorzystuj wersjonowanie:** Implementuj `@Version` w encjach, które mogą być modyfikowane równocześnie przez wielu użytkowników.
- **Optymalizuj zapytania:** Używaj lazy loading i fetch joinów tam, gdzie to konieczne, aby poprawić wydajność aplikacji.

# Przykłady praktyczne

**Przykład 1: Prosta encja z automatycznym generowaniem klucza głównego**

```java
@Entity
public class Kategoria {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;
    private String nazwa;

    // Konstruktor, gettery i settery
}
```

**Przykład 2: Encja z niestandardowym mapowaniem kolumn**

```java
@Entity
@Table(name = "produkty")
public class Produkt {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "nazwa_produktu", nullable = false)
    private String nazwa;

    @Column(precision = 10, scale = 2)
    private BigDecimal cena;

    // Konstruktor, gettery i settery
}
```

**Przykład 3: Encja z polem transient**

```java
@Entity
public class Raport {
    @Id
    private Long id;
    private String tytul;

    @Transient
    private String podsumowanie;

    // Konstruktor, gettery i settery
}
```

# Pytania rekrutacyjne

## Podstawowe

1. **Co to jest adnotacja `@Entity` i do czego służy?**

   **Odpowiedź:** Adnotacja `@Entity` oznacza klasę jako encję JPA, czyli mapuje ją na tabelę w bazie danych. Pozwala to na zarządzanie danymi przy użyciu obiektów Java.

2. **Jak oznaczyć pole jako klucz główny w encji?**

   **Odpowiedź:** Pole oznacza się jako klucz główny, używając adnotacji `@Id`.

3. **Do czego służy adnotacja `@GeneratedValue`?**

   **Odpowiedź:** Adnotacja `@GeneratedValue` wskazuje, że wartość klucza głównego będzie generowana automatycznie według określonej strategii.

4. **Kiedy używamy adnotacji `@Transient`?**

   **Odpowiedź:** Adnotacja `@Transient` jest używana, gdy chcemy, aby pole w klasie nie było mapowane na kolumnę w bazie danych.

5. **Jakie są podstawowe atrybuty adnotacji `@Column`?**

   **Odpowiedź:** Podstawowe atrybuty to `name`, `nullable`, `length`, `unique`, które pozwalają na dostosowanie mapowania pola na kolumnę.

## Zaawansowane

1. **Jak działa mechanizm wersjonowania encji przy użyciu adnotacji `@Version`?**

   **Odpowiedź:** Adnotacja `@Version` umożliwia implementację optymistycznej kontroli współbieżności. Każda zmiana encji zwiększa wartość pola wersji, co pozwala wykryć konflikty podczas równoczesnych modyfikacji.

2. **Czym różnią się strategie generowania klucza głównego w `@GeneratedValue`?**

   **Odpowiedź:** Strategie `AUTO`, `IDENTITY`, `SEQUENCE`, `TABLE` różnią się sposobem generowania wartości:
    - `AUTO`: dostawca JPA wybiera strategię automatycznie.
    - `IDENTITY`: wykorzystuje auto-increment bazy danych.
    - `SEQUENCE`: używa sekwencji bazy danych.
    - `TABLE`: emuluje sekwencje za pomocą tabeli.

3. **Jak mapować encję na istniejącą tabelę o innej nazwie niż klasa?**

   **Odpowiedź:** Używając adnotacji `@Table` z atrybutem `name`, można wskazać nazwę tabeli w bazie danych, która różni się od nazwy klasy.

4. **Czy można mieć więcej niż jedno pole oznaczone `@Id` w encji? Jak to obsłużyć?**

   **Odpowiedź:** Tak, można mieć złożony klucz główny. W takim przypadku używa się adnotacji `@IdClass` lub `@EmbeddedId` do zdefiniowania klucza złożonego.

5. **Jakie są konsekwencje pominięcia adnotacji `@Transient` przy polu, które nie powinno być mapowane?**

   **Odpowiedź:** Jeśli nie oznaczymy pola jako `@Transient`, dostawca JPA spróbuje je zmapować na kolumnę w bazie danych. Może to prowadzić do błędów podczas uruchamiania aplikacji, jeśli typ pola nie jest wspierany lub kolumna nie istnieje.