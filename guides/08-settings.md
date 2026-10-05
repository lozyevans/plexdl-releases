# Settings explained

Every box on the **Settings** page has a **?** that opens its part of this guide. Changes only take effect when
you press **Save** in that box (the library switches under Compare scope save straight away). **Discard** puts
back what was saved.

## Your Plex server

Where your own Plex Media Server is. On the Plex PC there's nothing to do: PlexDL finds it by itself. If PlexDL
runs on another PC, enter the Plex server's address here: its private IP address and port, shown in Plex →
**Settings → Remote Access** (usually port 32400). Only a server your Plex account owns, at an address plex.tv
lists for it, is accepted. See [Plex on a different PC](07-plex-on-another-pc.md).

## Compare scope

Which libraries count. Every Movie and TV library on your server counts as **owned**, so a film in Kids Films
isn't reported missing; every library a friend shares is a **source** you can download from.

- Untick **Counts as owned** or **Compare** to leave a library out of the comparison.
- Turn **Sync** off to stop PlexDL reading a library at all (a huge library you never want from, say).
- **Automatically include new libraries on friends' servers**: a library a friend adds later is compared
  without you ticking it.
- **+ Add a Jellyfin server**: a friend's Jellyfin server, signed in to with the account they made for you.

A **Downloads not permitted** badge means the owner hasn't allowed downloads from that library.

## Downloads

How downloads use your connection and your friends' upload.

- **Downloads at once** and **Per friend server**: how many run together. One or two per friend is kind to them.
- **Connections per file**: big files download in this many parts at once, which is much faster from far away.
- **Total bandwidth cap** and **Per-server cap**: speed limits in Mbit/s (0 = no limit).
- **Keep free on staging drive** and **Space needed per GB downloaded**: a download only starts if it fits
  with this much to spare, leaving room for the converted copy.
- **Retry a failed download** / **Spread the retries over** / **Then try once a day for**: how hard PlexDL
  tries before giving up (see [When downloads fail](03-compare-and-download.md#when-downloads-fail)).
- **Keep part-downloaded files of failed downloads**: so **Retry** carries on where it stopped.
- **Staging folder**: where downloads wait while they're converted. The same drive as your library makes
  adding to Plex instant.
- **Download half from each** when two friends have the identical file.
- **Only download during a time window**, with what happens at its end and an optional slower speed outside
  it. Each friend's server can have its own window in its own time zone, a data limit, pausing while they
  stream, and a share of their upload (see
  [When things run](04-automation.md#when-things-run)).

## Conversion

How downloads are made to play everywhere. Files that already play on every Plex app are copied as they are;
the rest are re-encoded.

- **ffmpeg** does the converting. **Install ffmpeg** downloads a tested version; you can also point PlexDL at
  your own. Once it shows a version number it's working, and installing again doesn't change anything.
- **Encoders**: what PlexDL found works on this PC, tested with a real encode. A graphics card is much faster
  than the processor (CPU). **Test encoders again** after updating a graphics driver.
- **Quality when re-encoding**: High quality, Recommended or Smaller files.
- **Keep audio in** and **Subtitles to keep or fetch**: language codes such as `en, fr`. **Also keep the
  film's original language** keeps, say, the Japanese track of an anime film.
- **Pause conversions while my Plex server is transcoding for someone**, so viewers come first.
- **Advanced**: H.264 or HEVC, an exact quality value, conversions at once, an extra stereo track, keeping
  AV1 as it is.

## Import into Plex

Where converted files go and how they're named.

- **Import automatically**: off means each title waits in the Queue for **Import**.
- **Send kids content to your Kids library**: titles rated U, PG, G or TV-Y, or from a friend's Kids library,
  go to your library with Kids or Children in its name.
- **Films go to** / **New TV shows go to**: the default library for each. New episodes of a show you have
  always go next to the ones you have.
- **Advanced**: the backup folder for replaced files, and how long to wait for Plex to match a file.

### Destination rules

Your own rules, checked before the defaults: "if the genre contains Documentary, send it to Documentaries".
Rules can look at the genre, rating, the friend's library name or the title; the first one that matches wins.
**Test** shows where a title would go and why.

### Library folders

PlexDL must be able to write to every folder Plex uses for your libraries. Each shows **OK** with its free
space, or why not. On the Plex PC this just works (with the limited account, run **Grant PlexDL access to
media folders** from the Start menu). From another PC, add a **folder mapping** such as `H:\` →
`\\server\H$`; the line under each folder checks that a file Plex has there really is at the mapped path.

## Notifications

Everything shows under the bell. You can also send each kind (added to Plex, problems, follows, the weekly
digest, progress) to **Discord**, **ntfy** (phone push) or **email**. **Send test** checks a channel works.
Passwords, webhooks and tokens are stored encrypted and never shown again. See
[Notifications](04-automation.md#notifications).

## Schedule

What runs by itself, in this PC's time: a **full sync** every night, **quick syncs** every few hours, the
**weekly digest** of what's new on friends' servers, and PlexDL's **daily backup** of its own data. **System**
shows when each last ran and runs next, with **Run now**.

## Security

**HTTPS** encrypts the connection between your browser and PlexDL, so nobody else on your network can read
your session. Choose a certificate PlexDL makes (your browser warns about it once) or your own certificate
files, then restart the PlexDL service. Plain `http://localhost:32500` on the PlexDL PC always keeps working,
so you can't lock yourself out.

## Upgrades

When a friend's copy counts as an **upgrade** of one you own: it scores at least the **Minimum improvement**
more than yours (one resolution step, say 720p to 1080p, is about 100 points), or yours uses an old codec
such as XviD and theirs doesn't. **Count 4K/HDR copies as upgrades** includes 4K. **Upgrade films
automatically** swaps them in by itself (see
[Upgrading films automatically](04-automation.md#upgrading-films-automatically)).

## Feedback

Problems and ideas you send with **Feedback** (top right) become issues in a GitHub repository, with the
screenshot and diagnostics attached. Without a GitHub token they're saved as a zip for you to send by hand.

## Manual matches

When PlexDL pairs the wrong titles, fix it from Compare: **I already have this** links a friend's title to one
of yours, **Not a match** splits two that were wrongly paired. They're listed here; **Remove** undoes one.

## Not downloading

Titles, seasons and episodes you marked **Don't download** in Compare. They're left out of the lists and every
count, and never followed automatically. **Download after all** puts one back.

## Export and import settings

Save your settings to a file, to set up PlexDL on another PC or give a friend a starting point. Your sign-in,
tokens, passwords and webhooks are never included. Importing shows what would change in each part and only
applies what you tick. See [Just the settings](02-install.md#just-the-settings-export-and-import).
