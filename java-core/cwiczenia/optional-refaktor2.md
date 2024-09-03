
# Refaktoryzacja: LibraryService - Kod o Niskiej Jakości

## Opis klasy LibraryService

Klasa `LibraryService` zarządza książkami i autorami w bibliotece oraz operacjami wypożyczania i zwalniania książek. Obecna implementacja jest niskopoziomowa i niechlujna, bez zastosowania nowoczesnych konstrukcji programistycznych, takich jak `Optional` czy `Stream`. Kod jest napisany w sposób, który nie stosuje zasad Clean Code, co czyni go trudnym do odczytania i utrzymania.

### Główne metody klasy:

1. **borrowBook(String title, String authorName)**:
    - Wypożycza książkę na podstawie tytułu i autora. Używa ręcznych pętli `for` do wyszukiwania autora i książki oraz instrukcji warunkowych `if` do sprawdzania dostępności.
    - Jeśli książka nie jest dostępna lub nie zostanie znaleziona, metoda rzuca wyjątek `IllegalStateException`.

2. **releaseBook(Long bookId)**:
    - Zwolnienie książki na podstawie jej ID. Również używa pętli `for` i instrukcji `if` do wyszukiwania książki i aktualizacji jej dostępności.
    - Rzuca `IllegalStateException` w przypadku, gdy książka nie może zostać zwolniona.

### Problemy wynikające z obecnego kodu:

1. **Duplikacja kodu**:
    - Kod zawiera wiele powtarzających się fragmentów, takich jak ręczne wyszukiwanie w pętlach `for` i warunki sprawdzające, co zwiększa ryzyko błędów i utrudnia konserwację kodu.

2. **Brak wykorzystania Optional i Stream**:
    - Kod mógłby być znacznie bardziej elegancki i zwięzły dzięki zastosowaniu `Optional` do zarządzania wartościami, które mogą być `null`, oraz `Stream` do operacji filtrowania i wyszukiwania.

3. **Zła obsługa wyjątków**:
    - Obecna implementacja wykorzystuje wiele miejsc, gdzie są rzucane wyjątki. Lepszym podejściem byłoby bardziej czytelne zarządzanie przypadkami wyjątkowymi z użyciem `Optional` i `orElseThrow()`.

4. **Brak zasady DRY (Don't Repeat Yourself)**:
    - Metody `borrowBook` i `releaseBook` zawierają podobną logikę wyszukiwania książki i jej aktualizacji, co mogłoby zostać wyabstrahowane do wspólnych metod pomocniczych.

5. **Niska czytelność i trudność w utrzymaniu**:
    - Kod jest napisany w sposób, który czyni go nieczytelnym, zbyt szczegółowym i trudnym do debugowania. Przyszłe zmiany mogą prowadzić do błędów, gdyż kod jest niechlujny i pełen duplikacji.

```java
public class LibraryService {
    private final List<Book> books;
    private final List<Author> authors;

    public LibraryService(List<Book> books, List<Author> authors) {
        this.books = books;
        this.authors = authors;
    }

    public Book borrowBook(String title, String authorName) {
        Author author = null;
        for (int i = 0; i < authors.size(); i++) {
            if (authors.get(i).name().equalsIgnoreCase(authorName)) {
                author = authors.get(i);
                break;
            }
        }

        if (author != null) {
            Book foundBook = null;
            for (int j = 0; j < author.books().size(); j++) {
                if (author.books().get(j).title().equalsIgnoreCase(title)) {
                    foundBook = author.books().get(j);
                    break;
                }
            }

            if (foundBook != null) {
                if (foundBook.available()) {
                    Book updatedBook = new Book(foundBook.id(), foundBook.title(), foundBook.author(), false);
                    books.remove(foundBook);
                    books.add(updatedBook);
                    return updatedBook;
                } else {
                    throw new IllegalStateException("Book is not available for borrowing.");
                }
            }
        }
        throw new IllegalStateException("Book is not available for borrowing.");
    }

    public Book releaseBook(Long bookId) {
        Book bookToRelease = null;
        for (int i = 0; i < books.size(); i++) {
            if (books.get(i).id().equals(bookId)) {
                bookToRelease = books.get(i);
                break;
            }
        }

        if (bookToRelease != null) {
            if (!bookToRelease.available()) {
                Book updatedBook = new Book(bookToRelease.id(), bookToRelease.title(), bookToRelease.author(), true);
                books.remove(bookToRelease);
                books.add(updatedBook);
                return updatedBook;
            } else {
                throw new IllegalStateException("Book is not available for release.");
            }
        } else {
            throw new IllegalStateException("Book is not available for release.");
        }
    }
}

```

### Cel refaktoryzacji:

1. **Zastosowanie Optional i Stream**:
    - Użyj `Optional` do zarządzania wartościami, które mogą być `null`, oraz strumieni do wyszukiwania i filtrowania danych.

2. **Poprawa czytelności i zarządzania wyjątkami**:
    - Użycie `orElseThrow()` zamiast ręcznego rzucania wyjątków poprawi czytelność kodu.

3. **Wyodrębnienie wspólnych metod**:
    - Refaktoryzacja powinna obejmować wyodrębnienie powtarzających się fragmentów kodu do metod pomocniczych, aby zmniejszyć duplikację i zwiększyć zrozumiałość.

## Kroki do wykonania refaktoryzacji:

1. **Użyj Optional w metodach wyszukiwania**:
    - Zmień metody `findBookByTitleAndAuthor` oraz `findBookById`, aby zwracały `Optional<Book>`.

2. **Zastosuj Stream API**:
    - Użyj `Stream` do filtrowania list książek i autorów, co uprości wyszukiwanie i operacje na kolekcjach.

3. **Użyj map() i filter() z Optional**:
    - Użyj kombinacji `map()` i `filter()` do zarządzania warunkami, zamiast rozbudowanych instrukcji `if`.

4. **Popraw obsługę wyjątków**:
    - Użyj `orElseThrow()` zamiast ręcznego rzucania `IllegalStateException`.

5. **Zastosuj zasadę DRY**:
    - Zrefaktoryzuj kod, aby wyeliminować powtarzające się fragmenty, takie jak operacje wyszukiwania i aktualizacji książek.
    - Stwórz metody prywatne `findBookByTitleAndAuthor`, `findBookById`, `findAuthorByName`, `updateBookAvailability`, każda zwracająca `Optional` by ułatwić operacje łańcuchowe

Po zastosowaniu tych kroków kod stanie się bardziej czytelny, elegancki i zgodny z zasadami Clean Code.

## Weryfikacja

Po zrefaktoryzowaniu kodu, upewnij się, że metody klasy `LibraryService` nadal działają poprawnie i wszystkie przypadki testowe zwracają oczekiwane wyniki.

```java
class LibraryServiceTest {

    private LibraryService libraryService;

    @BeforeEach
    void setUp() {
        // Inicjalizacja autorów
        Author author1 = new Author(1L, "J.K. Rowling", new ArrayList<>());
        Author author2 = new Author(2L, "George R.R. Martin", new ArrayList<>());

        // Inicjalizacja książek
        Book book1 = new Book(1L, "Harry Potter", author1, true);  // Książka dostępna
        Book book2 = new Book(2L, "Game of Thrones", author2, false);  // Książka niedostępna

        // Dodaj książki do autorów
        author1.books().add(book1);
        author2.books().add(book2);

        // Inicjalizacja serwisu
        List<Book> books = new ArrayList<>(List.of(book1, book2));
        List<Author> authors = new ArrayList<>(List.of(author1, author2));
        libraryService = new LibraryService(books, authors);
    }

    @Test
    void testBorrowBook_Success() {
        // Wypożycz książkę, która jest dostępna
        Book borrowedBook = libraryService.borrowBook("Harry Potter", "J.K. Rowling");
        assertNotNull(borrowedBook);
        assertEquals("Harry Potter", borrowedBook.title());
        assertFalse(borrowedBook.available());
    }

    @Test
    void testBorrowBook_BookNotAvailable() {
        // Próba wypożyczenia książki, która jest już wypożyczona (niedostępna)
        assertThrows(IllegalStateException.class, () -> {
            libraryService.borrowBook("Game of Thrones", "George R.R. Martin");
        });
    }

    @Test
    void testBorrowBook_BookNotFound() {
        // Próba wypożyczenia książki, która nie istnieje
        assertThrows(IllegalStateException.class, () -> {
            libraryService.borrowBook("Nonexistent Book", "J.K. Rowling");
        });
    }

    @Test
    void testReleaseBook_Success() {
        // Zwolnij książkę, która jest wypożyczona
        Book releasedBook = libraryService.releaseBook(2L);
        assertNotNull(releasedBook);
        assertEquals("Game of Thrones", releasedBook.title());
        assertTrue(releasedBook.available());
    }

    @Test
    void testReleaseBook_BookAlreadyAvailable() {
        // Próba zwolnienia książki, która jest już dostępna
        assertThrows(IllegalStateException.class, () -> {
            libraryService.releaseBook(1L);
        });
    }

    @Test
    void testReleaseBook_BookNotFound() {
        // Próba zwolnienia książki, która nie istnieje
        assertThrows(IllegalStateException.class, () -> {
            libraryService.releaseBook(999L);
        });
    }
}
```