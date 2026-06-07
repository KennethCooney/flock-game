# Flock — Play Online (beta) setup

The online mode lets two people in different places race the same words. This note covers what it needs and how to start a game.

## How it works (plain version)

When one player taps **Create Game**, their browser becomes the host and generates a 4-letter room code. The other player types that code into **Join**, and the two browsers connect directly to each other (peer-to-peer over WebRTC). A free public PeerJS server is used only for the initial handshake (matchmaking) — the actual game data flows straight between the two of you. There are no accounts, logins, or personal data stored.

## The one requirement: a shared URL

Opening the file from your hard drive (`file:///…/flock.html`) works for solo and same-device multiplayer, but your sister can't reach a file on your computer. For online play, the page has to live at a web address you both open. It also has to be HTTPS, which WebRTC requires. Any static host works. Two easy options:

**Netlify Drop (fastest, no account needed to try)**
1. Go to https://app.netlify.com/drop
2. Drag `flock.html` onto the page (rename it `index.html` first so it loads at the root).
3. You get a URL like `https://something.netlify.app`. Share it.

**GitHub Pages**
1. Put `flock.html` in a repo (rename to `index.html`).
2. Repo Settings → Pages → deploy from the main branch.
3. Use the `https://<you>.github.io/<repo>/` URL it gives you.

## Starting a game

1. Both of you open the same URL.
2. One person: **Play Online → enter name → Create Game**, then read the code aloud / text it.
3. The other: **Play Online → enter name → type the code → Join**.
4. You connect, get a 3-2-1 countdown, and race the same 16 words. First to sort all four groups wins the round, spins the wheel, and moves. First to FINISH wins.

## What this beta does and doesn't do

Included: room-code connect, identical words for both players, live opponent progress, round-win detection, synced spin and pawn movement, synced game-over, opponent-left handling.

Not in this version (works in local same-device play, just not online yet):
- Online is 2 players only. Local multiplayer still supports 3-4.
- No bonus mini-game on the ★ spaces online — the pawn just lands and play continues.
- No Skip button online (Skip needs both boards on one device).
- If a player reloads or closes the tab, the match ends.

## Known limitations

- Needs an internet connection (the PeerJS library loads from a CDN, and the broker handles matchmaking).
- A small number of strict office/corporate networks block direct WebRTC connections. Home and phone networks almost always work. If a connection won't establish, that's usually why; a later version can add a TURN relay to cover those cases.
- The public PeerJS broker is free and occasionally flaky. For something more permanent you can self-host the broker later.
