# CLAUDE.md

## Brag videos are Instagram Reels

`.claude/skills/brag` and `.claude/skills/brag-slim` are vendored from
https://github.com/latent-spaces/brag (MIT). Don't edit them in place; put
overrides here so the skills can be re-synced from upstream.

Every `/brag` or `/brag-slim` run in this repo is for an Instagram Reel unless
the user says otherwise:

- **Format:** always `--format vertical` (1080×1920, 9:16, 30fps), even when
  the user doesn't pass it.
- **Length:** 14-19 seconds. The hook has to land in the first 2 seconds, because
  viewers scroll past before that.
- **Safe zone:** Instagram covers the top ~220px (header) and the bottom
  ~420px (caption, audio label, buttons), plus ~120px on the right edge
  (like/comment/share icons). Keep titles, product names and CTAs inside the
  middle of the frame, never against an edge.
- **Captions:** most people watch with the sound off, so any spoken or
  essential line must also appear as on-screen text.
- **Music:** the bundled ende.app tracks have unverified license terms (see
  `.claude/skills/brag/assets/music/README.md`). Also render a `--no-music`
  version so the user can add licensed or trending audio inside Instagram.
- **Export:** H.264 video + AAC audio MP4, under 100MB.
- **Share copy:** write an Instagram caption (hook line, 1–3 short lines,
  3–5 hashtags) in place of the default X/LinkedIn copy.

## Changing the voice on a finished Reel

When the user uploads a finished Reel and asks for a different voice:

1. Transcribe it with timestamps (Whisper small.en + silero VAD via the
   `sherpa-onnx` pip package; models from the k2-fsa/sherpa-onnx GitHub
   releases, `asr-models` tag).
2. Separate the music bed from the old voice with UVR-MDX-NET-Inst_HQ_4
   (sherpa-onnx `source-separation-models` release).
3. Generate each line with `kokoro-onnx` (model files from the
   thewh1teagle/kokoro-onnx `model-files-v1.0` release), starting at the
   original line's timestamp; speed a line up (max 1.3x) only if it overruns
   its scene.
4. Match the old voice's loudness, mix over the music bed, re-encode to
   H.264 + AAC, and also export a voice-only version.
5. Transcribe the result to confirm every line is present and none of the old
   voice remains. If the user didn't name a voice, pick one clearly different
   from the original and include a short sample file of several Kokoro voices.
