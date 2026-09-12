
# Installation and activation

This guide covers the Cool Video direct-sale Netteria License edition 1.4.10
supplied through
[prestaexpert.pl](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html).

## Requirements

| Requirement | Details |
| --- | --- |
| PrestaShop | 1.7.x, 8.x, or 9.x |
| PHP and database | A PHP and MySQL or MariaDB combination supported by the installed PrestaShop version |
| PHP extension | cURL is required for license activation and validation |
| Network | The shop server must be able to make outbound HTTPS requests to `prestaexpert.pl` |
| Browser | A current browser with JavaScript and `fetch` support is recommended for back-office management and listing videos |
| Theme | Classic and Hummingbird are integrated directly; compatible custom themes can use the standard-hook fallback |
| Permissions | A back-office employee account allowed to install modules and edit products |
| License | A Cool Video activation key assigned to the shop domain used during purchase |

Before installing on a production shop, create a current backup of the shop
files and database. Testing the installation on a staging copy is recommended
when the shop uses a heavily customized theme, strict Content Security Policy,
or aggressive JavaScript optimization.

## Download the correct package

Download the licensed package delivered after purchase from the official
[Cool Video product page](https://prestaexpert.pl/strona-glowna/24-modul-wideo-do-galerii-produktu-prestashop-cool-video.html).
The filename may be `coolvideo-1.4.10-netteria-license.zip` or a delivery name
such as `coolvideo.zip`.

Do not unpack and re-compress the archive. The ZIP must contain a top-level
`coolvideo` directory with `coolvideo.php` inside it. A double-wrapped archive,
for example `coolvideo/coolvideo/coolvideo.php`, will not install correctly.

The repository may also contain Marketplace or development builds. Those are
separate distributions and can have different activation behavior. Use the
package supplied with the prestaexpert.pl purchase for this guide.

## Install the module

1. Sign in to the PrestaShop back office with an account allowed to install
   modules.
2. Open **Modules > Module Manager**. On some PrestaShop 1.7 installations the
   menu label can appear as **Modules and Services**.
3. Select **Upload a module**.
4. Drop the supplied ZIP file into the upload area or choose it from disk.
5. Wait for PrestaShop to unpack and install the module.
6. Confirm that Cool Video is listed as installed and enabled.
7. Select **Configure** to open the license screen.

If installation fails, do not repeatedly upload different archives. First
verify the ZIP structure, writable permissions for the PrestaShop `modules`
directory, PHP upload limits, available disk space, and the PrestaShop log.

## Activate the direct-sale license

1. Open **Modules > Module Manager** and find **Cool Video Product - Netteria
   License**.
2. Select **Configure**.
3. Read the **Shop domain** displayed in the license status panel.
4. Confirm that this domain is the one assigned to the key during purchase.
   The validator compares host names without protocol, port, path, or a leading
   `www.`.
5. Paste the activation code into **License key**.
6. Select **Activate license**.
7. Confirm that the page displays **License active**. The saved key is shown in
   masked form. If the license has an expiry date, the page also displays it.

The key permits only letters, numbers, and hyphens and can contain up to 120
characters. Keep it private. Do not send the complete key in screenshots,
tickets, public repositories, or browser-console output.

### How validation behaves

- A successful result is cached for 24 hours.
- An invalid result or temporary connection failure is retried after 5 minutes.
- After at least one successful online validation, a temporary licensing-server
  outage can use the most recent valid confirmation for up to 7 days.
- A key that has never been validated online cannot use the offline grace
  period.
- If the license is inactive, video management is blocked and front-office
  gallery and listing output is not rendered.

The server-side validation request is sent over HTTPS to:

```text
https://prestaexpert.pl/modules/netterialicenseprovisioner/api/v1/validate.php
```

Allow outbound TCP port 443, DNS resolution, and trusted certificate validation
for that host. The module needs PHP cURL for the request and should be able to
write its status cache under `modules/coolvideo/cache/`.

## Verify the installation

Complete this check before configuring many products:

1. Open a product that has already been saved and therefore has a product ID.
2. Find Cool Video in the product's **Modules** section.
3. Add one supported public URL, for example a standard YouTube watch URL.
4. Leave **Active** enabled and set **Gallery position** to `2`.
5. Save the position if you changed it.
6. Open the public product page in a private browser window.
7. Confirm that the video thumbnail appears after the first product image and
   that selecting it starts the player.
8. Open the image or media modal and confirm that the video is available there.
9. Check the same page at a mobile width.
10. If product-list display is needed, set the video to position `1`, enable
    **Show on product listings**, and verify a category or search page.

## Update without losing assignments

Use an in-place module update. Do not uninstall the old version first because
uninstallation removes the table containing every product-video assignment.

1. Back up the shop files and database.
2. Record the installed Cool Video version and confirm that the license is
   active.
3. Obtain the new licensed ZIP from the official purchase channel.
4. Use PrestaShop's module update or upload workflow to replace the module in
   place.
5. Let PrestaShop run the included upgrade scripts.
6. Confirm that the module remains enabled and that the license page reports an
   active license.
7. Clear the PrestaShop cache. If CCC or another optimization system combines
   CSS and JavaScript, clear that cache as well.
8. Open a product with existing videos and confirm that its assignments,
   positions, and options remain present.
9. Test the product gallery, native media modal, mobile layout, and a product
   listing page.

The upgrade to the direct-sale 1.4.10 edition is designed to preserve existing
video assignments. A backup remains essential because server configuration,
third-party optimizers, and interrupted updates are outside the module's
control.

## Domain changes and multistore

The direct-sale license is bound to the normalized shop domain. Changing the
PrestaShop shop URL, moving from a staging host to production, or adding another
domain can cause **Domain mismatch** until the license assignment is updated.
Use the official product and support channel to confirm the licensing terms and
request a domain change when required.

In a multistore installation, switch to the intended shop context before
opening the license screen and verify the domain shown for each storefront.
Do not assume that one key covers every independent domain.

## Disable or uninstall

Disabling the module stops its back-office video manager and front-office
output but normally leaves saved assignments in the database. Re-enabling the
module and restoring a valid license makes them available again.

Uninstalling is destructive:

- all product-video assignments are deleted;
- the module database table is removed;
- the stored Cool Video activation key and local license-status cache are
  removed; and
- the hidden administration tab used by the video manager is removed.

Export or back up the database before uninstalling if the assignments may be
needed later. PrestaShop does not provide an undo operation for the removal.

## Next step

Continue with the [User guide](USER_GUIDE.md) to add videos and configure their
gallery, autoplay, and listing behavior.
