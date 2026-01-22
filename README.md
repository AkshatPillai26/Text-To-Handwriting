# ✍️ Text to Handwriting Synthesis

A procedural **text-to-handwriting synthesis system** that converts typed text into handwritten-style images using real handwritten character samples.

Instead of relying on fonts or pre-trained models, this project builds handwriting dynamically by composing individual character images with realistic spacing, alignment, and variation. The focus is on **handwriting layout, preprocessing, and rendering**, similar to how document and typography engines work internally.

---

## Why I Built This

Most existing “text-to-handwriting” tools either:

- Use static handwriting fonts, or
- Hide everything behind a large neural model

I wanted to understand **what actually makes handwriting look natural**, such as:

- Why spacing matters more than randomness  
- How baseline alignment affects readability  
- Why raw scanned data breaks naive rendering approaches  

This project is my attempt to solve those problems **from first principles**, using real handwritten data and an explicit, debuggable pipeline.

---

## What This Project Does

- Takes input text (for example, `"HELLO WORLD"`)
- Selects real handwritten variants for each character
- Cleans and normalizes character images
- Places characters on a shared baseline
- Applies natural spacing and small variations
- Outputs a single handwritten image

Each render is slightly different while remaining readable.

---

## Key Features

- Uses **real handwritten character samples** (not fonts)
- Multiple variants per character for natural variation
- Automatic preprocessing pipeline:
  - Cropping to visible ink
  - Removal of empty or low-content artifacts
  - Contrast enhancement for faint strokes
- Per-character normalization to avoid tiny or oversized letters
- Deterministic and controllable rendering logic
- Designed to scale toward ML-based handwriting generation later

---

## How It Works (Overview)

1. **Dataset Structure**
   - Each character (A–Z, digits, etc.) is stored as its own folder
   - Each folder contains multiple handwritten samples of that character

2. **Preprocessing**
   - Crop each image to its ink content
   - Remove extraction artifacts (empty tiles, fragments)
   - Strengthen faint ink strokes
   - Normalize character sizes using per-character median statistics

3. **Synthesis**
   - Process input text character by character
   - Randomly select a handwritten variant per character
   - Align characters to a shared baseline
   - Apply natural spacing and minor positional jitter
   - Compose and export the final handwritten image

The entire pipeline is explicit and modular—nothing is hidden behind a black box.

---

## Project Structure

```text
text-to-handwriting/
│
├── src/                 # Core logic
│   ├── load_data.py     # Dataset loading
│   ├── preprocess.py   # Cropping, filtering, enhancement
│   ├── normalize.py    # Size normalization logic
│   └── synthesize.py   # Rendering engine
│
├── data/                # Handwritten character images (not tracked)
│   └── chars/
│       ├── A/
│       ├── B/
│       └── ...
│
├── notebooks/           # Experiments and visual debugging
├── outputs/             # Generated handwriting images
│
├── requirements.txt
├── README.md
└── .gitignore
