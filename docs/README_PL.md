# Dokumentacja klienta Cool Video

| Element | Szczegóły |
| --- | --- |
| Produkt | Cool Video: wideo w galerii produktu i autoodtwarzanie |
| Edycja | Edycja Netteria License 1.4.10 sprzedawana bezpośrednio |
| Sprzedawca i kanał wsparcia | [prestaexpert.pl](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html) |
| Wydawca | Netteria.NET |
| Wersja dokumentacji | 1.0, 12 września 2026 r. |

> Ta dokumentacja dotyczy licencjonowanego pakietu kupionego w
> prestaexpert.pl. Pakiety Marketplace i wersje deweloperskie mogą nie
> wyświetlać ekranu aktywacji licencji, ale podstawowy sposób zarządzania
> filmami pozostaje taki sam.

## Co robi Cool Video

Cool Video pozwala sprzedawcy dodawać zewnętrznie hostowane filmy do galerii
produktu PrestaShop bez edytowania szablonów motywu i bez wklejania kodu
osadzającego. Moduł:

- rozpoznaje obsługiwane adresy URL YouTube, Vimeo i Dailymotion;
- tworzy miniaturę filmu i umieszcza ją między zdjęciami produktu;
- pozwala dodać kilka filmów do jednego produktu;
- umożliwia włączanie i ukrywanie poszczególnych filmów;
- może próbować uruchomić wyciszone autoodtwarzanie, gdy film staje się
  aktywnym elementem galerii;
- może wyświetlać film z pozycji 1 na kartach produktów w kategoriach,
  wynikach wyszukiwania i innych listach produktów;
- integruje się bezpośrednio z galeriami Classic i Hummingbird oraz udostępnia
  oddzielny tryb zgodności dla kompatybilnych motywów niestandardowych;
- wyświetla responsywne odtwarzacze na komputerach, tabletach i urządzeniach
  mobilnych.

Filmy pozostają na serwerach swoich dostawców. Moduł zapisuje adres URL,
dostawcę, identyfikator filmu, wygenerowany adres miniatury, pozycję i opcje
wyświetlania. Nie kopiuje pliku wideo na serwer sklepu.

## Zestaw dokumentacji

| Dokument | Zastosowanie |
| --- | --- |
| [Instalacja i aktywacja](INSTALLATION_PL.md) | Wymagania, instalacja, aktywacja licencji, aktualizacja i usuwanie modułu |
| [Instrukcja użytkownika](USER_GUIDE_PL.md) | Dodawanie filmów, obsługiwane adresy URL, pozycje, autoodtwarzanie i listy produktów |
| [Rozwiązywanie problemów](TROUBLESHOOTING_PL.md) | Problemy z licencją, adresem URL, galerią, miniaturą, autoodtwarzaniem, listami i motywem |
| [Dokumentacja techniczna](TECHNICAL_REFERENCE_PL.md) | Hooki, przechowywanie danych, endpointy, zewnętrzne hosty, bezpieczeństwo, prywatność i limity |

## Konfiguracja w pięć minut

1. Pobierz licencjonowany pakiet ZIP Cool Video dostarczony po zakupie w
   [prestaexpert.pl](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html).
2. W panelu administracyjnym PrestaShop otwórz **Modules > Module Manager**
   (Moduły > Menedżer modułów), wybierz **Upload a module** i prześlij plik ZIP
   bez jego rozpakowywania.
3. Otwórz **Configure** dla Cool Video, wklej kod aktywacyjny otrzymany po
   zakupie i wybierz **Activate license**.
4. Sprawdź, czy wyświetla się status **License active** oraz czy wartość
   **Shop domain** odpowiada domenie przypisanej do klucza.
5. Otwórz **Catalog > Products** (Katalog > Produkty), edytuj zapisany produkt
   i znajdź Cool Video w sekcji **Modules** produktu.
6. Wklej obsługiwany publiczny adres URL filmu i wybierz **Add video**.
7. Ustaw odpowiednio **Gallery position**, **Active**, **Autoplay (muted)**
   oraz **Show on product listings**.
8. Sprawdź stronę produktu na komputerze i urządzeniu mobilnym. Jeśli włączono
   wyświetlanie na listach, sprawdź także stronę kategorii lub wyników
   wyszukiwania.

## Ważne informacje przed rozpoczęciem

- Wersja 1.4.10 obsługuje YouTube, Vimeo i Dailymotion.
- Bezpośrednie adresy MP4, przesyłanie plików wideo, playlisty, kanały oraz
  strony dostawcy, które nie wskazują jednego filmu, nie są obsługiwane.
- Nowo utworzony produkt należy przynajmniej raz zapisać, zanim Cool Video
  będzie mógł przypisać do niego film.
- Pozycje galerii obejmują zdjęcia i filmy oraz zaczynają się od `1`.
- Aby wyświetlić film na listach produktów, włącz go, zaznacz opcję listy
  i ustaw jego pozycję w galerii na `1`.
- Ręczne wybranie filmu rozpoczyna odtwarzanie również wtedy, gdy opcja
  autoodtwarzania jest wyłączona. Opcja ta steruje automatycznym odtwarzaniem,
  gdy film staje się początkowym lub aktywnym elementem galerii.
- Zasady przeglądarki i dostawcy nadal mogą zablokować autoodtwarzanie. Cool
  Video żąda odtwarzania bez dźwięku, aby spełnić typowe wymagania
  przeglądarek.
- Nie używaj odinstalowania jako metody aktualizacji. Odinstalowanie usuwa
  tabelę bazy danych zawierającą wszystkie powiązania produktów z filmami.

## Uzyskiwanie pomocy

Informacje o zakupie, licencji, aktualizacji i wsparciu znajdują się na
oficjalnej
[stronie produktu Cool Video](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html).

W zgłoszeniu problemu podaj wersję Cool Video, wersję PrestaShop i PHP, nazwę
i wersję motywu, adres URL produktu, dokładne kroki oraz zrzut ekranu.
W przypadku problemów z licencją podaj wyświetlaną domenę sklepu i wyłącznie
zamaskowany klucz. Nigdy nie wysyłaj pełnego klucza aktywacyjnego w publicznej
wiadomości.

