# MP3 Converter

A single-page web app that converts audio files to MP3 right in your browser. Files are decoded and encoded on your device and are never uploaded.

## Features

- Converts M4A, WAV, OGG, FLAC, AAC, Opus and other formats your browser can decode
- Batch conversion: add several files and convert them in one go
- Choose a bitrate: 128, 192 (default), 256 or 320 kbps
- Drag and drop or file picker
- Per-file progress bar and one-click MP3 download
- Light and dark mode (follows your system setting)
- Works offline after the first load, apart from the font and encoder library (see below)

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app: markup, styles and script |
| `mp3-converter-icon.png` | Tab/favicon icon, referenced by `index.html` |

Keep both files in the same folder.

## Usage

1. Open `index.html` in a browser, or host the folder on any static web host.
2. Click **Choose audio files** or drop files onto the page.
3. Pick a quality from the **Quality** menu.
4. Click **Convert to MP3**.
5. When a file shows **Done**, click **Download MP3**. The output keeps the original name with a `.mp3` extension.

Use **Clear list** to remove all files and start over.

## How it works

1. The file is read into memory.
2. The browser's Web Audio API (`decodeAudioData`) decodes it to raw audio.
3. [lamejs](https://github.com/zhuker/lamejs) encodes the audio to MP3 in small blocks, so the page stays responsive and can show progress.
4. The result is offered as a download through a temporary object URL.

Stereo is preserved. Sources with more than two channels are reduced to the first two.

## Dependencies

Loaded from CDNs, so an internet connection is needed the first time:

- `lamejs` 1.2.1 from cdnjs.cloudflare.com (MP3 encoder)
- Bricolage Grotesque from Google Fonts (falls back to system fonts if unavailable)

To run fully offline, download `lame.min.js` and the font, and point `index.html` at the local copies.

## Browser support

Any modern browser with the Web Audio API: current Chrome, Edge, Safari and Firefox. Which input formats work depends on what the browser can decode. If a file fails with "Couldn't convert this file", try another browser or convert that file to WAV first.

## Limitations

- Whole files are decoded into memory, so very long recordings (for example, multi-hour files) may fail on low-memory devices.
- Output is encoded from decoded audio, so converting from an already lossy format (such as AAC or OGG) cannot improve quality.
- Metadata and cover art from the source file are not copied to the MP3.

## Privacy

Everything happens locally in the browser tab. No audio is sent to a server.
