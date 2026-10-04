# Arun & Sunita – Engagement Invitation Website

A single-page animated engagement invitation with an interactive envelope, background music, a scroll cue and a Google Maps link. It has no build step and needs no server code, so it can be hosted on any static host (Vercel, Netlify, GitHub Pages).

Live link: https://arun-sunita-engagement-invitation.vercel.app/

## Files

| File | What it is |
|------|------------|
| `index.html` | The whole website. The envelope, the story, the illustration and the music are all inside this one file (about 1.1 MB). |
| `og-image.png` | The preview picture WhatsApp shows when the link is shared (1200 × 630). |

Both files must sit at the top level of the site, next to each other.

## How the experience works

1. **Envelope:** guests see a closed burgundy envelope with a gold "A&S" seal and tap it. The flap opens, the card slides up, and the music starts.
2. **Story:** the invitation then plays on the same page, one screen at a time:
   - "Some stories are written… but the most beautiful ones are chosen."
   - The proposal illustration with "One question… One moment… One beautiful forever."
   - A drawn diamond ring with "And she said Yes."
   - "Save the Date" with the date below it
   - The final invitation
3. **Final invitation:** the illustration, the families' line, names, date, time, venue, full address and a **View location on Google Maps** button. A bouncing "Scroll" arrow and a soft fade at the bottom show when there is more to read below, and disappear once the guest reaches the end.
4. **Controls:** a small speaker icon (top-right) mutes and unmutes the music. The music pauses when the guest switches to another app or tab and resumes when they come back.

## Layout on phones and laptops

- **Phones:** the page fills the screen.
- **Laptops and tablets (wider than about 700 px):** the invitation sits in a centred, phone-width column (about 440 px) on a dark background, so it looks the same as on a phone.
- All sizes inside the page are based on the width of that column, not the whole screen. Please keep this in mind when editing the styles: use `cqw` and `cqh` units (like the existing code), not `vw` and `vh`.

## Changing the details

Open `index.html` in any text editor and search for the text below.

| To change | Search for |
|-----------|------------|
| Names, date, time, venue, city (final screen) | `function apply()` near the bottom |
| Names, date and seal on the envelope card | `class="e-card"` and `class="e-seal"` |
| Date under "Save the Date" | `Save the Date` |
| Full address | `52MW+4FX` |
| Google Maps button | `class="map"` (change the link in `href`) |
| Page title and WhatsApp text | `og:title` and `og:description` near the top |
| Preview picture address | `og:image` near the top |
| Time each story screen stays (milliseconds) | `data-t=` on each `class="scene"` (current values: 5200, 6800, 5200, 4000) |
| Music volume | `VOL=0.9` and `muted?0:0.9` (1 is full volume) |
| Colours | the `:root{--bg: …}` block at the top of the style section |
| The ring drawing | `class="ring2"` (an inline picture you can edit or replace) |

After editing, upload the file again to your host.

### Replacing the illustration

The picture is stored inside the file as a very long text value in `--art:url(data:image/png;base64,…)`. To replace it, convert your image to base64 and paste it in place of that value.

- Mac: `base64 -i yourimage.png | tr -d '\n'`
- Linux: `base64 -w0 yourimage.png`

Use a high-resolution image, because small pictures look soft when enlarged.

**Warning:** do not run a find-and-replace across the whole file. The picture and music are long blocks of encoded text, and replacing letters or numbers inside them corrupts the image or the sound.

### Replacing the music

The music is stored in the page as `var B64='…'`, an MP3 encoded as text.

1. Use an MP3 you have permission to use. Keep it short (30–60 seconds) to keep the page light.
2. Convert it to base64 with the commands above (use `yourmusic.mp3`).
3. Paste the result between the quotes in `var B64='…'`.

The track loops while the guest stays on the page.

## Deploying

**Vercel**
1. Put `index.html` and `og-image.png` in one folder.
2. Upload the folder to your Vercel project (or drag it into a new project on vercel.com).
3. Open the live link on your phone and on a laptop and test it.

**Netlify and GitHub Pages** work the same way: upload both files at the top level.

If your web address changes, update the `og:image` line near the top of `index.html` so it points to the new address of `og-image.png` (it must be a full `https://` address).

## Sharing on WhatsApp

- Send your live link. WhatsApp shows the preview picture and title from `og-image.png` and the `og:` lines.
- WhatsApp remembers previews. If you change the picture or text after sharing the link once, try a new chat, or a slightly different link (for example `…/?v=2`).
- The preview picture only appears if `og-image.png` is uploaded and its address in `og:image` is correct.

## Browser notes

- **Sound needs a tap:** browsers block sound until the guest taps something. That is why the music starts when the envelope is tapped.
- **iPhone:** the silent switch can mute sound from web pages.
- **Fonts:** Cormorant Garamond and Pinyon Script load from Google Fonts. Without an internet connection, similar fallback fonts are used.
- **Audio:** the soundtrack was generated by code (a soft piano-style piece), not a studio recording. It is original, so there are no copyright issues.
- **Older browsers:** the sizing uses container units (`cqw`), which need Chrome 105+, Safari 16+ or a similar recent browser.
- **Testing:** the page has been checked for script errors, but please test on a real phone (Chrome and Safari) and a laptop before sharing it widely.

## Privacy

The site has no forms or tracking, and uses no external services other than Google Fonts and the Google Maps link.
