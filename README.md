# Natas Walkthrough (Levels 0-18)

Working notes from the [OverTheWire Natas](https://overthewire.org/wargames/natas/) web-security wargame, written up as a level-by-level walkthrough: the vulnerability, the approach taken, the payload, and the password that unlocks the next level.

*Started 2 Nov 2026 · @Alex*

## At a glance

| Level | Vulnerability / technique | Notes |
|-------|---------------------------|-------|
| 0-3 | Warm-up: password exposed in page source | [natas00-03](levels/natas00-03.md) |
| 4 | Referer header forgery | [natas04](levels/natas04.md) |
| 5 | Cookie tampering | [natas05](levels/natas05.md) |
| 6 | Include-file disclosure | [natas06](levels/natas06.md) |
| 7 | Local file inclusion (path traversal) | [natas07](levels/natas07.md) |
| 8 | Reversible encoding | [natas08](levels/natas08.md) |
| 9 | Command injection | [natas09](levels/natas09.md) |
| 10 | Command injection with a character filter | [natas10](levels/natas10.md) |
| 11 | XOR-encrypted cookie tampering | [natas11](levels/natas11.md) |
| 12 | Unrestricted file upload (extension) | [natas12](levels/natas12.md) |
| 13 | File upload: magic-byte bypass | [natas13](levels/natas13.md) |
| 14 | SQL injection: auth bypass | [natas14](levels/natas14.md) |
| 15 | Blind SQL injection (boolean) | [natas15](levels/natas15.md) |
| 16 | Command-injection oracle, filtered | [natas16](levels/natas16.md) |
| 17 | Blind SQL injection (time-based) | [natas17](levels/natas17.md) |
| 18 | Admin session (in progress) | [natas18](levels/natas18.md) |

## Getting started

Log in to <http://natas0.natas.labs.overthewire.org> with username `natas0` and password `natas0`. Each level `natasN` lives at `http://natasN.natas.labs.overthewire.org` and uses username `natasN` with the password recovered from the previous level.

## Tools used

- Browser view-source / dev tools
- [Burp Suite](https://portswigger.net/burp) as an intercepting proxy
- `hexedit` for crafting file headers
- Python for scripting blind extraction (see [`scripts/`](scripts/))

## Repository layout

```
.
├── README.md        # this overview
├── levels/          # one write-up per level
└── scripts/         # helper scripts (blind SQLi / oracle brute force)
```

## A note on passwords

Per OverTheWire's request not to publish solutions' credentials, every password and secret in these notes is replaced with a placeholder like `<natas5 password>`. Follow the steps to recover them yourself.

The real values live in a local `.env` file, which is git-ignored. Copy the template to start your own:

```bash
cp .env.example .env
```
