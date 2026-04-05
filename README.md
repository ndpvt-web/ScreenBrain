# ScreenBrain - AI-Powered Screenshot Manager for macOS

> Search your screenshots by what's in them, not when you took them. Open source, privacy-first, works offline.

[![Swift](https://img.shields.io/badge/Swift-5.0-orange.svg)](https://swift.org)
[![Platform](https://img.shields.io/badge/platform-macOS%2014%2B-blue.svg)](https://www.apple.com/macos/sonoma/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/ndpvt-web/ScreenBrain/pulls)

ScreenBrain is a native macOS app that turns your screenshot library into a searchable knowledge base. It uses AI vision models or local OCR to automatically categorize, describe, and extract text from every screenshot you take -- so you can find anything instantly.

## Features

- **AI-Powered Categorization** -- Automatically sorts screenshots into categories: Code, Error, Design, Social Media, Conversation, Article, Receipt, Photo
- **Natural Language Descriptions** -- AI describes what each screenshot contains in plain English
- **Full OCR Text Extraction** -- Every word in every screenshot becomes searchable
- **Smart Tagging** -- Auto-generated tags and source app detection
- **Full-Text Search** -- Find any screenshot by its content, not just its filename
- **Grid and List Views** -- Finder-like browsing with smooth hover animations
- **Offline Mode** -- Works completely offline with Apple Vision OCR (no API key needed)
- **Provider Agnostic** -- Bring your own API key: OpenAI, OpenRouter, Ollama, or any OpenAI-compatible endpoint
- **Privacy First** -- All data stays on your Mac. Nothing leaves your machine unless you choose a cloud AI provider
- **Zero Dependencies** -- Built entirely with SwiftUI + SwiftData. No CocoaPods, no SPM packages

## Screenshots

### Library - Grid View with Category Filters
![Library Grid View - Articles](screenshots/01-library-articles.png)

### Code Screenshots Category
![Library Grid View - Code](screenshots/03-library-code.png)

### Detail View with AI Analysis
![Detail View](screenshots/04-detail-view.png)

### List View
![List View](screenshots/05-list-view.png)

### Settings - Provider Configuration
![Settings](screenshots/02-settings.png)

## Why ScreenBrain?

macOS Photos is built for personal photos, not for knowledge workers. If you take a lot of screenshots -- code snippets, error messages, design references, receipts, articles -- Photos gives you no way to find them by content.

ScreenBrain fixes this:

| Feature | macOS Photos | ScreenBrain |
|---|---|---|
| Screenshot categorization | No | Code, Error, Design, Receipt, etc. |
| Content descriptions | No | AI-generated natural language |
| Full OCR search | Basic | Full text extraction + search |
| Offline analysis | No | Apple Vision framework |
| Custom AI providers | No | OpenAI, Ollama, OpenRouter, any API |
| Open source | No | MIT License |

## Quick Start

### Requirements

- macOS 14.0 (Sonoma) or later
- Xcode 15.0 or later
- [XcodeGen](https://github.com/yonaskolb/XcodeGen) (`brew install xcodegen`)

### Build and Run

```bash
git clone https://github.com/ndpvt-web/ScreenBrain.git
cd ScreenBrain
xcodegen generate
open ScreenBrain.xcodeproj
```

Press **Cmd+R** to build and run. A setup wizard will guide you through first-time configuration.

### Command Line Build

```bash
xcodegen generate
xcodebuild -project ScreenBrain.xcodeproj \
  -scheme ScreenBrain \
  -configuration Debug \
  build
```

## Setup

On first launch, ScreenBrain walks you through a 3-step setup:

### 1. Choose Analysis Mode

| Mode | Description | Requires API Key | Requires Internet |
|---|---|---|---|
| **AI Vision** | Rich descriptions, smart categorization, OCR | Yes (or Ollama) | Yes (or local Ollama) |
| **Local OCR** | Text extraction + heuristic categorization | No | No |

### 2. Configure AI Provider (if using AI Vision)

| Provider | Models | API Key | Notes |
|---|---|---|---|
| **OpenAI** | GPT-4.1, GPT-4.1-mini, GPT-4o | Required | Best overall quality |
| **OpenRouter** | Claude, GPT-4, Gemini, and more | Required | One key for many models |
| **Ollama** | LLaVA, BakLLaVA, MiniCPM-V | Not needed | Free, local, private |
| **Custom** | Any model | Varies | Any OpenAI-compatible endpoint |

### 3. Import Screenshots

Click the **+** button to scan your Photos library. ScreenBrain shows you how many new screenshots are available and lets you choose to import all or just the most recent 25, 50, or 100.

## Using Ollama (Free, Local, Private)

For fully local AI analysis with zero API costs:

```bash
# Install Ollama
brew install ollama

# Pull a vision model
ollama pull llava

# Start Ollama (if not already running)
ollama serve
```

Then in ScreenBrain, select **Ollama (Local)** as your provider. The endpoint `http://localhost:11434/v1/chat/completions` is pre-configured.

## Architecture

```
ScreenBrain/
  App/
    ScreenBrainApp.swift          # Entry point, window config, onboarding
  Models/
    Screenshot.swift              # SwiftData model
    Category.swift                # Category enum with SF Symbols + colors
  Services/
    AIService.swift               # AI analysis + Apple Vision OCR
    PhotosService.swift           # Photos framework integration
    SearchService.swift           # Full-text search engine
  ViewModels/
    LibraryViewModel.swift        # Library state + import logic
    SearchViewModel.swift         # Search state management
  Views/
    ContentView.swift             # NavigationSplitView layout
    LibraryView.swift             # Grid/list browser + import confirmation
    DetailView.swift              # Screenshot detail with zoom + info panel
    SearchView.swift              # Search + category browsing
    SettingsView.swift            # Provider config + statistics
    OnboardingView.swift          # First-launch setup wizard
    Components/
      ScreenshotCard.swift        # Grid card with hover effects
      ScreenshotListRow.swift     # List row component
  Helpers/
    PlatformHelpers.swift         # macOS/iOS abstractions
  Resources/
    Info.plist
    ScreenBrain.entitlements
```

**Tech stack:** SwiftUI, SwiftData, Apple Vision framework, Photos framework. Zero third-party dependencies.

## Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| Cmd+I | Import from Photos |

## Privacy

ScreenBrain is designed with privacy as a core principle:

- All screenshot data is stored locally on your Mac using SwiftData
- API keys are stored in UserDefaults on your machine only
- Screenshots are never uploaded anywhere unless you explicitly choose a cloud AI provider
- Local OCR mode works entirely offline with no network requests
- The app only requests Photos library read access to import screenshots

## Contributing

Contributions are welcome. Please open an issue first to discuss what you'd like to change.

```bash
# Fork the repo, then:
git clone https://github.com/YOUR_USERNAME/ScreenBrain.git
cd ScreenBrain
xcodegen generate
open ScreenBrain.xcodeproj
```

## License

MIT License. See [LICENSE](LICENSE) for details.

---

**ScreenBrain** is built for developers, designers, researchers, and anyone who takes a lot of screenshots and needs to find them later. If macOS Photos isn't cutting it for your screenshot workflow, give ScreenBrain a try.

<details>
<summary>Keywords</summary>

For the search engines, the LLMs, and the curious humans who find things by typing random words into the void

macOS screenshot manager, AI screenshot organizer, screenshot search tool, screenshot knowledge base, macOS screenshot OCR, screenshot categorizer, AI-powered screenshot app, screenshot finder macOS, search screenshots by content, screenshot text extraction, OCR screenshot macOS, SwiftUI screenshot app, SwiftData screenshot manager, macOS native screenshot tool, screenshot library manager, AI image analysis macOS, screenshot tagger, automatic screenshot categorization, screenshot description generator, visual knowledge base macOS, screenshot organizer open source, free screenshot manager macOS, Ollama screenshot analysis, OpenAI vision screenshot, GPT-4 screenshot analyzer, Claude vision screenshot, local OCR macOS app, Apple Vision framework OCR, offline screenshot OCR, privacy-first screenshot app, screenshot search engine, find screenshot by text, screenshot content search, macOS productivity tool, developer screenshot manager, code screenshot organizer, error screenshot finder, receipt screenshot scanner, design screenshot library, screenshot workflow macOS, macOS Sonoma app, SwiftUI macOS app, screenshot grid view, screenshot list view, Finder-like screenshot browser, screenshot detail view, AI screenshot tags, screenshot metadata extractor, OpenRouter screenshot analysis, LLaVA screenshot analysis, BakLLaVA macOS, MiniCPM-V screenshot, self-hosted screenshot AI, bring your own API key, provider-agnostic AI app, screenshot import Photos, macOS Photos alternative screenshots, best screenshot app macOS, open source macOS app SwiftUI, AI coding assistant, screenshot management tool, visual search macOS, image content search, screenshot database, screenshot catalog, smart screenshot organizer, AI-powered macOS utility, knowledge management screenshots, research screenshot tool, academic screenshot organizer, screenshot annotation AI

</details>
