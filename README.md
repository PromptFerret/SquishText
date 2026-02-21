# SquishText

Compress text into a shareable encoded string, and decompress it back. No server, no accounts, no dependencies - the compressed data IS the payload. Runs entirely in your browser.

**Live:** [promptferret.github.io/SquishText](https://promptferret.github.io/SquishText/)

## What It Does

- **Squish**: paste any text, get a compact base64-encoded string with a human-readable header
- **Unsquish**: paste an encoded string, get the original text back (byte-for-byte identical)
- **Share via link**: payload embedded in the URL hash - anyone with the link sees the decoded text instantly
- **Copy to clipboard**: encoded output includes decode instructions that LLMs can follow directly

Typical English text compresses 35-50% smaller. Highly repetitive text (tables, lists, structured data) compresses much better.

## How It Works

1. **Compress**: deflate-raw via the browser's `CompressionStream` API
2. **Encode**: base64 for universal pasteability (Discord, chat, email, anywhere)
3. **Checksum**: CRC32 appended to detect corruption
4. **Header**: human/LLM-readable decode instructions prepended

The header is informational only - stripping it doesn't affect decompression. Old and new payloads are fully interchangeable.

## Use Cases

- Share a full D&D character sheet as a single pasteable blob
- Compress session notes, item lists, or build guides for sharing
- Pack markdown output from the [GSheetCharacterExporter](https://promptferret.github.io/GSheetCharacterExporter/) into a compact format
- Light obfuscation (not encryption) - text isn't casually readable
- Link sharing - payload in URL hash, auto-decodes on open

## Getting Started

### Use it online

Visit [promptferret.github.io/SquishText](https://promptferret.github.io/SquishText/) - nothing to install.

### Run locally

```bash
git clone https://github.com/PromptFerret/SquishText.git
open SquishText/index.html
```

Works directly from `file://` - no server needed, no fetch calls, no CORS issues.

### Host it yourself

Copy `index.html` to any web server or static hosting (GitHub Pages, Netlify, S3, etc.). It's a single self-contained file with no external dependencies.

## Browser Support

Requires `CompressionStream` / `DecompressionStream`:
- Chrome 80+
- Firefox 113+
- Safari 16.4+

No polyfill - if the API isn't available, a message suggests upgrading.

## URL Length Limits

Share links encode the payload in the URL hash. Practical limits:

| Browser | URL length |
|---------|-----------|
| Chrome  | ~2MB      |
| Firefox | ~65,000 chars |
| Safari  | ~80,000 chars |

Typical character sheets compress to 2,000-6,000 characters - well within all limits.

## Contributing

This is a single HTML file - no build step, no package manager, no framework. Edit `index.html` and refresh.

1. Fork the repo
2. Make your changes to `index.html`
3. Test in a browser
4. Submit a pull request

Read `CLAUDE.md` for detailed architecture documentation (compression pipeline, payload format, UI design, CRC32 implementation).

## License

[MIT License](LICENSE) - Copyright (c) 2026 PromptFerret

## Links

- [All PromptFerret Tools](https://promptferret.github.io/tools/)
- [PromptFerret](https://promptferret.github.io)
