# Focused Privacy

This document describes the behavior of Focused version 0.4.0 as verified against source commit `57c284ed6e522ea489a348eb6955af613b53d6d8`.

## Summary

Focused contains no Focused-operated backend and does not transmit analytics, telemetry, advertising identifiers, or behavioral tracking events. Provider requests are made directly from the extension service worker to the AI endpoint selected in Settings. Focused does not receive or proxy those requests.

Hosted provider support is limited to OpenAI, Anthropic, and Gemini. Ollama is also supported and defaults to `http://localhost:11434`; its URL is configurable, so Ollama traffic is local only when the configured endpoint is local.

## Data sent to AI providers

Before Focused first sends tab data to an AI provider, it displays a one-time data notice and stores the acknowledgement locally. Requests used only to list available models can authenticate with the configured API key without tab data.

Depending on the feature used, the provider request can contain:

- **Organize:** titles and URLs for eligible loose HTTP(S) tabs in the selected window; existing group names, colors, and grouped-tab titles; custom grouping instructions; and ephemeral tab or group identifiers.
- **Command bar:** the command text and titles and URLs for HTTP(S) tabs across all normal Chrome windows in the same regular or incognito browsing mode, including pinned and grouped tabs; current-window group names, colors, and counts; and ephemeral identifiers.
- **Stash brief:** the chosen group's name and the titles and URLs of its HTTP(S) tabs.

These requests go directly to the provider selected by the user. OpenAI, Anthropic, Gemini, and any configured Ollama server process the data under their own terms and privacy policies.

## Optional page snippets

Focused can request the optional `<all_urls>` host permission after showing the data notice. If granted, it may read a short excerpt of rendered page text to give the selected provider more context:

- Organize and the command bar can send up to 800 normalized characters from each of up to six selected tabs.
- A stash brief can send up to 600 normalized characters from each of the first four tabs in the group when permission has already been granted.

Denying or revoking this permission leaves title-and-URL features available. Stash does not request page access itself; it uses snippets only when access was granted previously.

## API keys and local storage

OpenAI, Anthropic, and Gemini API keys are stored in `chrome.storage.local`. Focused never writes them to `chrome.storage.sync`. Keys are sent directly to the selected provider to authenticate requests and are not encrypted separately by Focused. The configured Ollama URL is also stored locally.

Other data is stored as follows:

- Noncredential preferences—including provider and model choices, grouping behavior, budget settings, and custom instructions—use `chrome.storage.sync`.
- Stashes use local storage and contain group names, tab titles, URLs, generated briefs, and recovery metadata.
- Active organization jobs and review results use session storage. Review results can temporarily contain tab titles.
- Undo information uses session storage with a local-storage fallback for regular browsing. Incognito undo data is kept in memory only.
- The one-time data-notice acknowledgement and estimated provider spend use local storage.
- Imported and exported group files are created and processed locally.

Stashing is disabled in incognito windows because extension local storage is shared with regular browsing. If the user enables Focused in incognito, other AI features can still send incognito tab data to the selected provider, and review results containing tab titles can exist temporarily in the extension's session storage.

## Chrome permissions

Focused declares these required extension permissions:

- `tabs`: read tab titles and URLs and organize tabs.
- `tabGroups`: create, update, move, and inspect Chrome tab groups.
- `storage`: store credentials, preferences, stashes, consent, progress, and recovery data.
- `scripting`: inject the optional page-snippet reader and the in-page popup overlay.
- `activeTab`: display and authorize the toolbar-triggered in-page overlay.

Required host permissions allow direct requests to the OpenAI, Anthropic, and Gemini APIs and to Ollama's default `localhost` and `127.0.0.1` addresses. The optional `<all_urls>` permission allows page snippets and can also authorize a user-configured non-local Ollama endpoint. A remote Ollama URL may send data off-device; plain HTTP does not encrypt that traffic.

## Other network and user actions

The only automatic runtime network destinations in this snapshot are the selected AI provider endpoints and the configured Ollama endpoint. The “Request a feature” control opens a pre-addressed email in the user's mail client only after the user clicks it.
