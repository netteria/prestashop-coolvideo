# Technical reference

This reference documents the Cool Video direct-sale Netteria License edition
1.4.10 sold through
[prestaexpert.pl](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html).
It is intended for shop administrators, integrators, hosting providers, and
support technicians.

## Module identity

| Property | Value |
| --- | --- |
| Technical name | `coolvideo` |
| Direct-sale version | `1.4.10` |
| Display name | Cool Video Product - Netteria License |
| Publisher | Netteria.NET |
| Product and sales channel | `prestaexpert.pl` |
| PrestaShop compatibility | 1.7.x, 8.x, and 9.x |
| Primary function | Add YouTube, Vimeo, and Dailymotion videos to product galleries and eligible product listing cards |
| Theme strategy | Native Classic adapter, native Hummingbird adapter, then standard-hook generic fallback |
| Local video upload | Not supported in version 1.4.10 |

The repository also includes Marketplace and development distributions. Their
activation rules can differ. This reference applies to the domain-bound
direct-sale package.

## Runtime requirements

- PHP and MySQL or MariaDB versions supported by the installed PrestaShop
  release.
- PHP cURL for direct-sale license validation.
- Server-side outbound HTTPS access to `prestaexpert.pl`.
- A writable module cache directory for efficient license-status caching.
- Front-office JavaScript and a browser with `fetch` for listing-page metadata.
- A theme that uses Classic, Hummingbird, or standard PrestaShop product hooks.

The module does not require jQuery for its front-office adapter and does not add
PrestaShop class overrides.

## Stored data

Installation creates the following table, where `{prefix}` is the configured
PrestaShop database prefix:

```text
{prefix}coolvideo_product_video
```

Each assignment stores:

| Field | Purpose |
| --- | --- |
| Product ID | Associates the row with one PrestaShop product |
| Original URL | Preserves the URL entered by the merchant |
| Provider and video ID | Identifies YouTube, Vimeo, or Dailymotion content |
| Generated title and description | Supplies accessible player labeling and optional text output |
| Thumbnail URL | Points to the provider-specific remote thumbnail |
| Position | Orders the video among product media, starting at 1 |
| Active | Controls all front-office visibility |
| Autostart | Requests muted autoplay for an active gallery video |
| Show in listing | Permits position-1 listing output |
| Width and height | Stores legacy embed dimensions; responsive layouts control the visible player |
| Created and updated timestamps | Records assignment lifecycle dates |

Rows are read in ascending position and then ascending internal video-row ID.
Product deletion removes the associated Cool Video rows. Module uninstallation
removes the complete table.

## Supported URL parsing

The parser accepts only `http` and `https` URLs no longer than 500 characters.
Provider and video IDs are extracted as follows.

| Provider | Accepted hosts and paths | ID validation |
| --- | --- | --- |
| YouTube | `youtu.be/{id}`; `youtube.com/watch?v={id}`; `/embed/{id}`; `/shorts/{id}`; `/live/{id}`; mobile and music watch hosts | 6 to 20 letters, digits, underscores, or hyphens |
| Vimeo | `vimeo.com/{numeric-id}` and `player.vimeo.com/video/{numeric-id}` | 1 to 20 digits |
| Dailymotion | `dai.ly/{id}`; `dailymotion.com/video/{id}`; `/embed/video/{id}`; supported geo host | 4 to 20 letters or digits |

Query-string start times and other non-ID parameters are not preserved in the
generated embed URL. Direct files and other providers are rejected.

## Generated external URLs

| Purpose | Host or URL pattern |
| --- | --- |
| YouTube player | `https://www.youtube-nocookie.com/embed/{id}?rel=0` |
| YouTube thumbnail | `https://img.youtube.com/vi/{id}/hqdefault.jpg` |
| Vimeo player | `https://player.vimeo.com/video/{id}` |
| Vimeo thumbnail | `https://vumbnail.com/{id}.jpg` |
| Dailymotion player | `https://www.dailymotion.com/embed/video/{id}` |
| Dailymotion thumbnail | `https://www.dailymotion.com/thumbnail/video/{id}` |

Autoplay adds the provider-specific autoplay and mute query parameters. Every
iframe allows autoplay, encrypted media, picture-in-picture, and fullscreen.

## Registered hooks

| Hook | Purpose |
| --- | --- |
| `displayBackOfficeHeader` | Loads product-video administration CSS and JavaScript |
| `displayAdminProductsExtra` | Renders the video manager in the product editor |
| `displayHeader` | Loads front assets and exposes product or listing configuration |
| `displayProductExtraContent` | Adds active videos to the standard Videos extra-content area |
| `displayAfterProductThumbs` | Supplies a hidden integration mount near product thumbnails |
| `displayFooterProduct` | Supplies a second standard-hook mount for broader theme compatibility |
| `actionObjectProductDeleteAfter` | Removes assignments after a product is deleted |

The installation and upgrade routines attempt to register every required hook,
even if one legacy hook fails, so a later retry can restore the complete state.

## Back-office operations

The hidden `AdminCoolvideoProductVideo` controller serves same-origin AJAX
operations for adding, deleting, toggling, and changing positions. Mutating
requests must:

- use HTTP POST;
- pass normal PrestaShop administration authentication and token checks;
- be made by an employee profile with edit access;
- refer to a video owned by the supplied product ID; and
- pass active direct-sale license validation.

Input positions are integers from 1 through 10000. Provider URLs are parsed and
validated server-side before a row is inserted.

## Listing endpoint

The front controller exposes a read-only same-origin action similar to:

```text
/module/coolvideo/ajax?ajax=1&action=GetListingVideos&product_ids=12,34,56
```

The endpoint:

- requires a valid direct-sale license;
- accepts no more than 100 unique positive product IDs;
- returns at most one qualifying row per product;
- returns only rows that are active, have listing display enabled, and use
  position `1`; and
- sends no-store cache headers because listing eligibility changes with gallery
  position.

The browser adapter observes dynamic product-card changes so it can reapply
controls after faceted navigation or compatible infinite-scroll updates.

## Gallery adapters

### Classic adapter

The adapter locates the standard main and modal thumbnail lists, inserts video
items into the combined media order, synchronizes thumbnail dimensions, and
replaces the cover image with a responsive iframe when a video is selected.

### Hummingbird adapter

The adapter creates video carousel slides and thumbnails, recalculates media
indexes, synchronizes active slides, and extends the Bootstrap-based product
media modal.

### Generic adapter

When neither known structure is available, the module finds a standard hook
mount or a recognized gallery anchor and renders a separate group of video
buttons. These buttons use the module's accessible responsive modal. The generic
adapter does not promise exact interleaving among theme image thumbnails.

### Product listing adapter

Recognized product cards receive a button over the image area or a 72-pixel
corner control, depending on available markup. Selecting it opens the module
modal and requests playback. The listing adapter processes up to 100 product
IDs in one request.

## License implementation

The direct-sale edition stores its activation key under the PrestaShop
configuration key:

```text
NETTERIA_LICENSE_COOLVIDEO
```

Validation uses server-side HTTPS POST requests to:

```text
https://prestaexpert.pl/modules/netterialicenseprovisioner/api/v1/validate.php
```

The request identifies the license key, normalized shop host, and technical
module name. The normalized host is lowercase and excludes protocol, port,
path, trailing dot, and a leading `www.`. Internationalized domains are
converted to ASCII when the PHP internationalization function is available.

Cache behavior:

| Result | Cache or retry interval |
| --- | --- |
| Valid | 24 hours |
| Invalid | 5 minutes |
| API unavailable | 5 minutes |
| Offline grace after a prior valid check | Up to 7 days from the last online validation |

Cache filenames include a hash of the API URL, module name, shop ID, domain,
and license key. The plain key is not written to the JSON status cache. The
license form displays a masked version of the configured key.

## Content Security Policy

A restrictive policy should allow the exact provider hosts used by the shop.
An illustrative policy fragment is:

```text
frame-src 'self' https://www.youtube-nocookie.com https://player.vimeo.com https://www.dailymotion.com;
img-src 'self' data: https://img.youtube.com https://vumbnail.com https://www.dailymotion.com;
connect-src 'self';
```

Merge these hosts into the existing policy rather than copying this fragment as
a complete policy. Server-side license validation is performed by PHP cURL and
is controlled by the server firewall, not browser CSP.

## Privacy and third-party services

The shop database stores the merchant-supplied URL and derived metadata, not
the video content. Visitors can connect to provider thumbnail and player hosts.
Those services can receive network metadata and can apply their own cookies,
tracking, privacy, age, and regional rules.

Review the shop privacy notice and consent-manager configuration for the chosen
providers. YouTube uses the privacy-enhanced `youtube-nocookie.com` player host,
but compliance requirements still depend on jurisdiction and shop policy.

## Lifecycle and recovery

- **Disable:** stops module output while normally preserving stored rows.
- **Enable:** restores output when the license and hooks are valid.
- **Update in place:** runs schema and recovery upgrades and preserves existing
  rows when the update completes successfully.
- **Uninstall:** deletes the assignment table, administration tab, activation
  configuration, and license cache.
- **Delete product:** removes rows associated with that product.

Back up the database before updates or uninstallation. Do not uninstall as an
update procedure.

## Operational limits and cautions

- One URL can identify only one supported provider video.
- URL length is limited to 500 characters.
- The administration position range is 1 through 10000.
- Listing lookup is limited to 100 unique product IDs per request.
- Only an active, listing-enabled position-1 video qualifies for a product
  card.
- The module does not verify in advance that a provider permits embedding.
- Remote thumbnail availability is controlled by the provider or thumbnail
  service.
- Browser autoplay remains subject to browser, device, consent, and provider
  policy.
- Custom themes can require selector or layout adaptation.

## Support handoff

For an efficient technical handoff, provide version details, the affected URLs,
theme and optimizer information, reproduction steps, console and network
errors, relevant server logs, and the displayed license state. Mask credentials
and activation keys.

Use the official
[Cool Video product page](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html)
for licensed-package support, updates, and domain-assignment questions.

