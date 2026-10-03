# Following shows and automation

## Following a show

Following a show means new episodes are downloaded as soon as any friend has them.

- In **Compare → TV**, press **☆ Follow** on a show, or search for any show on the **Follows** page.
- Choose the quality, whether to include specials, which friends to take it from, which library it goes to,
  and whether to fetch the episodes you're already missing too.
- After every sync PlexDL looks for new episodes of the shows you follow and queues them. **Check now** on the
  Follows page does it straight away.

**Media Manager → Missing episodes in your seasons** offers **Follow this show** for shows with gaps.

## Your Plex Watchlist

Turn it on in the **Follows** page. Films you add to your Plex Watchlist (on any Plex app) are downloaded as
soon as a friend has them (1080p or 4K, your choice); shows are followed. Each title is acted on once, and the
page shows what happened to each one.

## When things run

**Settings → Schedule**:

- a full sync every night (03:00 by default) and quick syncs every few hours;
- a weekly digest of what was added and what's new on your friends' servers;
- PlexDL's own backup every day (04:30, keeping 14).

**Settings → Downloads** sets download windows. Each friend's server can have its own window **in its own time
zone** (pick the zone by city or country), so a server in another country is only used during its night. Outside
the window downloads can pause or carry on at a slower speed.

**System** shows when each task last ran and when it runs next, with **Run now**.

## Notifications

The bell (top right) lists what happened: titles added to Plex, problems, follows and updates. Read ones can be
cleared; everything else goes after 90 days.

**Settings → Notifications** can also send them elsewhere, choosing which kinds go where:

- **Discord**: paste a channel webhook URL.
- **ntfy**: a topic on ntfy.sh (or your own ntfy server) for phone notifications.
- **Email**: your mail provider's SMTP server and an app password.

**Send test** checks each one. Passwords, webhooks and tokens are stored encrypted and never shown again.
