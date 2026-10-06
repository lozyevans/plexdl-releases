# Words used in PlexDL

Words with a dotted underline in PlexDL show their meaning from here when you point at them.

## Direct play

A Plex app playing a file exactly as it is, without your Plex server converting it on the fly. It's the
smoothest way to watch, and it doesn't load your server. PlexDL's conversions aim for files every Plex app can
direct play.

## Transcoding

Your Plex server converting a video as someone watches it, because their device can't play the file as it is.
It works, but it makes the server work hard. PlexDL pauses its own conversions while Plex is transcoding, and
pauses downloads from a friend while their server is.

## Remux

Copying the video and audio into a new container (for example MKV to MP4) without changing them. Takes
minutes, and the picture is exactly the same. PlexDL remuxes whenever the video already plays everywhere.

## Re-encode

Turning the video into a different format (for example XviD or 10-bit H.264 into H.264). Takes much longer than
a remux, and uses the quality you chose in Settings → Conversion. A graphics card does it far faster than the
processor.

## H.264

The video format every Plex app, TV, phone and browser plays. PlexDL's default for re-encoded files.

## HEVC

Also called H.265 or x265. Files are about a third smaller than H.264 at the same quality, but some older TVs,
phones and browsers can't play it, so Plex transcodes it for them. 4K and HDR films use HEVC.

## Hardware encoding

Converting video on a graphics card instead of the processor (CPU): many times faster. PlexDL tries NVIDIA
(NVENC), Intel (Quick Sync) and AMD (AMF), tests each with a real encode, and uses the processor when none
works. On a PC without such a card that's normal; converting just takes longer.

## Quality presets

How good a re-encoded file looks against how big it is. **Recommended** looks like the original at a sensible
size; **High quality** is bigger and visually lossless; **Smaller files** suits phones and smaller TVs.

## Staging folder

Where downloads wait while they're checked and converted, before they go into your library. Put it on a drive
with room for a few films; on the same drive as your library, adding to Plex is instant.

## Kids routing

Sending children's titles (rated U, PG, G or TV-Y, or from a friend's Kids library) to your library with Kids or
Children in its name, instead of your main one.

## Folder mapping

When PlexDL runs on another PC, it reaches your library folders by a different path than Plex uses, for example
Plex's `H:\Films` as `\\server\H$\Films`. A mapping tells PlexDL how to turn one into the other.

## Download window

The hours downloads are allowed, in this PC's time, so they don't slow your evenings down. Each friend's server
can have its own window in its own time zone. Outside it, downloads pause or carry on slowly, as you choose.

## Going easy on friends

PlexDL's limits that keep downloads polite: a share of each friend's upload speed (half in their daytime), an
optional data limit per day or week, pausing while their server is streaming to someone, and resting a server
that keeps failing.

## Connection

How PlexDL reaches a server. **Local**: on your own network, fastest. **Remote**: over the internet, directly.
**Relay**: through Plex's relay, which Plex limits to a slow speed; fixing the friend's Remote Access fixes it.

## Full sync and quick sync

PlexDL keeps its own list of what's on every server. A **full sync** reads everything; a **quick sync** only
fetches what changed since. Both run on their own (Settings → Schedule).

## Upgrade

A friend's copy of something you own that's clearly better: higher resolution or a better format, by at least
the minimum set in Settings → Upgrades. Your old copy goes to the backup folder, so it can be undone.

## Basket

Titles you've added with **+ Add**, waiting for you to review (pick the friend, 4K or 1080p) and queue them.

## Follow

Following a show downloads its new episodes as soon as any friend has them.

## Don't download

Titles, seasons or episodes you never want. They leave every list and count; Settings → Not downloading
brings them back.

## PlexDL Backup

The folder next to each library where replaced and removed files go, so every change can be undone. Old backups
can be deleted from Media Manager → PlexDL backups, or automatically each night if you turn that on.

## Night shift

Media Manager converting the files in your library that Plex has to transcode, a few each night in the hours you
choose, until they're all done.

## SDH

Subtitles for the deaf and hard of hearing: as well as what's said, they describe sounds ("[door slams]") and
say who's speaking. Plex lists them as SDH; PlexDL saves them as `Title.en.sdh.srt`.
