# Dokumentacja techniczna

Ten dokument opisuje edycję Cool Video Netteria License 1.4.10 sprzedawaną
bezpośrednio przez
[prestaexpert.pl](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html).
Jest przeznaczony dla administratorów sklepów, integratorów, dostawców hostingu
i pracowników wsparcia technicznego.

## Identyfikacja modułu

| Właściwość | Wartość |
| --- | --- |
| Nazwa techniczna | `coolvideo` |
| Wersja sprzedaży bezpośredniej | `1.4.10` |
| Nazwa wyświetlana | Cool Video Product - Netteria License |
| Wydawca | Netteria.NET |
| Produkt i kanał sprzedaży | `prestaexpert.pl` |
| Zgodność z PrestaShop | 1.7.x, 8.x i 9.x |
| Główne działanie | Dodawanie filmów YouTube, Vimeo i Dailymotion do galerii produktów i odpowiednich kart na listach produktów |
| Strategia obsługi motywów | Natywny adapter Classic, natywny adapter Hummingbird, a następnie ogólny tryb zgodności oparty na standardowych hookach |
| Przesyłanie lokalnego filmu | Nieobsługiwane w wersji 1.4.10 |

Repozytorium zawiera również dystrybucje Marketplace i deweloperskie. Ich
zasady aktywacji mogą się różnić. Ten dokument dotyczy pakietu sprzedaży
bezpośredniej przypisanego do domeny.

## Wymagania środowiska

- Wersje PHP oraz MySQL lub MariaDB obsługiwane przez zainstalowane wydanie
  PrestaShop.
- PHP cURL do weryfikacji licencji sprzedaży bezpośredniej.
- Wychodzący dostęp HTTPS po stronie serwera do `prestaexpert.pl`.
- Zapisywalny katalog pamięci podręcznej modułu zapewniający wydajne
  buforowanie statusu licencji.
- JavaScript w sklepie i przeglądarka z `fetch` do pobierania danych na listach
  produktów.
- Motyw korzystający z Classic, Hummingbird lub standardowych hooków produktów
  PrestaShop.

Adapter sklepu nie wymaga jQuery, a moduł nie dodaje nadpisań klas PrestaShop.

## Przechowywane dane

Instalacja tworzy poniższą tabelę, gdzie `{prefix}` oznacza skonfigurowany
prefiks bazy danych PrestaShop:

```text
{prefix}coolvideo_product_video
```

Każde powiązanie przechowuje:

| Pole | Zastosowanie |
| --- | --- |
| Identyfikator produktu | Wiąże wiersz z produktem PrestaShop |
| Oryginalny adres URL | Zachowuje adres wprowadzony przez sprzedawcę |
| Dostawca i identyfikator filmu | Identyfikuje materiał YouTube, Vimeo lub Dailymotion |
| Wygenerowany tytuł i opis | Zapewnia dostępną etykietę odtwarzacza i opcjonalny tekst |
| Adres URL miniatury | Wskazuje zdalną miniaturę właściwą dla dostawcy |
| Pozycja | Ustala kolejność filmu w multimediach produktu, zaczynając od 1 |
| Aktywność | Steruje całą widocznością filmu w sklepie |
| Autostart | Żąda wyciszonego autoodtwarzania aktywnego filmu galerii |
| Wyświetlanie na liście | Pozwala wyświetlać na liście film z pozycji 1 |
| Szerokość i wysokość | Przechowuje starsze wymiary osadzenia; widocznym odtwarzaczem steruje układ responsywny |
| Znaczniki czasu utworzenia i aktualizacji | Rejestrują daty cyklu życia powiązania |

Wiersze są odczytywane według rosnącej pozycji, a następnie rosnącego
wewnętrznego identyfikatora wiersza filmu. Usunięcie produktu usuwa powiązane
wiersze Cool Video. Odinstalowanie modułu usuwa całą tabelę.

## Parsowanie obsługiwanych adresów URL

Parser przyjmuje wyłącznie adresy `http` i `https` o długości nieprzekraczającej
500 znaków. Dostawca i identyfikator filmu są wyznaczane następująco:

| Dostawca | Akceptowane hosty i ścieżki | Walidacja identyfikatora |
| --- | --- | --- |
| YouTube | `youtu.be/{id}`; `youtube.com/watch?v={id}`; `/embed/{id}`; `/shorts/{id}`; `/live/{id}`; mobilne i muzyczne hosty watch | Od 6 do 20 liter, cyfr, podkreśleń lub łączników |
| Vimeo | `vimeo.com/{numeric-id}` oraz `player.vimeo.com/video/{numeric-id}` | Od 1 do 20 cyfr |
| Dailymotion | `dai.ly/{id}`; `dailymotion.com/video/{id}`; `/embed/video/{id}`; obsługiwany host regionalny | Od 4 do 20 liter lub cyfr |

Czas rozpoczęcia z parametrów zapytania i inne parametry niezwiązane
z identyfikatorem nie są zachowywane w wygenerowanym adresie osadzenia.
Bezpośrednie pliki i inni dostawcy są odrzucani.

## Generowane adresy zewnętrzne

| Zastosowanie | Host lub wzorzec adresu URL |
| --- | --- |
| Odtwarzacz YouTube | `https://www.youtube-nocookie.com/embed/{id}?rel=0` |
| Miniatura YouTube | `https://img.youtube.com/vi/{id}/hqdefault.jpg` |
| Odtwarzacz Vimeo | `https://player.vimeo.com/video/{id}` |
| Miniatura Vimeo | `https://vumbnail.com/{id}.jpg` |
| Odtwarzacz Dailymotion | `https://www.dailymotion.com/embed/video/{id}` |
| Miniatura Dailymotion | `https://www.dailymotion.com/thumbnail/video/{id}` |

Autoodtwarzanie dodaje parametry zapytania właściwe dla dostawcy, sterujące
autoodtwarzaniem i wyciszeniem. Każdy iframe dopuszcza autoodtwarzanie,
zaszyfrowane multimedia, obraz w obrazie i pełny ekran.

## Zarejestrowane hooki

| Hook | Zastosowanie |
| --- | --- |
| `displayBackOfficeHeader` | Ładuje CSS i JavaScript administracji filmami produktów |
| `displayAdminProductsExtra` | Renderuje menedżer filmów w edytorze produktu |
| `displayHeader` | Ładuje zasoby sklepu i udostępnia konfigurację produktu lub listy |
| `displayProductExtraContent` | Dodaje aktywne filmy do standardowego obszaru dodatkowej zawartości Videos |
| `displayAfterProductThumbs` | Udostępnia ukryty punkt integracji obok miniaturek produktu |
| `displayFooterProduct` | Udostępnia drugi punkt standardowego hooka dla szerszej zgodności motywów |
| `actionObjectProductDeleteAfter` | Usuwa powiązania po usunięciu produktu |

Procedury instalacji i aktualizacji próbują zarejestrować każdy wymagany hook,
nawet jeśli jeden starszy hook zgłosi błąd. Dzięki temu kolejna próba może
przywrócić pełny stan.

## Operacje panelu administracyjnego

Ukryty kontroler `AdminCoolvideoProductVideo` obsługuje operacje AJAX w tej
samej domenie: dodawanie, usuwanie, przełączanie i zmianę pozycji. Żądania
modyfikujące muszą:

- używać metody HTTP POST;
- przejść standardowe uwierzytelnienie administracyjne PrestaShop i kontrolę
  tokenu;
- pochodzić od profilu pracownika z prawem edycji;
- odnosić się do filmu należącego do przekazanego identyfikatora produktu;
- przejść weryfikację aktywnej licencji sprzedaży bezpośredniej.

Pozycja wejściowa musi być liczbą całkowitą od 1 do 10000. Adres dostawcy jest
parsowany i weryfikowany po stronie serwera przed dodaniem wiersza.

## Endpoint list produktów

Kontroler frontowy udostępnia akcję tylko do odczytu w tej samej domenie,
podobną do:

```text
/module/coolvideo/ajax?ajax=1&action=GetListingVideos&product_ids=12,34,56
```

Endpoint:

- wymaga poprawnej licencji sprzedaży bezpośredniej;
- przyjmuje najwyżej 100 unikalnych dodatnich identyfikatorów produktów;
- zwraca najwyżej jeden kwalifikujący się wiersz dla produktu;
- zwraca wyłącznie aktywne wiersze z włączonym wyświetlaniem na listach
  i pozycją `1`;
- wysyła nagłówki `no-store`, ponieważ kwalifikacja do listy zmienia się wraz
  z pozycją galerii.

Adapter przeglądarkowy obserwuje dynamiczne zmiany kart produktów, aby ponownie
zastosować elementy sterujące po nawigacji fasetowej lub zgodnych
aktualizacjach przewijania nieskończonego.

## Adaptery galerii

### Adapter Classic

Adapter lokalizuje standardowe listy miniaturek głównych i modalnych, wstawia
filmy do wspólnej kolejności multimediów, synchronizuje wymiary miniaturek
i zastępuje zdjęcie okładki responsywnym iframe po wybraniu filmu.

### Adapter Hummingbird

Adapter tworzy slajdy i miniatury filmów w karuzeli, ponownie oblicza indeksy
multimediów, synchronizuje aktywne slajdy i rozszerza oparty na Bootstrapie
modal multimediów produktu.

### Adapter ogólny

Gdy żadna znana struktura nie jest dostępna, moduł odnajduje punkt standardowego
hooka albo rozpoznaną kotwicę galerii i renderuje oddzielną grupę przycisków
filmów. Przyciski korzystają z dostępnego, responsywnego modalu modułu. Adapter
ogólny nie gwarantuje dokładnego przeplatania filmów z miniaturami zdjęć
motywu.

### Adapter list produktów

Rozpoznawane karty produktów otrzymują przycisk nad obszarem zdjęcia lub
72-pikselowy przycisk w rogu, zależnie od dostępnego kodu. Wybranie go otwiera
modal modułu i żąda odtwarzania. Adapter przetwarza do 100 identyfikatorów
produktów w jednym żądaniu.

## Implementacja licencji

Edycja sprzedaży bezpośredniej zapisuje klucz aktywacyjny w następującym kluczu
konfiguracji PrestaShop:

```text
NETTERIA_LICENSE_COOLVIDEO
```

Weryfikacja korzysta z żądań HTTPS POST po stronie serwera wysyłanych do:

```text
https://prestaexpert.pl/modules/netterialicenseprovisioner/api/v1/validate.php
```

Żądanie identyfikuje klucz licencji, znormalizowany host sklepu i techniczną
nazwę modułu. Znormalizowany host jest zapisany małymi literami i nie zawiera
protokołu, portu, ścieżki, końcowej kropki ani początkowego `www.`. Domeny
umiędzynarodowione są konwertowane do ASCII, jeśli dostępna jest funkcja
internacjonalizacji PHP.

Działanie pamięci podręcznej:

| Wynik | Okres pamięci lub ponowienia |
| --- | --- |
| Poprawny | 24 godziny |
| Nieprawidłowy | 5 minut |
| API niedostępne | 5 minut |
| Okres offline po wcześniejszej poprawnej weryfikacji | Do 7 dni od ostatniej weryfikacji online |

Nazwa pliku pamięci zawiera skrót adresu API, nazwy modułu, identyfikatora
sklepu, domeny i klucza licencji. Pełny klucz nie jest zapisywany w pamięci
statusu JSON. Formularz licencji wyświetla zamaskowaną wersję skonfigurowanego
klucza.

## Content Security Policy

Restrykcyjna polityka powinna zezwalać na dokładne hosty dostawców używane
przez sklep. Przykładowy fragment:

```text
frame-src 'self' https://www.youtube-nocookie.com https://player.vimeo.com https://www.dailymotion.com;
img-src 'self' data: https://img.youtube.com https://vumbnail.com https://www.dailymotion.com;
connect-src 'self';
```

Połącz te hosty z istniejącą polityką zamiast kopiować fragment jako kompletną
politykę. Weryfikację licencji wykonuje PHP cURL po stronie serwera, więc
kontroluje ją zapora serwera, a nie CSP przeglądarki.

## Prywatność i usługi zewnętrzne

Baza sklepu zapisuje adres podany przez sprzedawcę i wyprowadzone metadane,
a nie treść filmu. Przeglądarki odwiedzających mogą łączyć się z hostami
miniaturek i odtwarzaczy dostawców. Usługi te mogą otrzymywać metadane sieciowe
oraz stosować własne pliki cookie, śledzenie, zasady prywatności, ograniczenia
wieku i regionu.

Sprawdź politykę prywatności sklepu i konfigurację menedżera zgód dla wybranych
dostawców. YouTube korzysta z hosta odtwarzacza o podwyższonej prywatności
`youtube-nocookie.com`, ale wymagania nadal zależą od jurysdykcji i polityki
sklepu.

## Cykl życia i odzyskiwanie

- **Wyłączenie:** zatrzymuje działanie modułu, zwykle zachowując zapisane
  wiersze.
- **Włączenie:** przywraca działanie, jeśli licencja i hooki są poprawne.
- **Aktualizacja w miejscu:** uruchamia aktualizacje schematu i procedury
  odzyskiwania oraz zachowuje istniejące wiersze, jeśli zakończy się poprawnie.
- **Odinstalowanie:** usuwa tabelę powiązań, kartę administracyjną, konfigurację
  aktywacji i pamięć licencji.
- **Usunięcie produktu:** usuwa wiersze powiązane z produktem.

Przed aktualizacją lub odinstalowaniem wykonaj kopię bazy danych. Nie używaj
odinstalowania jako procedury aktualizacji.

## Limity operacyjne i ostrzeżenia

- Jeden adres URL może identyfikować tylko jeden film obsługiwanego dostawcy.
- Długość adresu URL jest ograniczona do 500 znaków.
- Zakres pozycji w panelu administracyjnym wynosi od 1 do 10000.
- Jedno żądanie listy może obejmować najwyżej 100 unikalnych identyfikatorów
  produktów.
- Do wyświetlenia na karcie produktu kwalifikuje się tylko aktywny film
  z włączoną opcją listy i pozycją 1.
- Moduł nie sprawdza z wyprzedzeniem, czy dostawca pozwala osadzać film.
- Dostępnością zdalnej miniatury steruje dostawca filmu lub usługi miniaturek.
- Autoodtwarzanie podlega zasadom przeglądarki, urządzenia, zgód i dostawcy.
- Motyw niestandardowy może wymagać dostosowania selektorów lub układu.

## Przekazanie zgłoszenia do wsparcia

Aby sprawnie przekazać problem techniczny, podaj wersję modułu, adresy stron,
których dotyczy problem, informacje o motywie i optymalizatorze, kroki
odtworzenia, błędy konsoli i sieci, odpowiednie logi serwera oraz wyświetlany
stan licencji. Zamaskuj dane logowania i klucze aktywacyjne.

W sprawach wsparcia licencjonowanego pakietu, aktualizacji i przypisania domeny
skorzystaj z oficjalnej
[strony produktu Cool Video](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html).

