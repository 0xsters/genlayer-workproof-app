# WorkProof App

The web frontend for the **WorkProof Verifier** Intelligent Contract on GenLayer.

WorkProof is a reusable acceptance primitive for work that is paid or credited on delivery: bounties, contribution programs, grants, and agent marketplaces. A task is registered in the contract with a title, acceptance criteria in plain language, a public evidence URL, and a pass score. When the work is done, anyone can resolve the task: GenLayer validators independently fetch the evidence page and grade it, and the verdict is stored on chain only when validators agree under a custom equivalence rule (verdict must match exactly, score within 15 points, criteria met count within 1).

## Live app

https://workproof-seven.vercel.app

## Contract

- Network: GenLayer Studionet (chain 61999)
- Contract address: 0xD974a24a033714a64987539EF13986f63E51d426
- Explorer: https://explorer-studio.genlayer.com/address/0xD974a24a033714a64987539EF13986f63E51d426
- Contract source, tests, and documentation: https://github.com/0xsters/genlayer-workproof-verifier

## What the app does

- Reads the live task count and every stored task and verdict directly from the contract (genlayer-js, Studionet).
- Connects a browser wallet, adding the GenLayer Studionet network when missing.
- Creates tasks with the contract's `create_task` method.
- Resolves tasks with `resolve_task`, which triggers validator grading of the evidence page, and waits for finalization before refreshing the verdict.

## Run it

This is a single static page. Serve `index.html` from any static host, or open the live app above. No build step and no backend: all reads and writes go straight to the GenLayer Studionet RPC through genlayer-js loaded from a CDN.

## Verification

Verified 2026-11-15 against the deployed contract and the live app.

- Contract: GenLayer Studionet (chain 61999), `0xD974a24a033714a64987539EF13986f63E51d426`. The address is the same in this README, in `index.html`, and on the live app.
- Live read path: the app reads `total_tasks` and `get_task` through genlayer-js 1.1.8 over the Studionet RPC. Checked independently with genlayer-verify-cli: `total_tasks()` returned `0` (exit 0), matching the live app, which renders "Tasks registered on chain: 0" and "No tasks yet. Register the first one above."
- Live app: https://workproof-seven.vercel.app returns HTTP 200 and serves the same `index.html` (contract address and genlayer-js 1.1.8 present).
- Layout: rendered in a real browser at desktop width (1919 px, 880 px container centered, no horizontal overflow) and measured headless at 390x844 and 1366x768 (no horizontal overflow at either size). All sections render: header, task-count card, register form, tasks list, footer.
- No wallet was connected and no transaction was sent during verification.
