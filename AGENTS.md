# Scratch

Practice project for learning Cursor, HTML, a little JavaScript, and Git. This is not a production site.

## Names

- The Linux computer this agent runs on is the cloud machine.
- Cursor Desktop is the app on the Mac. The Agents Window is the chat screen. This conversation is a cloud agent.
- The iPhone app is only the chat. It cannot open these files or this page. Do not tell the user to preview the page on the iPhone.

## Layout

- `sites/` is the only folder the Python server should serve.
- `sites/index.html` is the page. The `<title>` and `<h1>` stay in this file. The `<script>` runs in the browser. It reads the two files below.
- `sites/about.txt` is the text under the heading. A blank line starts a new paragraph.
- `sites/notes.csv` is the list. The first row is `done,text`. `yes` checks the box. `no` leaves it empty. Split on the first comma, so a note may contain a comma.
- `README.md` is the human explanation of how to run the page.
- `AGENTS.md` is this file. It stays outside `sites/` so the Python server does not serve it.
- Do not commit `.index.html.swp`. It is a leftover Vim swap file.

## Python server

There is no Python code in this project. The Python server only sends files. Start it so the served folder is `sites`:

```
python3 -m http.server 43117 --bind 0.0.0.0 --directory sites
```

Open http://127.0.0.1:43117

Opening `index.html` from the disk leaves the paragraph and the list empty, because `fetch` needs the Python server. Do not add Node, nginx, Apache, Next.js, or CSS unless the user asks.

## Phases

- Phase 1 and Phase 2 are done. The page is plain HTML, and the paragraph and list come from files.
- Phase 3 is GitHub. The project is not on GitHub yet. When the user asks, create the repository, then show a commit, a branch, and a pull request. A small automated test (CI) can check that the page has the expected heading. That test is part of Phase 3.
- Phase 4 is Coolify, after GitHub. `http://66.179.209.175:8000` is the Coolify dashboard, not the public page. Do not contact that server until the user asks. A deploy would get its own address.

## Git

The user is learning Git and often wants to type `git add`, `git commit`, and `git push` themselves. A change in a file is not a commit. A commit on the cloud machine is not on the remote copy until `git push`. `main` and `origin/main` are the same branch in two places: here, and Cursor's remote copy.

## How to answer

Keep explanations short and plain. The user knows HTML and is new to CSS, JavaScript, and Git. Say "Python server" when you mean the `http.server` process.
