
# Transakcje w Springu - Podstawowe i Średniozaawansowane Koncepty

## 1. Wprowadzenie do transakcji

Transakcje to kluczowy element zarządzania danymi w aplikacjach. Pozwalają one na grupowanie wielu operacji na bazie danych w jedną jednostkę pracy, która jest wykonywana atomowo. Oznacza to, że wszystkie operacje w ramach transakcji muszą zakończyć się sukcesem, aby zmiany zostały zapisane w bazie danych. Jeśli jedna z operacji nie powiedzie się, cała transakcja jest wycofywana (rollback), a baza danych wraca do stanu sprzed rozpoczęcia transakcji.

## 2. Czym jest transakcja?

Transakcja to seria operacji na bazie danych, które są wykonywane jako jeden niepodzielny krok. W ramach transakcji operacje są wykonywane w sposób atomowy, co oznacza, że wszystkie zmiany są zatwierdzane (commit) lub wycofywane (rollback) jako jedna całość. Transakcje zapewniają spójność danych, nawet w przypadku awarii systemu.

## 3. Rodzaje transakcji

- **Lokalne transakcje:** Obejmują operacje wykonywane w ramach jednej bazy danych.
- **Rozproszone transakcje:** Obejmują operacje wykonywane w więcej niż jednej bazie danych lub systemie. Wymagają one koordynacji między różnymi zasobami (np. za pomocą protokołu dwufazowego zatwierdzania, 2PC).

## 4. Zasady ACID w transakcji

ACID to akronim, który opisuje cztery kluczowe właściwości transakcji:

- **Atomicity (Atomowość):** Wszystkie operacje w ramach transakcji są wykonywane jako jedna całość. Jeśli jedna z operacji zawiedzie, wszystkie są wycofywane.
- **Consistency (Spójność):** Transakcje przekształcają bazę danych z jednego spójnego stanu do drugiego.
- **Isolation (Izolacja):** Operacje wykonywane w ramach transakcji są izolowane od innych równoczesnych transakcji.
- **Durability (Trwałość):** Po zatwierdzeniu transakcji, jej wyniki są trwałe i przetrwają awarie systemu.

## 5. Czym jest rollback? Jak jest on zrobiony w Springu?

- **Definicja Rollbacku**: Rollback to proces cofania wszystkich operacji wykonanych w ramach transakcji, gdy nie uda się wykonać jednej z operacji. W ten sposób zapewniana jest spójność danych w bazie.

- **Mechanizm Rollbacku w Springu**:
    - **Proxy w Springu**: Spring wykorzystuje mechanizm proxy, aby zarządzać transakcjami w aplikacji. Gdy metoda oznaczona adnotacją `@Transactional` jest wywoływana, Spring dynamicznie tworzy obiekt proxy, który otacza oryginalną metodę logiką zarządzania transakcjami.
    - **Tworzenie Transakcji**: Gdy proxy wykrywa, że metoda jest oznaczona jako `@Transactional`, Spring prosi menedżera transakcji o rozpoczęcie nowej transakcji.
    - **Zarządzanie Rollbackiem**: Jeśli podczas wykonania metody dojdzie do wyjątku, proxy interweniuje i informuje menedżera transakcji, aby wycofał wszystkie zmiany dokonane przez tę transakcję.
        - **Domyślne Zachowanie**: Spring domyślnie wykonuje rollback w przypadku wystąpienia niekontrolowanego wyjątku (`RuntimeException`) lub błędu (`Error`).
        - **Kontrolowanie Rollbacku**: Możesz dostosować, które wyjątki powodują rollback, używając atrybutów `rollbackFor`, `noRollbackFor`, `rollbackForClassName` i `noRollbackForClassName` w adnotacji `@Transactional`.
    - **Ciągłość Operacji**: Jeśli żadna operacja nie rzuci wyjątku, proxy pozwala na zakończenie transakcji z sukcesem poprzez zatwierdzenie jej (commit).

- **Przykład Konfiguracji Rollbacku**:
    - **Standardowa konfiguracja**:
      ```java
      @Transactional
      public void processOrder(Order order) {
          // operacje na zamówieniu
      }
      ```
    - **Zaawansowana konfiguracja rollbacku**:
      ```java
      @Transactional(rollbackFor = Exception.class, noRollbackFor = SpecificException.class)
      public void processOrder(Order order) throws Exception {
          // operacje na zamówieniu, które powinny wycofać transakcję w przypadku wyjątku
      }
      ```

## 6. Izolacje transakcji

Izolacja transakcji określa, w jaki sposób zmiany dokonane przez jedną transakcję są widoczne dla innych równocześnie działających transakcji. Poziomy izolacji, które można ustawić w Springu, obejmują:

- **READ_UNCOMMITTED:** Transakcje mogą widzieć zmiany niezakończonych transakcji innych użytkowników.
- **READ_COMMITTED:** Transakcje widzą tylko zmiany, które zostały zatwierdzone (commit).
- **REPEATABLE_READ:** Dane odczytane przez transakcję nie mogą być zmienione przez inne transakcje, dopóki pierwsza transakcja nie zakończy się.
- **SERIALIZABLE:** Najwyższy poziom izolacji, gdzie transakcje są wykonywane sekwencyjnie, eliminując możliwość konfliktu.

## 7. Problemy z izolacją transakcji

Podczas pracy z transakcjami mogą wystąpić różne problemy związane z izolacją danych. Są to:

1. **Dirty Reads (Brudne odczyty)**:
    - Występują, gdy jedna transakcja odczytuje dane, które zostały zmienione przez inną transakcję, która jeszcze nie zakomituje swoich zmian. Jeśli ta druga transakcja zostanie wycofana (rollback), pierwsza transakcja będzie bazować na niespójnych danych.

2. **Non-Repeatable Reads (Niezapewniające powtórnego odczytu)**:
    - Występują, gdy w ramach tej samej transakcji następuje odczyt tego samego rekordu wielokrotnie, ale dane te ulegają zmianie między odczytami przez inną transakcję, która zakomituje swoje zmiany. W efekcie, w ramach jednej transakcji, te same zapytania mogą zwrócić różne wyniki.

3. **Phantom Reads (Fantomowe odczyty)**:
    - Występują, gdy w ramach jednej transakcji wielokrotnie wykonywane są zapytania, które filtrują pewien zestaw rekordów na podstawie określonych kryteriów, ale inne transakcje zakomituje w tym czasie nowe rekordy, które spełniają te kryteria. W efekcie, kolejne odczyty mogą zwrócić różną liczbę rekordów.

### Jak to się wiąże z poziomami izolacji:

- **READ UNCOMMITTED**: Pozwala na Dirty Reads, Non-Repeatable Reads, i Phantom Reads.
- **READ COMMITTED**: Zapobiega Dirty Reads, ale pozwala na Non-Repeatable Reads i Phantom Reads.
- **REPEATABLE READ**: Zapobiega Dirty Reads i Non-Repeatable Reads, ale może pozwalać na Phantom Reads.
- **SERIALIZABLE**: Zapobiega wszystkim trzem problemom, ale może prowadzić do większych blokad i mniejszej wydajności.

## 8. Propagacja transakcji

Propagacja transakcji definiuje, jak nowa transakcja powinna być uruchomiona w kontekście już istniejącej transakcji. Spring oferuje kilka typów propagacji, w tym:

- **REQUIRED:** (Domyślna) Jeśli istnieje bieżąca transakcja, metoda jest wykonywana w jej kontekście, w przeciwnym razie rozpoczynana jest nowa transakcja.
- **REQUIRES_NEW:** Zawsze rozpoczyna nową transakcję, zawieszając bieżącą, jeśli taka istnieje.
- **NESTED:** Tworzy nową transakcję wewnątrz istniejącej transakcji (tylko dla JDBC).
- **MANDATORY:** Wymaga, aby już istniała transakcja, w przeciwnym razie rzuca wyjątek.
- **SUPPORTS:** Jeśli istnieje transakcja, metoda jest w niej wykonywana, ale jeśli nie ma transakcji, działa bez transakcji.
- **NOT_SUPPORTED:** Metoda zawsze działa bez transakcji, zawieszając bieżącą, jeśli taka istnieje.
- **NEVER:** Metoda działa bez transakcji i rzuca wyjątek, jeśli jakaś transakcja istnieje.

## 9. Wyjątki i transakcje

W Springu, sposób, w jaki wyjątki wpływają na transakcje, zależy od ich typu:
- **Unchecked exceptions (`RuntimeException`)** domyślnie powodują wycofanie transakcji.
- **Checked exceptions** nie powodują domyślnie rollbacku, ale można to zmienić, konfigurując atrybuty `rollbackFor` i `noRollbackFor` w adnotacji `@Transactional`.

## 10. Alternatywy dla tradycyjnych transakcji

W rozproszonych systemach, gdzie klasyczne transakcje ACID mogą być trudne do osiągnięcia, stosuje się inne podejścia, takie jak:
- **Eventual Consistency:** Zapewnia spójność danych w dłuższej perspektywie, ale pozwala na chwilowe niespójności.
- **Sagas:** Selekcja transakcji, gdzie każda operacja ma odpowiednią akcję kompensacyjną na wypadek niepowodzenia.
