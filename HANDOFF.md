# NETS PTT — FULL HANDOFF
### Everything a new session needs. Read all of it before doing anything.

---

# PART 0 — HOW TO TALK TO MARK

Mark Levinson is the UX designer. Not an engineer. He does not read code and does not
want tech vocabulary. He gets angry fast when an answer is long or evasive.

## Hard rules
1. Military-style short form only.
2. No babbling. No intro sentence. No outro sentence.
3. No tech jargon. Plain English. If a technical thing must be explained, explain it in
   terms of what the user of the app sees.
4. Answer in under 12 words when possible. 1–2 words is the best possible answer.
5. Do not narrate what you are about to do. Do it, then report the result in one line.
6. Do not say "I'm thinking" or "let me check". Think silently, execute.
7. **Exception:** when he asks a question, give ALL the detail you have, as a numbered or
   bulleted list. He wants completeness on questions, brevity on actions.
8. When he asks you to change something, rewrite the WHOLE item after fixing it and show
   it in full. Never show only the diff or say "changed X to Y".
9. Task lists: one table, item + status. Never prose. Never split across sections.
10. When you are wrong, say it in one line and fix it. No apology paragraphs.
11. He often sends corrections mid-turn while you are still working. Read them and adapt
    inside the same turn.

## Things that made him angry — do not repeat
- Explaining that the environment is a cloud container instead of just doing the task.
- Offering three options instead of picking one.
- Saying "I can't" without immediately giving the thing he can use.
- Faking behaviour to hide a failure (I once faked a mic animation when the mic was
  blocked — he tested it and caught it. Never do this. Surface failures.)
- Repeating the same wrong assumption twice.

---

# PART 0.5 — THE UX AND THE DESIGN CONCEPT
### This is the heart of the project. If you only read one part, read this one.

## The core idea, in one sentence
**A chat can become a walkie-talkie. One chat at a time. You switch it on, you hold a
button, you talk. You switch it off and it goes back to being a normal chat.**

## Why this shape and not another
We tried three shapes before landing here.

**Shape 1 — channels, like Zello.** A separate list of radio channels, separate from
chats. Rejected: NETS may never have channels, and it would mean building a second
parallel social graph next to the chats people already use. Every channel task is parked.

**Shape 2 — a "PTT target" picked in Settings.** One screen with a radio list of chats;
whichever is selected receives your voice. Rejected: it hides the most important state of
the whole feature behind a settings screen. A user in the middle of an incident should
never have to remember where their voice is going.

**Shape 3 — a dedicated 1-on-1 PTT call.** Rejected by Daniel: PTT is not a phone call
and it is not WhatsApp. It is operational, for a team, during an event.

**Shape 4, the one we are building — PTT is a mode of a chat.** It reuses the graph that
already exists. It puts the state where the user is already looking. It costs one icon.

## The design principles behind it

**1. Where you talk is where you already are.**
The people you would talk to are already in a chat together. No new list, no new group,
no new mental model. Open the chat, flip the switch.

**2. The state must be impossible to lose.**
When a chat is in PTT mode you see it three ways at once: the header icon is filled blue,
a blue banner sits under the header, and the text input is gone and replaced by a mic.
You cannot be in PTT mode and not know it.

**3. Exactly one.**
Only one chat can be in PTT mode. This is the single most important constraint in the
feature. It removes the entire class of "where did my voice just go" errors. Turning it
on somewhere else moves it, silently, with a toast that names the chat it left.

**4. It is optional, and off is the normal state.**
Most chats are just chats. PTT is something you reach for when an incident starts.

**5. Nothing is ever lost.**
Every transmission becomes a normal message in the thread. Voice, text, and photos live
in one timeline. Turning PTT off does not delete anything. You can replay any of it later.

**6. Never clip the first word.**
Recording starts the instant the finger touches the button, before the network is ready,
and the buffer is sent when the floor opens. The user never waits and never has to learn
a "wait for the beep" habit. This is why there is no "requesting floor" state — we solved
the problem in the plumbing instead of pushing it onto the user.

**7. Sound carries the state, not just the screen.**
A user running toward an incident is not looking at the phone. Rising tones mean *you are
sending*. Falling tones mean *they finished*. The pitch direction is the message.

**8. Show failure honestly.**
If the mic is blocked, the meter freezes and a red strip says why. We never animate a fake
meter to make a dead mic look alive. Mark tested exactly this and caught it once.

## The interaction, moment by moment

**Switching it on.** The walkie-talkie icon lives in the chat header next to the video and
phone icons — the same row a user already scans for "how do I reach this person". Tapping
it fills the icon blue and drops a blue banner. The banner is not decoration: it carries
the X that turns PTT off, so exiting is always one tap and always in the same place.

**The input bar is replaced, not extended.** This is deliberate. A big mic button sitting
next to a text field would ask the user to choose every time. Replacing the whole bar with
one 96px blue circle says: right now, this chat is voice. Nothing else to decide.

**Holding.** Press and the button scales down slightly, a C5 beep fires, and a three-bar
meter appears beside it driven by the real microphone level. The meter is the proof that
you are being heard. It is the same three-bar pattern used everywhere else in the app, so
the user learns one shape.

**Releasing.** A rising three-note run — D#5, G5, C6. Rising because something left you.
A voice bubble lands in the thread on your side with duration and timestamp.

**Receiving.** A single A5 chirp, then their audio plays by itself. The bubble appears on
their side with their avatar. When they stop, a falling three-note run — C6, F5, C5.
Falling because something arrived and ended. Your mic is grey and locked while they hold
the floor, so you physically cannot talk over them.

**Outside the chat.** If you are on the map and a transmission comes in, it still plays,
and the dock at the bottom of the map shows who is talking with a live meter, plus their
position on the map lights up with a blue waveform badge and a red ring. The same three
bars, the same language.

## The visual language, and why each piece exists

**The dock on the map.** A white capsule tucked under the blue mic, permanently visible
while a channel is open. Three dots at rest — the channel is open and quiet. The dots
stretch into vertical bars when there is audio. No text at all: Mark removed the "משדר…"
label deliberately, because the shape says it faster than a word does, and it works in
any language. The capsule's right edge is pinned to the mic so the bars never move; only
the pill grows leftwards to make room for a name and avatar when someone else is talking.

**The idle heartbeat.** Every five seconds the three dots hop twice, for about a second.
It is the "the radio is on" signal. A completely static dock reads as broken.

**Blue is you and them; red is danger only.** The waveform is blue whether you are talking
or listening, so voice always looks the same. Red is reserved for the alert button, the
on-air ring on a map marker, and error strips.

**The map marker.** Round avatar, blue ring normally. While that person is talking the
ring turns red and a blue circular badge with three white bars appears beside them, and
the other people on the map dim to 55%. You can see who is speaking without reading.

**One footer everywhere.** Mark rejected having a different bottom nav on the chats screen.
There is one nav — צ׳אטים, הקפצות, אירועים, מפה — and only the active item changes colour.

## The states, as a designer sees them
```
Chat, normal          input bar, walkie-talkie icon outlined
Chat, PTT on          blue icon, blue banner, big mic, grey tray
Chat, PTT transmitting big mic pressed, 3-bar meter beside it
Chat, PTT locked      big mic grey, someone else has the floor
Chat, PTT error       red strip under the header, mic grey
Map, idle             dock with three dots, heartbeat every 5s
Map, transmitting     blue mic scaled down, dots become a live meter
Map, receiving        mic grey with a speaker glyph, dock shows avatar + name + meter,
                      talker's map marker gets a red ring and a blue badge
Settings              PTT on/off; when off the mic greys everywhere and the icon vanishes
```

## The conversation model
It is a real back-and-forth, not a broadcast. In the prototype: you hold and release,
one second of silence, then מל דוד answers, and two seconds after he finishes ערן רותם
comes back with "קיבלתי". That rhythm — talk, pause, answer, acknowledge — is what a radio
net actually sounds like, and it is what the prototype demonstrates.

## What we deliberately left out
- No "requesting floor" wait state. Solved by buffering instead.
- No confirmation dialog when moving PTT to another chat. Just move it and toast.
- No queueing when the floor is busy. The button is simply locked.
- No replay of a transmission you joined late. The finished bubble is there afterwards.
- No hearing your own voice played back. A radio user never does.

---

# PART 1 — WHAT WE ARE BUILDING

## The company and the app
**NETS** is an Israeli civilian security / emergency response app used by settlement
standby squads (כיתות כוננות), security coordinators (רבש״צים), and regional commanders.
The app already exists. It has a map home screen, chats, events (אירועים), and alerts
(הקפצות). Everything is Hebrew, right-to-left.

## The feature
Add **Push-To-Talk** — walkie-talkie voice — to the existing NETS app.

- Jira epic: **NOD-1150** — https://nodoots.atlassian.net/browse/NOD-1150
- Reference app: **Zello**. That is the bar Daniel set. Channels, big PTT button,
  hold-to-talk, chirp on grant, "X is talking", saved transmissions.
- Backend: already started by **Dor**.
- PM: **Daniel Turgeman**.
- Designer: **Mark Levinson** (the user you are talking to).
- Also mentioned: **Ofir** — proposed a per-settlement toggle between old PTR and new PTT.
  Daniel dislikes that idea.
- Priority: **#1 operational.** Everything else waits.

## Why it matters
Standby squads currently coordinate during a live incident by typing in chat or by phone.
Both are too slow when someone is running toward an event. Voice that arrives instantly,
hands-free-ish, with no dialling, is the point.

---

# PART 2 — THE PRODUCT MODEL (this is the current decision, it changed twice)

## Current model — PTT is a mode inside a chat
1. PTT is a **mode** you switch on inside a chat.
2. It is **optional**. A chat does not have to be PTT.
3. **Exactly ONE chat can be in PTT mode at any moment.** Not two. Not three.
   Everything else stays a normal chat.
4. There is **no separate 1-on-1 PTT mode** and no separate PTT screen.
5. A system-level setting `PTT כן / לא` decides whether PTT exists in the app at all.
   When it is off, the walkie-talkie icon disappears from every chat header.

## How it looks
- A **walkie-talkie icon** sits in the chat header next to the phone and video icons.
- Tap it → icon fills blue, a **blue banner** appears under the header reading
  `מצב PTT מופעל` with an **X** on the left to exit.
- The normal input bar (mic / camera / paperclip) is **replaced by one big blue mic button**
  on a light grey tray.
- The conversation becomes voice bubbles back and forth — play button, waveform,
  duration `0:10`, timestamp `12:22`.

## How we got here — the decision history, in order
1. **First idea:** a channel-based PTT like Zello, with a channel list.
   *Killed* — Mark is not sure NETS will have channels at all. B4, B7, A3 are parked.
2. **Second idea:** a "requesting floor" wait state after pressing, before you are live.
   *Killed* — Mark asked why the user should care. Answer: without it you clip your first
   word and only the listeners notice. We solved it a better way instead:
   **buffer-and-send** — start recording the instant the finger lands, hold it locally,
   send when the floor opens. Nothing is clipped, no wait state needed.
3. **Third idea:** PTT target chosen from a single-select list in settings.
   *Superseded* — replaced by the per-chat toggle above.
4. **Daniel's constraint, from WhatsApp 1:30–1:36:**
   - "אני לא חושב שזה צריך להיות בכלל אופציה. זה לא וואטסאפ. זה נץ. אתה לא אמור להשתמש
     בזה לצורך פלירטוטים עם הבחורה בשער. זה מבצעי נטו."
   - "עושים ptt אך ורק בצוות כשיש אירוע"
   - Daniel pushed back: a lone commander or rabshatz may be alone, sending a written
     message, and need real time with one other person.
   - Landing point: you open a chat with whoever you want and press **start-PTT** inside it.
   - Daniel: "אבל גם ככה יש לך את האייקון של ההגדרות שבו אתה בוחר את הקבוצה, שזה בעצם
     הצ׳אטים. אז מה הבעיה להוסיף שם פלוס כדי להוסיף בן אדם או קבוצה חדשה."
   - Mark: "נראה לי שהגיוני שצריך. כי אחרת זה UX קצת עקום, שהם צריכים להבין שהם צריכים
     ליצור קבוצה בשביל זה. מהההגדרות הם אמורים לעשות הכל, ככה זה ממקום אחד"
   - Daniel closed with: "תקרא את כל מה שכתבתי כי היו שם כמה נקודות מהותיות"

---

# PART 3 — ALL FLOWS
### This is the authoritative spec. It also lives in PTT-FLOWS.md.

## A. Turning PTT on

**A1 — Enable PTT on a chat**
1. Open any chat, 1-on-1 or group
2. Tap the walkie-talkie icon in the header
3. Icon fills blue · blue banner `מצב PTT מופעל` with X appears under the header
4. Input bar (text / camera / clip) is replaced by one big mic button
5. Chat is now the active PTT chat

**A2 — Enable when another chat already has PTT**
1. Tap the walkie-talkie in chat B while chat A is the PTT chat
2. PTT moves to B immediately, no dialog
3. Chat A silently drops back to a normal chat
4. Toast: `PTT הועבר מ״<שם צ׳אט A>״`
*(Mark explicitly rejected a confirmation dialog here. Just switch and toast.)*

**A3 — Enable while PTT is switched off in settings**
1. Tap the walkie-talkie
2. Toast: `PTT כבוי בהגדרות` with a shortcut to settings
3. Nothing is enabled

## B. Turning PTT off

**B1 — Close the banner**
Tap X → banner slides away, icon returns to outline, input bar returns. No PTT chat.

**B2 — Toggle the header icon**
Same result as B1.

**B3 — PTT switched off in settings**
The system-level `PTT כן / לא` setting is turned off → the active PTT chat drops to
normal, the walkie-talkie icon disappears from every chat header, mic button gone.

**B4 — Moved to another chat**
See A2. The old chat reverts with no prompt and no message in the thread.

**B5 — Leaving the chat**
Leaving a group or deleting the chat clears PTT. Nothing else inherits it.

## C. Talking

**C1 — Send, happy path**
1. Press and hold the mic
2. C5 beep, capture starts on contact, mic level meter animates
3. Release → D#5-G5-C6, buffer sent
4. A voice bubble appears in the thread, right side, duration + timestamp

**C2 — Too short**
Press under ~300ms → no send, short buzz, nothing added to the thread.

**C3 — Cancel mid-send**
Slide the finger off the mic before release → capture discarded, no bubble.

**C4 — Someone else is talking**
Mic is grey and locked. Pressing does nothing. Their bubble streams in live.

**C5 — Talking from outside the chat**
While a PTT chat is set, the map screen's mic transmits to that same chat.
The map dock shows the chat name so it is never ambiguous.

## D. Receiving

**D1 — Incoming while the chat is open**
1. Chirp (A5), then their audio plays automatically
2. Voice bubble appears on the left with avatar, waveform, duration, timestamp
3. Falling C6-F5-C5 when they finish

**D2 — Incoming while on another screen**
Audio still plays. The map dock shows the speaker's avatar, name and live meter.

**D3 — Incoming while the app is backgrounded**
Audio plays. Notification shows `<שם> משדר` — tapping opens the PTT chat.

**D4 — Incoming while the phone is on silent**
No sound, OS-level. Vibration + visual meter only. Bubble still lands in the thread.

**D5 — Two people talk at once**
First to get the floor wins. The other gets the busy state (C4).

**D6 — Late join**
Opening the chat mid-transmission joins live. No replay of the missed part — but the
finished bubble stays in the thread and can be played back.

## E. History

**E1 — Playback** — every transmission is a normal message. Tap play to hear it again.
**E2 — Mixed thread** — voice, text, photos in one thread in time order. Turning PTT off
does not remove them.
**E3 — Unread** — unplayed voice messages count as unread, same badge as text.

## F. Failure and edge cases

**F1 — Mic permission denied** — banner explains, mic disabled, PTT stays on until the
user turns it off.
**F2 — No network / reconnecting** — mic greys, banner `מתחבר מחדש…`. A transmission cut
mid-send is dropped silently, no half bubble. PTT mode survives the reconnect.
**F3 — Phone call arrives** — PTT audio pauses, mic locks. On call end PTT resumes.
**F4 — Battery saver / app killed** — PTT mode is remembered. Same chat on next launch.
**F5 — Removed from the group** — PTT clears, chat read-only, toast explains.
**F6 — Two devices, same user** — PTT active on the last device that enabled it.

## G. Screens touched
| Screen | Change |
|---|---|
| Chat, 1-on-1 and group | walkie-talkie header icon, blue banner, big mic replacing the input bar, voice bubbles |
| Chats list | the PTT chat shows a small walkie-talkie marker on its row |
| Map / home | mic transmits to the PTT chat; dock shows the chat name and incoming speaker |
| Settings | system-level `PTT כן / לא`; shows which single chat is currently PTT |
| Notifications | incoming transmission while backgrounded |

## H. Open questions for Daniel
1. Replace the old blue mic button entirely, or keep it and add a toggle? He leans replace.
2. Any usage metrics on the current mic tool? Usage zero → just replace it.
3. Can a group have PTT, or only 1-on-1?
4. Should the PTT chat pin to the top of the chats list?
5. Does turning PTT on post a system line in the thread, or stay silent?
6. Should the map mic be disabled when no chat has PTT?

---

# PART 4 — TASK LIST

| # | Item | Status |
|---|---|---|
| B1 | Idle → Talk, press & hold | done |
| B2 | Receiving audio from another user | done |
| B3 | Floor denied / busy | done — grey locked mic says it, no extra feedback needed |
| D1 | "Start PTT" inside any chat | in progress — screens built, needs the one-chat-only rule wired |
| C1 | Settings — PTT on/off + which chat is PTT | rework, the old chat-picker is superseded |
| D2 | "+" in settings to add a person or a new group | open |
| D3 | No forced group creation for one person | open |
| D4 | PTT = team + event only, framing and copy | open |
| D5 | Real-time 1-on-1 for lone commanders | open, covered by D1 |
| B5 | Connection loss / reconnect | open |
| B6 | Latecomer mid-transmission | open |
| A2 | Open group PTT call | open |
| A4 | Voice history | open |
| A5 | Integrate with existing users + chats | open |
| A6 | Reconcile the always-on record button into ONE solution | open |
| A7 | Old mic button: replace or toggle | blocked on Daniel, questions 1 and 2 |
| A1 | Open 1-on-1 PTT call | superseded by D1 |
| B4 | Channel switching | parked — channels may not exist |
| B7 | Multi-channel monitoring | parked |
| A3 | Channel management | parked |

**Deprioritized until PTT ships:** design refactor, app logo update, Mark's own backlog.

---

# PART 5 — THE PROTOTYPE

## Where it is
- Repo `marklevi7/temp-public-3`, branch **`claude/nets-ptt-prototype-init-avqddf`**
- One file: **`ptt-wireframe.html`**, ~148KB, no build step, no dependencies,
  all images and audio inlined as base64 data URIs.
- Viewport target 360×800, also verified at 390×844, 375×667, 430×932.
- `<html lang="he" dir="rtl">`, `<meta charset="UTF-8">` — the charset meta is mandatory,
  without it every Hebrew string turns to mojibake. This already happened once.

## Screens inside the file
1. **Map / home** — the default. Status widget, map, avatars, FAB row, footer.
2. **Chats list** — `#chatsScreen`, 8 cards, opens from the צ׳אטים tab.
3. **Chat with PTT** — `#chatScreen`, opens from any chat card.
4. **Settings** — `#settings`, full-screen sheet from the cog.
5. **Dev control panel** — `#devbar`, dark bar pinned above the phone. Not product.

## Key DOM ids
```
devbar  markup
micBtn micIcon spkIcon micNote pill
spkAv spkFace spkInit spkName
incomingAudio incomingAudioB
mapTabbar chatsTabbar tabChats
settings setBack pttToggle pttState chatList
chatsScreen
chatScreen chPtt chBx chBody chWarn chMeter chBigMic chToast
tPen tArrow tClear
```

## Key JS functions
```
startTalk stopTalk            press-and-hold on the map mic
beginCapture armCapture endCapture ensureStream    microphone capture
driveDots setDot resetDots    live mic meter on the three dots
startReceiving stopReceiving  incoming transmission, takes 'a' or 'b'
driveIncoming stopIncomingMeter   incoming audio drives both meters
playBlips tone                all sounds
micUnavailable                surfaces a real mic failure, never fakes it
applyPtt                      settings PTT on/off
openChats closeChats          chats list
openChat closeChat chatPttOn showToast   chat screen and PTT mode
devMark devReset devStates    control panel
```

## State classes to know
```
.fab-mic.live      you are transmitting
.fab-mic.locked    someone else has the floor
.fab-mic.off       PTT switched off in settings
.talk-pill.active  transmitting, dots become the meter
.talk-pill.rx      receiving, shows avatar + name + meter
.map.rx            a transmission is playing
.talker-marker.talking   that person is the one talking
.chat.ptt          chat is in PTT mode
.chat.talking      big mic held down
.chat.warn         red strip under the header
.settings.open .chats.open .chat.open
```

## The control panel — how to reach every state
Dark bar at the top, three groups:
- **מצבים** — רגיל · משדר · מקבל שידור · שיחה מלאה
- **מסכים** — הגדרות · בחירת צ׳אט · מסך צ׳אטים
- **סימון** — עיפרון · חץ · נקה  *(markup tools, may or may not be present)*
- **קצה** — PTT כבוי · מיקרופון חסום

Every button resets all state first, then enters the requested one, and lights up blue.

---

# PART 6 — INTERACTION DETAIL THAT WAS HARD-WON

## Buffer-and-send
Capture starts on `pointerdown`, measured **4–5ms** warm, **41ms** on the very first cold
press. The audio is buffered locally and would be sent once the floor opens, so nothing is
clipped and no "please wait" state is needed. This replaced the requesting-floor idea.

## The microphone permission race — a real bug that was fixed
The first press opens the iOS permission dialog, which blocks the page. By the time the
promise resolves the finger is already up, so the old code saw `ptteLive === false`, threw
the stream away, and the meter never started. First press could never work.
**Fix:** acquire the stream once (`ensureStream`), cache it for the whole session, never
stop the tracks on release. A fast path starts `MediaRecorder` synchronously when the
stream is already warm.

## The tap-swallowing bug — another real one
`stopTalk` is bound to `window` as a safety net. It called `e.preventDefault()` **before**
checking whether we were transmitting, so every `touchend` anywhere on the page was
cancelled — which kills the synthesized `click` in touch mode. The settings cog and the
demo button silently did nothing.
**Fix:** only `preventDefault` while actually transmitting.

## The meter must never move
The pill's right padding used to differ between idle and receiving, which slid the bars
sideways. Now every state uses the same 86px right padding, so the pill's right edge is
pinned to the mic and it only grows leftwards.
Verified three ways: state-to-state (0.00px), animations frozen (0.00px), and continuous
sampling during live audio (32 frames transmitting, 52 receiving, 0.00px x-drift,
0.01px centre-Y drift) while bar heights swung 27px.

## Never fake a failure
There used to be a fallback animation when `getUserMedia` was rejected. It made a blocked
mic look identical to a working one and Mark caught it. It is gone. Now the dots stay
still and a red banner says why: `הגישה למיקרופון נחסמה — פתחו בדפדפן`, or no-mic-found,
or HTTPS-required.

---

# PART 7 — SOUNDS

All verified by instrumenting `OscillatorNode.start()` and reading the actual frequencies.

| Event | Notes | Timing |
|---|---|---|
| Press the mic | **C5** 523.25 Hz, single beep | 0 |
| Release the mic | **D#5** 622.25 → **G5** 783.99 → **C6** 1046.50, rising | 0 / 0.07 / 0.14s |
| Incoming starts | **A5** 880 Hz chirp | 0 |
| Incoming ends | **C6** 1046.50 → **F5** 698.46 → **C5** 523.25, falling | 0 / 0.07 / 0.14s |

Implementation notes:
- Web Audio only, no audio files for the beeps.
- `tone(freq, offset, len, peak)` — sine, exponential attack 6ms, exponential decay.
- Gain climbs across a rising sequence (0.40 → 0.50 → 0.60) because equal-gain sine tones
  sound *quieter* as pitch rises, which made an ascending run feel like it was falling.
  Mark noticed this before the fix.
- `audioCtx.resume()` must be awaited before scheduling against `currentTime`, otherwise
  nothing plays when the context starts suspended. This was a real bug.
- Mark iterated on these tones about eight times. Do not change them without being asked.

---

# PART 8 — VOICE AND IMAGE ASSETS

## Hebrew voice clips, both embedded as base64
1. `#incomingAudio` — **מל דוד**: *"מוקד, כאן ניידת שתיים. הכל תקין."* ~2.85s
2. `#incomingAudioB` — **ערן רותם**: *"קיבלתי."* ~1.18s

Made with:
```
python3 -c "from gtts import gTTS; gTTS(text='...', lang='iw').save('src.mp3')"
ffmpeg -i src.mp3 -af "asetrate=24000*0.72,aresample=24000,atempo=1.389,atempo=1.44,highpass=f=80" -ac 1 -b:a 48k out.mp3
```
The `asetrate` + `atempo` chain pitches the Google voice down into a male range and keeps
the speed. `gTTS` and `imageio-ffmpeg` are already installed.

## The face photo
Mark's own photo. It arrived as a chat upload, which does **not** land on disk. Extract it
from the session transcript, where it is stored as base64:
```
/root/.claude/projects/-home-user-temp-public-3/<session-id>.jsonl
```
Look for content blocks with `"type":"image"`, take `source.data`, base64-decode.
It is cropped square and scaled to 140×140 before embedding.

---

# PART 9 — DESIGN SYSTEM

## Colours from the Figma file
```
#1B293B  Primary / Dark Blue      titles, body text
#2C86F1  Primary / Medium Blue    FAB, unread badge, PTT banner, active chats tab
#2D85F2  Primary CTA / Regular    active nav item
#64748B  Text / Secondary         nav labels
#767F89  Grays / Gray Dark        timestamps, secondary
#A4A9B1  Grays / Gray 1           placeholder, nav icons on the chats nav
#BBBFC4  Grays / Gray 2           event avatar background
#D1D4D8  Grays / Gray 3           card top border, header avatar
#F4F4F5  Grays / Gray 5           search field, dividers
#52CC52  Status / Green           availability dot
#F34545  Status / Red             notification dot
#0A84FF                           unread dot in the chat picker, brighter on purpose
```
Prototype-only tokens still in the file: `--accent #1f6f8b`, `--danger #c0453a`,
`--lock #9aa4ae`. These are wireframe leftovers on the map screen.

## Type
**Assistant.** 16/20 regular = body 1 · 16/20 semibold = body 1 semibold ·
14/20 regular = body 2 · 14/20 bold = body 2 bold · 12 = caption.

## Geometry
- Header 80 = status bar 24 + app bar 56
- Bottom nav 72, four items, 64 tall each, 8px bottom padding, 20px side padding
- Chat card 88, padding 24 horizontal / 16 vertical, top border #D1D4D8
- Avatar block 44×40, the 40px circle offset 2px, status badge 16px at left 0 top 24
- Chats FAB 56, radius 75, at x24 y656, shadow `0 4px 7px rgba(0,0,0,.38)`
- PTT dock: mic 60 at right 20 bottom 22, pill same height, right padding always 86

---

# PART 10 — FIGMA

## Files and node ids
**Nets-Desktop** — https://www.figma.com/design/q5NsqoTX9ZOpXvoeKBGKWE/Nets-Desktop
- `6701:69442` — m 960, the reference map screen
- `6701:69508` — header
- `6701:69516` — bottom nav, first version
- `6772:96155` — bottom nav, the one actually implemented, 4 exact SVGs

**Nets_Product-mobile-Design** — https://www.figma.com/design/Uz08r68EETcGiP0L7VtKK5/Nets_Product-mobile-Design
- `1520:44708` — Chat Tab section, 9 frames
- `1520:44709` — (1) Chat Tab, the chats screen we replicated
- `1520:44714` / `1520:44716` — Card_Chat, person and event variants
- `1520:44736` — Nav Menu used on the chats screen (we dropped it, see below)
- `1520:44737` — 56/Add, the blue FAB
- `1520:44955` — (9) Group Chat, the chat thread reference
- `3861:76809` — **Section 4** — 8 map screens already uploaded and laid out
- `3866:76810` — **Section 5** — TARGET for the 12 PTT flow screens, **NOT DONE**

Note: Mark asked for one footer everywhere, so the chats screen reuses the map footer.
Only the active tab differs. The bespoke 4-item nav from `1520:44736` was deleted.

## How to upload screenshots into Figma — the procedure that worked
```
1. mcp__Figma__upload_assets  fileKey=<key>  count=N  scaleMode=FIT
   → returns N single-use submitUrls
2. For each file:
   curl -s -X POST -F "file=@shot.png;type=image/png" "<submitUrl>"
   → returns {"success":true,"imageHash":"…","placedOnNodeId":"3862:2"}
3. mcp__Figma__use_figma with plugin-API JavaScript:
   - getNodeByIdAsync on each placedOnNodeId
   - resize(360, 800), set x / y, set name
   - section.appendChild(node)
   - add an Inter Semi Bold text label above each
   - await figma.setCurrentPageAsync(section.parent) first
   - font style is "Semi Bold" with a space, not "SemiBold"
4. Verify with mcp__Figma__get_screenshot on the section node.
```

## The blocker you are inheriting
The last session could not finish this. Every Figma write returned
`MCP error -32003: MCP tool call requires approval`, starting right after the Figma MCP
server disconnected and reconnected. It had worked earlier in the same session.
Mitigation already applied — the tools are whitelisted in:
- `/home/user/temp-public-3/.claude/settings.json`
- `/home/user/temp-public-3/.claude/settings.local.json`
- `/root/.claude/settings.json`
- `/root/.claude/launcher-settings.json`  (original backed up in `~/.claude/backups/`)
These are read at session start, so a fresh session should run clean.

## The 12 screenshots waiting to be uploaded
In `flows/` in the repo. Consistent names, keep them:
```
A1-enable-ptt-on-a-chat      A2-moved-from-another-chat   A3-ptt-off-in-settings
B1-ptt-turned-off            C1-transmitting              C2-too-short
C3-cancelled                 C4-floor-taken               D1-receiving
E1-voice-history             F1-mic-denied                F2-reconnecting
```
Also in `flows/`, already in Section 4:
```
01-idle  02-transmitting  03-receiving  04-ptt-off  05-mic-blocked
06-settings  08-chats-screen  09-receiving-second
```

---

# PART 11 — HOW TO SHOW MARK ANYTHING

## The preview rule, from CLAUDE.md, non-negotiable
When he says **"preview"**, **"run preview"**, or **"/p"**:
1. Publish `ptt-wireframe.html` with the `Artifact` tool. **Same file path every time**
   so the URL stays stable.
2. Reply with the artifact URL.
3. **Always also include the githack link.** Every single time.
```
https://raw.githack.com/marklevi7/temp-public-3/claude/nets-ptt-prototype-init-avqddf/ptt-wireframe.html
```
Never use `SendUserFile` for the prototype — iOS Quick Look does not run JavaScript and
he will see a broken page.

## Why two links
- The **artifact** renders in the side panel inside the Claude app. Good for looking.
  It is a sandboxed iframe, so **the microphone never works there**. Do not argue about
  this, do not suggest workarounds, just always give the second link.
- **githack** is a real public URL, opens in Safari or Chrome, mic permission prompt
  appears, real recording works. Cache lags 30–60 seconds behind a push.

## What he does not have
There is no in-app browser panel with arrow and pencil tools in this session. That is a
local-session feature. This session is a cloud container, so `localhost` is unreachable
from his Mac. He asked for it repeatedly and got frustrated. Do not relitigate it —
give the two links and move on.

---

# PART 12 — TESTING RULES

Always verify before showing him anything.

```python
from playwright.sync_api import sync_playwright
b = p.chromium.launch(executable_path='/opt/pw-browsers/chromium')
c = b.new_context(viewport={'width':390,'height':844}, device_scale_factor=2,
                  is_mobile=True, has_touch=True)
```
- Chromium lives at `/opt/pw-browsers/chromium`. Do **not** run `playwright install`.
- Always `is_mobile=True, has_touch=True`. Plain `--window-size` below ~500px is silently
  floored at 500 and will give you a wrong clientWidth. This wasted a whole round once.
- Check on 390×844, 375×667, 430×932, and 360×800 for Figma parity.
- Always assert: no horizontal overflow, no `pageerror`, geometry measured with
  `bounding_box()` — never eyeballed from a screenshot.
- For the mic: `--use-fake-ui-for-media-stream --use-fake-device-for-media-stream` plus
  `permissions=['microphone']`.
- For autoplay: `--autoplay-policy=no-user-gesture-required`.
- To verify sounds, monkey-patch `AudioContext.prototype.createOscillator` in an init
  script and record `frequency.value` and the scheduled start offset.
- To verify a meter is really live, sample it every 50ms and prove consecutive frames
  differ; to verify it does not move, prove x drift is 0.00px across frames.

**When Mark says "check three times", do three genuinely different checks.** Not the same
check repeated. He will call it out.

---

# PART 13 — ENVIRONMENT TRAPS

1. This runs in a **cloud container**, not on Mark's Mac. `localhost` never reaches him.
2. The artifact panel is a **sandboxed iframe** — mic is blocked there, always.
3. Pasted images are **not on disk**. Pull them out of the session transcript jsonl.
4. `gTTS` and `imageio-ffmpeg` are installed. There is no system `ffmpeg` on PATH —
   get it with `python3 -c "import imageio_ffmpeg;print(imageio_ffmpeg.get_ffmpeg_exe())"`.
5. githack cache lags 30–60s behind a push. Say so if he reports a stale page.
6. The `gh` CLI does not exist. Use the GitHub MCP tools.
7. A stop hook nags about uncommitted files. Commit and push at the end of every turn.
8. MCP servers disconnect and reconnect constantly and their tool prefixes change between
   a friendly name like `mcp__Figma__*` and a uuid like `mcp__2529e674-…__*`.
   Re-run `ToolSearch` when a call fails with "no matching tool".

## Git conventions
```
git add -A && git commit -q -m "…" && git push -u origin claude/nets-ptt-prototype-init-avqddf
```
53 commits so far. Never push to another branch.

---

# PART 14 — HEBREW GLOSSARY

```
הקפצה / הקפצות     alert / alerts — a call-out to the standby squad
כיתת כוננות         standby squad
רבש״ץ / רבשצ        settlement security coordinator
חמ״ל                operations room
מוקד                dispatch centre
ניידת               patrol car
מצב PTT מופעל       PTT mode is on
משדר                transmitting
מדבר                talking
מתחבר מחדש…         reconnecting…
הגישה למיקרופון נחסמה   microphone access blocked
משתתפים             participants
צ׳אטים / צאטים      chats
אירועים             events
מפה                 map
עידכונים            updates
בית                 home
תרגול               drill / exercise
הדרכות דניאל        a settlement name used in the mock data
```

## Mock data used in the prototype
People: יוסי ישראלי · ראובן עוז · אילן מעוז · נדב אבידן · גיל בן פורת · אביגדור נאמן ·
מל דוד · ערן רותם · דניאל תורג׳מן
Groups: כיתת כוננות רמת גן · מפקדי מרחב · קבוצה גדולה
Events: הרצל 60, נתניה · השקמה 2, נתניה · זיהוי רחפן - חיישן קולי
Widget: הקפצת תרגיל · תרגול · רמת גן • אביר לילה ב׳ • 22:03 · counters 1 2 21 101 / 3 2 4

---

# PART 15 — WHAT TO DO FIRST

1. Finish the Figma upload — 12 screens into Section 5 `3866:76810`, grouped per flow
   letter, labels kept exactly as the filenames.
2. Wire the one-chat-only rule for PTT, so turning it on in chat B turns it off in chat A
   with the A2 toast.
3. Then continue down the task list.

Do not ask him to re-explain anything in this document. It is all here.
