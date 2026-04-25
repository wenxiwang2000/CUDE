# 🧠 CUDE — Clustered Utility for Deep Embedding Rearrangement

> A local folder-cleaning and rearrangement tool with a simple GUI, embedding-based clustering, reversible folder operations, and optional LLM/vision-powered deep summarisation.

---

## ✨ What CUDE Does

CUDE helps you turn a messy folder into a clearer structure.

It first uses **file/folder names + embeddings** to cluster items into meaningful folders.  
Then, if you choose deep mode, it can use a **local GGUF LLM + optional vision/text summary workflow** to create deeper semantic organisation.

Most importantly, CUDE creates an undo manifest, so you can **derearrange / restore** the folder after the first rearrangement step.

---

## 🧩 Core Workflow

| Step | Action | Output |
|---:|---|---|
| 1️⃣ | Select one folder in the GUI | Root folder is loaded |
| 2️⃣ | Run name-based embedding rearrangement | Cluster folders are created |
| 3️⃣ | CUDE saves undo manifest | `_rearrange_deep_manifest.json` |
| 4️⃣ | App asks whether to run deep mode | Yes / No |
| 5️⃣ | Deep mode uses local LLM + summaries | Semantic nested folder structure |
| 6️⃣ | Undo button restores name-based rearrangement | Files move back using manifest |

---

## 🖥️ Main Features

| Feature | Description |
|---|---|
| 🪟 Simple GUI | Clean panel with folder selection, Run, Clear, and Undo |
| 🧠 Embedding clustering | Uses sentence embeddings to group files/folders |
| 🗂️ Cluster folder naming | Folder names are based on cluster center / semantic similarity |
| 🔁 Reversible rearrangement | Writes a JSON manifest for undo |
| 🦙 Local LLM support | Supports llama.cpp + GGUF model for deep summarisation |
| 🖼️ Optional vision summary | Can work with image/vision summarisation tools when configured |
| 📦 PyPI-style package | Can be installed and run as a Python package |
| 🍎 macOS app build | Includes scripts to build a `.app` on Mac |

---

## 📁 Recommended Folder Layout

For normal GUI use:

```text
cude_mac_app/
├── run_cude_mac.command
├── build_mac_app.command
├── run_gui.py
├── pyproject.toml
├── requirements_mac.txt
├── clean_taxonomy.txt
├── cude/
└── README.md
```

For deep mode with llama.cpp:

```text
cude_mac_app/
├── llama/
│   ├── llama-cli
│   └── model.gguf
├── run_cude_mac.command
├── build_mac_app.command
├── run_gui.py
├── clean_taxonomy.txt
└── cude/
```

---

## 🚀 Quick Start on macOS

### 1. Unzip the project

```bash
unzip cude.zip
cd cude_mac_app
```

### 2. Give permission to command files

```bash
chmod +x run_cude_mac.command build_mac_app.command
```

### 3. Run the GUI directly

```bash
./run_cude_mac.command
```

Then:

1. Select one folder.
2. Click **Run**.
3. Wait for name-based rearrangement.
4. Choose whether to run deep mode.
5. Use **Undo** if you want to restore the first rearrangement.

---

## 🍎 Build a macOS `.app`

Inside the unzipped project folder:

```bash
./build_mac_app.command
```

After build, the app should appear at:

```text
dist/Cude_Rearranger.app
```

You can zip it for private sharing:

```bash
cd dist
zip -r Cude_Rearranger_mac.zip Cude_Rearranger.app
```

> ⚠️ For public macOS distribution, you should sign and notarize the app with an Apple Developer ID.

---

## 📦 Install as a Python Package

Inside the project folder:

```bash
python3 -m pip install .
```

Then run:

```bash
cude-gui
```

Other available commands may include:

| Command | Purpose |
|---|---|
| `cude-gui` | Start the GUI |
| `cude-api` | Start the API server |
| `cude-summary` | Run summary builder |
| `cude-compare` | Compare summaries and create semantic layers |
| `cude-rearrange-deep` | Run name/embedding-based rearrangement |
| `cude-derearrange-deep` | Restore using manifest |
| `cude-download` | Download optional models, if configured |

---

## 🧪 Publish to PyPI

Build the package:

```bash
python3 -m pip install --upgrade pip build twine
python3 -m build
```

Upload to TestPyPI first:

```bash
python3 -m twine upload --repository testpypi dist/*
```

Upload to PyPI:

```bash
python3 -m twine upload dist/*
```

Recommended package name format:

```toml
[project]
name = "cude-rearranger"
version = "0.1.0"
```

Then users can install with:

```bash
pip install cude-rearranger
```

---

## 🔁 Undo / Derearrange

CUDE writes a manifest after name-based rearrangement:

```text
_rearrange_deep_manifest.json
```

The GUI **Undo** button uses this file to restore moved items.

CLI version:

```bash
cude-derearrange-deep --manifest "/path/to/_rearrange_deep_manifest.json"
```

Dry-run first:

```bash
cude-derearrange-deep --manifest "/path/to/_rearrange_deep_manifest.json" --dry-run
```

---

## 🧠 Deep Mode Requirements

Deep mode is optional.

To use it, place a llama.cpp folder beside the app files:

```text
llama/
├── llama-cli
└── model.gguf
```

Example supported GGUF models:

| Model Type | Use Case |
|---|---|
| Small GGUF model | Faster folder summaries |
| Larger GGUF model | Better summary quality |
| Vision model | Optional image/screenshot understanding |

CUDE does **not** include large model weights by default.

---

## ⚠️ Important Safety Notes

| Risk | Recommendation |
|---|---|
| Files are moved during rearrangement | Run on a copied folder first |
| Deep mode can be slow | Use a small GGUF model first |
| macOS may block unsigned apps | Right-click → Open, or sign/notarize the app |
| LLM summaries may be imperfect | Check important folders manually |
| Undo depends on manifest | Do not delete `_rearrange_deep_manifest.json` |

---

## 🧱 Project Structure

```text
cude/
├── __init__.py
├── summary.py
├── compare_sum.py
├── rearrange_deep.py
├── derearrange_deep.py
├── download_all_models.py
└── path_ui.py

app/
├── gui_app.py
├── app.py
└── __main__.py
```

---

## 🧾 Third-Party Software and Dependencies

CUDE uses or can interact with several third-party open-source tools and Python packages.

| Software / Package | Purpose | License Note |
|---|---|---|
| Python | Runtime | Python Software Foundation License |
| Tkinter | GUI framework | Bundled with Python |
| NumPy | Numerical computation | BSD-style license |
| scikit-learn | Clustering / similarity tools | BSD license |
| sentence-transformers | Embedding model interface | Apache-2.0 license |
| PyMuPDF | PDF text extraction | AGPL/commercial dual licensing; check your use case |
| Pillow | Image loading | HPND-style license |
| pytesseract | OCR wrapper | Apache-2.0; requires Tesseract OCR separately |
| Tesseract OCR | OCR engine | Apache-2.0 license |
| Hugging Face Hub | Model download | Apache-2.0 license |
| Transformers | Model loading | Apache-2.0 license |
| PyTorch / TorchVision | ML backend | BSD-style license |
| llama.cpp | Local GGUF inference | MIT license |
| FastAPI | Optional API server | MIT license |
| Uvicorn | API server runtime | BSD-style license |
| PyInstaller | macOS app build | GPL with bootloader exception |
| Ollama | Optional local vision/text model runtime | Check Ollama license and model licenses |

> ⚠️ Always check the license of each model you download.  
> A model’s license can be different from the software license.

---

## 📜 License

This project is released under the **MIT License** unless otherwise specified.

You may:

| Permission | Status |
|---|---|
| Use privately | ✅ |
| Use commercially | ✅ |
| Modify | ✅ |
| Distribute | ✅ |
| Sublicense | ✅ |

You must:

| Requirement | Status |
|---|---|
| Keep the copyright notice | ✅ |
| Keep the license notice | ✅ |

---

## © Copyright

Copyright (c) 2026 CUDE Project Authors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files, to use, copy, modify, merge,
publish, distribute, sublicense, and/or sell copies of the software, subject to
the conditions of the MIT License.

Third-party software, dependencies, models, and external tools remain under
their own licenses. CUDE does not claim ownership of third-party packages,
model weights, llama.cpp, Python, PyTorch, Transformers, Tesseract, Ollama, or
other external software.

---

## 🧑‍💻 Author / Maintainer

| Item | Information |
|---|---|
| Project | CUDE |
| Full Name | Clustered Utility for Deep Embedding Rearrangement |
| Maintainer | Your Name / Your Team |
| Contact | your_email@example.com |
| License | MIT License |

---

## ✅ Recommended First Test

Before using CUDE on important files:

```text
1. Copy a messy folder.
2. Run CUDE on the copied folder.
3. Check cluster folders.
4. Test Undo.
5. Only then use it on real work folders.
```

---

## 📝 Short Description for GitHub

> CUDE is a local GUI-based folder rearrangement tool that uses embedding clustering, reversible manifests, and optional local LLM/vision summarisation to clean and reorganise messy folders.

---

## ⭐ If You Use CUDE

If CUDE helps your workflow, please consider giving the GitHub repository a star.
