# 🧠 UltraCodeAI – IntelliJ AI Assistant (Ultra-fast, Local + Cloud LLMs)

> "An IDE-first AI copilot for IntelliJ IDEA with chat, diagnostics, and project-aware insights."

![Platform](https://img.shields.io/badge/Platform-IntelliJ%20IDEA-blue?style=for-the-badge)
![Language](https://img.shields.io/badge/Built%20With-Java%2017-red?style=for-the-badge)
![UI](https://img.shields.io/badge/UI-Swing%20%7C%20JetBrains%20UI-8A2BE2?style=for-the-badge)
![License](https://img.shields.io/badge/License-Apache--2.0-green?style=for-the-badge)

---

## 🚀 Overview

UltraCodeAI is an IntelliJ IDEA plugin that embeds an AI coding copilot directly in the IDE:
- Multi-model chat with streaming responses
- Real‑time Diagnostics tab powered by IntelliJ inspections
- Project‑aware Insights (RAG-ready structure)
- One clean, native, tabbed tool window: Chat • Diagnostics • Insights

It works with both local models (privacy-first) and cloud models (frontier capabilities), and is built 100% in Java for deep IntelliJ integration.

---

## ✨ Features

- 🤖 Chat tab with streaming responses (token-by-token)
- 🔍 Diagnostics tab with live IntelliJ error/warning highlights
- 💡 Insights tab scaffold for project-aware guidance (RAG-ready)
- 🧩 Local + Cloud model support via a unified execution service
- 🧭 Native tool window (right dock), theme-aware, keyboard-friendly
- 🧱 Pluggable services (execution strategies, RAG/indexer, MCP/logs)
- 🧰 Context controls: add files/snippets/directories from project view

---

## 🧩 Architecture

- Tool Window UI: com.devoxx.genie.ui.window.UltraCodeAIToolWindowFactory
- Prompt Pipeline: com.devoxx.genie.service.prompt.PromptExecutionService
- Streaming Interface: com.devoxx.genie.service.prompt.response.ResponseListener
- Diagnostics Listener: com.devoxx.genie.service.diagnostics.UltraCodeAIDiagnosticsService
- Settings Panels: multiple projectConfigurable entries in plugin.xml
- Optional Panels: MCP Logs (bottom tool window), Appearance, Costs, Web Search
- Extensibility: RAG indexer, providers, threading, cancellation, memory

---

---

## 📦 Installation

From source:
bash
  git clone https://github.com/Vivek-the-creator/UltraCodeAI.git
  cd UltraCodeAI
  ./gradlew buildPlugin

text


Install into IDE:
- Open IntelliJ → Settings → Plugins → Install from Disk
- Select zip from build/distributions/

Dev run:
bash
  ./gradlew runIde


Requirements:
- IntelliJ IDEA 2023.3.4+ recommended
- Java 17+

---

## ⚙ Configuration

Open Settings → UltraCodeAI:
- Select provider (local or cloud)
- Optionally set API keys for cloud providers
- Adjust appearance, cost estimation, context window preferences
- Enable/disable MCP, Web Search, RAG (if available in your build)

Tool window:
- View → Tool Windows → UltraCodeAI (right side)

---

## 🔧 Usage

Chat:
1) Open UltraCodeAI tool window
2) Type a prompt (optionally include code context)
3) Watch streamed response in real time

Add context:
- Right‑click code editor/project files → “Add To Conversation”
- Add directory or calculate tokens for large context

Diagnostics:
- Open Diagnostics tab
- Edit code; issues auto‑populate from IntelliJ analyzer
- (Optional) Click entries to navigate (if wired in your build)

Insights:
- Open Insights tab
- See contextual recommendations (when connected to your RAG/provider flow)

---

## 🧠 Key Components (Glue Code Highlights)

- UltraCodeAIToolWindowFactory
  - Builds the 3-tab UI
  - Hooks Chat send-button to PromptExecutionService.executePrompt(...)
- PromptExecutionService
  - Primary pipeline: command processing → strategy selection → execution → cancellation → cleanup
  - Overload provided for simple String + ResponseListener Chat integration
- ResponseListener
  - Minimal interface: onTokenReceived, onComplete
- UltraCodeAIDiagnosticsService
  - Listens to IntelliJ daemon analyzer completion
  - Feeds current file highlights to Diagnostics tab UI callback

---

## 🛠 Building Blocks You Can Extend

- Providers: add your own local/cloud services under chatmodel/
- Strategies: register new PromptExecutionStrategy variants
- RAG: wire your indexer/retriever to enrich Insights tab
- WebView: swap JTextArea for JCEF/HTML+Prism for rich rendering
- Actions: add editor/project view actions to push context to chat

---

## 🧪 Tips

- For streaming UIs, append tokens on EDT using SwingUtilities.invokeLater(...)
- For large projects, avoid blocking EDT; use background tasks
- Prefer project services (project.getService(...)) for scoped lifecycles
- Keep plugin.xml single source of truth for factories, services, actions

---

## 🧭 Roadmap (suggested)

- Click-to-navigate diagnostics entries (offset → line → OpenFileDescriptor)
- AI fix suggestions inline in Diagnostics (one-click apply where safe)
- Rich chat rendering via JCEF + Markdown + code highlight
- Provider presets and smart model recommendations by task
- Full RAG wiring with local embeddings + retrieval panel

---

## 🤝 Contributing

PRs welcome! Suggested flow:
1) Fork and branch: feature/<name>
2) Code + tests
3) ./gradlew buildPlugin
4) Open PR with a clear description and screenshots/GIFs for UI changes

---

## 📜 License

MitLicense-2.0 (see LICENSE in the repo)

---

## 🙌 Credits
[Vivek K K](https://github.com/Vivek-The-Creator),
[Vishnupriyan P R](https://github.com/vishnupriyanpr183207),
[Akshaya K](https://github.com/Akshaya1215), 
[Sanjit M](https://github.com/Sanjit-123).  

Crafted by the MeshMinds. Inspired by modern agentic IDE workflows and built with the IntelliJ Platform SDK + Java.
