# NETS PTT — working agreements

## "preview" / "run preview" / "/p" / "show me the app"
When the user says any of these, do this immediately, no questions, no alternatives:
1. Open it live in the Browser pane: `preview_start` with `{name: "ptt"}` (starts/reuses the local server on port 8934), then `navigate` to `http://localhost:8934/ptt-wireframe.html` (use `force: true` to bypass cache). This is the part the user actually needs — it's what they mean by "show me" / "run preview here". Links alone are NOT a substitute for this step; do it every time, even if you already gave links earlier in the session.
2. ALWAYS include the githack link too, every single time — it is the only one where the microphone works:
   https://raw.githack.com/marklevi7/temp-public-3/claude/nets-ptt-prototype-init-avqddf/ptt-wireframe.html
   Note: this link only reflects what's actually pushed to GitHub — if there are uncommitted local changes, it will be stale. Check `git status` and offer to commit+push if needed so this link isn't out of date.

Do NOT publish a `claude.ai/code/artifact` link — the user does not want it, explicitly opted out. Do NOT send the file with `SendUserFile` either (iOS Quick Look doesn't run JS).
The Browser-pane preview is the live in-session view; the githack link is for real mic testing. Do both.

## Project
Single file: `ptt-wireframe.html` — mobile PTT wireframe, Hebrew RTL, light theme only.
Branch: `claude/nets-ptt-prototype-init-avqddf`
