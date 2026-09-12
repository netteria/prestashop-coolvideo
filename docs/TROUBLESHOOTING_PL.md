# Rozwiązywanie problemów

Ta instrukcja dotyczy edycji Cool Video Netteria License 1.4.10 sprzedawanej
bezpośrednio. Zacznij od szybkiej diagnostyki, a następnie przejdź do sekcji
odpowiadającej objawowi.

## Szybka diagnostyka

1. Sprawdź, czy Cool Video jest zainstalowany i włączony w **Modules > Module
   Manager**.
2. Otwórz **Configure** i sprawdź status **License active** dla wyświetlanej
   domeny sklepu.
3. Upewnij się, że produkt został zapisany i ma identyfikator produktu.
4. Sprawdź, czy film ma włączone **Active** i korzysta z obsługiwanego
   publicznego adresu URL.
5. Otwórz adres dostawcy bezpośrednio w prywatnym oknie przeglądarki i upewnij
   się, że film istnieje oraz pozwala na osadzanie.
6. Wyczyść pamięć podręczną PrestaShop oraz powiązane pamięci CCC, reverse
   proxy, CDN i całych stron.
7. Przeprowadź test bez rozszerzeń przeglądarki. Jeśli menedżer zgód blokuje
   zewnętrzne odtwarzacze, zaakceptuj kategorię zgody dla multimediów lub
   marketingu.
8. Sprawdź układ komputerowy i mobilny.
9. W przypadku motywu niestandardowego tymczasowo przetestuj jego domyślną
   konfigurację galerii albo motyw Classic na sklepie stagingowym.
10. Sprawdź konsolę przeglądarki, nieudane żądania sieciowe, logi PrestaShop
    oraz logi serwera WWW i PHP.

## Tabela objawów

| Objaw | Najbardziej prawdopodobna przyczyna | Pierwsze działanie |
| --- | --- | --- |
| Cool Video nie pojawia się w edytorze produktu | Produkt nie został zapisany, moduł jest wyłączony, licencja jest nieaktywna albo pracownik nie ma dostępu | Zapisz produkt, sprawdź moduł i licencję, a następnie uprawnienia |
| **Invalid or unsupported video URL** | Adres URL nie odpowiada żadnemu rozpoznawanemu formatowi pojedynczego filmu | Skopiuj bezpośredni adres filmu YouTube, Vimeo lub Dailymotion z listy obsługiwanych formatów |
| Miniatura jest pusta lub uszkodzona | Host miniatury jest zablokowany, film jest niedostępny albo Content Security Policy odrzuca obraz | Sprawdź host miniatury w narzędziach sieciowych przeglądarki i popraw CSP lub reguły zapory |
| Miniatura działa, ale film się nie odtwarza | Dostawca wyłączył osadzanie, film jest prywatny lub ograniczony albo host iframe jest zablokowany | Sprawdź adres osadzania dostawcy i ustawienia prywatności filmu |
| Filmu nie ma w galerii | Film jest nieaktywny, pamięć podręczna jest nieaktualna, licencja jest nieaktywna, brakuje hooka motywu albo występuje konflikt JavaScript | Włącz film, wyczyść pamięci, sprawdź licencję i konsolę przeglądarki |
| Pozycja w galerii jest ignorowana | Działa ogólny tryb zgodności motywu albo kod galerii pochodzi z pamięci podręcznej | Wyczyść pamięci i sprawdź, czy strona używa adaptera Classic, Hummingbird czy ogólnego |
| Filmu nie ma na liście produktów | Film nie jest aktywny, opcja listy jest wyłączona albo pozycja nie wynosi `1` | Włącz obie opcje i zapisz pozycję `1` w galerii |
| Autoodtwarzanie się nie uruchamia | Zablokowała je polityka przeglądarki, dostawcy, zgód, baterii lub oszczędzania danych | Sprawdź, czy wyciszone autoodtwarzanie jest włączone, i przetestuj po bezpośrednim działaniu użytkownika |
| Zmiany nie są widoczne | Pamięć PrestaShop, CCC, CDN, service workera lub strony jest nieaktualna | Wyczyść wszystkie odpowiednie pamięci i wykonaj twarde odświeżenie strony |
| Po aktualizacji wszystko zniknęło | Moduł został wyłączony, hooki nie zostały przywrócone, licencja jest nieaktywna albo przeglądarka używa starych zasobów | Włącz moduł, sprawdź licencję, wyczyść pamięci i rejestrację wymaganych hooków |

## Problemy z aktywacją licencji

### Brak klucza licencji

Otwórz konfigurację modułu, wklej kod aktywacyjny otrzymany po zakupie
w prestaexpert.pl i wybierz **Activate license**. Użyj licencjonowanego pakietu
sprzedaży bezpośredniej, a nie archiwum Marketplace lub deweloperskiego.

### Nie znaleziono licencji

Sprawdź każdy znak klucza. Usuń spacje na początku i końcu oraz upewnij się, że
klucz należy do Cool Video. Jeśli nadal nie działa, skorzystaj z oficjalnego
[kanału wsparcia produktu](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html).

### Niezgodność domeny

Porównaj **Shop domain** na stronie konfiguracji modułu z domeną podaną przy
zakupie. Walidator pomija protokół, port, ścieżkę i początkowe `www.`, ale inny
host lub subdomena nadal oznacza inną domenę.

Sprawdź **Shop Parameters > Traffic & SEO > Set shop URL** lub równoważne
ustawienia adresu sklepu PrestaShop. W trybie multistore przełącz się do
właściwego kontekstu sklepu. Gdy trzeba zmienić licencjonowaną domenę,
skontaktuj się z oficjalnym kanałem sprzedaży.

### Licencja wygasła

Sprawdź **Valid until** na ekranie konfiguracji i odnów lub skoryguj licencję
przez oficjalny kanał sprzedaży. Nie zmieniaj zegara serwera, aby obejść ten
status.

### Serwer licencji jest niedostępny

Sprawdź na serwerze sklepu:

- czy PHP cURL jest włączony dla PHP obsługującego stronę WWW, a nie tylko dla
  PHP wiersza poleceń;
- czy DNS rozwiązuje `prestaexpert.pl`;
- czy dozwolony jest wychodzący HTTPS na porcie TCP 443;
- czy działa weryfikacja certyfikatów TLS i serwer ma aktualny zestaw
  certyfikatów CA;
- czy data i godzina serwera są poprawne;
- czy proxy, WAF lub zapora hostingu nie zmieniają ani nie blokują żądania.

Endpoint weryfikacji:

```text
https://prestaexpert.pl/modules/netterialicenseprovisioner/api/v1/validate.php
```

Po wcześniejszym udanym sprawdzeniu moduł może przez maksymalnie 7 dni używać
ostatniego poprawnego potwierdzenia podczas tymczasowej awarii. Tymczasowy błąd
jest ponawiany po 5 minutach. Klucz, który nigdy nie został potwierdzony, nie
może aktywować modułu offline.

### Licencja działa krótko i jest zbyt często sprawdzana

Upewnij się, że katalog `modules/coolvideo/cache/` istnieje i jest zapisywalny
dla konta PHP lub serwera WWW. Nie nadawaj prawa zapisu dla wszystkich do
całego katalogu modułu. Użyj najmniejszych uprawnień wymaganych przez
środowisko hostingowe.

## Brak menedżera filmów

Moduł wymaga istniejącego identyfikatora produktu. Zapisz nowy produkt, a potem
odśwież lub ponownie otwórz jego edytor.

Jeśli panelu Cool Video nadal nie ma przy istniejącym produkcie:

1. Sprawdź, czy moduł jest włączony w bieżącym kontekście sklepu.
2. Sprawdź, czy licencja jest aktywna.
3. Upewnij się, że profil pracownika może edytować produkty i ma dostęp do
   ukrytego kontrolera administracyjnego modułu.
4. Wyczyść pamięć panelu administracyjnego i wykonaj twarde odświeżenie.
5. Sprawdź rejestrację modułu w `displayAdminProductsExtra` oraz
   `displayBackOfficeHeader`.
6. Przejrzyj logi PrestaShop i PHP pod kątem błędów z `coolvideo`.

## Odrzucony adres URL

Użyj pełnego adresu `http://` lub `https://`, najlepiej HTTPS. Adres musi
wskazywać jeden film i zawierać identyfikator w rozpoznawanym miejscu.

Wypróbuj format kanoniczny:

```text
https://www.youtube.com/watch?v=VIDEO_ID
https://vimeo.com/123456789
https://www.dailymotion.com/video/VIDEO_ID
```

Nie używaj bezpośredniego adresu MP4, playlisty, kanału, wyniku wyszukiwania
ani skracacza linków innego niż `youtu.be` lub `dai.ly`. Usuń dodatkowy tekst
skopiowany przed adresem lub po nim. Jeśli link udostępniania dostawcy
przekierowuje, otwórz go w przeglądarce i skopiuj końcowy, kanoniczny adres
filmu.

## Problemy z miniaturami

Cool Video tworzy zdalne adresy miniaturek. Nie pobiera ani nie zapisuje obrazu
lokalnie.

Sprawdź dostęp do właściwego hosta:

| Dostawca | Host miniatury |
| --- | --- |
| YouTube | `img.youtube.com` |
| Vimeo | `vumbnail.com` |
| Dailymotion | `www.dailymotion.com` |

Restrykcyjna Content Security Policy musi zezwalać na te hosty w `img-src`.
Filtry prywatności, blokery reklam, filtrowanie DNS lub blokada regionalna też
mogą ukryć miniaturę. Upewnij się, że sam film nadal istnieje.

## Problemy z odtwarzaniem

Otwórz stronę filmu u dostawcy i sprawdź, czy jest publiczny, dostępny w regionie
odwiedzającego i może być odtwarzany w osadzonym iframe. Ograniczeń dostawcy
dotyczących prywatności, wieku, praw własności lub osadzania nie można obejść
za pomocą Cool Video.

Restrykcyjna Content Security Policy musi zezwalać na właściwy host odtwarzacza
w `frame-src`:

```text
https://www.youtube-nocookie.com
https://player.vimeo.com
https://www.dailymotion.com
```

Sprawdź także narzędzia zgód na pliki cookie. Niektóre z nich celowo blokują
zewnętrzne iframe'y, dopóki odwiedzający nie zaakceptuje kategorii multimediów
lub marketingu. Skonfiguruj narzędzie tak, aby zastąpiło lub zwolniło iframe
Cool Video po udzieleniu zgody.

## Problemy z galerią lub modalem

1. Sprawdź, czy film jest aktywny.
2. Wyczyść pamięć PrestaShop i pamięci łączonych zasobów.
3. Tymczasowo wyłącz opóźnianie, `defer` i optymalizację JavaScript w sklepie
   stagingowym.
4. Sprawdź błędy konsoli przeglądarki przed wybraniem filmu i po nim.
5. Ustal, czy strona zawiera galerię Classic, karuzelę produktu Hummingbird czy
   punkt trybu zgodności `data-coolvideo-mount`.
6. Sprawdź, czy motyw renderuje przynajmniej jeden standardowy hook produktu
   używany przez moduł.
7. Przetestuj oryginalną galerię motywu bez nadpisań i zmian page buildera.

Gdy Cool Video nie może zintegrować się ze znaną galerią, potrafi wyświetlić
ogólny rząd przycisków filmów. W tym trybie filmy otwierają się w oddzielnym
responsywnym modalu, a ich pozycja liczbowa nie może dokładnie przeplatać ich
z miniaturami zdjęć.

## Problemy z listami produktów

Dla każdego produktu sprawdź wszystkie poniższe warunki:

- film jest aktywny;
- **Show on product listings** jest włączone;
- zapisana pozycja galerii wynosi dokładnie `1`;
- dla przewidywalnego wyniku tylko jeden film listy ma pozycję `1`;
- oglądana strona jest listą, a nie stroną szczegółów produktu;
- dostępne są JavaScript i `fetch`;
- karta produktu zawiera `data-id-product` lub obsługiwany kod karty produktu;
- endpoint listy w tej samej domenie nie jest blokowany przez pamięć podręczną,
  WAF ani regułę bezpieczeństwa.

Moduł wysyła najwyżej 100 unikalnych identyfikatorów produktów w jednym
żądaniu listy. Niestandardowy mechanizm przewijania nieskończonego lub kod page
buildera może wymagać integracji właściwej dla danego motywu.

## Problemy z autoodtwarzaniem

Autoodtwarzanie jest żądaniem, a nie gwarancją. Sprawdź, czy **Autoplay
(muted)** jest włączone i czy film jest początkowym lub aktywnym elementem.
Przetestuj w prywatnym oknie z wyłączonymi rozszerzeniami.

Przeglądarka lub urządzenie może zablokować autoodtwarzanie ze względu na
preferencje użytkownika, tryb oszczędzania energii lub danych, wymaganie
wcześniejszej interakcji, uprawnienia iframe albo zasady dostawcy. Ręczny wybór
powinien nadal uruchomić odtwarzanie. Cool Video zawsze żąda wyciszonego
autoodtwarzania; dźwięk można włączyć w odtwarzaczu dostawcy.

## Zmiany nie są widoczne

Wyczyść pamięci w tej kolejności:

1. Pamięć PrestaShop w **Advanced Parameters > Performance**.
2. Pamięć CCC dla CSS i JavaScript.
3. Pamięć motywu lub page buildera.
4. Pamięć reverse proxy lub hostingu.
5. Pamięć CDN.
6. Pamięć przeglądarki, a następnie twarde odświeżenie.

Jeśli zainstalowano service workera, zaktualizuj go lub wyrejestruj
w przeglądarce testowej. Sprawdź, czy strona ładuje bieżącą wersję CSS
i JavaScript Cool Video.

## Przygotowanie użytecznego zgłoszenia

Dołącz:

- wersję Cool Video i rodzaj pakietu;
- wersję PrestaShop;
- wersję PHP i informację, czy PHP obsługujący stronę ma włączony cURL;
- nazwę i wersję motywu oraz używany page builder;
- adresy URL produktu i listy, których dotyczy problem;
- dostawcę i dokładny adres URL filmu;
- oczekiwany i rzeczywisty wynik;
- dokładne kroki odtworzenia problemu;
- typ urządzenia i wersję przeglądarki;
- istotne błędy konsoli i żądań sieciowych przeglądarki;
- istotne wpisy logów PrestaShop, PHP i serwera WWW;
- zrzut ekranu lub krótkie nagranie ekranu.

Przy problemach z aktywacją podaj wyświetlaną znormalizowaną domenę sklepu,
stan licencji, kod lub treść błędu i zamaskowany klucz. Nigdy nie podawaj
pełnego klucza aktywacyjnego ani danych logowania do panelu.

