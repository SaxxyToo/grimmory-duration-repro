# Sample files: folder audiobook length recorded at 2x

Free and public reproduction files for
[grimmory-tools/grimmory discussion #2777](https://github.com/orgs/grimmory-tools/discussions/2777).

Every file is a plain sine tone generated with ffmpeg — no third-party audio, no rights
attached. Released as CC0 / public domain.

| Folder | Real length | Recorded as |
|---|---|---|
| `samples/audiobook-stereo-22050/` — 3 tracks, 22.05 kHz stereo CBR 64k | 60 s | **120 s** |
| `samples/control-mono-22050/` — same rate and bitrate, mono | 20 s | 20 s |

(The tracks are just over 20 s each, so the measured total is 60.26 s — the recorded 120 s is
the sum of each track read as 40.12 s instead of 20.06 s.)

## How to reproduce

1. Add a library in Grimmory with Organization Mode "Book Per Folder".
2. Point it at `samples/audiobook-stereo-22050/`.
3. Scan, then read `book_file.duration_seconds` — it is `120` instead of `60`.
4. Do the same with `samples/control-mono-22050/` — that one is correct.

## Regenerating the files

```sh
ffmpeg -f lavfi -i "sine=frequency=440:duration=20" -ac 2 -ar 22050 \
       -c:a libmp3lame -b:a 64k track-01.mp3
```

`-ac 2` for the stereo folder, `-ac 1` for the mono control.