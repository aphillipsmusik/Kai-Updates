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
overrule them. (The picture above is where this is going, not where it is.)

## What this repository is

**The release channel, not the source.** It holds the release notes and each
build's `manifest.json` — its version, size and SHA-256. The code lives in a
private repository.

Kai checks here for updates. Because this repo is public, it does that with no
account, no token, and nobody's permission.

## Getting Kai

**The installer is not attached to these releases, and that is deliberate.**
Kai is early software that watches a child through a webcam, so using it means
agreeing to terms first. From **0.1.3** onwards the installer is fetched by the
app itself, through a function that checks you are signed in and have accepted
those terms, and then hands out a link that expires in fifteen minutes. That is
how the terms can be required without making this repository private and
handing out read-only tokens.

So there are two paths, depending on what you already have:

| | |
|---|---|
| **Already running Kai** | **Settings → Updates → Check**. It fetches, verifies and installs. Nothing to download by hand. |
| **No copy yet** | Ask for the handout zip. It is one file — installer, licence, checksum and a README — and it is the only sanctioned way in for a first install. |

There is no download button on this page. If you are looking for a `.exe` in
the release assets, that is why it is not there.

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

### Check what you were given

Every release ships a `manifest.json` carrying the installer's SHA-256:

```powershell
Get-FileHash ".\Kai Setup 0.1.4.exe" -Algorithm SHA256
```

Compare it to the `sha256` field. Kai's own updater does this on every download
and refuses to run an installer that does not match — a release published
without a checksum is one Kai will not install at all.

A handout zip carries the same checksum in its README. If that zip was built
from a local rebuild rather than the published build, it says so in place of
the manifest rather than shipping a checksum that describes a different file.

## What you need

| | |
|---|---|
| Windows | 10 or 11 |
| Webcam | only for the hand-watching. A fixed mount or tripod helps a lot — it wants a roughly head-on view of the keys, from slightly above |
| MIDI keyboard | only for note confirmation. Without one, the built-in piano still plays |
| VST3 plugins | optional, if you would rather play through your own instruments |
| A Google account | how Kai knows whose practice is whose, and what lets it fetch updates |

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

Ideas raised here get used. Releases credit the people whose suggestions went
into them, by GitHub username, in the notes for that version.

## Your data

Kai watches a child play the piano, so it is worth being plain about what
leaves the machine.

- **No video and no audio ever leaves your computer.** The camera frames are
  processed on the machine and discarded. What is stored is a summary — which
  notes were played, which faults were seen, how often — never the footage.
  The database rules reject any record containing frames, audio or landmarks,
  so this is enforced rather than promised.
- **Practice summaries are visible to your teacher**, which is the point of
  the product, and to nobody else.
- **Lessons and exercises a teacher writes are shared with other teachers by
  default**, so that Kai can offer one teacher's exercise to another teacher's
  student who is stuck on the same thing. Any of them can be switched off.
- **Assignments are never shared.** An assignment names a student and describes
  what they are finding hard. There is no setting for this and there is no way
  to publish one.

## Status

Early, and honest about it. Watching, listening, the keybed detector, the
plugin host and this update path all work, and the backend behind sign-in,
material import and the gated download is deployed and live.

Still missing: no teacher account has yet set an assignment, so the teacher
side has nothing to read. The keybed detector has only ever been tested against
synthetic images, not a real piano in real light. Nothing is code-signed.

Each release's notes say what actually changed.
