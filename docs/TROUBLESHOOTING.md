# Troubleshooting

Use this guide for the Cool Video direct-sale Netteria License edition 1.4.10.
Start with the quick checks, then use the symptom-specific sections.

## Quick diagnostic checklist

1. Confirm that Cool Video is installed and enabled in **Modules > Module
   Manager**.
2. Open **Configure** and confirm **License active** for the displayed shop
   domain.
3. Confirm that the affected product has been saved and has a product ID.
4. Confirm that the video is **Active** and uses a supported public URL.
5. Open the provider URL directly in a private browser window and confirm that
   the video exists and permits embedding.
6. Clear the PrestaShop cache and any CCC, reverse-proxy, CDN, or full-page
   cache involved in the storefront.
7. Test without browser extensions and accept the shop's media or marketing
   consent category if a consent manager blocks external players.
8. Check both desktop and mobile layouts.
9. If a custom theme is used, temporarily test with its default gallery
   configuration or the Classic theme on a staging shop.
10. Review the browser console, failed network requests, PrestaShop logs, and
    web-server or PHP logs.

## Symptom reference

| Symptom | Most likely cause | First action |
| --- | --- | --- |
| Cool Video is absent from the product editor | Product not saved, module disabled, license inactive, or employee lacks access | Save the product, confirm module and license status, then check permissions |
| **Invalid or unsupported video URL** | URL is not one of the recognized single-video formats | Copy a direct YouTube, Vimeo, or Dailymotion video URL from the supported list |
| Thumbnail is blank or broken | Thumbnail host is blocked, video is unavailable, or Content Security Policy rejects the image | Open the thumbnail host in browser network tools and update CSP or firewall rules |
| Thumbnail appears but playback fails | Provider disabled embedding, video is private or restricted, or iframe host is blocked | Test the provider's embed URL and video privacy settings |
| Video is missing from the gallery | Video inactive, stale cache, inactive license, missing theme hook, or JavaScript conflict | Enable the video, clear caches, verify license, and inspect the browser console |
| Gallery position is ignored | Generic theme fallback is active or cached gallery markup is stale | Clear caches and check whether the page uses the Classic, Hummingbird, or generic adapter |
| Listing video is missing | Video is not active, listing option is off, or position is not `1` | Enable both options and save gallery position `1` |
| Autoplay does not start | Browser, provider, consent, battery, or data-saving policy blocked it | Confirm muted autoplay is enabled and test after explicit user interaction |
| Changes do not appear | PrestaShop, CCC, CDN, service worker, or page cache is stale | Purge all relevant caches and hard-refresh the page |
| Everything disappeared after update | Module became disabled, hooks were not restored, license is inactive, or old assets remain cached | Enable the module, verify license, clear caches, and check required hook registrations |

## License activation problems

### Missing license key

Open the module configuration, paste the activation code supplied with the
prestaexpert.pl purchase, and select **Activate license**. Use the licensed
direct-sale package, not a Marketplace or development archive.

### License not found

Check every character in the key. Remove leading and trailing spaces and make
sure the key belongs to Cool Video. If the key still fails, use the official
[product support channel](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html).

### Domain mismatch

Compare **Shop domain** on the module configuration page with the domain used
for the purchase. The validator ignores protocol, port, path, and a leading
`www.`, but a different host or subdomain is still a different domain.

Check **Shop Parameters > Traffic & SEO > Set shop URL** or the equivalent
PrestaShop shop-URL settings. In multistore, switch to the intended shop context
before checking. Contact the official sales channel when the licensed domain
must be changed.

### License expired

Review **Valid until** on the configuration screen and renew or correct the
license through the official sales channel. Do not change the server clock to
work around the status.

### Licensing server unavailable

Check the following on the shop server:

- PHP cURL is enabled for the web PHP runtime, not only for command-line PHP;
- DNS resolves `prestaexpert.pl`;
- outbound HTTPS on TCP port 443 is allowed;
- TLS certificate verification works and the server has a current CA bundle;
- the server date and time are correct; and
- no proxy, WAF, or hosting firewall rewrites or blocks the request.

The validation endpoint is:

```text
https://prestaexpert.pl/modules/netterialicenseprovisioner/api/v1/validate.php
```

After a prior successful check, the module can use the last valid confirmation
for up to 7 days during a temporary outage. It retries temporary failures after
5 minutes. A key that has never been confirmed cannot activate offline.

### License works briefly but is checked too often

Confirm that `modules/coolvideo/cache/` exists and is writable by the PHP or web
server account. Do not make the entire module directory world-writable. Use the
least permissions required by the hosting environment.

## The video manager is missing

The module needs an existing product ID. Save a new product once, then refresh
or reopen the product editor.

If an existing product still has no Cool Video panel:

1. Confirm that the module is enabled in the current shop context.
2. Confirm that the license is active.
3. Confirm that the employee profile can edit products and access the module's
   hidden administration controller.
4. Clear the back-office cache and hard-refresh the page.
5. Check that the module is registered on `displayAdminProductsExtra` and
   `displayBackOfficeHeader`.
6. Review PrestaShop and PHP logs for errors from `coolvideo`.

## A URL is rejected

Use a full `http://` or `https://` URL, preferably HTTPS. The URL must point to
one video and contain an ID in a recognized location.

Try a canonical format:

```text
https://www.youtube.com/watch?v=VIDEO_ID
https://vimeo.com/123456789
https://www.dailymotion.com/video/VIDEO_ID
```

Do not use a direct MP4 URL, playlist, channel, search result, or link-shortener
URL other than `youtu.be` or `dai.ly`. Remove extra text copied before or after
the URL. If a provider-generated share link redirects, open it in a browser and
copy the final canonical video URL.

## Thumbnail problems

Cool Video generates remote thumbnail addresses. It does not download and
store the image locally.

Check access to the relevant host:

| Provider | Thumbnail host |
| --- | --- |
| YouTube | `img.youtube.com` |
| Vimeo | `vumbnail.com` |
| Dailymotion | `www.dailymotion.com` |

A strict Content Security Policy must allow these hosts in `img-src`. Privacy
filters, ad blockers, DNS filtering, or a regional block can also hide a
thumbnail. Confirm that the video itself still exists.

## Playback problems

Open the video's provider page and verify that it is public, available in the
visitor's region, and allowed to play in an embedded iframe. Provider-level
privacy, age, ownership, or embedding restrictions cannot be overridden by
Cool Video.

A strict Content Security Policy must allow the relevant player host in
`frame-src`:

```text
https://www.youtube-nocookie.com
https://player.vimeo.com
https://www.dailymotion.com
```

Also check cookie-consent tools. Some tools intentionally block third-party
iframes until the visitor accepts a media or marketing category. Configure the
consent tool to replace or release the Cool Video iframe after consent.

## Gallery or modal problems

1. Confirm that the video is active.
2. Clear PrestaShop and asset-combination caches.
3. Disable JavaScript delay, defer, or optimization features temporarily on a
   staging shop.
4. Check for browser-console errors before and after selecting the video.
5. Inspect whether the page contains a Classic gallery, Hummingbird product
   carousel, or a `data-coolvideo-mount` fallback point.
6. Confirm that the theme renders at least one standard product hook used by
   the module.
7. Test the theme's original gallery without overrides or page-builder changes.

Cool Video can render a generic row of video buttons when it cannot integrate
with a known gallery. In that mode, videos open in a separate responsive modal
and their numeric position cannot interleave them precisely among image
thumbnails.

## Product listing problems

For every affected product, confirm all of the following:

- the video is active;
- **Show on product listings** is enabled;
- the saved gallery position is exactly `1`;
- only one listing video is configured at position `1` for predictable output;
- the page is a listing page, not a product detail page;
- JavaScript and `fetch` are available;
- the product card exposes `data-id-product` or supported product-card markup;
  and
- the same-origin listing endpoint is not blocked by a cache, WAF, or security
  rule.

The module requests at most 100 unique product IDs per listing request. Custom
infinite-scroll or page-builder markup can require theme-specific integration.

## Autoplay problems

Autoplay is a request, not a guarantee. Confirm that **Autoplay (muted)** is
enabled and that the video is the initial or active item. Test in a private
window with browser extensions disabled.

Browsers and devices can block autoplay because of user preferences, power or
data-saving modes, prior interaction rules, iframe permissions, or provider
policy. Manual selection should still start playback. Cool Video always
requests muted autoplay; visitors can unmute in the provider player.

## Changes are not visible

Purge caches in this order:

1. PrestaShop cache from **Advanced Parameters > Performance**.
2. CSS and JavaScript CCC cache.
3. Theme or page-builder cache.
4. Reverse-proxy or hosting cache.
5. CDN cache.
6. Browser cache, followed by a hard refresh.

If a service worker is installed, update or unregister it on the test browser.
Confirm that the page loads the current Cool Video CSS and JavaScript version.

## Prepare a useful support report

Include:

- Cool Video version and package edition;
- PrestaShop version;
- PHP version and whether web PHP has cURL enabled;
- theme name, theme version, and page builder if used;
- affected product and listing URLs;
- provider and exact video URL;
- expected result and actual result;
- exact steps to reproduce;
- desktop or mobile device and browser version;
- relevant browser-console and network errors;
- relevant PrestaShop, PHP, and web-server log entries; and
- screenshot or short screen recording.

For activation issues, include the displayed normalized shop domain, license
state, error code or message, and masked license key. Never include the complete
activation key or back-office credentials.

