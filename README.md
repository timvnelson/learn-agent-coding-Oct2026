# Scratch

A plain HTML page. The heading is written in `sites/index.html`. The other words come from other files in that same folder.

## Files

- `sites/index.html` is the page. The `<title>` is the browser tab text. The `<h1>` is the heading. A short script reads the two files below and fills in the paragraph and the list.
- `sites/about.txt` is the text under the heading. A blank line starts a new paragraph. Change it, save, and refresh.
- `sites/notes.csv` is the list. The first row is the header `done,text`. Each later row is one item. `no` means not done, and `yes` means done. The script splits on the first comma, so a note may contain a comma.
- `AGENTS.md` is notes for an agent. It is outside `sites`, so the Python server does not serve it.

## Run it

From this folder:

```
python3 -m http.server 43117 --directory sites
```

Open http://127.0.0.1:43117

The script can read the other files only when the page is served this way. Opening `index.html` straight from the disk leaves the paragraph and the list empty.

## GitHub and CI

The project lives at `timvnelson/learn-agent-coding-Oct2026` on GitHub. Changes go in through pull requests. A small automated check runs on every push and pull request: it confirms `sites/index.html` still has the expected `<h1>` heading. See `.github/workflows/test.yml`.

## Coolify

The page auto-deploys from `main` to `http://a3rpxrrt2enquwxubsymwqmz.66.179.209.175.sslip.io`. Every pull request also gets its own live preview deployment at a similar address, so a change can be viewed before merging. See "Phase 4 status" in `AGENTS.md` for the setup details.

## Next experiments

A few things not started yet — see "Next experiments" in `AGENTS.md` for details: a real domain and HTTPS for Coolify, branch protection on `main`, practicing a real merge conflict, and a permanent fix for a websocket warning currently worked around by disabling an ad blocker.
