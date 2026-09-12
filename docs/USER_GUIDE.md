# User guide

This guide explains how to manage Cool Video after the direct-sale package has
been installed and activated. For setup requirements, see
[Installation and activation](INSTALLATION.md).

## Open the video manager

1. Sign in to the PrestaShop back office.
2. Open **Catalog > Products**.
3. Edit the required product.
4. If this is a new product, save it once so that PrestaShop assigns a product
   ID, then reopen or refresh the editor.
5. Open the product's **Modules** section and locate Cool Video.

The exact placement of the **Modules** section varies slightly between
PrestaShop 1.7, 8, and 9. If the manager displays a license warning instead of
the URL field, open the module configuration and activate the license first.

## Supported video URLs

Cool Video version 1.4.10 accepts one public video URL from one of the following
providers.

| Provider | Supported examples |
| --- | --- |
| YouTube | `https://www.youtube.com/watch?v=VIDEO_ID` |
| YouTube short link | `https://youtu.be/VIDEO_ID` |
| YouTube embed | `https://www.youtube.com/embed/VIDEO_ID` |
| YouTube Shorts | `https://www.youtube.com/shorts/VIDEO_ID` |
| YouTube Live | `https://www.youtube.com/live/VIDEO_ID` |
| Vimeo | `https://vimeo.com/123456789` |
| Vimeo player | `https://player.vimeo.com/video/123456789` |
| Dailymotion | `https://www.dailymotion.com/video/VIDEO_ID` |
| Dailymotion embed | `https://www.dailymotion.com/embed/video/VIDEO_ID` |
| Dailymotion short link | `https://dai.ly/VIDEO_ID` |

Mobile YouTube watch URLs from `m.youtube.com` and YouTube Music watch URLs from
`music.youtube.com` are also recognized. Use the direct URL for a single video.

The following are not supported in version 1.4.10:

- direct MP4, MOV, WebM, or other video-file URLs;
- uploading a local video file to PrestaShop;
- YouTube playlists, channels, search results, or URLs without a video ID;
- generic Vimeo profile, showcase, or collection pages;
- generic Dailymotion channel or playlist pages; and
- unsupported redirect or tracking links that do not expose the provider's
  video ID in a recognized format.

The source video must permit embedding and must be available to the visitors
who will view it. Private, deleted, age-restricted, region-restricted, or
embedding-disabled videos can produce a valid thumbnail but refuse playback.

## Add a video

1. Copy the public page URL for one supported video.
2. Paste it into **Video URL** in the Cool Video panel.
3. Select **Add video**.
4. Wait for the success notification and page refresh.
5. Confirm that a video card appears with a thumbnail, provider name, generated
   title, and provider video ID.

Cool Video derives the provider, ID, embed URL, and thumbnail URL from the
address. In version 1.4.10 the generated title and description are not edited
from the product panel.

New videos use these defaults:

| Setting | Default |
| --- | --- |
| Gallery position | The next position after the product's existing Cool Video entries |
| Active | Enabled |
| Autoplay (muted) | Disabled |
| Show on product listings | Disabled |
| Player ratio | Responsive 16:9 embed inside the Classic and fallback players |

## Understand the video card

| Control | Effect | Save behavior |
| --- | --- | --- |
| **Gallery position** | Places the video among product images and other videos | Select **Save position** after entering a whole number from 1 to 10000 |
| **Active** | Shows or hides the video in front-office output | Saved immediately when toggled |
| **Autoplay (muted)** | Requests muted automatic playback when this video becomes the initial or active gallery item | Saved immediately when toggled |
| **Show on product listings** | Allows the position-1 video to appear on recognized product cards | Saved immediately when toggled |
| **Delete** | Permanently removes the assignment from this product | Requires confirmation and has no undo |

If a toggle cannot be saved, the control returns to its previous value and the
back office displays an error notification.

## Set the gallery position

Positions are shared by product images and videos and begin at `1`.

For a product with three images named A, B, and C:

| Video position | Resulting order |
| --- | --- |
| `1` | Video, Image A, Image B, Image C |
| `2` | Image A, Video, Image B, Image C |
| `3` | Image A, Image B, Video, Image C |
| `4` or higher | Image A, Image B, Image C, Video |

On Classic and Hummingbird, the video is inserted into the combined media
order. A position-1 video becomes the initial gallery item when the product page
opens. On a custom theme that uses the generic fallback, videos appear as a
separate thumbnail row near the gallery, so an exact position among images may
not be available.

Use a unique position for every video when predictable ordering matters. If
several videos use the same position, their internal creation order resolves
the tie and may not match the order expected by a merchant.

## Active and inactive videos

Keep **Active** enabled to render the video in the gallery, native media modal,
Videos extra-content tab, generic fallback, and eligible product listing card.

Disable **Active** to hide the video without deleting its assignment. The URL,
position, and options remain stored and can be restored later by enabling the
control again.

Deleting a video is different from disabling it. Delete removes the row from
the database and cannot be undone from the module interface.

## Autoplay behavior

**Autoplay (muted)** tells Cool Video to request muted playback when the video
becomes the initial or active gallery item. Muting is included because modern
browsers normally block audible autoplay.

Important behavior:

- If a position-1 video has autoplay enabled, Cool Video attempts to start it
  when the gallery opens on that video.
- Selecting a video thumbnail manually starts playback even when the autoplay
  option is disabled.
- Opening a listing video or modal manually also starts playback.
- A browser, device, privacy extension, consent tool, or video provider can
  still block autoplay.
- Cool Video does not force sound on. Visitors can use the provider player to
  unmute after playback begins.

For the least intrusive storefront experience, leave autoplay disabled unless
the product presentation clearly benefits from it.

## Show a video on product listings

The listing option can add a video thumbnail or cover button to recognized
product cards on category, search, and other listing pages. Selecting that
button opens a responsive video modal and starts the video.

All three conditions are required:

1. **Active** is enabled.
2. **Show on product listings** is enabled.
3. **Gallery position** is exactly `1`.

Only one qualifying video is returned for each product card. For predictable
results, enable the listing option on one video per product and make that video
the only video at position `1`.

Depending on theme markup, the video control either covers the product image
area or appears as a smaller control in its lower corner. If the control is not
visible on a custom theme, see [Troubleshooting](TROUBLESHOOTING.md).

## Front-office behavior by theme

### Classic

- Video thumbnails are inserted into the standard thumbnail strip.
- Selecting a video replaces the main product image with a responsive player.
- Video entries are also inserted into the native product media modal.
- Selecting a normal product image removes the active video player and restores
  the image.

### Hummingbird

- Video slides and thumbnails are inserted into the product carousel.
- The active media item and provider player are synchronized with the carousel.
- The native media modal receives the same ordered image and video items.

### Compatible custom themes

Cool Video first looks for known Classic and Hummingbird structures. If neither
is available, it uses standard product hooks to place a separate row of video
buttons near the product gallery. Selecting a button opens Cool Video's own
responsive modal. Highly customized themes that omit the standard hooks or use
unrecognized product-card markup may need theme-specific integration.

### Videos extra-content tab

When the theme displays PrestaShop product extra content, active videos are also
available in a **Videos** tab or section. This provides an additional access
path even when the gallery adapter is limited by theme markup.

## Manage multiple videos

You can add multiple supported videos to one product. A practical sequence is:

1. Put the most important product demonstration first.
2. Add installation, sizing, care, or comparison videos later in the gallery.
3. Give each video a unique position.
4. Enable listing display only for the single position-1 video.
5. Disable outdated content before deleting it so the storefront can be
   checked safely.
6. Verify desktop, mobile, and modal behavior after changing several positions.

There is no drag-and-drop sorter in version 1.4.10. Enter each numeric position
and select **Save position** on that video card.

## Performance, privacy, and consent

Product pages load provider thumbnails before a visitor starts a video. The
provider iframe is created when needed by the gallery or modal, while the
extra-content tab uses lazy-loaded iframes. Listing pages request eligible video
metadata from the same shop and add controls only to recognized product cards.

Video playback and thumbnails make network requests to third-party provider
domains. Review the shop's privacy notice, cookie-consent configuration, and
Content Security Policy. YouTube playback uses the `youtube-nocookie.com` embed
domain, but this does not remove every privacy or consent obligation.

## Remove a video

1. Open the product's Cool Video panel.
2. Find the correct provider, thumbnail, and video ID.
3. If uncertain, disable **Active** and check the storefront first.
4. Select **Delete**.
5. Confirm the prompt.
6. Verify the product page and listing page.

Removal affects only the PrestaShop assignment. It does not delete the original
video from YouTube, Vimeo, or Dailymotion.

