# NETS PTT — working agreements

## "preview" / "run preview" / "/p" / "show me the app"
When the user says any of these, do this immediately, no questions, no alternatives:
1. Open it live in the Browser pane: `preview_start` with `{name: "ptt"}` (starts/reuses the local server on port 8934), then `navigate` to `http://localhost:8934/ptt-wireframe.html` (use `force: true` to bypass cache). This is the part the user actually needs — it's what they mean by "show me" / "run preview here". Links alone are NOT a substitute for this step; do it every time, even if you already gave links earlier in the session.
2. Do NOT post the githack link — Mark said he doesn't need it. Just push commits to the GitHub repo.

Do NOT publish a `claude.ai/code/artifact` link — the user does not want it, explicitly opted out. Do NOT send the file with `SendUserFile` either (iOS Quick Look doesn't run JS).
The Browser-pane preview is the live in-session view. That plus a push is all he wants.

## Project
Single file: `ptt-wireframe.html` — mobile PTT wireframe, Hebrew RTL, light theme only.
Branch: `claude/nets-ptt-prototype-init-avqddf`
