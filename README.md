# Linear Cipher v6.00 (beta)

**End‑to‑end message encryption you can hold in your hand and read for yourself.**
Argon2id + AES‑256‑GCM, fully offline, no accounts, no servers, no telemetry.

Linear Cipher encrypts short messages and turns the result into plain `LC5.` letters
(or stealthy symbols) that you paste into any chat, e‑mail, or file. You share one
passphrase out of band; that's the whole system.

The **command‑line tool (`lc`)** is the centerpiece — small, auditable, scriptable.
The **HTML page** is a second, self‑contained implementation kept as a conceptual
proof: the same cryptography in one file you open in any browser, no install. A
message made by one decrypts in the other.

> **This is the first public beta of the v6 keyfile‑first CLI.** The cryptography and
> wire format are unchanged and stable since v4.06 — v6 interoperates with every
> earlier version and with the HTML tool (confirm with `lc verify`). Please report
> anything rough.

## Downloads

**All downloads are on the [Releases page](../../releases/latest)** — the CLI, the
HTML tool, the Android/PWA build, the guides (PDF), the test vectors, and
`SHA256SUMS.txt`. Grab what you need there.

You can also just open the browser tool directly:
**[linear-cipher-6.00.html](linear-cipher-6.00.html)** (download it and double‑click —
it works offline).

## The command‑line tool

Requires Python 3.8+ (already on macOS and Linux). Download `linear-cipher-cli-6.00.zip`
from the [Releases page](../../releases/latest), unzip it, then:

```bash
cd linear-cipher-cli-6.00
python3 -m venv .venv && source .venv/bin/activate
pip install -e .          # installs the `lc` command

lc new coffeehouse --save me    # make your key and save it (offers a master password)
lc import alice                 # save a key someone shared (shows the match code)
lc e "hello"                    # encrypt: pick a saved key from a list
lc d "LC5.…"                    # decrypt: finds the right saved key by itself
lc verify                       # confirm this build matches the test vectors
```

The full Quick Start and User Guide (PDF) are attached to the release, and `lc help`
/ `lc howto` cover everything in‑tool.

### What's new in v6 (keyfile‑first)

- Save keys by name; **`lc e` shows a picker**, **`lc d` auto‑finds** the right key.
- **`lc import NAME`** enters a received passphrase once, confirmed by its match code.
- **Keyfile protected by default** — the first save offers a master password (default
  yes), with an ssh‑style ~10‑minute session unlock and `lc lock`.
- `--pass` still works but is a demoted scripting escape hatch.
- Warn‑only passphrase checks, `lc ls`, `lc keyring rename`, decoupled modules.

## The HTML tool (conceptual proof)

Open **[linear-cipher-6.00.html](linear-cipher-6.00.html)** in any browser —
double‑click, no server, works offline. Same passphrase, same messages as the CLI.

## Verifying your download

Each release includes `SHA256SUMS.txt`:

```bash
sha256sum -c SHA256SUMS.txt     # Linux, in the folder with the files
shasum -a 256 <file>            # macOS, compare to the line in SHA256SUMS.txt
```

Then `lc verify` confirms cryptographic compatibility.

## License

Linear Cipher is free software, licensed under the **GNU General Public License v3.0**
(or, at your option, any later version) — see [LICENSE](LICENSE). Every modified or
redistributed version must remain open source under the same terms, so no one can
ship a closed, unauditable fork of a tool people trust with their private messages.

## Status & scope

Protects message content in transit and at rest. It does **not** hide that a message
exists or its length, and cannot protect an already‑compromised device. A lightweight,
transparent tool for everyday privacy — not a vetted secure messenger for high‑risk use.
