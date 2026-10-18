# Scratch

A plain HTML page. The heading is written in `index.html`. The other words come from other files.

## Files

- `index.html` is the page. The `<title>` is the browser tab text. The `<h1>` is the heading. A short script reads the two files below and fills in the paragraph and the list.
- `about.txt` is the paragraph under the heading. Change the sentence, save, and refresh.
- `notes.csv` is the list. The first row is the header `done,text`. Each later row is one item. `no` means not done, and `yes` means done. The script splits on the first comma, so a note may contain a comma.

## Run it

From this folder:

```
python3 -m http.server 43117
```

Open http://127.0.0.1:43117

The script can read the other files only when the page is served this way. Opening `index.html` straight from the disk leaves the paragraph and the list empty.
