# Takkie Translate Offline

### Privacy-first text translation for macOS. Powered by Google TranslateGemma 12b.

Takkie Translate isn't just a simple wrapper around an LLM. It's a thoughtfully engineered solution for local AI translation - powered by TranslateGemma 12b Q4_K_M.

This project provides a template for packaging AI for use in places where there's no internet. It eliminates the "technical friction" usually associated with local LLMs by automating the entire environment setup - from port detection to model management. 

Takkie is essentially a portable, folder-based translation app that doesn't require complex system-wide installation.


<br>

<img src="images/image3.png" alt="Laptop on a desk." height="400">

<br>

- Double-click to install and run.
- Supports 55 languages and regional variants (e.g., pt-BR vs. pt-PT or zh-Hant vs. zh-Hans).
- Web based Flask app that looks and feels like a native macOS application.
- Your data never leaves your machine. Total privacy for sensitive work.
- Ephemeral data processing. No sensitive data is stored.
- Bundles all binary executables together with the app - including Ollama and the model.
- Copies of the installed app can be shared using a thumb-drive or AirDrop.
- All dependencies travel with the copy.
- Runs completely offline.
- Can be run on an external SSD.
- Runs in a virtual environment. Other software on the user's computer is not disturbed.
- Easy to audit by Human and AI. Uses a single-file architecture.


<br>
<img src="images/image2.png" alt="Web page" height="400">
<p>GoogleTranslate style UI</p>
<br>

<img src="images/image1.png" alt="Web page" height="400">
<p>Includes regional language variants</p>
<br>

## Security

- <strong>Strictly local network binding</strong> — Flask is hardcoded to bind on ```127.0.0.1``` only. A check_host() guard aborts the process immediately if any attempt is made to bind to a non-loopback address, making the app unreachable from other devices on the network.
Dynamic port assignment — Both the Flask server and the bundled Ollama instance use dynamically selected free ports rather than fixed, well-known ports, reducing the risk of port-squatting attacks and conflicts with other services.

- <strong>No data persistence</strong> — Translation input and output are processed ephemerally in memory. No user text, history, or session data is written to disk at any point.

- <strong>Input validation and allowlisting</strong> — The ```/translate``` endpoint validates source and target languages against a pre-loaded allowlist (```_VALID_LANG_PAIRS```) and enforces a 32,000-character input limit. Malformed or missing fields return a 400 error before any model interaction occurs.
  
- <strong>Strict HTTP security headers</strong> — Every response includes ```Content-Security-Policy``` (restricting resource loading to ```self```), ```X-Frame-Options: DENY```, ```X-Content-Type-Options: nosniff```, ```Referrer-Policy: no-referrer```, and a ```Permissions-Policy``` blocking camera, geolocation, and payment APIs.

- <strong>No caching of sensitive content</strong> — All responses include ```Cache-Control: no-store``` and ```Pragma: no-cache``` to prevent translation content from being stored by the browser or any intermediary cache.

- <strong>Bundled, isolated Ollama binary</strong> — The app uses its own bundled Ollama binary pointed at a project-local model directory, preventing cross-contamination with any system-level Ollama installation or models.
  
- <strong>Incognito WebView</strong> — The app window opens with ```private_mode=True```, so no cookies, browsing history, or cached data persists after the session ends. This also prevents the WebView from inheriting state from other browser sessions on the machine.
  
- <strong>Isolated virtual environment</strong> — The app runs in a self-contained Python virtual environment, ensuring it cannot interfere with or be affected by other software on the user's system.

- <strong>Auditable single-file architecture</strong> — All application logic lives in a single ```app.py```, making the full codebase straightforward for users or security reviewers to inspect in its entirety.

## Data Hygiene Best Practices

Even with a secure app, "Human Error" can leave trails. Please follow these rules:

- <strong>The Clipboard Rule</strong>: If you "Copy" a sensitive translation to paste into a report, that text stays in the Mac’s "Clipboard" (the temporary memory).<br>
Safety Tip: After you finish your work, copy a random, non-sensitive word (like the word "Orange") to "bump" the sensitive text out of the computer's memory.

- <strong>The USB Rule</strong>: If you are running the app from a thumb drive, always "Eject" the drive properly before unplugging it. This ensures the temporary "Virtual Environment" closes correctly and leaves no fragments on the host Mac.


<br>

## System Requirements

To ensure optimal performance, your system should meet the following specifications:

- Operating System: macOS
- Processor: Apple Silicon (M1, M2, M3, etc.)
- Memory: 16 GB RAM
- Storage: 8.5 GB free disk space

<br>

## Where to download

The project folder is stored as a HuggingFace dataset. Hugging Face automatically generates SHA256 hashes for every file in a dataset repository.<br>
Please click this link to auto download:<br>
https://huggingface.co/datasets/vbookshelf/Takkie-Translate-Offline-TDA/resolve/main/Takkie-Translate-v1.0-TDA.zip?download=true

<br>

## How to install

Simply double click the ```start-mac-app.command``` file to install and run.

A quick installation guide is included in the project folder.

<br>

## References

- Thumb-Drive-App-Concept<br>
https://github.com/vbookshelf/Thumb-Drive-App-Concept

- Single-File Architecture: One file to rule them all<br>
https://github.com/vbookshelf/Single-File-Flask-Web-App

- pywebview<br>
https://github.com/r0x0r/pywebview

- Ollama - translategemma:12b<br>
  https://ollama.com/library/translategemma:12b

<br>

## Revision History
Version 1.0<br>
5-March-2026<br>
Prototype. Released for testing.

<br>

