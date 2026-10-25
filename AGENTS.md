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
- Phase 3 is GitHub. The repository exists: `timvnelson/learn-agent-coding-Oct2026`, private. Commits, branches, and pull requests all happen there now. A CI test runs on every push and pull request: `.github/workflows/test.yml` checks that `sites/index.html` still has the expected `<h1>` line. If the heading text changes on purpose, update the `grep` line in that workflow to match, or the check will fail.
- Phase 4 is Coolify, after GitHub. `http://66.179.209.175:8000` is the Coolify dashboard, not the public page. Do not contact that server until the user asks. A deploy would get its own address.

### Phase 4 status (started, not finished)

The user decided on a plan but has not started clicking through it yet. Whichever agent picks this up next (Cursor or a cloud agent) should pick up from here, not re-ask the questions already settled:

- **What to set up:** Coolify's GitHub App integration, with Preview Deployments turned on. This builds a live, temporary deploy for each open pull request, with its own URL, so the user can click and view it before merging — separate from the GitHub Actions CI test, which still runs and shows pass/fail on the same PR.
- **How to set it up:** the user chose to click through Coolify's dashboard themselves, with the agent guiding step by step (describe what you see, agent says what's next). No Coolify credentials or tokens should be requested from or typed into the agent — this was a deliberate choice, not an oversight.
- **Known complication:** this project has no `Dockerfile` and no Node/package build config — it is a plain folder served by Python's `http.server`. Coolify will likely need either a small `Dockerfile` written for it, or its static-site option pointed at `sites/`. Expect this to take more than one try.
- **Not started yet:** nobody has logged into the Coolify dashboard for this as of this note. Start at "log into Coolify, find the GitHub integration settings."

## Git

The user is learning Git and often wants to type `git add`, `git commit`, and `git push` themselves. A change in a file is not a commit. A commit on the cloud machine is not on the remote copy until `git push`. `main` and `origin/main` are the same branch in two places: here, and Cursor's remote copy.

Three things can change this repo: this cloud agent, Cursor (including edits Cursor makes straight on the GitHub website), and the user typing Git commands directly. Pull `main` before starting new work if any of those might have moved it.

## Pull requests and this agent's branch

This cloud agent's branch is `claude/intelligent-fermi-spdl22`. Pull requests go through GitHub, not plain `git merge`, so the work is visible and the CI test runs first. Once a pull request for this branch is merged, the branch is done — pushing more commits to it will not reopen or update that pull request. Before starting the next change, reset the branch from the latest `main` first, then make the change and push; a new pull request covers that new work.

## How to answer

Keep explanations short and plain. The user knows HTML and is new to CSS, JavaScript, and Git. Say "Python server" when you mean the `http.server` process.
