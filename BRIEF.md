# 🎙 NETS — PTT Feature · Brief

**Source:** Daniel Turgeman (PM) chat, 23–30 Jul 2026 + UX flow work in this session.
**Priority:** #1 operational. Everything else waits.
**Jira:** https://nodoots.atlassian.net/browse/NOD-1150
**Reference app:** **Zello** — best-in-class PTT, the UX bar we're matching.
**Backend:** already started by Dor.

## Goal
Add Zello-style Push-To-Talk to the NETS app.

---

## Master task list

Merged from Daniel's spec (product scenarios) and the standard PTT UX flows
(interaction states). Both are in scope — the flows are *how* the scenarios
feel; the scenarios are *what* ships.

### A. Product scenarios (Daniel's spec)

| # | Item | Detail | Status |
|---|---|---|---|
| A1 | **Open 1-on-1 PTT call** | Replicate Zello UX for starting a voice channel with one user. | ⬜ |
| A2 | **Open group PTT call** | Start / join talk with a group. | ⬜ |
| A3 | **Channel management** | Full call/session management UX — switch, mute, leave. Zello-style. | ⬜ |
| A4 | **Voice history** | Store + play back past transmissions (Zello saves calls). | ⬜ |
| A5 | **Integrate with existing users + chats** | PTT must use NETS' *current* user & chat mechanism — not a separate parallel system. | ⬜ |
| A6 | **Reconcile the always-on record button** | The home-screen button that always records to a group must be merged with PTT into **ONE** unified solution. | ⬜ |
| A7 | **Old mic button decision** | Replace the current blue mic button (bottom-right) outright, **or** keep it and add a toggle. Ofir proposed a per-settlement toggle (old PTR vs new PTT). Daniel dislikes the toggle, prefers PTT for everyone. Mark's open question to Daniel: is the old mic used at all? If usage = 0 → just replace it. | ⬜ blocked on Q1/Q2 |

### B. UX interaction flows

| # | Flow | Detail | Status |
|---|---|---|---|
| B1 | **Idle → Talk (happy path)** | Press & hold PTT → "Requesting floor…" state → floor granted (solid button, active mic icon, waveform, "You are talking") → release → idle + end tone/haptic. | 🟡 mostly built — **missing the "requesting floor" intermediate state** |
| B2 | **Receiving audio** | Another user talking → PTT button disabled/locked (grey, speaker icon) so you can't transmit over them. Shows "Talking: [Name]" + live waveform. Optional incoming chirp before audio. Re-enables on their release. | ⬜ |
| B3 | **Floor denied / busy channel** | Press PTT while someone else holds the floor → button flashes red / shakes, short busy tone or haptic buzz. **No queueing** — user retries after the current speaker releases. | ⬜ |
| B4 | **Channel switching** | Select a different channel from a list/scroll view. Channel-name banner slides in + short tone on switch. If currently transmitting, switching **force-releases the floor first**. | ⬜ |
| B5 | **Connection loss / reconnect** | Network drops mid-session → PTT greys out, "Reconnecting…" banner. On reconnect banner clears, button re-enables. A transmission that dropped mid-flight ends **silently** — no partial resume. | ⬜ |
| B6 | **Latecomer / missed transmission** | Opening the app or channel while someone is already talking → join mid-stream, immediately see "Talking: [Name]". **No replay** of the missed portion. | ⬜ |
| B7 | **Multi-channel monitoring** *(if in scope)* | Passively monitor a secondary channel (audio plays, PTT inactive) while the primary channel stays interactive. Switching "active" channel promotes the monitored one to primary. | ⬜ scope TBD |

### C. Settings

| # | Item | Detail | Status |
|---|---|---|---|
| C1 | **System setting requested by Daniel** | A setting Daniel asked for in the settings screen. Specifics pending — user will supply. | ⬜ details TBD |

---

## Open questions for Daniel
1. **Replace the old mic entirely, or add a toggle?** *(Daniel leans: replace — PTT for everyone.)*
2. **Any usage metrics on the current mic tool?** *(Drives replace-vs-keep. Usage = 0 → just replace.)*
3. **What exactly is the settings item you asked for?** (C1)

## Explicitly deprioritized — after PTT ships
- Design refactor
- App logo update
- Mark's backlog

**PTT first.**

---

## Current prototype state
Single file `ptt-wireframe.html` — mobile wireframe, Hebrew RTL, light theme only.
Built so far (part of B1): press-and-hold mic, blue button stays blue and scales
while live, "משדר…" banner aligned to the mic with red blinking dot + animated
waveform bars, start beep (C6) / stop beep (E5), haptic on both.
