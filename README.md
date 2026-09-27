# Weekend Activity Finder (QVAC)

Describe what you feel like doing, like "relaxing and cozy", "active and outdoors" or "a cheap day out", pick who you're with, tick **free only** or **it's raining**, and find **weekend activities that fit by meaning** from a list of 32. Add them to **Saturday** or **Sunday** to build your weekend plan, then copy it to share.

It runs **on your own computer** using [QVAC](https://github.com/tetherto/qvac), Tether's open-source AI SDK.
No API key, no cloud service, and what you type never leaves your machine.

![screenshot](screenshot.png)

## SDK version

`@qvac/sdk` **0.19.0** (declared in `package.json`)

Functions used: `loadModel` and `embed`, with the `EMBEDDINGGEMMA_300M_Q4_0` model.

## Install

You need [Node.js](https://nodejs.org) 22 or newer and some free disk space for the model.

```bash
git clone https://github.com/misaki-codex/qvac-weekend-planner.git
cd qvac-weekend-planner
npm install
```

## Run

```bash
npm start
```

Then open **http://localhost:3095** (the address, not the HTML file). The first start downloads the model.
While it loads, keyword matching is used instead, so it always works.

## How it works

- `activities.js` holds 32 activities, each with cost (free, $ or $$), indoor or outdoor, who it suits and a description. Add your own.
- The filters are applied first (rain removes outdoor-only activities). Then `server.js` ranks the rest with QVAC's `embed`.
- Your weekend plan is saved in your browser.
- The server listens on `127.0.0.1`, so only your own computer can reach it.

## Troubleshooting

If you see `RPC_INIT_TIMEOUT`, the QVAC worker was slow to start. `server.js` already waits 3 minutes.
Set `QVAC_RPC_INIT_TIMEOUT_MS` (milliseconds) before `npm start` to wait longer, and make sure no other
QVAC app is running at the same time. If you see `ERR_MODULE_NOT_FOUND`, delete the `node_modules` folder
and run `npm install` again (this usually means an install was interrupted, for example by a full disk).

## License

MIT
