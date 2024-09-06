# Programowanie obiektowe (OOP) w Javie

## 1. Wprowadzenie do Programowania Obiektowego (OOP)

Programowanie obiektowe (OOP) jest paradygmatem programowania, który polega na modelowaniu rzeczywistości za pomocą
obiektów. Obiekty są instancjami klas, które zawierają zarówno dane (atrybuty), jak i zachowanie (metody). W Javie
programowanie obiektowe jest fundamentalnym podejściem do pisania kodu, co pozwala na łatwiejsze utrzymanie i rozwój
aplikacji.

### Zalety stosowania OOP:

- Modułowość: Kod jest podzielony na klasy, które mogą być wielokrotnie używane.
- Łatwość utrzymania: Zmiany w kodzie mogą być wprowadzane lokalnie w klasie bez wpływu na cały system.
- Możliwość dziedziczenia: Ponowne użycie kodu w klasach pochodnych.
- Polimorfizm: Możliwość użycia tych samych metod w różnych klasach.

---

## 2. Klasy i Obiekty

Klasa jest szablonem dla obiektów, a obiekt jest instancją klasy. W Javie używamy słowa kluczowego `class` do
definiowania klasy, a obiekty tworzymy za pomocą słowa kluczowego `new`.

### Przykład z życia: pojęcie samochodu

#### 1. Klasa
Wyobraź sobie **klasę** jako szablon lub plan dla czegoś. Na przykład, klasa `Car` (samochód) może reprezentować ogólny koncept samochodu, opisujący jego właściwości i zachowanie, takie jak `brand` (marka), `model`, `year` (rok), oraz metody takie jak `drive()` (jechać) czy `stop()` (zatrzymać). Klasa jest zatem abstrakcyjną definicją, która nie istnieje fizycznie, a jedynie opisuje cechy i działania.

#### 2. Obiekt
**Obiekt** to konkretny egzemplarz klasy. Kiedy budujemy samochód na podstawie planów (czyli klasy `Car`), tworzymy obiekt. Na przykład, obiektem może być konkretny samochód marki **Toyota** model **Corolla** z roku **2020**. Obiekt jest "rzeczywistym" reprezentantem klasy i posiada wartości przypisane do atrybutów klasy.

#### 3. Instancja
**Instancja** jest terminem często używanym zamiennie z obiektem, ale bardziej technicznie odnosi się do **konkretnego przypadku** obiektu klasy. Kiedy tworzymy obiekt `myCar` na podstawie klasy `Car`, `myCar` jest **instancją** klasy `Car`. Możemy mieć wiele instancji tej samej klasy – na przykład `car1`, `car2`, `car3` mogą być różnymi instancjami klasy `Car`, gdzie każdy obiekt ma swoje unikalne wartości atrybutów (np. różne marki, modele, lata produkcji).

### Podsumowanie

- **Klasa** to plan (np. plan samochodu).
- **Obiekt** to konkretny przykład czegoś, co zostało zbudowane na podstawie planu (np. Toyota Corolla 2020).
- **Instancja** to techniczny termin na konkretny obiekt klasy (np. `myCar` to instancja klasy `Car`).

### Przykład:

```java
public class Car {
    String brand;
    String model;
    int year;

    public static void main(String[] args) {
        Car audi = new Car();
        car.brand = "audi";
        car.model = "a5";
        car.year = 2012;
       System.out.println("Car(" + audi.brand + ", " + audi.model + ", " + audi.year + " )");
       System.out.printf("Car(%s, %s, %d)%n", audi.brand, audi.model, audi.year);
    }
}
```
> [!NOTE]
> **`System.out.printf()`** - metoda w Javie do formatowanego wypisywania tekstu na konsolę, podobna do `String.format()`, ale bezpośrednio wypisuje wynik. Używa specyfikatorów formatu, np. `%s` (String), `%d` (int), aby dynamicznie tworzyć sformatowany tekst.

#### Zadania:

1. Napisz klasę `Car` z atrybutami: `brand`, `model` i `year`. Utwórz 2 obiekty tej klasy i nadpisz jego atrybuty. Za
   pomocą wykonań `sout` wyświetl ich atrybuty.
2. Stwórz klasę `Student` z atrybutami `name`, `age`, `major`. Utwórz 2 obiekty tej klasy i nadpisz jego atrybuty. Za
   pomocą wykonań `sout` wyświetl ich atrybuty.

---

## 3. Atrybuty i Metody

Atrybuty to zmienne instancji, które przechowują dane dotyczące obiektu. Metody są funkcjami definiowanymi w klasach,
które określają zachowanie obiektu.

### Przykład:

```java
public class BankAccount {
    String accountNumber;
    double balance;

    public void deposit(double amount) {
        balance += amount;
    }

    public void withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
        } else {
            System.out.println("Insufficient funds.");
        }
    }

    public void showBalance() {
        System.out.println("Current balance: " + balance);
    }
}
```

#### Zadania:

1. Napisz klasę `BankAccount` z atrybutami `accountNumber`, `balance` oraz metodami `deposit()` i `withdraw()`. Dodaj
   metodę `showBalance()`, która zwróci bieżące saldo. Utwórz obiekt tej klasy i wykonaj kilka operacji.
2. Stwórz klasę `Rectangle` z atrybutami `length` i `width` oraz metodą `calculateArea()`, która zwraca pole prostokąta.
   Dodaj metodę `calculatePerimeter` do obliczenia obwodu prostokąta i przetestuj oba obliczenia.

## 4. Konstruktory

Konstruktory to specjalne metody, które są wywoływane podczas tworzenia obiektu. Używane są do inicjalizacji obiektów.
Konstruktor może przyjmować parametry, co pozwala na różne sposoby inicjalizacji obiektu. Można również przeciążać
konstruktory, definiując wiele konstruktorów o różnych zestawach parametrów.

### Przykład:

```java
public class Person {
    String name;
    int age;
    String address;

    // Konstruktor z dwoma parametrami
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Konstruktor z trzema parametrami
    public Person(String name, int age, String address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }
}
```

#### Zadania:

1. Napisz klasę `Person` z dwoma konstruktorami: jednym przyjmującym tylko `name` i `age`, a drugim przyjmującym
   wszystkie dane: `name`, `age`, `address`. Utwórz kilka obiektów, korzystając z obu konstruktorów.
2. Stwórz klasę `Circle` z atrybutem `radius` i konstruktorem inicjalizującym ten atrybut. Dodaj metodę
   `calculateArea()` (pi * r^2) do obliczenia pola koła, a także metodę `calculateCircumference()` (2 * pi * r) do
   obliczenia obwodu. Przetestuj obie metody.

---

## 5. Kapsułkowanie (Encapsulation) oraz modyfikatory dostępu

Kapsułkowanie to jeden z filarów OOP. Polega na ukrywaniu szczegółów implementacji obiektu i udostępnianiu tylko
niezbędnych interfejsów. W Javie kapsułkowanie osiąga się za pomocą modyfikatorów dostępu (`private`, `public`,
`protected`) oraz metod `getter` i `setter`.

| Modyfikator Dostępu          | Poziom Dostępu                                                                          | Dostęp w tej samej klasie | Dostęp w pakiecie | Dostęp w podklasie (poza pakietem) | Dostęp globalny (poza pakietem) |
|------------------------------|-----------------------------------------------------------------------------------------|---------------------------|-------------------|------------------------------------|---------------------------------|
| `private`                    | Dostęp tylko wewnątrz tej samej klasy                                                   | ✔                         | ✘                 | ✘                                  | ✘                               |
| `default` (bez modyfikatora) | Dostęp w ramach pakietu, brak dostępu poza pakietem                                     | ✔                         | ✔                 | ✘                                  | ✘                               |
| `protected`                  | Dostęp w ramach pakietu oraz w podklasach (nawet jeśli znajdują się w innych pakietach) | ✔                         | ✔                 | ✔                                  | ✘                               |
| `public`                     | Pełen dostęp, wszędzie (zarówno w tym samym pakiecie, jak i poza nim)                   | ✔                         | ✔                 | ✔                                  | ✔                               |

### Przykład:

```java
public class Employee {
    private String name;
    private String position;
    private double salary;

    // Getter for name
    public String getName() {
        return name;
    }

    // Setter for name
    public void setName(String name) {
        this.name = name;
    }

    // Podobne metody getter i setter dla innych atrybutów...
}
```

#### Zadania:

1. Napisz klasę `Employee` z atrybutami `name`, `position`, `salary`. Zastosuj modyfikator `private` do wszystkich
   atrybutów i stwórz odpowiednie `getter` i `setter` metody. Utwórz obiekt tej klasy i przetestuj dostęp do atrybutów
   za pomocą getterów i setterów.
2. Stwórz klasę `Book` z atrybutami `title`, `author`, `price`. Zastosuj kapsułkowanie, a następnie utwórz metodę
   `displayDetails()`, która wyświetli informacje o książce. Przetestuj tę metodę na kilku obiektach.

## 6. Dziedziczenie (Inheritance)

Dziedziczenie to mechanizm, który pozwala jednej klasie (klasie pochodnej) na dziedziczenie atrybutów i metod innej
klasy (klasy bazowej). Dzięki dziedziczeniu możemy tworzyć nowe klasy na podstawie istniejących, co ułatwia ponowne
wykorzystanie kodu i zachęca do organizowania kodu w hierarchiczne struktury.

### Przykład:

```java
// Klasa bazowa
public class Animal {
    public void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

// Klasa pochodna
public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Dog barks");
    }
}
```

#### Zadania:

1. Napisz klasę `Animal` z metodami `makeSound()` i `sleep()`. Następnie utwórz klasy `Dog` i `Cat`, które dziedziczą po
   `Animal`. Każda z tych klas powinna nadpisać metodę `makeSound()`. Utwórz obiekty tych klas i przetestuj ich metody.
2. Stwórz klasę `Vehicle` z atrybutami `brand` i `speed`. Dodaj klasy `Car` i `Bike`, które dziedziczą po `Vehicle`.
   Każda z tych klas powinna mieć dodatkowy atrybut specyficzny dla danego typu pojazdu (np. `numberOfDoors`,
   `hasCarrier`). Utwórz obiekty tych klas i przetestuj ich działanie.

---

## 7. Polimorfizm (Polymorphism)

Polimorfizm to zdolność do przyjmowania wielu form. W kontekście programowania obiektowego oznacza to możliwość
wywołania tej samej metody na różnych obiektach i uzyskania różnych zachowań, zależnie od klasy obiektu. W Javie
polimorfizm osiąga się głównie poprzez przesłanianie metod (override).

### Przykład:

```java
public class Shape {
    public void draw() {
        System.out.println("Drawing a shape");
    }
}

public class Circle extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}

public class Rectangle extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle");
    }
}
```

#### Zadania:

1. Stwórz hierarchię klas `Shape`, `Circle`, `Rectangle`, gdzie `Shape` jest klasą bazową z metodą `draw()`, a `Circle`
   i `Rectangle` nadpisują tę metodę. Napisz metodę, która przyjmuje listę obiektów typu `Shape` i wywołuje dla nich
   metodę `draw()`.
2. Napisz program, w którym klasa `Employee` ma metodę `calculateSalary()`, a klasy `Manager` i `Developer` dziedziczą
   po `Employee` i nadpisują tę metodę. Przetestuj polimorfizm, tworząc obiekty obu klas i wywołując metodę
   `calculateSalary()`.

