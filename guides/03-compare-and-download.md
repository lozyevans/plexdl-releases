# Finding and downloading

## Keeping the lists up to date

PlexDL keeps its own index of your library and your friends' libraries. The **Dashboard** shows each server
with what you're missing from it. **Full sync** reads everything; **Quick sync** only fetches what changed.
Both also run on their own (a full sync every night and quick syncs through the day: Settings → Schedule).

Choose which friends' libraries count in **Settings → Compare scope**. Titles are matched by their IMDb, TMDB
and TVDB ids, not by name or library, so it doesn't matter what your friends call their libraries.

## Compare

- **Movies**: films a friend has and you don't. Filter by friend, year, genre, rating or quality; each row says
  who has it, in what quality and how big it is.
- **TV**: shows grouped by show and season. Shows you don't have at all, and the episodes missing from shows you
  do have. **Add season** or **Add all missing** takes everything missing at once.
- **Upgrades**: titles a friend has in clearly better quality than your copy (how much better, and whether 4K
  counts, is set in Settings → Upgrades).

A **Downloads not permitted** badge means the owner hasn't allowed downloads from that library; those titles
are listed but can't be added.

**Don't download**: tick titles (or **Select all** for everything matching your filters) and choose **Don't
download**, or use the ⋯ menu on one title, season or episode. They leave the lists and every count on the
Dashboard, and are never auto-followed. Changed your mind? Tick **Show "don't download"**, select them and choose
**Download after all** (or use Settings → Not downloading).

## Basket, review and queue

1. **+ Add** puts a title in the **Basket** (top right).
2. **Review** the basket before anything downloads:
   - when several friends have a title, pick the source (PlexDL suggests the best and fastest);
   - for films that come in 4K, choose 4K or 1080p (TV defaults to 1080p);
   - sizes and rough download times are shown, and PlexDL warns you if a drive would run short.
3. **Queue** them. The **Queue** page shows every title as it downloads, converts and is added to Plex, with
   **Pause**, **Resume**, **Cancel**, **Retry** and priority.

Downloads resume where they stopped after a restart or a dropped connection, and large files download in
several parts at once (much faster from a far-away server). Speed limits, how many run at once and night-time
windows per friend's server are in **Settings → Downloads**.

## Converting

Each download is checked and, if needed, converted so it plays directly on TVs, phones and browsers without
Plex converting it on the fly: an MP4 with H.264 (or HEVC for 4K), audio your devices play, and subtitles in
your languages kept. Files that already play everywhere are just repackaged. Your graphics chip is used when
there is one. **Settings → Conversion** sets the quality, languages and video format; PlexDL pauses conversions
while someone is watching something Plex has to convert.

## Adding to Plex

PlexDL puts each title in the right library and folder with Plex's naming:

- a show you already have goes into its existing folder, in the same season-folder style;
- children's titles can go to a Kids library;
- your own rules (by genre, rating, friend's library or title) come first: **Settings → Import into Plex**,
  with a tester that shows where a title would go and why.

Then it asks Plex to scan just that folder and checks Plex matched the right title. Anything doubtful waits in
the Queue for you to look at, with a link to it in Plex.

Upgrades replace your old copy; the old one is kept in the `PlexDL Backup` folder next to that library.

## History and undo

**History** lists everything added to Plex. **Undo** takes an import back out: its files move to
`PlexDL Backup\Undone <date>` (never deleted), and for an upgrade your previous copy comes back. Plex is told to
rescan both places.
