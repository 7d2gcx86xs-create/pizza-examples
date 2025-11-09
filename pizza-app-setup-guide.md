# Pizza App Setup Guide

This guide explains how to set up and run the **Pizza App** using the OpenAI Apps SDK.  The steps below follow the official freeCodeCamp tutorial on building a Pizza App for ChatGPT.  The repository contains a complete example app (`openai‑apps‑sdk‑examples`) along with the **Pizzaz** demo server.

## 1. Clone the examples repository

Start by cloning OpenAI’s examples repository and installing the dependencies.  The tutorial suggests using `pnpm`, but `npm` or `yarn` work as well.  To clone and install:

```
sh
git clone https://github.com/openai/openai-apps-sdk-examples.git
cd openai-apps-sdk-examples
pnpm install
```

The repository contains all of the widget source code for the app.  After installing, build the assets and start the development server using the following commands:

```
sh
pnpm run build
pnpm run dev
```

## 2. Run the Pizza App server

The Pizzaz demo uses a small Model Context Protocol (MCP) server to expose the pizza widgets as tools and resources.  To start it, navigate into the server directory and run:

```
sh
cd pizzaz_server_node
pnpm start
```

On startup the server prints its endpoints to the console, for example `http://localhost:8000/mcp` for the SSE stream and `http://localhost:8000/mcp/messages` for posting messages.  You should see output like:

```
Pizzaz MCP server listening on http://localhost:8000
  SSE stream: GET http://localhost:8000/mcp
  Message post endpoint: POST http://localhost:8000/mcp/messages
```

## 3. Expose your local server

ChatGPT can only access your app if it has a publicly reachable URL.  The tutorial recommends using **ngrok** to expose your local port 8000.  After signing up for ngrok and installing it, authenticate with your token and start a tunnel:

```
sh
ngrok config add-authtoken <your_authtoken>
ngrok http 8000
```

This command gives you an HTTPS URL such as `https://xyz.ngrok.app` and maps it to your local server.  Make sure you use the `/mcp` path when connecting ChatGPT (for example `https://xyz.ngrok.app/mcp`).

## 4. Create your ChatGPT app

With your MCP server running and exposed to the internet, open ChatGPT and enable **Developer Mode** under **Settings → Apps & Connectors → Advanced Settings**.  Then create a new app:

1. Go back to **Settings → Apps & Connectors** and click **Create**.
2. Enter a name for your app (e.g. *Pizza App*) and an optional description.
3. Set **MCP Server URL** to the public URL from ngrok, including the `/mcp` path.
4. Choose **No authentication**, check **I trust this application**, and click **Create** to finish.

## 5. Use the Pizza App

After creating the app, start a new chat, click the **+** icon, and pick your Pizza App from the list.  ChatGPT can now call your widgets directly.  Try prompts like:

- “Show me a pizza map with pepperoni topping.”
- “Show me a pizza carousel with mushroom topping.”
- “Show me a pizza album with veggie topping.”
- “Show me a pizza list with cheese topping.”
- “Show me a pizza video with chicken topping.”

Each command asks ChatGPT to call one of your tools, and the server responds with metadata telling ChatGPT which widget to render.  You can extend the app by adding new widgets or hooking into real APIs as described in the tutorial.

---

This repository was downloaded and included here as `pizza_app.zip`.  Extract it, follow the steps above, and you will have a fully working Pizza App that integrates with ChatGPT.
