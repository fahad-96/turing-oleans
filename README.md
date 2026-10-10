# turing-oleans

Prebuilt (compiled) Lean 4 library files for Mathlib and its dependencies,
so that a fresh machine can `import Mathlib` without building it.

This repository holds nothing but this README. The files are release assets:

    https://github.com/fahad-96/turing-oleans/releases/tag/mathlib-9944fe29-lean-4.33.0-rc1

## What is inside

- Lean toolchain: `leanprover/lean4:v4.33.0-rc1`
- Mathlib commit: `9944fe2973b8dc0b86949101ed98232c07cd54a0`
- The `.lake/build/lib/lean` output of eight packages, produced by a normal
  `lake build` of the unmodified upstream sources on Windows x64:
  mathlib, batteries, aesop, Qq, proofwidgets, importGraph, LeanSearchClient, plausible.
- `oleans_01.tgz` .. `oleans_09.tgz`: the `.olean` and `.olean.private` files
- `server_01.tgz`: the `.olean.server` files
- `ir_01.tgz`: the `.ir` and `.ir.sig` files
- `pack_manifest.txt`, `pack_server_manifest.txt`, `pack_ir_manifest.txt`:
  chunk name, file count, raw bytes, compressed bytes

Lean needs all three kinds of file. Every archive contains paths of the form
`<package>/.lake/build/lib/lean/...`, so all of them extract into one folder.
The sha256 of every asset is in the release notes.

## Use

    REL=https://github.com/fahad-96/turing-oleans/releases/download/mathlib-9944fe29-lean-4.33.0-rc1
    mkdir -p pkgs
    for f in oleans_01 oleans_02 oleans_03 oleans_04 oleans_05 oleans_06 oleans_07 oleans_08 oleans_09 server_01 ir_01; do
      curl -L -f -o $f.tgz $REL/$f.tgz && tar -xzf $f.tgz -C pkgs && rm $f.tgz
    done
    P=$PWD/pkgs
    export LEAN_PATH=$P/mathlib/.lake/build/lib/lean:$P/batteries/.lake/build/lib/lean:$P/aesop/.lake/build/lib/lean:$P/Qq/.lake/build/lib/lean:$P/proofwidgets/.lake/build/lib/lean:$P/importGraph/.lake/build/lib/lean:$P/LeanSearchClient/.lake/build/lib/lean:$P/plausible/.lake/build/lib/lean

Then run `lean File.lean` with the `lean` binary of exactly toolchain
v4.33.0-rc1 (https://github.com/leanprover/lean4/releases/tag/v4.33.0-rc1).
About 2.0 GB to download, 5.7 GB extracted.

## Sources and licences

Compiled from these open-source projects, each under the Apache License 2.0
(see the LICENSE file of each repository). No source was modified.

| package          | repository                                                | commit |
|------------------|-----------------------------------------------------------|--------|
| mathlib          | https://github.com/leanprover-community/mathlib4          | 9944fe2973b8dc0b86949101ed98232c07cd54a0 |
| batteries        | https://github.com/leanprover-community/batteries         | 45337c634fbcb2bb22fb45c9847faaa10d4d1b67 |
| aesop            | https://github.com/leanprover-community/aesop             | 57d3325be72a842920813bcb40f96a6f7393c185 |
| Qq               | https://github.com/leanprover-community/quote4            | ee41917ae11d38479fb8fb24745f7ca4bf0a784d |
| proofwidgets     | https://github.com/leanprover-community/ProofWidgets4     | b1436dc749e722c9920036b52cdc43b3451d0b69 |
| importGraph      | https://github.com/leanprover-community/import-graph      | 18a90119a5d316358fde6c86e0ca24e59212e32c |
| LeanSearchClient | https://github.com/leanprover-community/LeanSearchClient  | 0498c7c070c143a3bf7379f4d99a2c63bb9d9715 |
| plausible        | https://github.com/leanprover-community/plausible         | b1c4a69a7e247ab7df20460212001673d74f08c0 |

These are unofficial convenience builds; they are not published or endorsed
by the Lean or Mathlib maintainers.
