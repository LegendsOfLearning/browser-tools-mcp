# BrowserTools MCP

> Make your AI tools 10x more aware and capable of interacting with your browser

This application is a powerful browser monitoring and interaction tool that enables AI-powered applications via Anthropic's Model Context Protocol (MCP) to capture and analyze browser data through a Chrome extension.

This is a fork maintained by Legends of Learning, originally from [AgentDeskAI/browser-tools-mcp](https://github.com/AgentDeskAI/browser-tools-mcp).

Read our [docs](https://browsertools.agentdesk.ai/) for the full installation, quickstart and contribution guides.

## Updates

v1.2.0 is out! Here's a quick breakdown of the update:
- You can now enable "Allow Auto-Paste into Cursor" within the DevTools panel. Screenshots will be automatically pasted into Cursor (just make sure to focus/click into the Agent input field in Cursor, otherwise it won't work!)
- Integrated a suite of SEO, performance, accessibility, and best practice analysis tools via Lighthouse
- Implemented a NextJS specific prompt used to improve SEO for a NextJS application
- Added Debugger Mode as a tool which executes all debugging tools in a particular sequence, along with a prompt to improve reasoning
- Added Audit Mode as a tool to execute all auditing tools in a particular sequence
- Resolved Windows connectivity issues
- Improved networking between BrowserTools server, extension and MCP server with host/port auto-discovery, auto-reconnect, and graceful shutdown mechanisms
- Added ability to more easily exit out of the Browser Tools server with Ctrl+C

  

Please make sure to update the version in your IDE / MCP client as so:
`npx @agentdeskai/browser-tools-mcp@1.2.0`

Also make sure to download the latest version of the chrome extension here:
[v1.2.0 BrowserToolsMCP Chrome Extension](https://github.com/AgentDeskAI/browser-tools-mcp/releases/download/v1.2.0/BrowserTools-1.2.0-extension.zip)

From there you can run the local node server like so:
`npx @agentdeskai/browser-tools-server@1.2.0`

Make sure to specify version 1.2.0 since NPX caching may prevent you from getting the latest version! You should only have to do this once for every update. After you do it once, you should be on the latest version.

And once you've opened your chrome dev tools, logs should be getting sent to your server 🦾

If you have any questions or issues, feel free to open an issue ticket! And if you have any ideas to make this better, feel free to reach out or open an issue ticket with an enhancement tag or reach out to me at [@tedx_ai on x](https://x.com/tedx_ai)

## Full Update Notes:

Coding agents like Cursor can run these audits against the current page seamlessly. By leveraging Puppeteer and the Lighthouse npm library, BrowserTools MCP can now:

- Evaluate pages for WCAG compliance
- Identify performance bottlenecks
- Flag on-page SEO issues
- Check adherence to web development best practices
- Review NextJS specific issues with SEO

...all without leaving your IDE 🎉

---

## 🔑 Key Additions

## Available Tools

### Browser Navigation Tools

| Tool Name | Description |
| --------- | ----------- |
| `mcp_Browser_Tools_reloadPage` | Reloads the current browser page |
| `mcp_Browser_Tools_clickElement` | Clicks an element matching the provided selector |
| `mcp_Browser_Tools_navigateTo` | Navigates to a specified URL |
| `mcp_Browser_Tools_goBack` | Goes back one page in browser history |
| `mcp_Browser_Tools_goForward` | Goes forward one page in browser history |

### Audit & Analysis Tools

| Tool Name | Description |
| --------- | ----------- |
| `mcp_Browser_Tools_runAccessibilityAudit` | WCAG-compliant checks for accessibility |
| `mcp_Browser_Tools_runPerformanceAudit` | Lighthouse-driven performance analysis |
| `mcp_Browser_Tools_runSEOAudit` | Evaluates on-page SEO factors |
| `mcp_Browser_Tools_runBestPracticesAudit` | Checks for web development best practices |
| `mcp_Browser_Tools_runNextJSAudit` | NextJS-specific audit |
| `mcp_Browser_Tools_runAuditMode` | Runs all auditing tools in sequence |
| `mcp_Browser_Tools_runDebuggerMode` | Runs all debugging tools in sequence |

### Console & Network Tools

| Tool Name | Description |
| --------- | ----------- |
| `mcp_Browser_Tools_getConsoleLogs` | Get browser console logs |
| `mcp_Browser_Tools_getConsoleErrors` | Get browser console errors |
| `mcp_Browser_Tools_getNetworkErrors` | Get network error logs |
| `mcp_Browser_Tools_getNetworkLogs` | Get all network logs |
| `mcp_Browser_Tools_wipeLogs` | Clear all stored logs |

### DOM & Visual Tools

| Tool Name | Description |
| --------- | ----------- |
| `mcp_Browser_Tools_takeScreenshot` | Capture current page screenshot |
| `mcp_Browser_Tools_getSelectedElement` | Get currently selected DOM element |

---

## 🛠️ Using Audit Tools

### ✅ **Before You Start**

Ensure you have:

- An **active tab** in your browser
- The **BrowserTools extension enabled**

### ▶️ **Running Audits**

**Headless Browser Automation**:  
 Puppeteer automates a headless Chrome instance to load the page and collect audit data, ensuring accurate results even for SPAs or content loaded via JavaScript.

The headless browser instance remains active for **60 seconds** after the last audit call to efficiently handle consecutive audit requests.

**Structured Results**:  
 Each audit returns results in a structured JSON format, including overall scores and detailed issue lists. This makes it easy for MCP-compatible clients to interpret the findings and present actionable insights.

The MCP server provides tools to run audits on the current page. Here are example queries you can use to trigger them:

#### Accessibility Audit (`runAccessibilityAudit`)

Ensures the page meets accessibility standards like WCAG.

> **Example Queries:**
>
> - "Are there any accessibility issues on this page?"
> - "Run an accessibility audit."
> - "Check if this page meets WCAG standards."

#### Performance Audit (`runPerformanceAudit`)

Identifies performance bottlenecks and loading issues.

> **Example Queries:**
>
> - "Why is this page loading so slowly?"
> - "Check the performance of this page."
> - "Run a performance audit."

#### SEO Audit (`runSEOAudit`)

Evaluates how well the page is optimized for search engines.

> **Example Queries:**
>
> - "How can I improve SEO for this page?"
> - "Run an SEO audit."
> - "Check SEO on this page."

#### Best Practices Audit (`runBestPracticesAudit`)

Checks for general best practices in web development.

> **Example Queries:**
>
> - "Run a best practices audit."
> - "Check best practices on this page."
> - "Are there any best practices issues on this page?"

#### Audit Mode (`runAuditMode`)

Runs all audits in a particular sequence. Will run a NextJS audit if the framework is detected.

> **Example Queries:**
>
> - "Run audit mode."
> - "Enter audit mode."

#### NextJS Audits (`runNextJSAudit`)

Checks for best practices and SEO improvements for NextJS applications

> **Example Queries:**
>
> - "Run a NextJS audit."
> - "Run a NextJS audit, I'm using app router."
> - "Run a NextJS audit, I'm using page router."

#### Debugger Mode (`runDebuggerMode`)

Runs all debugging tools in a particular sequence

> **Example Queries:**
>
> - "Enter debugger mode."

## Architecture

There are three core components all used to capture and analyze browser data:

1. **Chrome Extension**: A browser extension that captures screenshots, console logs, network activity and DOM elements.
2. **Node Server**: An intermediary server that facilitates communication between the Chrome extension and any instance of an MCP server.
3. **MCP Server**: A Model Context Protocol server that provides standardized tools for AI clients to interact with the browser.

```
┌─────────────┐     ┌──────────────┐     ┌───────────────┐     ┌─────────────┐
│  MCP Client │ ──► │  MCP Server  │ ──► │  Node Server  │ ──► │   Chrome    │
│  (e.g.      │ ◄── │  (Protocol   │ ◄── │ (Middleware)  │ ◄── │  Extension  │
│   Cursor)   │     │   Handler)   │     │               │     │             │
└─────────────┘     └──────────────┘     └───────────────┘     └─────────────┘
```

Model Context Protocol (MCP) is a capability supported by Anthropic AI models that
allow you to create custom tools for any compatible client. MCP clients like Claude
Desktop, Cursor, Cline or Zed can run an MCP server which "teaches" these clients
about a new tool that they can use.

These tools can call out to external APIs but in our case, **all logs are stored locally** on your machine and NEVER sent out to any third-party service or API. BrowserTools MCP runs a local instance of a NodeJS API server which communicates with the BrowserTools Chrome Extension.

All consumers of the BrowserTools MCP Server interface with the same NodeJS API and Chrome extension.

#### Chrome Extension

- Monitors XHR requests/responses and console logs
- Tracks selected DOM elements
- Sends all logs and current element to the BrowserTools Connector
- Connects to Websocket server to capture/send screenshots
- Allows user to configure token/truncation limits + screenshot folder path

#### Node Server

- Acts as middleware between the Chrome extension and MCP server
- Receives logs and currently selected element from Chrome extension
- Processes requests from MCP server to capture logs, screenshot or current element
- Sends Websocket command to the Chrome extension for capturing a screenshot
- Intelligently truncates strings and # of duplicate objects in logs to avoid token limits
- Removes cookies and sensitive headers to avoid sending to LLMs in MCP clients

#### MCP Server

- Implements the Model Context Protocol
- Provides standardized tools for AI clients
- Compatible with various MCP clients (Cursor, Cline, Zed, Claude Desktop, etc.)

## Installation

Installation steps can be found in our documentation:

- [BrowserTools MCP Docs](https://browsertools.agentdesk.ai/)

## Usage

Once installed and configured, the system allows any compatible MCP client to:

- Monitor browser console output
- Capture network traffic
- Take screenshots
- Analyze selected elements
- Wipe logs stored in our MCP server
- Run accessibility, performance, SEO, and best practices audits

## Compatibility

- Works with any MCP-compatible client
- Primarily designed for Cursor IDE integration
- Supports other AI editors and MCP clients

## Development Setup

### 1. Local Development

Clone and set up the repository:
```bash
git clone https://github.com/LegendsOfLearning/browser-tools-mcp.git
cd browser-tools-mcp/browser-tools-mcp
npm install
npx tsc
```

### 2. Configure Cursor

Edit your Cursor MCP configuration at `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "Browser Tools": {
      "command": "node",
      "args": [
        "/path/to/your/browser-tools-mcp/browser-tools-mcp/dist/mcp-server.js"
      ]
    }
  }
}
```

Replace `/path/to/your` with your actual path to the project.

### 3. Chrome Extension

1. Install the BrowserTools MCP extension from Chrome Web Store
2. Configure it to connect to `127.0.0.1:3025` (default)

### 4. Running the Server

You can run the server in two ways:

#### Development Mode
```bash
cd browser-tools-mcp
npm install
npx tsc
node dist/mcp-server.js
```

#### Production Mode (via npm)
```bash
npx @agentdeskai/browser-tools-mcp@1.1.0
```

The server will attempt to discover available ports starting from 3025.

## Development Workflow

1. Make changes to the TypeScript source
2. Run `npx tsc` to compile
3. Restart the server
4. Cursor will automatically connect to your local development version

## Troubleshooting

- If "Client closed" appears in Cursor's MCP panel:
  1. Ensure the server is running
  2. Check the path in `mcp.json` is correct
  3. Restart Cursor or refresh the MCP panel

- If the Chrome extension isn't connecting:
  1. Verify the server is running on port 3025
  2. Check extension settings
  3. Ensure no other instances are running (`pkill -f "browser-tools-mcp"`)

## Production vs Development

- **Production**: Uses the npm package `@agentdeskai/browser-tools-mcp`
- **Development**: Uses your local version for testing changes

Remember to recompile TypeScript (`npx tsc`) after making changes to the source code.

---

## Development Guide (LoL Fork)

### Branch Strategy

- `main`: Synced with upstream AgentDeskAI repo
- `lol-main`: Our customized version with LoL-specific changes

### Updating from Upstream

```bash
# Update main from upstream
git checkout main
git fetch upstream
git merge upstream/main

# Update lol-main with changes
git checkout lol-main
git merge main
```

### Latest Features (v1.2.1-lol.0)

- 🆕 Added simplified navigation tools:
  - `reloadPage`
  - `clickElement`
  - `navigateTo`
  - `goBack`
  - `goForward`
- 🔄 Auto-reconnect for more stable connections
- 🚀 Improved error handling and logging
