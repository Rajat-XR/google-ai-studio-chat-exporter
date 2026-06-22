# AI Chat Exporter: Save Conversations to PDF, Markdown, and JSON

[![Chrome Web Store](https://img.shields.io/chrome-web-store/v/pmccmopibnkjfmaddlloincblhcnmndd.svg?label=Chrome%20Web%20Store&color=blue)](https://chromewebstore.google.com/detail/pmccmopibnkjfmaddlloincblhcnmndd)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Privacy: Local Only](https://img.shields.io/badge/Privacy-100%25_Local-success.svg)](#privacy-and-security)

AI Chat Exporter is a privacy-first browser extension designed to export conversations from ChatGPT, Gemini, and Google AI Studio into beautifully formatted PDF, Markdown, and JSON files. 

While AI platforms provide excellent environments for prompt engineering and research, native export functionality is often limited or requires days to process full data backups. Manual copying breaks code formatting, destroys tables, and creates messy documents. This extension solves the extraction problem natively within the browser, allowing professionals to save and backup AI conversations instantly.

## Supported Platforms

The extension currently supports one-click exports from the following platforms:
* ChatGPT (chatgpt.com)
* Google Gemini (gemini.google.com)
* Google AI Studio (aistudio.google.com)

## Core Features

* **Rich Text and Code Preservation:** Utilizes an internal Abstract Syntax Tree (AST) parser to perfectly retain code blocks, syntax highlighting, lists, bold and italic text, and tables.
* **Intelligent Document Formatting:** Automatically detects and structures conversation turns, ensuring your exported documentation is clean, readable, and ready for professional use.
* **Deep DOM Extraction:** Bypasses virtual scrollers and pierces Shadow DOM boundaries to reliably capture long, multi-turn conversations from start to finish.
* **Multiple Output Formats:**
  * **Markdown (.md):** Optimized for seamless pasting and integration into knowledge management systems like Obsidian, Notion, or GitHub.
  * **PDF (.pdf):** Generates a clean, print-ready document with native support for both Light and Dark modes.
  * **JSON (.json):** Exports a structured dataset including role labels (User vs. Model) and AST trees, ideal for creating training datasets, fine-tuning LLMs, or developing Retrieval-Augmented Generation (RAG) pipelines.
* **100% Local and Private:** Operates entirely within your local browser instance. No external APIs, no analytics, no telemetry.

## Installation

AI Chat Exporter is distributed through the official Chrome Web Store to ensure the highest security standards, verified permissions, and automated updates.

**[Download AI Chat Exporter from the Chrome Web Store](https://chromewebstore.google.com/detail/pmccmopibnkjfmaddlloincblhcnmndd)**

## Usage Guide

1. Open a conversation in a supported AI platform (ChatGPT, Gemini, or Google AI Studio).
2. Click the AI Chat Exporter extension icon in your browser toolbar.
3. Configure your export settings (e.g., toggle Dark Mode for PDF formatting).
4. Select your preferred output format (PDF, Markdown, or JSON).
5. Click the Export button. The file will generate locally and download automatically.

*Note for extensive conversations: The extension may automatically scroll the page to mount and capture unloaded content. Please keep the tab active until the download completes.*

## Technical Overview

Extracting structured data from modern AI web interfaces requires advanced DOM traversal techniques due to their use of highly optimized virtual scrollers, obfuscated CSS classes, and nested Shadow DOM components.

Instead of relying on basic text scraping, AI Chat Exporter:
1. Orchestrates viewport scrolling to force the underlying UI framework to mount hidden conversation chunks.
2. Traverses the Document Object Model (including open shadow boundaries) to isolate individual message components.
3. Deduplicates nodes to prevent overlapping content.
4. Parses the raw elements into a standardized AST format.
5. Compiles the AST into the requested file format natively using Blob URLs, ensuring zero data transmission.

## Privacy and Security

Data security is the primary architectural principle of this tool. 

The extension requires the standard permissions necessary to read the Document Object Model of the active tab and compile the export file. 

**Zero Data Collection Policy:** There is no tracking, no usage analytics, and no communication with external servers. Your prompts, API keys, and model outputs remain strictly confined to your local machine. This makes the tool safe for exporting sensitive corporate data, source code, and confidential research.

## Contributing

Contributions, issue reports, and feature requests are welcome. 

If you encounter a formatting edge-case (such as a broken table layout or an unparsed code block on a newly updated AI platform), please open an issue in this repository with a sample of the raw structure so the AST parser can be updated.

## License

This project is distributed under the MIT License. See the `LICENSE` file for more information.
