# Cool Video: wideo w galerii produktu i autoodtwarzanie

Cool Video dodaje zewnętrznie hostowane filmy z YouTube, Vimeo i Dailymotion
do galerii produktów PrestaShop. Sprzedawca zarządza filmami w edytorze
produktu, ustala ich pozycję między zdjęciami, włącza wyciszone
autoodtwarzanie i może wyświetlać film na kartach produktów na listach.

## Oficjalna strona produktu i kanał sprzedaży

Licencjonowana edycja dla klientów opisana w tym repozytorium jest sprzedawana
bezpośrednio przez
[prestaexpert.pl](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html).
Dostarczenie zakupionego modułu, aktywacja przypisana do domeny, aktualizacje
i wsparcie komercyjne tej edycji są realizowane przez PrestaExpert.

Repozytorium zawiera również pakiety przeznaczone do innych kanałów
dystrybucji. Mogą one korzystać z innych zasad aktywacji. Polska dokumentacja
klienta w katalogu [`docs/`](docs/README_PL.md) dotyczy sprzedawanej
bezpośrednio edycji Netteria License 1.4.10.

## Zgodność

- PrestaShop 1.7.x, 8.x i 9.x
- Adaptery galerii Classic i Hummingbird
- Oddzielny tryb zgodności dla motywów niestandardowych udostępniających
  standardowe hooki produktu
- Wersje PHP oraz MySQL lub MariaDB obsługiwane przez zainstalowaną wersję
  PrestaShop
- PHP cURL i wychodzący dostęp HTTPS wymagane do aktywacji edycji sprzedawanej
  bezpośrednio

## Dokumentacja klienta

- [Strona główna dokumentacji](docs/README_PL.md)
- [Instalacja i aktywacja](docs/INSTALLATION_PL.md)
- [Instrukcja użytkownika](docs/USER_GUIDE_PL.md)
- [Rozwiązywanie problemów](docs/TROUBLESHOOTING_PL.md)
- [Dokumentacja techniczna](docs/TECHNICAL_REFERENCE_PL.md)

## Ważne ograniczenia

- Wersja 1.4.10 przyjmuje adresy stron filmów z YouTube, Vimeo i Dailymotion.
  Nie przesyła ani nie odtwarza samodzielnie hostowanych plików MP4.
- Opcja wyświetlania na listach działa tylko dla aktywnego filmu przypisanego
  do pozycji `1` w galerii.
- Odinstalowanie modułu usuwa wszystkie zapisane powiązania produktów
  z filmami. Moduł należy aktualizować w miejscu, a przed odinstalowaniem
  wykonać kopię zapasową.

## Licencja

Licencję kodu źródłowego opisuje plik [`LICENSE.txt`](LICENSE.txt). Pakiet
sprzedawany bezpośrednio wymaga dodatkowo aktywnego klucza przypisanego do
domeny sklepu podanej przy zakupie.

