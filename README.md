# roc-reify-nightlies

This repo holds the "reify" nightly releases of the new Roc compiler.

The compiler source is the `reify` branch of [Karakatiza666/roc](https://github.com/Karakatiza666/roc). That branch is rebased on an upstream nightly from [roc-lang/nightlies](https://github.com/roc-lang/nightlies/releases).

This repo is a copy of roc-lang/nightlies. The workflow is changed for the fork.

## Manual only

Nothing here runs on a schedule. Nothing runs on a pull request. You must start each release by hand.

The workflow has two inputs:

- `ref`: the Karakatiza666/roc branch or commit to build. The default is `reify`.
- `base_nightly`: the upstream nightly tag that the ref is rebased on. This input is required.

The workflow does these checks before it builds:

- `base_nightly` must look like `nightly-YYYY-MM-DD-<sha>`.
- The base commit must be an ancestor of the commit to build.
- The release tag must not exist yet.

There is no CI check for the fork. You choose the commit.

## How to run one

```
gh workflow run nightly_new_compiler_all_os.yml -R Karakatiza666/roc-reify-nightlies -f base_nightly=nightly-2026-11-03-34bd006
```

To build another branch or commit, add `-f ref=<branch or commit>`.

## Names

The release tag and title are `nightly-reify-<date>-<sha7>`. The date comes from `base_nightly`. The sha is the first 7 characters of the built commit.

The archives are named like this:

- `roc_nightly-reify-<platform>-<date>-<sha7>.tar.gz` (`.zip` on Windows)
- `roc_nightly-reify-source-<date>-<sha7>.tar.gz` and `.zip`
- `playground.wasm.zst`, `repl.wasm.zst` and `echo.wasm.zst`

The platforms are `linux_x86_64`, `linux_arm64`, `macos_x86_64`, `macos_apple_silicon` and `windows_x86_64`.

`roc version` in a release prints the release tag.
