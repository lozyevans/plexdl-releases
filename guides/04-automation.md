# Following shows and automation

## Following a show

Following a show means new episodes are downloaded as soon as any friend has them.

- In **Compare → TV**, press **☆ Follow** on a show, or search for any show on the **Follows** page.
- Choose the quality, whether to include specials, which friends to take it from, which library it goes to,
  and whether to fetch the episodes you're already missing too.
- After every sync PlexDL looks for new episodes of the shows you follow and queues them. **Check now** on the
  Follows page does it straight away.

**Media Manager → Missing episodes in your seasons** offers **Follow this show** for shows with gaps.

## Upcoming episodes: the calendar

**Calendar** (in the menu) lists the episodes of shows you follow by the day they air: the last week, today,
and the next two weeks. Air dates come from Plex's own catalogue and are checked again twice a day.

For each episode it shows:

- whether it's **coming up**, has aired and is **waiting for friends**, **a friend has it**, it's **in the
  Queue** or already **in Plex**;
- which friend usually has new episodes of that show first, and how long after airing (PlexDL learns this from
  when your friends added the last few episodes);
- roughly when PlexDL expects to download it, inside your download hours.

An episode that aired a while ago and still isn't on any friend's server shows as **Late**, at the top. Turn on
**Also show my other shows that are still airing** to see the shows you have but don't follow (they aren't
downloaded by themselves; **Follow…** takes you to the show in Compare). The **Coming up** box on the Dashboard
shows the next few days, and the weekly digest lists what airs in the coming week.

## Your Plex Watchlist

Turn it on in the **Follows** page. Films you add to your Plex Watchlist (on any Plex app) are downloaded as
soon as a friend has them (1080p or 4K, your choice); shows are followed. Each title is acted on once, and the
page shows what happened to each one.

## Upgrading films automatically

PlexDL can replace films you own when a friend has a clearly better copy (the same rule as **Compare →
Upgrades**: enough extra quality, or yours uses an old codec like XviD). It's off until you choose:

- **Pick single films**: in **Compare → Movies** (Already owned) or **Compare → Upgrades**, open a film's **…**
  menu and choose **Upgrade automatically when better**. It gets an **Auto-upgrade** badge, and is upgraded
  whenever a friend has a better copy, now or later.
- **Settings → Upgrades → Upgrade films automatically**: only films you pick, those plus whole libraries, or
  all your films. Limits: 4K only if you allow it, a largest file size (40 GB to start with) and at most so
  many films a week (10 to start with; the biggest improvements go first).

It checks after every sync (or **Check now**). Films you marked **Don't download** are left alone, and so are
films where you chose **Stop upgrading automatically** (even with "all my films"). An upgrade that failed or
was cancelled isn't tried again for 30 days after it ended, and a copy that was already brought in is never
fetched again for the same film, even if you clear the Queue. As with any upgrade, your old copy goes to the
`PlexDL Backup` folder and **History** can undo it.

## When things run

**Settings → Schedule**:

- a full sync every night (03:00 by default) and quick syncs every few hours;
- a weekly digest of what was added and what's new on your friends' servers;
- PlexDL's own backup every day (04:30, keeping 14).

**Settings → Downloads** sets download windows. Each friend's server can have its own window **in its own time
zone** (pick the zone by city or country), so a server in another country is only used during its night. Outside
the window downloads can pause or carry on at a slower speed.

PlexDL also **goes easy on friends' servers** on its own:

- While a friend's Plex server is converting a stream for someone, downloads from it pause, then carry on where
  they stopped. (Plex only tells PlexDL about converted streams; someone playing a file directly shows up as the
  server getting much slower, below.) You can turn this off per server.
- A server that keeps failing is rested for 2 minutes, then 10, 30 and 60, instead of being retried straight away.
- A server that's much slower than usual for a couple of minutes gets one download at a time for 15 minutes, or a
  10-minute rest.
- Each friend's server can have a **data limit** per day or per week (weeks start on Monday). At the limit,
  downloads from it stop until the next day or week.
- PlexDL uses **at most a share of each friend's upload speed**: 50% in their daytime and 90% overnight by
  default (overnight means inside the download window, or midnight to 7am their time if there isn't one), so
  their own viewers and household still have room. Plex doesn't tell friends a server's upload speed, so PlexDL
  measures it about once a week during a night-time download (it lifts the limit for under a minute) and starts
  from your earlier download speeds until then. If you know the figure, enter it. Change the shares or the
  upload speed per friend in **Settings → Downloads**, under "Go easy on friends' servers".

The Dashboard shows how much has come from each friend this week, and the Queue says why a download is waiting.

**System** shows when each task last ran and when it runs next, with **Run now**.

## Notifications

The bell (top right) lists what happened: titles added to Plex, problems, follows and updates. Read ones can be
cleared; everything else goes after 90 days.

**Settings → Notifications** can also send them elsewhere, choosing which kinds go where:

- **Discord**: paste a channel webhook URL.
- **ntfy**: a topic on ntfy.sh (or your own ntfy server) for phone notifications.
- **Email**: your mail provider's SMTP server and an app password. The password is only ever sent over an
  encrypted connection (port 465, or 587 with STARTTLS); a server that can't encrypt is refused.

**Send test** checks each one. Passwords, webhooks and tokens are stored encrypted and never shown again.
