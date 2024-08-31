
# Java Collections Framework

Java Collections Framework (JCF) to zestaw klas i interfejsów w języku Java, które umożliwiają przechowywanie i manipulowanie grupami obiektów. Ułatwia operacje takie jak wyszukiwanie, sortowanie, insercje, usuwanie itp. JCF zawiera interfejsy, implementacje oraz algorytmy, które upraszczają operacje na kolekcjach danych.

![medium-mbanaee61.webp](..%2Fresources%2Fmedium-mbanaee61.webp) <br>
https://medium.com/@mbanaee61/mastering-the-java-collections-framework-hierarchy-with-java-code-and-junit-testing-ab2eb87746ed

## 1. Interfejs `Iterator`

`Iterator` to interfejs w Java Collections Framework, który pozwala na iterację po elementach w kolekcji w kontrolowany sposób. Każda kolekcja implementująca interfejs `Iterable` może zwrócić `Iterator`.

- **Metody**:
  - `hasNext()` - sprawdza, czy w kolekcji są jeszcze elementy do przetworzenia.
  - `next()` - zwraca następny element w kolekcji.
  - `remove()` - usuwa ostatni zwrócony element z kolekcji (opcjonalne).

### Czym jest `Iterable`?

Interfejs `Iterable` to interfejs, który definiuje jedną metodę `iterator()`, która zwraca obiekt `Iterator`. Kolekcje implementujące `Iterable` mogą być przeglądane w pętli `for-each`.

## 2. Interfejs `List`

`List` to sekwencyjna kolekcja, która pozwala na przechowywanie duplikatów oraz dostęp do elementów przez indeksy.

### Metody interfejsu `List`:

- `add(E element)` - dodaje element na końcu listy.
- `add(int index, E element)` - dodaje element na określonym indeksie.
- `get(int index)` - zwraca element pod określonym indeksem.
- `remove(int index)` - usuwa element pod określonym indeksem.
- `remove(Object o)` - usuwa pierwsze wystąpienie określonego obiektu.
- `set(int index, E element)` - zastępuje element na określonym indeksie nowym elementem.
- `indexOf(Object o)` - zwraca indeks pierwszego wystąpienia określonego elementu lub `-1`, jeśli element nie istnieje.
- `size()` - zwraca liczbę elementów na liście.
- `contains(Object o)` - sprawdza, czy element jest na liście.

### 2.1 `ArrayList`

`ArrayList` jest jedną z implementacji interfejsu `List` opartą o tablicę dynamiczną.

- **Charakterystyka**:
  - `ArrayList` jest implementacją `List` opartą na **dynamicznej tablicy**. <br> Dynamiczna tablica jest strukturą danych, która może zmieniać swój rozmiar podczas działania programu. Kiedy liczba elementów przekroczy bieżącą pojemność tablicy, nowa, większa tablica jest tworzona w pamięci, a wszystkie istniejące elementy są do niej kopiowane.
  - Szybki dostęp do elementów przez indeks (`O(1)`), ponieważ jest to operacja stałoczasowa.
  - Wolne operacje dodawania i usuwania elementów w środku listy (`O(n)`), ponieważ wymagają przesunięcia elementów w tablicy.
  - Efektywne, gdy trzeba często uzyskiwać dostęp do elementów lub modyfikować elementy na końcu listy.

#### Tworzenie własnej implementacji `ArrayList`:

Aby stworzyć własną implementację `ArrayList`, wykonaj następujące kroki:

1. **Definiuj dynamiczną tablicę**: Rozpocznij od utworzenia wewnętrznej tablicy o początkowym rozmiarze.
2. **Zarządzaj rozmiarem tablicy**: Dodaj logikę, która sprawdza, czy tablica osiągnęła swoją pojemność. Jeśli tak, utwórz nową tablicę o większym rozmiarze i skopiuj wszystkie elementy z oryginalnej tablicy.
3. **Implementuj metody `List`**: Napisz metody takie jak `add(E element)`, `remove(int index)`, `get(int index)`, które manipulują dynamiczną tablicą.
4. **Zarządzaj wskaźnikiem rozmiaru**: Upewnij się, że zawsze śledzisz aktualny rozmiar (liczbę elementów) w tablicy i aktualizujesz go podczas dodawania lub usuwania elementów.

### Dodatkowe metody `ArrayList`:

- `ensureCapacity(int minCapacity)` - zwiększa pojemność listy do co najmniej minimalnej określonej pojemności.

### 2.2 `LinkedList`

`LinkedList` jest kolejną implementacją interfejsu `List` opartą o więzły.

- **Charakterystyka**:
  - `LinkedList` jest implementacją `List` opartą na **liście dwukierunkowej**. <br>Lista dwukierunkowa to struktura danych, w której każdy element (nazywany "węzłem") zawiera odniesienia do swojego poprzedniego i następnego elementu. Dzięki temu, dodawanie i usuwanie elementów na początku lub końcu listy jest bardzo szybkie (`O(1)`).
  - Wolniejszy dostęp do elementów przez indeks (`O(n)`), ponieważ wymaga iteracji przez listę.
  - Efektywny, gdy często trzeba dodawać/usuwać elementy na początku lub końcu listy.

#### Tworzenie własnej implementacji `LinkedList`:

Aby stworzyć własną implementację `LinkedList`, wykonaj następujące kroki:

1. **Definiuj węzeł (Node)**: Stwórz wewnętrzną klasę `Node` z referencjami do poprzedniego i następnego węzła oraz przechowywanym elementem.
2. **Zarządzaj wskaźnikami**: Dodaj wskaźniki do głowy (head) i ogona (tail) listy, które będą wskazywać pierwszy i ostatni element.
3. **Implementuj metody `List`**: Napisz metody takie jak `addFirst(E e)`, `removeLast()`, `get(int index)` itp., które manipulują węzłami.
4. **Obsługuj dodawanie/usuwanie**: Pamiętaj o prawidłowym aktualizowaniu referencji w węzłach podczas dodawania i usuwania elementów.

### Dodatkowe metody `LinkedList`:

- `addFirst(E e)` - dodaje element na początku listy.
- `addLast(E e)` - dodaje element na końcu listy.
- `removeFirst()` - usuwa pierwszy element.
- `removeLast()` - usuwa ostatni element.
