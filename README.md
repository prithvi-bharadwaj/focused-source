# Focused

One click: understands your open tabs and sorts them into named Chrome tab groups using your choice of OpenAI, Anthropic, Gemini, or local Ollama.

Works in Chrome, Brave, Edge, Arc, Vivaldi — any Chromium browser that supports Manifest V3 tab groups.

## Source availability

Focused is **source-available, not open source**. This repository makes the extension auditable for privacy and security review and permits personal use and modifications within the license terms. The PolyForm Shield License prohibits using the software to provide a competing product.

The Prithvi-owned portions are licensed under [PolyForm Shield 1.0.0](LICENSE). Some shadcn/ui-derived portions retain their upstream terms; see [Third-Party Notices](THIRD_PARTY_NOTICES.md). The snapshot's private-source lineage is recorded in [Provenance](PROVENANCE.md).

## Features

- **Organize tabs** — groups loose tabs by task and intent, adds relevant tabs to existing groups, and orders focused work before entertainment. Tabs file into their groups as a visible ~2.5s cascade.
- **Command bar** — create or extract a targeted group, move tabs into an existing group, rename or recolor a group, ungroup one or every group, remove duplicates, and merge related groups with natural-language prompts. It can also jump to a described tab or answer a question from your open tabs with a Go-to-tab button.
- **Stash + resume briefs** — stash a whole group: its saveable web tabs close and Focused writes an AI "where you left off" brief (prices, options, what was still unchecked). Resume later to reopen those URLs as a fresh Chrome group — browser history, page and form state, and non-web tabs aren't restored. Unavailable in incognito because extension storage is shared.
- **Hybrid context** — optionally reads a short page snippet when a title and URL are too ambiguous to classify. Declining page access still leaves title/URL organization fully usable.
- **Quick actions** — ungroup everything, close duplicate URLs, or undo the last organize/ungroup/cleanup action from the popup.
- **Duplicate protection** — keeps pinned tabs and the active tab, otherwise retaining the most recently accessed copy. Cleanup can run automatically before organization.
- **Review mode** — inspect proposed groups and choose which ones to apply.
- **Custom instructions** — save personal grouping and naming rules, such as keeping every Wikipedia tab in a group called "wowow".
- **Persistent progress** — close and reopen the popup without losing the active organize state or result.
- **Budget cap** — estimates provider spend from reported token usage and stops requests at your configured limit. Ollama remains free.
- **Import and export** — copy/download the current window's groups as JSON and recreate them later.
- **Flexible grouping** — choose a minimum group size or group every loose tab.

## Provider setup

Open the extension popup, choose the gear, then select a provider and model:

- **OpenAI** — create an API key at [platform.openai.com/api-keys](https://platform.openai.com/api-keys) and paste it into Settings. The default is `gpt-5.6-luna` with low reasoning effort.
- **Anthropic** — create an API key at [console.anthropic.com](https://console.anthropic.com), then paste it into Settings. The default is `claude-haiku-4-5`.
- **Gemini** — create an API key in [Google AI Studio](https://aistudio.google.com/app/apikey), then paste it into Settings. The default is `gemini-3.1-flash-lite`.
- **Ollama** — install a model locally, set the Ollama URL (default `http://localhost:11434`), and allow extension origins when starting the server:

  ```sh
  OLLAMA_ORIGINS="chrome-extension://*" ollama serve
  ```

  Focused selects the first installed model if none has been chosen. If Ollama is already running as a desktop app or service, restart it with the same `OLLAMA_ORIGINS` environment setting.

Model lists are fetched live after provider settings are saved, with built-in fallbacks for hosted providers.

## Install

Prerequisites: Node `^20.19.0` or `>=22.12.0` and pnpm 10.

```sh
pnpm install --frozen-lockfile
pnpm build
```

Then in your browser:

1. Open `chrome://extensions` (or your browser's equivalent).
2. Enable **Developer mode**.
3. Click **Load unpacked** and select the `dist/` folder.
4. Pin **Focused** from the extensions menu.

## Development

```sh
pnpm dev
```

This rebuilds on changes. Reload the extension from the browser's extensions page to pick up a new build.

Run the complete verification suite with:

```sh
pnpm check
```

Stack: React 19, TypeScript, Tailwind v4, shadcn-style components, Radix primitives, and Vite. The service worker (`public/background.js`) is dependency-free plain JavaScript.

## Privacy

- Focused contains no Focused-operated backend and sends no analytics, telemetry, or tracking events.
- OpenAI, Anthropic, and Gemini keys are stored in `chrome.storage.local`, never Chrome sync, and are sent directly to the selected provider for authentication.
- AI features send relevant tab titles, URLs, group context, and user instructions directly to the selected provider. Optional short page snippets are sent only after the one-time data notice and optional page-access permission.
- Ollama defaults to `http://localhost:11434`, but its endpoint is configurable; data stays local only when the configured server is local.
- Noncredential preferences use Chrome sync. Stashes and some recovery data are stored locally or for the browser session.

See [Privacy](PRIVACY.md) for the exact data scopes, storage behavior, permissions, and incognito caveats verified against this source snapshot.

## License

Except for identified third-party material, Focused is licensed under the [PolyForm Shield License 1.0.0](LICENSE), with the required notice in [NOTICE](NOTICE). This is a source-available license, not an open-source license, and competing products are prohibited.

See [Third-Party Notices](THIRD_PARTY_NOTICES.md) for shadcn/ui-derived portions that remain under the MIT License and for dependency-license guidance.
