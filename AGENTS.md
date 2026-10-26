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
- Phase 3 is GitHub. The repository exists: `timvnelson/learn-agent-coding-Oct2026`, **public** (changed from private so branch protection would actually enforce — see below; GitHub does not enforce branch protection on a private repo without a paid plan). Commits, branches, and pull requests all happen there now. A CI test runs on every push and pull request: `.github/workflows/test.yml` checks that `sites/index.html` still has the expected `<h1>` line. If the heading text changes on purpose, update the `grep` line in that workflow to match, or the check will fail.
- `main` is protected by a GitHub **Ruleset** (Settings → Rulesets): requires a pull request before merging, requires the `check-heading` status check to pass, blocks force pushes, restricts deletions. Confirmed working two ways: a direct commit through GitHub's web editor was blocked, and a direct write via the GitHub API (the same connection this agent uses) was rejected with "Repository rule violations found."
- Phase 4 is Coolify, after GitHub. `http://66.179.209.175:8000` is the Coolify dashboard, not the public page. A deploy gets its own address.

### Phase 4 status (done)

Coolify is set up and working:

- **How it is set up:** a Coolify GitHub App integration (name `vivacious-vulture-9fyz93jdx0gh` in Coolify) is connected to `timvnelson/learn-agent-coding-Oct2026`. The application uses the **Static** build pack, base directory `/sites`, web server `nginx:alpine` — not the project's own Python server. No Dockerfile was needed.
- **Production page:** pushes to `main` auto-deploy to `http://a3rpxrrt2enquwxubsymwqmz.66.179.209.175.sslip.io` (a free wildcard-DNS address standing in for a real domain).
- **Preview Deployments are on.** Opening a pull request builds a separate, temporary preview at a `{{pr_id}}.<same sslip.io host>` address, so the user can view the change live before merging — confirmed working on pull request #10.
- **Known quirk, not a bug:** the Coolify dashboard sometimes shows "Cannot connect to real-time service." Ports 6001/6002 are correctly open (confirmed from both the server and an external port checker); the likely cause is a browser ad blocker flagging the websocket connection to a raw IP. Disabling the ad blocker for that site is the workaround in use. See "Next experiments" below for the real fix.

### Real domain for Coolify (in progress, paused — DNSSEC broke email, waiting ~48h)

Two subdomains of `timvnelson.com` (registered at DreamHost, which also hosts its DNS) were set up to point at `66.179.209.175`: `learn-agents.timvnelson.com` (the public page) and `coolify.timvnelson.com` (the Coolify dashboard itself, via its Instance Domain setting). Both are configured correctly in Coolify and in DreamHost's DNS records, but neither was confirmed loading yet when this was paused.

- **Real blocker found along the way:** `timvnelson.com` has a broken DNSSEC setup — a DS record exists at the registry level with nothing on DreamHost's nameservers able to sign for it (DreamHost's own nameservers do not support DNSSEC signing at all; it requires moving to an external DNS host, which the user does not want to do right now). This causes every DNSSEC-validating resolver (Google's, and apparently the user's own) to refuse to resolve **anything** under `timvnelson.com` — not just the new subdomains. Confirmed by querying `https://dns.google/resolve?name=timvnelson.com` (returns `Status: 2`, "DNSSEC validation failure"), and bypassing it by adding `&cd=true` to that same query, which shows the real, current records underneath.
- **While hunting for the DS record to remove it, the user accidentally deleted the domain's MX and TXT records** (confirmed gone via the same `cd=true` DNS-over-HTTPS trick). This broke email on `@timvnelson.com`, unrelated to the DNSSEC problem itself. DreamHost support was not yet contacted about restoring them as of this note; the email provider used for the address was not identified either — either of those would be the fastest way to fix the email side, independent of the DNSSEC fix.
- **Decision:** wait roughly 48 hours and recheck everything (DNS, email, DNSSEC) rather than keep digging live. Whoever picks this up next should re-run the `cd=true` DNS-over-HTTPS check above before assuming anything is still broken or still fixed.

### Next experiments (not started, for whenever the user wants to try them)

- **Practice a real merge conflict on purpose** — edit the same line of a file on two branches and resolve the conflict by hand. Everything merged so far has gone cleanly, so this hasn't come up yet.

## Git

The user is learning Git and often wants to type `git add`, `git commit`, and `git push` themselves. A change in a file is not a commit. A commit on the cloud machine is not on the remote copy until `git push`. `main` and `origin/main` are the same branch in two places: here, and Cursor's remote copy.

Three things can change this repo: this cloud agent, Cursor (including edits Cursor makes straight on the GitHub website), and the user typing Git commands directly. Pull `main` before starting new work if any of those might have moved it.

## Pull requests and this agent's branch

This cloud agent's branch is `claude/intelligent-fermi-spdl22`. Pull requests go through GitHub, not plain `git merge`, so the work is visible and the CI test runs first. Once a pull request for this branch is merged, the branch is done — pushing more commits to it will not reopen or update that pull request. Before starting the next change, reset the branch from the latest `main` first, then make the change and push; a new pull request covers that new work.

## How to answer

Keep explanations short and plain. The user knows HTML and is new to CSS, JavaScript, and Git. Say "Python server" when you mean the `http.server` process.
