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
