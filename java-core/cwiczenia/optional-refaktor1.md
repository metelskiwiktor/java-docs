
# Zadanie Refaktoryzacyjne: Konwersja na `Optional`

## Wprowadzenie

Celem tego zadania jest zrefaktoryzowanie klasy Java, która służy do walidacji atrybutów produktu. Obecna implementacja mocno polega na zagnieżdżonych instrukcjach `if` oraz ręcznych sprawdzeniach `null`. Twoim zadaniem jest przekształcenie tej klasy przy użyciu `Optional`, aby kod stał się bardziej czytelny, łatwiejszy do utrzymania i nowoczesny.

Klasa `Optional` w Javie może pomóc uniknąć potencjalnych wyjątków `NullPointerException` i wyeliminować rozwlekły, powtarzalny kod sprawdzający `null`. Ta refaktoryzacja pomoże Ci zrozumieć siłę programowania funkcyjnego w Javie oraz poprawić jakość kodu.

## Klasa ProductValidator

### Opis Klasy i Metod

Klasa `ProductValidator` zawiera metody do walidacji atrybutów produktów, zarówno wymaganych jak i opcjonalnych:

1. **`validateProductAttributes(String productCode, String price, String productName)`**  
   Waliduje wymagane atrybuty produktu, takie jak kod produktu, cena i nazwa produktu.
    - **Kod produktu (`productCode`)**: Musi być niepusty, spełniać wzorzec wyrażenia regularnego `^[A-Za-z0-9]{5,10}$`, który dopuszcza od 5 do 10 znaków alfanumerycznych.
    - **Cena (`price`)**: Musi być niepusta, spełniać wzorzec wyrażenia regularnego `^[0-9]+(\.[0-9]{1,2})?$`, który dopuszcza liczby dziesiętne z maksymalnie dwoma miejscami po przecinku, i być większa od zera.
    - **Nazwa produktu (`productName`)**: Musi być niepusta i zaczynać się od wielkiej litery.

2. **`validateProductOptionalAttributes(String description, String category)`**  
   Waliduje opcjonalne atrybuty produktu, takie jak opis i kategoria.
    - **Opis (`description`)**: Może być pusty lub `null`, ale jeśli nie jest pusty, musi mieć co najmniej 15 znaków.
    - **Kategoria (`category`)**: Musi być niepusta i należeć do zestawu `VALID_CATEGORIES` (np. "Electronics", "Books", "Clothing", "Home", "Toys").

### Kod Źródłowy Klasy

Poniżej znajduje się kod źródłowy klasy `ProductValidator`:

```java
public class ProductValidator {

   private static final Pattern PRODUCT_CODE_PATTERN = Pattern.compile("^[A-Za-z0-9]{5,10}$");
   private static final Pattern PRICE_PATTERN = Pattern.compile("^[0-9]+(\\.[0-9]{1,2})?$");
   private static final Set<String> VALID_CATEGORIES = Set.of("Electronics", "Books", "Clothing", "Home", "Toys");

   public boolean validateProductAttributes(String productCode, String price, String productName) {
      boolean isProductCodeValid = false;
      if (productCode != null) {
         if (!productCode.trim().isEmpty()) {
            if (PRODUCT_CODE_PATTERN.matcher(productCode).matches()) {
               isProductCodeValid = true;
            }
         }
      }

      boolean isPriceValid = false;
      if (price != null) {
         if (!price.trim().isEmpty()) {
            if (PRICE_PATTERN.matcher(price).matches()) {
               double parsedPrice = Double.parseDouble(price);
               if (parsedPrice > 0) {
                  isPriceValid = true;
               }
            }
         }
      }

      boolean isProductNameValid = false;
      if (productName != null) {
         if (!productName.trim().isEmpty()) {
            if (Character.isUpperCase(productName.charAt(0))) {
               isProductNameValid = true;
            }
         }
      }

      return isProductCodeValid && isPriceValid && isProductNameValid;
   }

   public boolean validateProductOptionalAttributes(String description, String category) {
      boolean isDescriptionValid = false;
      if (description != null) {
         String trimmedDescription = description.trim();
         if (trimmedDescription.isEmpty()) {
            isDescriptionValid = true;
         } else if (trimmedDescription.length() >= 15) {
            isDescriptionValid = true;
         }
      } else {
         isDescriptionValid = true;
      }

      boolean isCategoryValid = false;
      if (category != null) {
         if (!category.trim().isEmpty()) {
            if (VALID_CATEGORIES.contains(category)) {
               isCategoryValid = true;
            }
         }
      } else {
         isCategoryValid = true;
      }

      return isDescriptionValid && isCategoryValid;
   }
}
```

## Uwaga

Kod powyżej zawiera **błędne praktyki programistyczne**, takie jak:
- Zbyt zagnieżdżone instrukcje `if`.
- Ręczne zarządzanie stanami zmiennych walidacyjnych.
- Jawne sprawdzanie `null` wartości w wielu miejscach.

Te praktyki prowadzą do rozwlekłego i trudnego do zarządzania kodu, który jest podatny na błędy.

## Zadanie Refaktoryzacyjne

Twoim zadaniem jest zrefaktoryzowanie powyższego kodu przy użyciu klasy `Optional` w Javie. Refaktoryzując ten kod:
- Użyj `Optional.ofNullable()` do zarządzania potencjalnie `null` wartościami.
- Zastąp zagnieżdżone instrukcje `if` metodami `.filter()`, `.map()` i `.isPresent()`.
- Uprość logikę walidacji i zmniejsz liczbę linii kodu, eliminując ręczne sprawdzania `null` i instrukcje warunkowe.

## Weryfikacja

Po zrefaktoryzowaniu kodu, upewnij się, że metody klasy `ProductValidator` nadal działają poprawnie i wszystkie przypadki testowe zwracają oczekiwane wyniki.
```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class ProductValidatorTest {

    private final ProductValidator validator = new ProductValidator();

    @Test
    void testValidateProductAttributesWithValidInputs() {
        // Testy z poprawnymi danymi
        assertTrue(validator.validateProductAttributes("ABC123", "19.99", "ProductName"));
        assertTrue(validator.validateProductAttributes("ABCDE12345", "0.01", "ValidProduct"));
        assertTrue(validator.validateProductAttributes("XYZ789", "100", "AnotherProduct"));
    }

    @Test
    void testValidateProductAttributesWithInvalidInputs() {
        // Testy z niepoprawnymi danymi
        assertFalse(validator.validateProductAttributes("AB", "abc", "product")); // Za krótki kod, błędna cena, nazwa z małej litery
        assertFalse(validator.validateProductAttributes("12345678901", "19.99", "ValidName")); // Za długi kod
        assertFalse(validator.validateProductAttributes("ABC123", "-5.99", "ProductName")); // Cena ujemna
        assertFalse(validator.validateProductAttributes("ABC123", "19.999", "ProductName")); // Za dużo miejsc po przecinku w cenie
        assertFalse(validator.validateProductAttributes("ABC123", "19.99", "productName")); // Nazwa z małej litery
    }

    @Test
    void testValidateProductAttributesWithNullValues() {
        // Testy z wartościami null
        assertFalse(validator.validateProductAttributes(null, "19.99", "ProductName"));
        assertFalse(validator.validateProductAttributes("ABC123", null, "ProductName"));
        assertFalse(validator.validateProductAttributes("ABC123", "19.99", null));
        assertFalse(validator.validateProductAttributes(null, null, null));
    }

    @Test
    void testValidateProductOptionalAttributesWithVariousInputs() {
        // Testy opcjonalnych atrybutów produktu
        assertTrue(validator.validateProductOptionalAttributes("This is a valid description", "Electronics"));
        assertTrue(validator.validateProductOptionalAttributes(null, "Books")); // Null description jest poprawne
        assertTrue(validator.validateProductOptionalAttributes("Valid Description", null)); // Null category jest poprawne
        assertTrue(validator.validateProductOptionalAttributes("", "Home")); // Pusty opis jest poprawny
        assertFalse(validator.validateProductOptionalAttributes("Short", "InvalidCategory")); // Zbyt krótki opis i niepoprawna kategoria
        assertFalse(validator.validateProductOptionalAttributes("This is a valid description", "")); // Pusta kategoria nie jest poprawna
    }
}
```
