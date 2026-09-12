# Instrukcja użytkownika

Ta instrukcja wyjaśnia, jak zarządzać Cool Video po zainstalowaniu i aktywacji
pakietu sprzedawanego bezpośrednio. Wymagania konfiguracyjne opisuje
[instrukcja instalacji i aktywacji](INSTALLATION_PL.md).

## Otwarcie menedżera filmów

1. Zaloguj się do panelu administracyjnego PrestaShop.
2. Otwórz **Catalog > Products** (Katalog > Produkty).
3. Edytuj wybrany produkt.
4. Jeśli jest to nowy produkt, zapisz go raz, aby PrestaShop nadał mu
   identyfikator, a następnie ponownie otwórz lub odśwież edytor.
5. Otwórz sekcję **Modules** produktu i znajdź Cool Video.

Dokładne położenie sekcji **Modules** nieznacznie różni się między PrestaShop
1.7, 8 i 9. Jeśli zamiast pola URL menedżer pokazuje ostrzeżenie o licencji,
najpierw otwórz konfigurację modułu i aktywuj licencję.

## Obsługiwane adresy URL filmów

Cool Video 1.4.10 przyjmuje publiczny adres URL jednego filmu od jednego
z poniższych dostawców.

| Dostawca | Obsługiwane przykłady |
| --- | --- |
| YouTube | `https://www.youtube.com/watch?v=VIDEO_ID` |
| Skrócony adres YouTube | `https://youtu.be/VIDEO_ID` |
| Osadzony YouTube | `https://www.youtube.com/embed/VIDEO_ID` |
| YouTube Shorts | `https://www.youtube.com/shorts/VIDEO_ID` |
| YouTube Live | `https://www.youtube.com/live/VIDEO_ID` |
| Vimeo | `https://vimeo.com/123456789` |
| Odtwarzacz Vimeo | `https://player.vimeo.com/video/123456789` |
| Dailymotion | `https://www.dailymotion.com/video/VIDEO_ID` |
| Osadzony Dailymotion | `https://www.dailymotion.com/embed/video/VIDEO_ID` |
| Skrócony adres Dailymotion | `https://dai.ly/VIDEO_ID` |

Rozpoznawane są również mobilne adresy YouTube z `m.youtube.com` i adresy
YouTube Music z `music.youtube.com`. Używaj bezpośredniego adresu pojedynczego
filmu.

W wersji 1.4.10 nie są obsługiwane:

- bezpośrednie adresy plików MP4, MOV, WebM ani innych plików wideo;
- przesyłanie lokalnego pliku wideo do PrestaShop;
- playlisty, kanały, wyniki wyszukiwania YouTube i adresy bez identyfikatora
  filmu;
- ogólne strony profilu, prezentacji lub kolekcji Vimeo;
- ogólne strony kanałów i playlist Dailymotion;
- nieobsługiwane przekierowania i linki śledzące, które nie zawierają
  identyfikatora filmu w rozpoznawanym formacie.

Film źródłowy musi pozwalać na osadzanie i być dostępny dla odwiedzających,
którzy będą go oglądać. Film prywatny, usunięty, ograniczony wiekowo lub
regionalnie albo z wyłączonym osadzaniem może mieć poprawną miniaturę, ale
odmówić odtwarzania.

## Dodawanie filmu

1. Skopiuj publiczny adres strony jednego obsługiwanego filmu.
2. Wklej go do pola **Video URL** w panelu Cool Video.
3. Wybierz **Add video**.
4. Poczekaj na komunikat powodzenia i odświeżenie strony.
5. Sprawdź, czy pojawiła się karta filmu z miniaturą, nazwą dostawcy,
   wygenerowanym tytułem i identyfikatorem filmu dostawcy.

Cool Video wyznacza z adresu dostawcę, identyfikator, adres osadzenia i adres
miniatury. W wersji 1.4.10 wygenerowanego tytułu i opisu nie edytuje się
w panelu produktu.

Nowe filmy otrzymują następujące wartości domyślne:

| Ustawienie | Wartość domyślna |
| --- | --- |
| **Gallery position** | Następna pozycja po istniejących wpisach Cool Video tego produktu |
| **Active** | Włączone |
| **Autoplay (muted)** | Wyłączone |
| **Show on product listings** | Wyłączone |
| Proporcje odtwarzacza | Responsywne osadzenie 16:9 w odtwarzaczach Classic i trybu zgodności |

## Elementy karty filmu

| Element | Działanie | Sposób zapisu |
| --- | --- | --- |
| **Gallery position** | Umieszcza film między zdjęciami produktu i innymi filmami | Po wpisaniu liczby całkowitej od 1 do 10000 wybierz **Save position** |
| **Active** | Pokazuje lub ukrywa film w sklepie | Zapisywane natychmiast po przełączeniu |
| **Autoplay (muted)** | Żąda wyciszonego autoodtwarzania, gdy film staje się początkowym lub aktywnym elementem galerii | Zapisywane natychmiast po przełączeniu |
| **Show on product listings** | Pozwala wyświetlić film z pozycji 1 na rozpoznawanych kartach produktów | Zapisywane natychmiast po przełączeniu |
| **Delete** | Trwale usuwa powiązanie filmu z produktem | Wymaga potwierdzenia i nie można go cofnąć |

Jeśli przełącznika nie da się zapisać, wraca on do poprzedniej wartości,
a panel administracyjny wyświetla komunikat błędu.

## Ustawianie pozycji w galerii

Pozycje są wspólne dla zdjęć i filmów produktu oraz zaczynają się od `1`.

Dla produktu z trzema zdjęciami A, B i C:

| Pozycja filmu | Wynikowa kolejność |
| --- | --- |
| `1` | Film, zdjęcie A, zdjęcie B, zdjęcie C |
| `2` | Zdjęcie A, film, zdjęcie B, zdjęcie C |
| `3` | Zdjęcie A, zdjęcie B, film, zdjęcie C |
| `4` lub więcej | Zdjęcie A, zdjęcie B, zdjęcie C, film |

W motywach Classic i Hummingbird film jest wstawiany do wspólnej kolejności
multimediów. Film z pozycji 1 staje się początkowym elementem galerii po
otwarciu strony produktu. W motywie niestandardowym korzystającym z ogólnego
trybu zgodności filmy pojawiają się w oddzielnym rzędzie miniaturek obok
galerii, dlatego dokładna pozycja między zdjęciami może nie być dostępna.

Jeśli przewidywalna kolejność ma znaczenie, nadaj każdemu filmowi unikalną
pozycję. Gdy kilka filmów ma tę samą pozycję, o kolejności decyduje wewnętrzna
kolejność ich utworzenia, która może różnić się od oczekiwanej.

## Filmy aktywne i nieaktywne

Pozostaw **Active** włączone, aby renderować film w galerii, natywnym modalu
multimediów, dodatkowej zakładce Videos, ogólnym trybie zgodności i na
kwalifikującej się karcie produktu.

Wyłącz **Active**, aby ukryć film bez usuwania jego powiązania. Adres URL,
pozycja i opcje pozostają zapisane. Film można później przywrócić przez ponowne
włączenie przełącznika.

Usunięcie filmu różni się od jego wyłączenia. **Delete** usuwa wiersz z bazy
danych i tej operacji nie można cofnąć w interfejsie modułu.

## Działanie autoodtwarzania

Opcja **Autoplay (muted)** nakazuje Cool Video zażądać wyciszonego odtwarzania,
gdy film staje się początkowym lub aktywnym elementem galerii. Dźwięk jest
wyciszany, ponieważ współczesne przeglądarki zwykle blokują słyszalne
autoodtwarzanie.

Ważne zachowania:

- jeśli film z pozycji 1 ma włączone autoodtwarzanie, Cool Video próbuje go
  uruchomić, gdy galeria otwiera się na tym filmie;
- ręczne wybranie miniatury filmu uruchamia odtwarzanie, nawet gdy opcja
  autoodtwarzania jest wyłączona;
- ręczne otwarcie filmu z listy lub modalu również rozpoczyna odtwarzanie;
- przeglądarka, urządzenie, rozszerzenie prywatności, narzędzie zgód lub
  dostawca filmu nadal mogą zablokować autoodtwarzanie;
- Cool Video nie wymusza dźwięku. Po rozpoczęciu odtwarzania odwiedzający może
  włączyć go w odtwarzaczu dostawcy.

Aby zapewnić najmniej inwazyjne działanie sklepu, pozostaw autoodtwarzanie
wyłączone, chyba że prezentacja produktu wyraźnie na nim zyskuje.

## Wyświetlanie filmu na listach produktów

Opcja listy może dodać miniaturę filmu lub przycisk na rozpoznawanych kartach
produktów w kategoriach, wynikach wyszukiwania i na innych listach. Wybranie
przycisku otwiera responsywny modal i uruchamia film.

Wymagane są wszystkie trzy warunki:

1. **Active** jest włączone.
2. **Show on product listings** jest włączone.
3. **Gallery position** ma dokładnie wartość `1`.

Dla każdej karty produktu zwracany jest tylko jeden kwalifikujący się film.
Aby uzyskać przewidywalny wynik, włącz opcję listy tylko dla jednego filmu
produktu i pozostaw go jako jedyny film na pozycji `1`.

W zależności od kodu motywu element filmu może pokrywać obszar zdjęcia produktu
albo pojawić się jako mniejszy przycisk w jego dolnym rogu. Jeśli nie jest
widoczny w motywie niestandardowym, zobacz
[rozwiązywanie problemów](TROUBLESHOOTING_PL.md).

## Działanie w sklepie zależnie od motywu

### Classic

- Miniatury filmów są wstawiane do standardowego paska miniaturek.
- Wybranie filmu zastępuje główne zdjęcie produktu responsywnym odtwarzaczem.
- Filmy są również dodawane do natywnego modalu multimediów produktu.
- Wybranie zwykłego zdjęcia usuwa aktywny odtwarzacz i przywraca zdjęcie.

### Hummingbird

- Slajdy i miniatury filmów są dodawane do karuzeli produktu.
- Aktywny element multimediów i odtwarzacz dostawcy są synchronizowane
  z karuzelą.
- Natywny modal multimediów otrzymuje tę samą uporządkowaną listę zdjęć
  i filmów.

### Zgodne motywy niestandardowe

Cool Video najpierw szuka znanej struktury Classic lub Hummingbird. Jeśli
żadnej nie znajdzie, używa standardowych hooków produktu, aby umieścić
oddzielny rząd przycisków filmów obok galerii. Wybranie przycisku otwiera
własny responsywny modal Cool Video. Mocno zmodyfikowane motywy, które pomijają
standardowe hooki lub korzystają z nierozpoznawanego kodu kart produktów, mogą
wymagać integracji przygotowanej dla danego motywu.

### Dodatkowa zakładka Videos

Gdy motyw wyświetla dodatkową zawartość produktu PrestaShop, aktywne filmy są
również dostępne w zakładce lub sekcji **Videos**. Zapewnia to dodatkową drogę
dostępu, nawet jeśli adapter galerii ma ograniczenia wynikające z kodu motywu.

## Zarządzanie wieloma filmami

Do jednego produktu można dodać wiele obsługiwanych filmów. Praktyczna
kolejność pracy:

1. Umieść najważniejszą prezentację produktu jako pierwszą.
2. Dodaj dalej w galerii filmy o instalacji, rozmiarze, pielęgnacji lub
   porównaniu.
3. Nadaj każdemu filmowi unikalną pozycję.
4. Włącz wyświetlanie na listach tylko dla jednego filmu z pozycji 1.
5. Przed usunięciem nieaktualnej treści najpierw ją wyłącz, aby bezpiecznie
   sprawdzić sklep.
6. Po zmianie kilku pozycji sprawdź działanie na komputerze, urządzeniu
   mobilnym i w modalu.

W wersji 1.4.10 nie ma sortowania metodą przeciągnij i upuść. Wpisz wartość
liczbową na każdej karcie filmu i wybierz **Save position**.

## Wydajność, prywatność i zgody

Strona produktu pobiera miniatury dostawcy, zanim odwiedzający uruchomi film.
Iframe dostawcy jest tworzony wtedy, gdy potrzebuje go galeria lub modal,
natomiast dodatkowa zakładka korzysta z iframe'ów ładowanych leniwie. Strony
list produktów pobierają dane kwalifikujących się filmów z tego samego sklepu
i dodają elementy sterujące tylko do rozpoznawanych kart produktów.

Odtwarzanie i miniatury powodują żądania sieciowe do domen zewnętrznych
dostawców. Sprawdź politykę prywatności sklepu, konfigurację zgód na pliki
cookie i Content Security Policy. YouTube korzysta z domeny osadzania
`youtube-nocookie.com`, ale nie usuwa to wszystkich obowiązków związanych
z prywatnością lub zgodami.

## Usuwanie filmu

1. Otwórz panel Cool Video wybranego produktu.
2. Znajdź właściwego dostawcę, miniaturę i identyfikator filmu.
3. W razie wątpliwości wyłącz **Active** i najpierw sprawdź sklep.
4. Wybierz **Delete**.
5. Potwierdź komunikat.
6. Sprawdź stronę produktu i listę produktów.

Usunięcie dotyczy wyłącznie powiązania w PrestaShop. Nie usuwa oryginalnego
filmu z YouTube, Vimeo ani Dailymotion.

