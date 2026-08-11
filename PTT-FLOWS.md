# NETS PTT — all flows

Model: PTT is a **mode** you switch on inside a chat. Optional. Per chat.
**Exactly one chat can be in PTT mode at a time.** Everything else stays a normal chat.

---

## A. The basic loop — talk, receive, and back

**A1 — Talk**
1. Press and hold the mic
2. C5 beep, capture starts on contact, mic level meter animates
3. Release → D#5-G5-C6, buffer sent
4. A voice bubble appears in the thread, right side, duration + timestamp

**A2 — Receive**
1. Chirp (A5), then their audio plays automatically
2. Voice bubble appears on the left with avatar, waveform, duration, timestamp
3. Falling C6-F5-C5 when they finish

**A3 — And back**
Someone replies a moment later — same as A2, same channel. The floor is free
the instant they finish; anyone, including you, can press and talk next.

---

## B. Turning PTT on

**B1 — Enable PTT on a chat**
1. Open any chat, 1-on-1 or group
2. Tap the walkie-talkie icon in the header
3. Icon fills blue · blue banner `מצב PTT מופעל` with X appears under the header
4. Input bar (text / camera / clip) is replaced by one big mic button
5. Chat is now the active PTT chat

**B2 — Enable when another chat already has PTT**
1. Tap the walkie-talkie in chat B while chat A is the PTT chat
2. PTT moves to B immediately, no dialog
3. Chat A silently drops back to a normal chat
4. Toast: `PTT הועבר מ״<שם צ׳אט A>״`

**B3 — Enable while PTT is switched off in settings**
1. Tap the walkie-talkie
2. Toast: `PTT כבוי בהגדרות` with a shortcut to settings
3. Nothing is enabled

---

## C. Turning PTT off

**C1 — Close the banner**
Tap X → banner slides away, icon returns to outline, input bar returns. No PTT chat.

**C2 — Toggle the header icon**
Same result as C1.

**C3 — PTT switched off in settings**
The system-level `PTT כן / לא` setting is turned off → the active PTT chat drops
to normal, the walkie-talkie icon disappears from every chat header, mic button gone.

**C4 — Moved to another chat**
See B2. The old chat reverts with no prompt and no message in the thread.

**C5 — Leaving the chat**
Leaving a group or deleting the chat clears PTT. Nothing else inherits it.

---

## D. Talking — edge cases

**D1 — Too short**
Press under ~300ms → no send, short buzz, nothing added to the thread.

**D2 — Cancel mid-send**
Slide the finger off the mic before release → capture discarded, no bubble.

**D3 — Someone else is talking**
Mic is grey and locked. Pressing does nothing. Their bubble streams in live.

**D4 — Talking from outside the chat**
While a PTT chat is set, the map screen's mic transmits to that same chat.
The map dock shows the chat name so it is never ambiguous.

---

## E. Receiving — edge cases

**E1 — Incoming while on another screen**
Audio still plays. The map dock shows the speaker's avatar, name and live meter.

**E2 — Incoming while the app is backgrounded**
Audio plays. Notification shows `<שם> משדר` — tapping opens the PTT chat.

**E3 — Incoming while the phone is on silent**
No sound (OS-level). Vibration + visual meter only. Bubble still lands in the thread.

**E4 — Two people talk at once**
First to get the floor wins. The other gets the busy state (D3).

**E5 — Late join**
Opening the chat mid-transmission joins live. No replay of the missed part —
but the finished bubble stays in the thread and can be played back.

---

## F. History

**F1 — Playback**
Every transmission is a normal message in the chat. Tap play to hear it again.

**F2 — Mixed thread**
Voice bubbles, text, photos live in one thread in time order.
Switching PTT off does not remove them.

**F3 — Unread**
Unplayed voice messages count as unread, same badge as text.

---

## G. Failure and edge cases

**G1 — Mic permission denied**
Banner explains, mic button is disabled, PTT stays on until the user turns it off.

**G2 — No network / reconnecting**
Mic greys, banner `מתחבר מחדש…`. A transmission cut mid-send is dropped silently —
no half bubble in the thread. PTT mode survives the reconnect.

**G3 — Phone call arrives**
PTT audio pauses, mic locks. On call end, PTT resumes in the same chat.

**G4 — Battery saver / app killed**
PTT mode is remembered. On next launch the chat is still the PTT chat.

**G5 — Removed from the group**
PTT clears, chat becomes read-only, toast explains why.

**G6 — Two devices, same user**
PTT is active on the last device that enabled it. The other shows the normal chat.

---

## H. Incoming PTT requests

**H1 — Request arrives, you're not in any PTT chat**
1. Full-screen dialog: their avatar, name, "מבקש/ת להתחיל איתך שיחת PTT"
2. Ring plays — 2 beeps, pause, 2 beeps — plus vibration
3. One button: `התחל PTT עם <שם>`

**H2 — Request arrives while you're already live with chat1**
Same dialog, over whatever screen is open. Accepting moves PTT to the requester
exactly like B2 — chat1 reverts, toast names it. No difference from H1 otherwise.

**H3 — Accept**
Tap the button → PTT switches to the requester's chat, banner appears there.

**H4 — Decline**
Tap X → dialog closes, nothing changes, no toast, no trace left for the requester.

**H5 — PTT is off in settings**
The request can't arrive — the sender hits B3 (`PTT כבוי בהגדרות`) before it reaches you.

**H6 — A second request arrives while the first is still open**
Replaces the dialog's content immediately. No stack, no queue — only the newest shows.

**H7 — Request arrives mid-transmission (you're holding the mic)**
Held back until you release. Can never interrupt an active press.

**H8 — Ignored**
No timeout. Stays open until Accept or X.

---

## I. Screens touched

| Screen | Change |
|---|---|
| Chat (1-on-1 and group) | walkie-talkie header icon, blue banner, mic button replacing the input bar, voice bubbles |
| Chats list | the PTT chat shows a small walkie-talkie marker on its row |
| Map / home | mic transmits to the PTT chat; dock shows the chat name and incoming speaker |
| Settings | system-level `PTT כן / לא`; shows which single chat is currently PTT |
| Notifications | incoming transmission while backgrounded |

---

## J. Open questions

1. Should the map mic be disabled entirely when no chat has PTT?
2. Does turning PTT on post a system line in the thread (`מצב PTT הופעל`), or stay silent?
3. Can a group have PTT, or only 1-on-1?
4. Should the PTT chat pin to the top of the chats list?
