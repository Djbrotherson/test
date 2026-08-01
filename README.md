# Lighthouse H700 GitHub Builder

This repository builds Lighthouse 1.0.1 natively on an ARM64 GitHub runner while restricting generated code to the ARMv8.0 Cortex-A53 instruction set used by the Anbernic H700 devices.

## Run the build

1. Sign in to GitHub and create a new **public** repository. A name such as `lighthouse-h700-builder` is fine.
2. Upload the contents of this folder to the repository. Make sure the hidden `.github` folder is included.
3. Open the repository's **Actions** tab.
4. Select **Build Lighthouse for H700** on the left.
5. Press **Run workflow**, then press the green **Run workflow** button.
6. Open the completed workflow run.
7. Under **Artifacts**, download **Lighthouse-H700-muOS**.
8. Extract `Lighthouse-H700-muOS.zip` from the downloaded artifact.
9. Copy its `lighthouse` folder over the existing Lighthouse port and allow it to replace `lighthouse/Lighthouse`.

Keep the existing launcher, controller configuration, assets and game data. The build artifact replaces only the executable.

## Source revisions

- Lighthouse: `4423e0c1a10e70c42301bce2a5fb969964cf3537`
- Required submodules are fetched recursively from that exact Lighthouse revision.

## CPU restrictions

The workflow compiles with:

```text
-march=armv8-a
-mcpu=cortex-a53
-mtune=cortex-a53
-mno-outline-atomics
```

It also disassembles the resulting executable and stops the build if it finds selected ARMv8.1+, LSE, RCpc or dot-product instructions.
