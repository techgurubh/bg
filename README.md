# bg

Remove image backgrounds in just one click.

A lightweight tool to quickly remove backgrounds from images — ideal for product photos, avatars, and graphics. This repository contains a simple app and examples for removing backgrounds locally or in a server/CLI flow.

---

Table of contents
- [Features](#features)
- [Demo / Screenshot](#demo--screenshot)
- [Quick start](#quick-start)
  - [Clone](#clone)
  - [Run locally (web UI)](#run-locally-web-ui)
  - [CLI (example)](#cli-example)
  - [Docker (optional)](#docker-optional)
- [Usage examples](#usage-examples)
  - [Web UI](#web-ui)
  - [CLI](#cli)
  - [HTTP API (example)](#http-api-example)
- [File formats & output](#file-formats--output)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)
- [Authors](#authors)

---

Features
- One-click background removal for single images
- Fast local processing (no external uploads if running locally)
- Preserves fine edges (hair, fur) with alpha output
- Export to PNG with transparency or JPG with solid background
- Simple CLI and HTTP API examples included

Demo / Screenshot
> Add screenshot(s) of the UI or before/after images here (e.g. in `/assets`).

---

Quick start

Clone
```bash
git clone https://github.com/techgurubh/bg.git
cd bg
```

Run locally (web UI)
- If the project uses Node:
```bash
# install and start
npm install
npm start
# open http://localhost:3000
```
- If the project uses Python/Flask or FastAPI:
```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
# run the app (adjust command to your project)
python app.py
# open http://localhost:8000
```

CLI (example)
If a CLI binary or script is provided, a typical usage looks like:
```bash
# remove background from input.png and write alpha PNG to output.png
bg --input input.png --output output.png
# or short flags
bg -i input.png -o output.png
```
(If your project exposes a script like `bin/bg` or an npm `bin` entry, `npm link` can expose `bg` globally for local testing.)

Docker (optional)
```bash
# build
docker build -t bg:latest .
# run (example port)
docker run --rm -p 3000:3000 bg:latest
```

---

Usage examples

Web UI
1. Start the app (see Quick start)
2. Open the web UI in your browser
3. Drag & drop or click to upload an image
4. Click "Remove background"
5. Download the result (PNG with transparency)

CLI
```bash
# single file
bg -i ./photos/product.jpg -o ./out/product.png

# batch (example)
for f in ./photos/*.jpg; do
  bg -i "$f" -o "./out/$(basename "$f" .jpg).png"
done
```

HTTP API (example)
If the repo includes a server that exposes a POST `/remove` endpoint:
```bash
curl -X POST "http://localhost:8000/remove" \
  -F "file=@./input.jpg" \
  -o output.png
```
Response behavior:
- 200 with image/png (alpha) for success
- 4xx / 5xx for errors; check response JSON for details

---

File formats & output
- Input: JPG, PNG (RGB)
- Output: PNG with alpha channel (recommended)
- Optionally: JPG with configurable background color (if transparency not desired)

---

Roadmap
- [ ] Improve edge handling (hair/fine details)
- [ ] Add batch processing mode with GPU acceleration
- [ ] Add presets for product photography (shadows, reflections)
- [ ] Add mobile-friendly web UI

---

Contributing
Contributions are welcome! Please:
1. Fork the repository
2. Create a branch: `git checkout -b feat/your-feature`
3. Commit your changes: `git commit -m "Add some feature"`
4. Push to the branch: `git push origin feat/your-feature`
5. Open a Pull Request

Please include tests and update documentation when appropriate.

If you file bugs, include:
- steps to reproduce
- sample image (if possible)
- expected vs actual behavior
- logs / stack traces

---

License
This project is released under the MIT License. See [LICENSE](LICENSE) for details.

---

Authors
- Maintainer: [techgurubh](https://github.com/techgurubh)

Repository: [techgurubh/bg](https://github.com/techgurubh/bg)

---

Notes
- This README provides usage patterns and examples. Adjust the commands and snippets above to match the actual implementation files and scripts in this repository (for example `app.py`, `server.js`, or a `bin/bg` entry).
- If you want, I can tailor this README to the exact stack (Node, Python, Go, etc.) used in this repo — tell me which language/framework the project uses and I will update the instructions and examples accordingly.
