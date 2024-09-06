# Hibernate ORM Annotations Documentation
[WARNING]
> W trakcie budowy

## 1. Wprowadzenie

Hibernate ORM (Object-Relational Mapping) jest frameworkiem do mapowania obiektów w Javie na tabele w relacyjnych bazach
danych. ORM ułatwia tworzenie i zarządzanie bazą danych przy użyciu obiektów Java, eliminując potrzebę pisania złożonych
zapytań SQL. Hibernate jest jednym z najpopularniejszych ORM-ów w środowisku Java i jest częścią ekosystemu JPA (Java
Persistence API).

### Główne cechy Hibernate:

- Mapowanie obiektowo-relacyjne
- Obsługa zapytań HQL (Hibernate Query Language)
- Obsługa transakcji
- Mechanizm zarządzania sesją i cachingiem
- Obsługa różnych strategii pobierania danych (fetching)

## 2. Podstawowe adnotacje

### 2.1 `@Entity`

Adnotacja `@Entity` jest używana do oznaczenia klasy Java jako encji, która jest mapowana na tabelę w bazie danych.

- **Atrybuty:**
    - `name` (String): Nazwa encji, domyślnie jest to nazwa klasy.

- **Przykład:**
  ```java
  @Entity
  public class User {
    @Id
    private Long id;
    private String name;
  }
  ```

### 2.2 `@Table`

Adnotacja `@Table` jest używana do określenia szczegółowych informacji o tabeli, do której ma być mapowana encja.

- **Atrybuty:**
    - `name` (String): Nazwa tabeli.
    - `schema` (String): Schemat, do którego należy tabela.
    - `catalog` (String): Katalog, do którego należy tabela.
    - `uniqueConstraints` (UniqueConstraint[]): Tablica ograniczeń unikalności dla tabeli.
    - `indexes` (Index[]): Tablica indeksów dla tabeli.

- **Przykład:**
  ```java
  @Entity
  @Table(name = "users", schema = "public")
  public class User {
    @Id
    private Long id;
    private String name;
  }
  ```

### 2.3 `@Id`

Adnotacja `@Id` jest używana do oznaczenia pola lub właściwości jako klucza głównego encji.

- **Atrybuty:** Brak atrybutów.

- **Przykład:**
  ```java
  @Entity
  public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
  }
  ```

### 2.4 `@GeneratedValue`

Adnotacja `@GeneratedValue` jest używana do określenia strategii generowania wartości dla klucza głównego.

- **Atrybuty:**
    - `strategy` (GenerationType): Strategia generowania wartości klucza. Możliwe wartości to:
        - `AUTO`: Strategia domyślna, dostosowana do konkretnej bazy danych.
        - `IDENTITY`: Wartość jest generowana przez kolumnę tożsamości w bazie danych.
        - `SEQUENCE`: Wartość jest generowana przez sekwencję w bazie danych.
        - `TABLE`: Wartość jest generowana przy użyciu specjalnej tabeli w bazie danych.
    - `generator` (String): Nazwa generatora używanego do generowania wartości.

- **Przykład:**
  ```java
  @Entity
  public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "user_seq")
    private Long id;
    private String name;
  }
  ```

## 3. Relacje między encjami

Adnotacje relacji w Hibernate są używane do definiowania powiązań między encjami. Każda relacja ma swoje specyficzne
atrybuty, takie jak `cascade`, `fetch` i `orphanRemoval`.

### Wartości dla `cascade`:

`cascade` (CascadeType[]) określa operacje kaskadowe, które mają być stosowane do powiązanych encji. Możliwe wartości
to:

- `ALL`: Wszystkie operacje (persist, merge, remove, refresh, detach) będą kaskadowane.
- `PERSIST`: Operacja `persist` (zapisanie nowej encji) będzie kaskadowana.
- `MERGE`: Operacja `merge` (aktualizacja encji) będzie kaskadowana.
- `REMOVE`: Operacja `remove` (usunięcie encji) będzie kaskadowana.
- `REFRESH`: Operacja `refresh` (odświeżenie encji z bazy danych) będzie kaskadowana.
- `DETACH`: Operacja `detach` (oddzielenie encji od kontekstu trwałości) będzie kaskadowana.

### Wartości dla `fetch`:

`fetch` (FetchType) określa strategię pobierania danych. Możliwe wartości to:

- `EAGER`: Dane są pobierane natychmiastowo, podczas ładowania encji.
- `LAZY`: Dane są pobierane tylko wtedy, gdy są faktycznie potrzebne.

### Atrybut `orphanRemoval`:

`orphanRemoval` (boolean) określa, czy powiązane encje, które nie są już powiązane z encją nadrzędną (sieroty), mają być
automatycznie usuwane. Domyślnie jest ustawione na `false`.

### 3.1 `@OneToOne`

Adnotacja `@OneToOne` jest używana do mapowania relacji jeden do jednego między dwoma encjami.

- **Atrybuty:**
    - `mappedBy` (String): Określa pole w drugiej encji, które jest właścicielem relacji.
    - `cascade` (CascadeType[]): Typ kaskady operacji.
    - `fetch` (FetchType): Strategia pobierania danych (EAGER, LAZY).
    - `optional` (boolean): Określa, czy wartość jest opcjonalna (domyślnie `true`).
    - `orphanRemoval` (boolean): Określa, czy sieroty mają być usuwane (domyślnie `false`).

- **Przykład:**
  ```java
  @Entity
  public class Person {
    @Id
    private Long id;

    @OneToOne(cascade = CascadeType.ALL, orphanRemoval = true)
    private Passport passport;
  }
  ```

### 3.2 `@OneToMany`

Adnotacja `@OneToMany` jest używana do mapowania relacji jeden do wielu między encją a listą powiązanych encji.

- **Atrybuty:**
    - `mappedBy` (String): Określa pole w drugiej encji, które jest właścicielem relacji.
    - `cascade` (CascadeType[]): Typ kaskady operacji.
    - `fetch` (FetchType): Strategia pobierania danych (EAGER, LAZY).
    - `orphanRemoval` (boolean): Określa, czy sieroty mają być usuwane (domyślnie `false`).

- **Przykład:**
  ```java
  @Entity
  public class Parent {
    @Id
    private Long id;

    @OneToMany(mappedBy = "parent", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Child> children;
  }
  ```

### 3.3 `@ManyToOne`

Adnotacja `@ManyToOne` jest używana do mapowania relacji wiele do jednego między encją a inną encją.

- **Atrybuty:**
    - `cascade` (CascadeType[]): Typ kaskady operacji.
    - `fetch` (FetchType): Strategia pobierania danych (EAGER, LAZY).
    - `optional` (boolean): Określa, czy wartość jest opcjonalna (domyślnie `true`).

- **Przykład:**
  ```java
  @Entity
  public class Child {
    @Id
    private Long id;

    @ManyToOne
    private Parent parent;
  }
  ```

### 3.4 `@ManyToMany`

Adnotacja `@ManyToMany` jest używana do mapowania relacji wiele do wielu między dwoma encjami.

- **Atrybuty:**
    - `mappedBy` (String): Określa pole w drugiej encji, które jest właścicielem relacji.
    - `cascade` (CascadeType[]): Typ kaskady operacji.
    - `fetch` (FetchType): Strategia pobierania danych (EAGER, LAZY).

- **Przykład:**
  ```java
  @Entity
  public class Student {
    @Id
    private Long id;

    @ManyToMany(mappedBy = "students", cascade = CascadeType.PERSIST)
    private List<Course> courses;
  }
  ```

## 4. Adnotacje dla mapowania dziedziczenia

### 4.1 `@Inheritance`

Adnotacja `@Inheritance` jest używana do określenia strategii dziedziczenia między klasami encji.

- **Atrybuty:**
    - `strategy` (InheritanceType): Typ strategii dziedziczenia. Możliwe wartości to:
        - `SINGLE_TABLE`: Wszystkie klasy dziedziczące są mapowane do jednej tabeli.
        - `TABLE_PER_CLASS`: Każda klasa dziedzicząca jest mapowana do oddzielnej tabeli.
        - `JOINED`: Każda klasa dziedzicząca jest mapowana do własnej tabeli, a relacje są zarządzane przez klucze obce.

- **Przykład:**
  ```java
  @Entity
  @Inheritance(strategy = InheritanceType.JOINED)
  public class Vehicle {
    @Id
    private Long id;
  }
  ```

### 4.2 `@DiscriminatorColumn`

Adnotacja `@DiscriminatorColumn` jest używana w strategii `SINGLE_TABLE` do rozróżniania między typami dziedziczącymi.

- **Atrybuty:**
    - `name` (String): Nazwa kolumny dyskryminatora.
    - `discriminatorType` (DiscriminatorType): Typ danych kolumny dyskryminatora (STRING, CHAR, INTEGER).
    - `length` (int): Długość kolumny dyskryminatora (tylko dla typu `STRING`).

- **Przykład:**
  ```java
  @Entity
  @Inheritance(strategy = InheritanceType.SINGLE_TABLE)
  @DiscriminatorColumn(name = "vehicle_type", discriminatorType = DiscriminatorType.STRING)
  public class Vehicle {
    @Id
    private Long id;
  }
  ```

### 4.3 `@DiscriminatorValue`

Adnotacja `@DiscriminatorValue` jest używana do określenia wartości kolumny dyskryminatora dla klasy dziedziczącej.

- **Atrybuty:**
    - `value` (String): Wartość, która będzie używana jako dyskryminator.

- **Przykład:**
  ```java
  @Entity
  @DiscriminatorValue("CAR")
  public class Car extends Vehicle {
    private int numberOfDoors;
  }
  ```

### 4.4 `@MappedSuperclass`

Adnotacja `@MappedSuperclass` jest używana do oznaczania klasy jako klasy bazowej, której pola są dziedziczone, ale sama
klasa nie jest encją.

- **Atrybuty:** Brak atrybutów.

- **Przykład:**
  ```java
  @MappedSuperclass
  public abstract class BaseEntity {
    @Id
    @GeneratedValue
    private Long id;
  }
  ```

### 4.5 `@Embeddable` i `@Embedded`

Umożliwiają osadzanie jednej klasy w innej encji. @Embeddable oznacza klasę, która może być osadzona, a @Embedded
oznacza pole, które będzie osadzać klasę oznaczoną jako @Embeddable. Te adnotacje różnią się od @OneToOne, ponieważ nie
tworzą osobnej tabeli ani klucza obcego. Cała struktura jest zapisywana w tej samej tabeli, co encja nadrzędna.

- **Atrybuty dla `@Embeddable`:** Brak atrybutów.
- **Atrybuty dla `@Embedded`:** Brak atrybutów.

**Przykład:**

  ```java

@Embeddable
public class Address {
    private String street;
    private String city;
}

@Entity
public class User {
    @Id
    private Long id;
    @Embedded
    private Address address;
}
```

## 5. Adnotacje do mapowania kluczy głównych i obcych

### 5.1 `@IdClass`

Adnotacja `@IdClass` jest używana do mapowania klucza głównego złożonego z więcej niż jednego pola (wielopolowego klucza
głównego). Jest używana na poziomie klasy encji i wskazuje klasę, która definiuje ten klucz.

- **Atrybuty:**
    - `value` (Class): Klasa reprezentująca złożony klucz główny.

- **Przykład:**
  ```java
  @Entity
  @IdClass(OrderId.class)
  public class Order {
    @Id
    private Long orderId;
    @Id
    private Long productId;
    private int quantity;
  }

  public class OrderId implements Serializable {
    private Long orderId;
    private Long productId;

    // Konstruktor, gettery, settery, hashCode, equals
  }
  ```

### 5.2 `@EmbeddedId`

Adnotacja `@EmbeddedId` jest używana do zdefiniowania złożonego klucza głównego, który jest wbudowany w encję jako
obiekt zdefiniowany przez klasę.

- **Atrybuty:** Brak atrybutów.

- **Przykład:**
  ```java
  @Entity
  public class Order {
    @EmbeddedId
    private OrderId orderId;
    private int quantity;
  }

  @Embeddable
  public class OrderId implements Serializable {
    private Long orderId;
    private Long productId;
  
    // Konstruktor, gettery, settery, hashCode, equals
  }
  ```

### 5.3 `@PrimaryKeyJoinColumn`

Adnotacja `@PrimaryKeyJoinColumn` jest używana do określenia kolumny klucza głównego, która jest używana do połączenia
tabel w przypadku dziedziczenia typu `JOINED`.

- **Atrybuty:**
    - `name` (String): Nazwa kolumny klucza głównego w tabeli potomnej.
    - `referencedColumnName` (String): Nazwa kolumny klucza głównego w tabeli nadrzędnej.

- **Przykład:**
  ```java
  @Entity
  @Inheritance(strategy = InheritanceType.JOINED)
  public class Vehicle {
    @Id
    private Long id;
  }

  @Entity
  @PrimaryKeyJoinColumn(name = "car_id", referencedColumnName = "id")
  public class Car extends Vehicle {
    private int numberOfDoors;
  }
  ```

### 5.4 `@JoinColumn`

Adnotacja `@JoinColumn` jest używana do określenia kolumny klucza obcego w relacji.

- **Atrybuty:**
    - `name` (String): Nazwa kolumny klucza obcego.
    - `referencedColumnName` (String): Nazwa kolumny w tabeli, do której ma się odnosić klucz obcy.
    - `nullable` (boolean): Określa, czy kolumna może być `NULL`.
    - `unique` (boolean): Określa, czy kolumna musi być unikalna.

- **Przykład:**
  ```java
  @Entity
  public class Employee {
    @Id
    private Long id;
    
    @ManyToOne
    @JoinColumn(name = "department_id", referencedColumnName = "id")
    private Department department;
  }
  ```

### 5.5 `@JoinTable`

Adnotacja `@JoinTable` jest używana do określenia tabeli pośredniej dla relacji wiele do wielu lub jeden do wielu, gdy
potrzeba dodatkowej kontroli nad kolumnami pośrednimi.

- **Atrybuty:**
    - `name` (String): Nazwa tabeli pośredniej.
    - `joinColumns` (JoinColumn[]): Kolumny, które odnosi się do klucza głównego encji właściciela.
    - `inverseJoinColumns` (JoinColumn[]): Kolumny, które odnosi się do klucza głównego drugiej encji.

- **Przykład:**
  ```java
  @Entity
  public class Student {
    @Id
    private Long id;
    
    @ManyToMany
    @JoinTable(
    name = "student_course",
    joinColumns = @JoinColumn(name = "student_id"),
    inverseJoinColumns = @JoinColumn(name = "course_id"))
    private List<Course> courses;
  }
  ```

## 6. Adnotacje związane z strategią pobierania danych

### 6.1 `@Fetch`

Adnotacja `@Fetch` jest specyficzną adnotacją Hibernate, która umożliwia określenie strategii pobierania dla kolekcji
lub złożonego pola w sposób bardziej precyzyjny niż `FetchType`.

- **Atrybuty:**
    - `value` (FetchMode): Określa strategię pobierania. Możliwe wartości to:
        - `SELECT`: Używa oddzielnych zapytań SELECT do pobierania kolekcji.
        - `JOIN`: Używa zapytania JOIN do pobrania kolekcji.
        - `SUBSELECT`: Używa zapytania podzapytań (subselect) do pobrania kolekcji.

- **Przykład:**
  ```java
  @Entity
  public class Department {
    @Id
    private Long id;
    
    @OneToMany(mappedBy = "department", fetch = FetchType.LAZY)
    @Fetch(FetchMode.SUBSELECT)
    private List<Employee> employees;
  }
  ```

### 6.2 `@BatchSize`

Adnotacja `@BatchSize` jest specyficzną adnotacją Hibernate, która określa rozmiar wsadowy do ładowania powiązanych
encji lub kolekcji.

- **Atrybuty:**
    - `size` (int): Rozmiar wsadu określający liczbę obiektów, które mają być ładowane w jednej operacji.

- **Przykład:**
  ```java
  @Entity
  public class Product {
    @Id
    private Long id;
    
    @ManyToMany(mappedBy = "products")
    @BatchSize(size = 10)
    private List<Category> categories;
  }
  ```

### 6.3 `@FetchProfile`

Adnotacja `@FetchProfile` jest specyficzną adnotacją Hibernate, która pozwala na określenie grup pobierania i strategii
dla złożonych zapytań.

- **Atrybuty:**
    - `name` (String): Nazwa profilu pobierania.
    - `fetchOverrides` (FetchProfile.FetchOverride[]): Tablica nadpisanych strategii pobierania.

- **Przykład:**
  ```java
  @Entity
  @FetchProfile(name = "employeeWithDepartment", fetchOverrides = {
  @FetchProfile.FetchOverride(entity = Employee.class, association = "department", mode = FetchMode.JOIN)
  })
  public class Employee {
    @Id
    private Long id;
    
    @ManyToOne
    @JoinColumn(name = "department_id")
  private Department department;
  }
  ```

## 7. Adnotacje związane z typami danych i konwersjami

### 7.1 `@Lob`

Adnotacja `@Lob` jest używana do oznaczenia pola, które powinno być mapowane na kolumnę typu Large Object w bazie
danych (np. BLOB lub CLOB).

- **Atrybuty:** Brak atrybutów.

- **Przykład:**
  ```java
  @Entity
  public class Document {
    @Id
    private Long id;
    
    @Lob
    private byte[] data;
  }
  ```

### 7.2 `@Temporal`

Adnotacja `@Temporal` jest używana do określenia typu danych czasowych, takich jak `Date` lub `Calendar`.

- **Atrybuty:**
    - `value` (TemporalType): Typ danych czasowych. Możliwe wartości to:
        - `DATE`: Tylko data.
        - `TIME`: Tylko czas.
        - `TIMESTAMP`: Data i czas.

- **Przykład:**
  ```java
  @Entity
  public class Event {
    @Id
    private Long id;
    
    @Temporal(TemporalType.TIMESTAMP)
    private Date eventDate;
  }
  ```

### 7.3 `@Enumerated`

Adnotacja `@Enumerated` jest używana do określenia, w jaki sposób wartości enum mają być zapisywane w bazie danych (jako
liczby lub ciągi znaków).

- **Atrybuty:**
    - `value` (EnumType): Typ danych dla wartości enum. Możliwe wartości to:
        - `ORDINAL`: Wartości enum są zapisywane jako ich indeksy (liczby całkowite).
        - `STRING`: Wartości enum są zapisywane jako ciągi znaków.

- **Przykład:**
  ```java
  @Entity
  public class Task {
    @Id
    private Long id;
    
    @Enumerated(EnumType.STRING)
    private Status status;
  }

  public enum Status {
    OPEN, IN_PROGRESS, DONE
  }
  ```
