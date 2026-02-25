## Cursor Cloud specific instructions

This is a Chrome browser extension (Manifest V2) called "谷歌访问助手" (Google Access Helper). It provides proxy-based access to Google services.

### Key facts
- **No build system, no package manager, no dependencies.** The extension is raw JS/HTML/CSS files.
- **No automated test suite.** There are no test files, test frameworks, or CI configuration.
- **Testing requires Chrome.** Load the `/workspace` directory as an unpacked extension in `chrome://extensions` with Developer Mode enabled.
- The core logic lives in `bg.js` (background script, ~3000 lines, obfuscated/formatted). `popup.html`/`popup.js` handle the browser action popup. `options.html`/`options.js` handle the settings page.
- The extension fetches proxy configurations from remote servers (`ggfwzs.com` and related domains) which are external and likely defunct. Full proxy functionality cannot be tested without those servers.

### Running / testing the extension

**Chrome 145+ (installed as `google-chrome`) does NOT support Manifest V2.** You must use Chrome 120, which is installed at `/tmp/chrome-linux64/chrome`. If it is not present, download it:
```bash
cd /tmp && curl -L -o chrome120.zip "https://storage.googleapis.com/chrome-for-testing-public/120.0.6099.109/linux64/chrome-linux64.zip" && unzip -q chrome120.zip
```

Launch with the extension pre-loaded:
```bash
/tmp/chrome-linux64/chrome --no-sandbox --no-first-run --user-data-dir=/tmp/chrome120-profile --load-extension=/workspace &
```

Alternatively, load manually:
1. Launch Chrome 120: `/tmp/chrome-linux64/chrome --no-sandbox --no-first-run --user-data-dir=/tmp/chrome120-profile &`
2. Navigate to `chrome://extensions`
3. Enable **Developer mode**
4. Click **Load unpacked** and select `/workspace`
5. The extension icon should appear in the toolbar; click it to open the popup.

### Lint / build / test
- There are no lint, build, or test commands. The extension has no `package.json` or equivalent.
- Manual verification in Chrome is the only testing method available.
