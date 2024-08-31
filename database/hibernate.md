
# Hibernate - Przewodnik po Podstawowych i Zaawansowanych Konceptach

## 1. Hibernate - Wprowadzenie

Hibernate to popularna biblioteka ORM (Object-Relational Mapping) dla Javy, która pozwala na mapowanie obiektów Javy na tabele w bazie danych. Jest zbudowana na bazie JDBC i JPA (Java Persistence API), co umożliwia łatwe i efektywne zarządzanie danymi w aplikacjach Java. 

Spring Data JPA korzysta z Hibernate jako domyślnej implementacji JPA, co pozwala na integrację Hibernate w aplikacjach Spring Boot bez dodatkowej konfiguracji.

## 2. Konfiguracja Hibernate w application.properties

Konfiguracja Hibernate i bazy danych w aplikacjach Spring Boot odbywa się za pomocą pliku `application.properties`. Oto najważniejsze ustawienia:

```properties
# Konfiguracja połączenia z bazą danych
spring.datasource.url=jdbc:postgresql://localhost:5432/mydb
spring.datasource.username=
spring.datasource.password=
spring.datasource.driver-class-name=

# Dialekt Hibernate
spring.jpa.database-platform=org.hibernate.dialect.

# Właściwości JPA i Hibernate
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

## 3. JPQL oraz JPA Criteria API

JPQL (Java Persistence Query Language) to zapytania oparte na obiektach, które pozwalają na wykonywanie operacji na encjach w sposób zbliżony do SQL, ale z użyciem nazw klas i pól zamiast tabel i kolumn. 

Przykład prostego zapytania JPQL:

```java
TypedQuery<User> query = entityManager.createQuery("SELECT u FROM User u WHERE u.email = :email", User.class);
query.setParameter("email", "example@example.com");
List<User> users = query.getResultList();
```

JPA Criteria API to typowo-bezpieczne zapytania, które są tworzone programowo, co pozwala na dynamiczne budowanie zapytań. 

Przykład zapytania za pomocą JPA Criteria API:

```java
CriteriaBuilder cb = entityManager.getCriteriaBuilder();
CriteriaQuery<User> cq = cb.createQuery(User.class);
Root<User> root = cq.from(User.class);
cq.select(root).where(cb.equal(root.get("email"), "example@example.com"));
TypedQuery<User> query = entityManager.createQuery(cq);
List<User> users = query.getResultList();
```

## 4. Sesja

### Sesja w Hibernate

Sesja (Session) w Hibernate to główny interfejs do pracy z bazą danych. Jest to połączenie między aplikacją a bazą danych, które zarządza trwałością (persistence) obiektów. Sesja jest odpowiedzialna za wykonywanie operacji CRUD (Create, Read, Update, Delete) oraz za zarządzanie cyklem życia obiektów.

- Sesja jest lekkim obiektem, który działa jako fabryka dla transakcji.
- Jest bezstanowa, co oznacza, że nie zachowuje informacji między wywołaniami metod.

## 5. Cache w Hibernate

Hibernate implementuje dwa poziomy cache:

- **Cache pierwszego poziomu (L1)**: Jest to cache specyficzny dla sesji, dostępny dla wszystkich operacji w tej samej sesji. Jest automatycznie zarządzany przez Hibernate.
  
- **Cache drugiego poziomu (L2)**: Jest współdzielony między sesjami i jest używany do przechowywania encji, kolekcji, oraz zapytań. Cache drugiego poziomu jest opcjonalny i musi być skonfigurowany dodatkowo.

Domyślnie, Hibernate używa cache pierwszego poziomu (L1). Cache drugiego poziomu można skonfigurować za pomocą dostawcy cache, np. EHCache.

### Jak cache jest używany przez Hibernate?

- **Cache pierwszego poziomu**: Każda sesja Hibernate utrzymuje cache pierwszego poziomu, gdzie przechowywane są obiekty, które są aktualnie zarządzane przez tę sesję.
  
- **Cache drugiego poziomu**: Może być używany przez wiele sesji do buforowania często używanych danych. Jest konfigurowalny i może przechowywać dane na różne sposoby, takie jak w pamięci, na dysku lub w rozproszonej pamięci cache.

## 6. Mechanizm Dirty Checking w Hibernate

Dirty Checking to mechanizm w Hibernate, który automatycznie wykrywa zmiany w obiektach zarządzanych przez sesję i synchronizuje je z bazą danych podczas zatwierdzania transakcji. Dzięki temu, Hibernate oszczędza na ręcznych operacjach aktualizacji.

Jak to działa:

1. Kiedy obiekt jest załadowany do sesji, Hibernate tworzy jego kopię.
2. Przed zatwierdzeniem transakcji, Hibernate porównuje oryginalny obiekt z jego aktualnym stanem.
3. Jeśli wykryte zostaną zmiany, Hibernate automatycznie generuje odpowiednie zapytanie SQL do zaktualizowania bazy danych.


## 7. Optymistyczne vs Pesymistyczne Blokowanie

### Optymistyczne Blokowanie

Optymistyczne blokowanie zakłada, że konflikty występują rzadko i umożliwia wielu użytkownikom jednoczesne odczytywanie i modyfikowanie danych. Podczas zapisu, Hibernate sprawdza, czy dane nie zostały zmienione przez innego użytkownika od czasu ich ostatniego odczytu.

- **Implementacja**: Używa pola wersji (`@Version`) do śledzenia zmian. Przed zapisaniem danych, Hibernate sprawdza, czy wartość wersji nie została zmieniona. Jeśli została, operacja zapisu jest przerywana i zgłaszany jest wyjątek.

Przykład:

```java
@Entity
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Version
    private int version;

    // inne pola
}
```

### Pesymistyczne Blokowanie

Pesymistyczne blokowanie zakłada, że konflikty występują często, dlatego blokuje dane od razu, aby zapobiec innym użytkownikom ich modyfikacji. 

- **Implementacja**: Używa blokad na poziomie bazy danych, aby zapobiec innym transakcjom odczytywanie lub modyfikowanie danych do czasu zakończenia transakcji.

Przykład:

```java
Product product = entityManager.find(Product.class, id, LockModeType.PESSIMISTIC_WRITE);
```
<hr>

> **_Informacja:_** 
Optymistyczne blokowanie jest preferowane w większości przypadków, ponieważ jest bardziej elastyczne i nie blokuje zasobów, podczas gdy pesymistyczne blokowanie jest bardziej odpowiednie w środowiskach o wysokiej konkurencji dostępu do danych.

