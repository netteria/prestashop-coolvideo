# Cool Video customer documentation

| Item | Details |
| --- | --- |
| Product | Cool Video: Product Gallery Videos and Autoplay |
| Edition | Direct-sale Netteria License edition 1.4.10 |
| Seller and support channel | [prestaexpert.pl](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html) |
| Publisher | Netteria.NET |
| Documentation revision | 1.0, 12 September 2026 |

> This documentation covers the licensed package purchased from
> prestaexpert.pl. Marketplace or development packages may not display the
> license activation screen, although the core video-management workflow is
> the same.

## What Cool Video does

Cool Video lets a merchant add externally hosted videos to a PrestaShop product
gallery without editing theme templates or pasting embed code. The module:

- recognizes supported YouTube, Vimeo, and Dailymotion URLs;
- creates a video thumbnail and inserts it among the product images;
- supports multiple videos for one product;
- lets the merchant enable or hide each video;
- can attempt muted autoplay when a video becomes the active gallery item;
- can expose the position-1 video on category, search, and other product
  listing cards;
- integrates directly with Classic and Hummingbird galleries and provides a
  separate fallback for compatible custom themes; and
- displays responsive players on desktop, tablet, and mobile layouts.

Videos remain hosted by their providers. The module stores the URL, provider,
video identifier, generated thumbnail URL, position, and display options. It
does not copy the video file to the shop server.

## Documentation set

| Document | Use it for |
| --- | --- |
| [Installation and activation](INSTALLATION.md) | Requirements, installation, license activation, updating, and removal |
| [User guide](USER_GUIDE.md) | Adding videos, supported URL formats, positions, autoplay, and product listings |
| [Troubleshooting](TROUBLESHOOTING.md) | License, URL, gallery, thumbnail, autoplay, listing, and theme problems |
| [Technical reference](TECHNICAL_REFERENCE.md) | Hooks, storage, endpoints, external hosts, security, privacy, and operational limits |

## Five-minute setup

1. Download the licensed Cool Video ZIP package supplied after purchase from
   [prestaexpert.pl](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html).
2. In the PrestaShop back office, open **Modules > Module Manager**, select
   **Upload a module**, and upload the ZIP file without unpacking it.
3. Open **Configure** for Cool Video, paste the activation code received after
   purchase, and select **Activate license**.
4. Confirm that **License active** is displayed and that **Shop domain** is the
   domain assigned to the key.
5. Open **Catalog > Products**, edit a saved product, and find Cool Video in the
   product's **Modules** section.
6. Paste a supported public video URL and select **Add video**.
7. Set **Gallery position**, **Active**, **Autoplay (muted)**, and **Show on
   product listings** as required.
8. Check the product page on desktop and mobile. If listing display is enabled,
   also check a category or search page.

## Important facts before you begin

- Supported providers in version 1.4.10 are YouTube, Vimeo, and Dailymotion.
- Direct MP4 URLs, uploaded video files, playlists, channels, and provider pages
  that do not identify one video are not supported.
- A newly created product must be saved once before Cool Video can attach a
  video to it.
- Gallery positions include both images and videos and start at `1`.
- To show a video on product listings, make it active, enable the listing
  option, and set its gallery position to `1`.
- Manual selection starts playback even when the autoplay option is disabled.
  The autoplay option controls automatic playback when the video becomes the
  initial or active gallery item.
- Browser and provider policies can still prevent autoplay. Cool Video requests
  muted playback to comply with common browser rules.
- Never uninstall the module as an update method. Uninstallation deletes the
  database table containing all product-video assignments.

## Getting support

Use the official
[Cool Video product page](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html)
for purchase, license, update, and support information.

When reporting a problem, include the Cool Video version, PrestaShop version,
PHP version, theme name and version, affected product URL, exact steps, and a
screenshot. For license issues, include the displayed shop domain and masked
key only. Never send the complete activation key in a public message.

