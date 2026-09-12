# Instalacja i aktywacja

Ta instrukcja dotyczy edycji Cool Video Netteria License 1.4.10 sprzedawanej
bezpośrednio i dostarczanej przez
[prestaexpert.pl](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html).

## Wymagania

| Wymaganie | Szczegóły |
| --- | --- |
| PrestaShop | 1.7.x, 8.x lub 9.x |
| PHP i baza danych | Wersje PHP oraz MySQL lub MariaDB obsługiwane przez zainstalowaną wersję PrestaShop |
| Rozszerzenie PHP | cURL jest wymagany do aktywacji i weryfikacji licencji |
| Sieć | Serwer sklepu musi mieć możliwość wykonywania wychodzących żądań HTTPS do `prestaexpert.pl` |
| Przeglądarka | Do zarządzania w panelu i obsługi filmów na listach zalecana jest aktualna przeglądarka z JavaScript i `fetch` |
| Motyw | Classic i Hummingbird są obsługiwane bezpośrednio; zgodne motywy niestandardowe mogą używać trybu opartego na standardowych hookach |
| Uprawnienia | Konto pracownika panelu z prawem instalowania modułów i edytowania produktów |
| Licencja | Klucz aktywacyjny Cool Video przypisany do domeny sklepu podanej podczas zakupu |

Przed instalacją w sklepie produkcyjnym wykonaj aktualną kopię plików i bazy
danych. Test na kopii stagingowej jest zalecany, gdy sklep używa mocno
zmodyfikowanego motywu, restrykcyjnej polityki Content Security Policy albo
agresywnej optymalizacji JavaScript.

## Pobranie właściwego pakietu

Pobierz licencjonowany pakiet dostarczony po zakupie na oficjalnej
[stronie produktu Cool Video](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html).
Nazwa pliku może mieć postać `coolvideo-1.4.10-netteria-license.zip` lub nazwę
dystrybucyjną, na przykład `coolvideo.zip`.

Nie rozpakowuj i nie kompresuj archiwum ponownie. ZIP musi zawierać katalog
główny `coolvideo`, a w nim plik `coolvideo.php`. Podwójnie opakowane archiwum,
na przykład `coolvideo/coolvideo/coolvideo.php`, nie zainstaluje się poprawnie.

Repozytorium może zawierać również pakiety Marketplace i deweloperskie. Są to
oddzielne dystrybucje, które mogą inaczej obsługiwać aktywację. W tej instrukcji
używaj pakietu dostarczonego po zakupie w prestaexpert.pl.

## Instalacja modułu

1. Zaloguj się do panelu administracyjnego PrestaShop na konto z uprawnieniem
   do instalowania modułów.
2. Otwórz **Modules > Module Manager** (Moduły > Menedżer modułów). W niektórych
   instalacjach PrestaShop 1.7 pozycja menu może nazywać się **Modules and
   Services**.
3. Wybierz **Upload a module**.
4. Przeciągnij otrzymany plik ZIP do obszaru przesyłania albo wybierz go
   z dysku.
5. Poczekaj, aż PrestaShop rozpakuje i zainstaluje moduł.
6. Sprawdź, czy Cool Video jest widoczny jako zainstalowany i włączony.
7. Wybierz **Configure**, aby otworzyć ekran licencji.

Jeśli instalacja się nie powiedzie, nie przesyłaj kolejno przypadkowych
archiwów. Najpierw sprawdź strukturę ZIP, uprawnienia zapisu do katalogu
`modules` PrestaShop, limity przesyłania PHP, wolne miejsce na dysku oraz logi
PrestaShop.

## Aktywacja licencji sprzedaży bezpośredniej

1. Otwórz **Modules > Module Manager** i znajdź **Cool Video Product - Netteria
   License**.
2. Wybierz **Configure**.
3. Odczytaj wartość **Shop domain** w panelu statusu licencji.
4. Upewnij się, że jest to domena przypisana do klucza podczas zakupu.
   Walidator porównuje nazwy hostów bez protokołu, portu, ścieżki i początkowego
   `www.`.
5. Wklej kod aktywacyjny w polu **License key**.
6. Wybierz **Activate license**.
7. Sprawdź, czy strona pokazuje **License active**. Zapisany klucz jest
   wyświetlany w postaci zamaskowanej. Jeśli licencja ma datę wygaśnięcia,
   strona również ją pokaże.

Klucz może zawierać wyłącznie litery, cyfry i łączniki, a jego długość nie może
przekraczać 120 znaków. Chroń go. Nie wysyłaj pełnego klucza na zrzutach
ekranu, w zgłoszeniach, publicznych repozytoriach ani w danych z konsoli
przeglądarki.

### Sposób działania weryfikacji

- Poprawny wynik jest zapisywany w pamięci podręcznej na 24 godziny.
- Nieprawidłowy wynik lub tymczasowy błąd połączenia jest ponawiany po
  5 minutach.
- Po co najmniej jednej udanej weryfikacji online moduł może przez maksymalnie
  7 dni korzystać z ostatniego poprawnego potwierdzenia podczas tymczasowej
  awarii serwera licencji.
- Klucz, który nigdy nie został poprawnie zweryfikowany online, nie może
  korzystać z okresu działania offline.
- Przy nieaktywnej licencji zarządzanie filmami jest blokowane, a galeria
  i elementy na listach produktów nie są renderowane w sklepie.

Żądanie weryfikacji po stronie serwera jest wysyłane przez HTTPS do:

```text
https://prestaexpert.pl/modules/netterialicenseprovisioner/api/v1/validate.php
```

Zezwól na ruch wychodzący TCP na porcie 443, rozwiązywanie DNS i poprawną
weryfikację certyfikatu dla tego hosta. Moduł potrzebuje PHP cURL oraz prawa
zapisu pamięci statusu w `modules/coolvideo/cache/`.

## Sprawdzenie instalacji

Wykonaj ten test przed skonfigurowaniem wielu produktów:

1. Otwórz produkt, który został już zapisany i ma identyfikator produktu.
2. Znajdź Cool Video w sekcji **Modules** produktu.
3. Dodaj jeden obsługiwany publiczny adres URL, na przykład standardowy adres
   filmu YouTube.
4. Pozostaw **Active** włączone i ustaw **Gallery position** na `2`.
5. Zapisz pozycję, jeśli została zmieniona.
6. Otwórz publiczną stronę produktu w prywatnym oknie przeglądarki.
7. Sprawdź, czy miniatura filmu pojawia się po pierwszym zdjęciu produktu i czy
   jej wybranie uruchamia odtwarzacz.
8. Otwórz modal zdjęć lub multimediów i sprawdź dostępność filmu.
9. Sprawdź tę samą stronę w szerokości urządzenia mobilnego.
10. Jeśli film ma być widoczny na listach produktów, ustaw pozycję `1`, włącz
    **Show on product listings** i sprawdź stronę kategorii lub wyszukiwania.

## Aktualizacja bez utraty powiązań

Aktualizuj moduł w miejscu. Nie odinstalowuj najpierw starej wersji, ponieważ
odinstalowanie usuwa tabelę zawierającą wszystkie powiązania produktów
z filmami.

1. Wykonaj kopię zapasową plików sklepu i bazy danych.
2. Zapisz numer zainstalowanej wersji Cool Video i sprawdź, czy licencja jest
   aktywna.
3. Pobierz nowy licencjonowany ZIP z oficjalnego kanału zakupu.
4. Użyj mechanizmu aktualizacji lub przesyłania modułu PrestaShop, aby zastąpić
   moduł w miejscu.
5. Pozwól PrestaShop uruchomić dołączone skrypty aktualizacyjne.
6. Sprawdź, czy moduł nadal jest włączony, a strona konfiguracji pokazuje
   aktywną licencję.
7. Wyczyść pamięć podręczną PrestaShop. Jeśli CCC lub inny system optymalizacji
   łączy CSS i JavaScript, wyczyść również jego pamięć.
8. Otwórz produkt z istniejącymi filmami i sprawdź, czy powiązania, pozycje
   i opcje nadal istnieją.
9. Przetestuj galerię produktu, natywny modal multimediów, układ mobilny i listę
   produktów.

Aktualizacja do edycji 1.4.10 sprzedawanej bezpośrednio została zaprojektowana
tak, aby zachować istniejące powiązania filmów. Kopia zapasowa pozostaje
konieczna, ponieważ konfiguracja serwera, zewnętrzne optymalizatory i przerwane
aktualizacje są poza kontrolą modułu.

## Zmiana domeny i multistore

Licencja sprzedaży bezpośredniej jest przypisana do znormalizowanej domeny
sklepu. Zmiana adresu sklepu w PrestaShop, przeniesienie ze środowiska
stagingowego na produkcyjne albo dodanie innej domeny może wywołać błąd
**Domain mismatch**, dopóki przypisanie licencji nie zostanie zaktualizowane.
Skorzystaj z oficjalnej strony produktu i kanału wsparcia, aby potwierdzić
warunki licencji oraz poprosić o zmianę domeny.

W instalacji multistore przełącz się do właściwego kontekstu sklepu przed
otwarciem ekranu licencji i sprawdź domenę wyświetlaną dla każdego sklepu. Nie
zakładaj, że jeden klucz obejmuje wszystkie niezależne domeny.

## Wyłączenie lub odinstalowanie

Wyłączenie modułu zatrzymuje menedżer filmów w panelu oraz wyświetlanie
w sklepie, ale zwykle pozostawia zapisane powiązania w bazie danych. Ponowne
włączenie modułu i przywrócenie poprawnej licencji udostępnia je ponownie.

Odinstalowanie powoduje trwałe skutki:

- wszystkie powiązania produktów z filmami są usuwane;
- tabela modułu w bazie danych jest usuwana;
- zapisany klucz aktywacyjny Cool Video i lokalna pamięć statusu licencji są
  usuwane;
- ukryta karta administracyjna używana przez menedżer filmów jest usuwana.

Wyeksportuj bazę lub wykonaj jej kopię przed odinstalowaniem, jeśli powiązania
mogą być potrzebne później. PrestaShop nie udostępnia funkcji cofnięcia tego
usunięcia.

## Następny krok

Przejdź do [instrukcji użytkownika](USER_GUIDE_PL.md), aby dodawać filmy
i konfigurować ich pozycję w galerii, autoodtwarzanie oraz wyświetlanie na
listach produktów.

