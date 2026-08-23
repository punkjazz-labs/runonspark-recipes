# runonspark-recipes

This repository is the remote recipe feed for basement. Machines read it.
People read the basement repository instead.

The feed is two files:

- `index.json` lists the recipes.
- `index.json.sig` is a detached ed25519 signature over `index.json`.

Every basement manager fetches both files every 6 hours. The manager
verifies the signature against a public key embedded in its binary before
it reads the list. A recipe with a higher version number than the built-in
recipe with the same ID replaces it in the catalog. Installed models do not
change until their owner starts an update.

Do not edit these files by hand. A hand edit breaks the signature, and
every manager will reject the file. The publish procedure lives in the
basement repository at `docs/RECIPE-FEED.md`. The tools that produce these
files are `cmd/build-index` and `cmd/sign-index` there.
