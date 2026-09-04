# Kai — releases

**An AI piano teacher that works alongside a human one — the practice partner
a student has at home, between lessons.**

![A student practising at a MIDI keyboard wearing a mixed-reality headset, with
a laptop, audio interface and handwritten manuscript on the desk](vision.jpg)

A piano teacher sees a student for half an hour a week. The other six days are
where the playing actually gets built, and nobody is watching. Kai is the thing
that sits with a student in between: it watches the hands through a webcam,
confirms the notes over MIDI, and keeps track of what needs work — against the
assignment the human teacher set. It reports back to that teacher. It does not
overrule them. (the picture above is a future vision of the project)

## What this repository is

**The release channel, not the source.** It holds installers, their checksums,
and what changed in each version. The code lives in a private repository.

Kai checks here for updates. Because this repo is public, it does that with no
account, no token, and nobody's permission.

## Install

1. Open [the latest release](../../releases/latest)
2. Download `Kai.Setup.<version>.exe`
3. Run it

### Windows will warn you, and it is right to

The installer is **not code-signed yet**, so SmartScreen shows "Windows
protected your PC". That warning is accurate: Windows genuinely cannot verify
who published this. If you trust where you got it, click **More info → Run
anyway**. A signing certificate is on the list of things to fix.

Some antivirus tools also flag the bundled plugin host, `kai-vst-host.exe`. It
is a small native program that loads VST3 audio plugins and talks to Kai over a
pipe — behaviour a heuristic scanner has no way to tell apart from something
worse. It has been flagged as a false positive before. If yours quarantines it,
Kai will start but will not be able to load your own instruments.

### Check what you downloaded

Every release ships a `manifest.json` carrying the installer's SHA-256:

```powershell
Get-FileHash .\Kai.Setup.0.1.2.exe -Algorithm SHA256
```

Compare it to the `sha256` field. Kai's own updater does this on every download
and refuses to run an installer that does not match — a release published
without a checksum is one Kai will not install at all.

## What you need

| | |
|---|---|
| Windows | 10 or 11 |
| Webcam | only for the hand-watching. A fixed mount or tripod helps a lot — it wants a roughly head-on view of the keys |
| MIDI keyboard | only for note confirmation. Without one, the built-in piano still plays |
| VST3 plugins | optional, if you would rather play through your own instruments |

## Updating

Kai checks here when it starts, and **Settings → Updates** has a Check button.
It never installs anything without being asked, verifies the download against
the checksum above, and relaunches into the new version. If an update lands
badly, the first launch afterwards writes a self-check saying so rather than
leaving you to guess.

## Feedback

[Open an issue](../../issues/new). There is a **feedback** link at the bottom
left of the app that fills one in for you — it opens this page with the title
and description already written, and you press Submit under your own GitHub
account. Kai never posts on your behalf, and holds no credential it could post
with.

It attaches the Kai version and your operating system. Not your name, not your
email. Issues here are public, so do not paste anything you would rather not
have read.

## Status

Early, and honest about it. Watching, listening, the keybed detector, the
plugin host and this update path all work. The teacher-facing backend is
written but not deployed, so assignments have nothing to read yet. Each
release's notes say what actually changed.
