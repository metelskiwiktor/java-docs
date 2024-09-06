# Praktyczne Zadania z Hibernate ORM

## Zadanie 1: Relacja `OneToMany` z `cascade = CascadeType.ALL`

### Opis

Utwórz relację `OneToMany` między dwiema encjami, gdzie encja nadrzędna ma ustawiony `cascade = CascadeType.ALL`. Sprawdź, co się stanie, gdy usuniesz encję podrzędną. Zademonstruj problem niezamierzonego usunięcia encji nadrzędnej.

### Cel
- Zrozumienie wpływu `CascadeType.ALL` na operacje usuwania w relacjach.
- Identyfikacja nieprawidłowości w zarządzaniu kaskadowym usuwaniem.

### Oczekiwany rezultat
- Usunięcie encji podrzędnej powoduje niezamierzone usunięcie encji nadrzędnej.

---

## Zadanie 2: Lazy Loading poza kontekstem transakcji

### Opis

Utwórz relację `OneToMany` z ładowaniem leniwym (`fetch = FetchType.LAZY`). Załaduj encję nadrzędną i spróbuj uzyskać dostęp do powiązanej kolekcji po zamknięciu transakcji lub sesji. Zaobserwuj, co się stanie.

### Cel
- Zrozumienie, jak działa `LazyInitializationException` i kiedy może wystąpić.
- Poznanie różnicy między `FetchType.LAZY` a `FetchType.EAGER`.

### Oczekiwany rezultat
- Wystąpienie `LazyInitializationException` podczas próby uzyskania dostępu do leniwie ładowanej kolekcji poza transakcją.

---

## Zadanie 3: Usunięcie elementu kolekcji przy `orphanRemoval = true`

### Opis

Stwórz relację `OneToMany` z `orphanRemoval = true`. Usuń element z kolekcji w encji nadrzędnej i sprawdź, czy ten element zostanie usunięty z bazy danych. Zademonstruj, jak `orphanRemoval` może prowadzić do niezamierzonego usuwania danych.

### Cel
- Zrozumienie, jak działa `orphanRemoval` w Hibernate.
- Nauka ostrożnego używania `orphanRemoval` w relacjach.

### Oczekiwany rezultat
- Usunięcie elementu z kolekcji w encji nadrzędnej powoduje jego usunięcie z bazy danych.

---

## Zadanie 5: Użycie `@JoinColumn` i brak tabeli pośredniej

### Opis

Utwórz relację `ManyToOne` lub `OneToOne` między dwiema encjami, korzystając z adnotacji `@JoinColumn`. Obserwuj, że w tej konfiguracji Hibernate tworzy kolumnę klucza obcego w istniejącej tabeli encji podrzędnej, zamiast tworzyć nową tabelę pośrednią, jak ma to miejsce przy użyciu `@JoinTable`.

### Cel
- Zrozumienie, jak działa `@JoinColumn` w porównaniu do `@JoinTable`.
- Zobaczenie, jak klucz obcy jest przechowywany bez tworzenia dodatkowej tabeli pośredniej.

### Oczekiwany rezultat
- Zobaczysz, że Hibernate tworzy kolumnę klucza obcego bez tworzenia nowej tabeli pośredniej.

---

## Zadanie 4: Problem zapytań `N+1` z `ManyToMany` i `EAGER`

### Opis

Utwórz relację `ManyToMany` między dwoma encjami i ustaw `fetch = FetchType.EAGER` dla obu stron. Pobierz wszystkie encje nadrzędne i zaobserwuj liczbę wykonanych zapytań SQL. Zademonstruj problem zapytań `N+1` i wyjaśnij, jak to wpływa na wydajność.

### Cel
- Identyfikacja problemu `N+1` zapytań w relacjach `ManyToMany`.
- Zrozumienie wpływu `FetchType.EAGER` na wydajność aplikacji.

### Oczekiwany rezultat
- Powstaje problem `N+1` zapytań, prowadzący do obniżenia wydajności aplikacji.

