# Figma-MCP-Augment-Code-Guide-Local-HTTP-mode-
Integration of Figma MCP server with Augment Code, using local Figma desktop app
A step-by-step setup for using Figma’s Dev Mode MCP server via HTTP (http://127.0.0.1:3845/mcp) together with Augment Code in VS Code.

⸻

🎯 Overview
	•	Figma’s Dev Mode MCP server lets AI agents (and tools) access structured design context (components, styles, layout, tokens) in real time.  ￼
	•	In local mode (via the Figma desktop app), it runs at http://127.0.0.1:3845/mcp (or sometimes SSE) when enabled.  ￼
	•	Augment Code (in VS Code) supports connecting to remote (or local) MCP servers via HTTP or SSE.  ￼

This guide shows using HTTP mode (/mcp) to connect Augment to your running Figma desktop MCP server.

⸻

✅ Prerequisites
	•	Figma desktop app installed and updated
	•	Augment Code extension in VS Code
	•	VS Code open and running
	•	Augment Code configured / working (you’ve already set up other MCPs or at least seen the MCP settings UI)

⸻

1. Enable local MCP server in Figma
	1.	Open the Figma desktop app and make sure it’s updated to the latest version.
	2.	Open any Figma design file.
	3.	Go to the Figma menu → Preferences → Enable local MCP server.  ￼
	4.	You should see a confirmation message that the MCP server is active.  ￼
	5.	By default, it binds to 127.0.0.1 (localhost), so external interfaces won’t see it.  ￼

⚠️ Note: In some documentation, /sse was used (e.g. http://127.0.0.1:3845/sse) but Figma’s newer guide emphasizes http://127.0.0.1:3845/mcp as the default endpoint.  ￼

⸻

2. Verify the MCP endpoint

You can test whether the endpoint is live by using a simple HTTP request. In a terminal:

curl http://127.0.0.1:3845/mcp

If it’s working, you might see a JSON response or some MCP handshake response. If it fails, check:
	•	That Figma’s local MCP is still enabled
	•	That no firewall or network rule blocks localhost:3845
	•	That nothing else is bound to port 3845

Also note: because it’s bound to 127.0.0.1, it will not respond on other network interfaces.  ￼

⸻

3. Configure Augment Code to use local Figma MCP
	1.	In VS Code, open the Augment panel.
	2.	Click on Settings (gear icon) and navigate to the MCP servers section.
	3.	Click Add remote MCP (because although it’s local, you’re connecting via HTTP endpoint).  ￼
	4.	In the “Edit MCP Server” dialog, fill in:
	•	Connection Type: HTTP
	•	Name: figma-local (or figma)
	•	URL: http://127.0.0.1:3845/mcp
	•	Authentication Type: leave as is.
	5.	Click Save.
	6.	Toggle the server on in the MCP list (so Augment starts connecting).
	7.	Optionally, reload VS Code / Augment so everything picks up freshly.

⸻

4. Using Figma MCP in Augment

Once the server is active and connected, Augment should detect the tools exposed by Figma’s MCP server (e.g. get_node, get_styles, etc.).

You can then invoke those tools in your Augment chat / agent conversation, for example:

@figma analyze https://www.figma.com/file/XYZ#/frame/1234

or, referencing the current selection in Figma, ask Augment to retrieve component properties, layout info, or style tokens.

⸻
