# Talking Explainer

A Claude Code skill that turns a topic into a narrated motion-design explainer: a cartoon presenter that really
talks (lip sync on your voice, poses on cue words, blinks), short kinetic text on screen, a clean Apple-style look,
a camera push and an emphasis beat in every scene, and your own brand on the opening, corner and end card.
1920x1080 at 60fps, with a 9:16 portrait cut for TikTok / Reels / Shorts when you want one.

Created by Kenneth Villar.

---

## What you need

| | |
|---|---|
| **Claude Code** | Any paid Claude plan. A film uses several parallel agents, so expect a long session (1-3 hours). |
| **Your voice** | An [ElevenLabs](https://elevenlabs.io) voice clone (best), or a clean recording of yourself reading the script in one take. |
| **A computer** | Windows 10/11 or macOS, about 5 GB free disk. A dedicated GPU makes the final render much faster. |
| **Tools** | Node.js 20+, Python 3.10+ (3.12 recommended), ffmpeg. The setup check tells you exactly what is missing. |
| **Optional** | Your own character (see "Your own presenter"), your logo, a background track you have the rights to. |

## Install

**1. Install the tools** (skip what you already have)

Windows (PowerShell):

```powershell
winget install OpenJS.NodeJS.LTS Python.Python.3.12 Gyan.FFmpeg
py -3.12 -m pip install numpy pillow scipy faster-whisper
```

macOS (Terminal, needs [Homebrew](https://brew.sh)):

```bash
brew install node python@3.12 ffmpeg
python3.12 -m pip install numpy pillow scipy faster-whisper
```

Then the video engine's helper skills (both systems):

```bash
npx hyperframes skills update general-video hyperframes-animation media-use
```

**2. Install the skills** - unzip this file, open a terminal in the unzipped folder (the one with `install.mjs`) and run:

```bash
node install.mjs
```

It copies three skills into `~/.claude/skills/` - `talking-explainer` (the one you talk to), plus `explainer-kit`
and `spatial-film` (the tools and the film engine it runs on) - and checks your machine. Restart Claude Code once
after it finishes.

**3. Start** - in any folder, tell Claude:

> make a talking explainer about how email marketing works

The first time, Claude runs the setup check and asks a few questions to build your profile: your brand name, logo,
colours, how you talk, your opener and closer lines, and which presenter. The profile lives in
`~/.talking-explainer/profile/` and every film after that uses it.

## How a film gets made

1. **Script** - Claude researches the topic and writes a hook-first script in your speaking style.
2. **Your take** - you record it (or generate it with your ElevenLabs clone) and hand Claude one MP3.
3. **Timings** - the take is transcribed to word timings; every animation is keyed to the word you say.
4. **Storyboard** - one frame per paragraph, each with a zoom beat and an emphasis beat. You approve the list.
5. **Build** - parallel workers build the scenes; the presenter, music and your brand are layered on top.
6. **Render + proof** - 60fps render, then a sync check on the rendered file and a frame check of every scene.

Ask for a portrait cut of a finished film with "make a portrait version for TikTok".

## Your own presenter

The skill ships with a talking demo presenter. To use your own character, ask Claude:

> make my own talking character

It gives you three image prompts to run with a reference picture of your character, then cuts the results into
poses, fits the blinks and the six mouth shapes, and shows you review sheets before any film uses it.

## Updating

Get the new zip, unzip it and run `node install.mjs` again. Your profile is kept.

## Credits

- Icons in the films: Solar by 480 Design (CC BY 4.0) - put "Icons: Solar by 480 Design (CC BY 4.0)" in your
  video description.
- Fonts: Geist, Montserrat, Poppins (SIL Open Font License 1.1).
- Video engine: [HyperFrames](https://www.npmjs.com/package/hyperframes).

See `LICENSE` for the terms, including the presenter artwork.
