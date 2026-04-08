# Google AI Studio Chat Exporter

[![Chrome Web Store](https://img.shields.io/chrome-web-store/v/pmccmopibnkjfmaddlloincblhcnmndd.svg?label=Chrome%20Web%20Store&color=blue)](https://chromewebstore.google.com/detail/chat-exporter-for-google/pmccmopibnkjfmaddlloincblhcnmndd)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Privacy: Local Only](https://img.shields.io/badge/Privacy-100%25_Local-success.svg)](#privacy--security)

A browser extension to export conversations from Google AI Studio into perfectly formatted Markdown, PDF, and JSON files. 

Google AI Studio is an excellent environment for prompt engineering and interacting with Gemini models, but it currently lacks a native export feature. Manual copy-pasting breaks code formatting, ruins tables, and captures messy internal model reasoning (`<thinking>` blocks). This extension solves the extraction problem natively within the browser.

<img width="1400" height="560" alt="Chat exporter (1400 x 560 px) (2)" src="https://github.com/user-attachments/assets/7730849b-c1ed-46da-a89b-6b0f558dbdb1" />

## Features

* **Rich Text Preservation:** Uses an internal AST (Abstract Syntax Tree) parser to perfectly retain code blocks, syntax highlighting, lists, bold/italics, and tables.
* **Intelligent 'Thought' Stripping:** Automatically detects and removes Gemini's internal reasoning/planning blocks, ensuring your exported documentation is clean and client-ready.
* **Deep DOM Extraction:** Bypasses Angular's virtual scroller and pierces Shadow DOMs to reliably capture massive, 1M+ token conversations from top to bottom.
* **Multiple Formats:**
  * **Markdown (`.md`):** Optimized for seamless pasting into Obsidian, Notion, or GitHub.
  * **PDF (`.pdf`):** Generates a clean, print-ready document with native Dark Mode support.
  * **JSON (`.json`):** Exports a structured AST tree with role labels, perfect for creating datasets, fine-tuning LLMs, or RAG pipelines.
* **100% Local & Private:** No external APIs, no analytics, no telemetry. Data processing happens entirely within your local browser instance.

## Installation

### Option 1: Chrome Web Store (Recommended)
You can install the official, stable release directly from the Chrome Web Store:
👉 **[Install Chat Exporter for Google AI Studio](https://chromewebstore.google.com/detail/chat-exporter-for-google/pmccmopibnkjfmaddlloincblhcnmndd)**

### Option 2: Manual Installation (Developer Mode)
If you prefer to build from source or inspect the code locally:
1. Clone this repository: `git clone https://github.com/Rajat-XR/google-ai-studio-chat-exporter.git`
2. Open Google Chrome and navigate to `chrome://extensions/`.
3. Enable **Developer mode** (toggle in the top right corner).
4. Click **Load unpacked**.
5. Select the `dist` or root directory of the cloned repository.

## Usage

1. Open a conversation in [Google AI Studio](https://aistudio.google.com/).
2. Click the **Chat Exporter** extension icon in your browser toolbar.
3. (Optional) Toggle **System Instructions** or **Dark Mode** on/off.
4. Select your desired format (**PDF, Markdown, or JSON**) and click **Export Now**.
5. *For long chats, the extension will automatically scroll the page to mount and capture unloaded DOM nodes. Please do not close the window until the export completes.*

## How It Works (Technical Overview)

Extracting data from AI Studio is non-trivial due to its use of a highly optimized virtual scroller and heavily nested Shadow DOM components. 

Instead of relying on basic `innerText` scraping, this extension:
1. Orchestrates the viewport scroll to force the UI framework to mount hidden conversation chunks.
2. Traverses the DOM tree (including open `shadowRoot` boundaries) to isolate `ms-prompt-chunk` and `ms-text-chunk` components.
3. Deduplicates nodes mathematically to prevent parent/child overlapping.
4. Parses the raw text into a standard AST format, applying strict Regex exclusions to omit `<thinking>` tags.
5. Compiles the AST into the requested file format natively via Blob URLs.

## Privacy & Security

This extension requires the `activeTab` and `scripting` permissions to read the DOM of the active AI Studio tab and compile the export file. 

**Zero Data Collection:** We do not track usage, we do not use analytics, and we do not communicate with external servers. Your prompts, API keys, and model outputs never leave your local machine.

## Contributing

Contributions, issues, and feature requests are welcome! 
If you notice a formatting edge-case (e.g., a broken table layout or un-parsed code block), please open an issue with a sample of the raw text so the AST parser can be updated.

## License

Distributed under the MIT License. See `LICENSE` for more information.
