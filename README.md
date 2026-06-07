# Aionios ata05 (ATA MPM-05) — Unofficial Technical Reference

An independent, community reverse-engineering reference for the **Aionios ata05**
teleoperated robot (internal hardware family **EC501**; FCC ID `2BQFZ-ATAMPM-05`).
It documents the hardware, boot/storage, software & network stack, the **LinxPort /
LinxKey accessory protocol**, the companion-MCU serial console, backup/recovery, and
a curated set of community findings — all obtained by hands-on investigation of a
device the author owns.

> ⚠️ **Unofficial & unaffiliated.** Not endorsed by or affiliated with Aionios,
> TOALL Design, or anyone else; all product and company names belong to their
> respective owners. Provided **as-is, with no warranty**. Modifying your device can
> void its warranty and may brick it — proceed at your own risk. See the full
> scope/legal note at the top of the reference document.

## What's inside

- **Hardware overview** — all four PCBs (main `EC501_MB`, sub `EC501_SUB`, the
  24 GHz radar daughter-board, and the Qi wireless-charging receiver), the key
  silicon, and annotated board photographs.
- **LinxPort / LinxKey accessory protocol** — frame format, CRC-16/MODBUS, and the
  full command set (`0x01` query-ID, `0x02` ID-reply, `0x03` operate, plus the
  app-side `0x45`/`0x46`/`0x47` frames), including the accessory-ID handshake and the
  laser on/off operate flow. Every example is **mathematically CRC-verified**.
- **Companion-MCU debug console** — wiring, 115200 8N1 / GBK decoding, and the
  decoded status-heartbeat telemetry (button / wireless-charge / wired-charger /
  supply-rail voltage).
- **Storage & boot, software & network stack, backup/recovery, known issues**, and a
  write-up of the public FCC-database records.

## Contents of this repository

| File | What it is |
|------|------------|
| `Aionios_ata05_Technical_Reference.md` | The full reference (Markdown). |
| `Aionios_ata05_Technical_Reference.pdf` | Same content, as a paginated PDF. |
| `images/` | Annotated board photographs referenced by the document. |
| `LICENSE` | Licensing terms (CC BY 4.0). |

*(If you keep the `_PUBLIC` suffix on the files, update the names above accordingly.)*

## Scope, method, and what is **not** here

Everything was learned from a device the author owns: serial-console observation,
analysis of the manufacturer's own published DIY material, and bench measurement.
Reverse engineering for interoperability and repair is generally permitted in the
EU/Germany; this document describes **findings**, not a means to infringe anyone's
rights.

Deliberately **excluded**: no firmware images or binaries (only descriptions of their
structure and the backup *method*); no confidential or embargoed FCC exhibits; and all
per-unit identifiers (device serial, production-traceability codes, accessory serial
strings) and third-party commenter names have been redacted. In the protocol examples
the 12-byte serial UID appears as `XXXXXXXXXXXX` — substitute your own device's
12-character serial and recompute the serial-dependent CRCs with the routine in the
CRC section.

## Status & contributing

The hardware and protocol sections are fairly complete. One known open item is the
`0x46` accessory-status byte for a *present* accessory (only the no-accessory value is
captured so far). Corrections, additional captures, and findings from other units are
welcome — please open an issue or pull request.

## License

Documentation and text are licensed under the **Creative Commons Attribution 4.0
International License (CC BY 4.0)** — see [`LICENSE`](LICENSE). You're free to share and
adapt the material, including commercially, as long as you give appropriate credit.
