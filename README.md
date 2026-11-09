# ptouch-print (fork with extra print options)

This is a fork of **[ptouch-print](https://git.familie-radermacher.ch/linux/ptouch-print)** by
**Dominic Radermacher**, a command line tool to print labels on Brother P-Touch printers on
Linux. All credit for ptouch-print goes to him; see [`README`](README) for the original
description and <https://dominic.familie-radermacher.ch/projekte/ptouch-print/> for the project
page. Please report problems with this fork here, not to the original author.

The fork exists for [Labeler](https://github.com/PhilippMundhenk/labeler), a web interface for
P-Touch printers, and adds options from Brother's raster command reference that ptouch-print 1.9
does not offer. The changes are meant to go back to the original project.

## Branches

- `master` and the tags: unchanged copy of the original repository.
- `labeler` (this branch): ptouch-print v1.9 plus the changes below, one commit each.

## Changes

See [CHANGES.fork](CHANGES.fork) for the list with dates.

| Option | Command sent to the printer |
| --- | --- |
| `--feed <dots>` | `ESC i d`: blank tape before and after the label (printer default 14 dots) |
| `--halfcut` | `ESC i K` half cut bit: cut the tape but not its backing (printers with a half cutter) |
| `--cut-every <n>` | `ESC i A n` with auto cut: with `--copies`, cut only after every n labels |
| `--hires` | `ESC i K` high resolution bit: twice the dots along the tape; images must be twice as long |

Also: the udev rule gives the group `lp` access (for services), and `size_t` values are printed
with `%zu` (no warnings on 32-bit systems such as Raspberry Pi OS).

Without the new options the program sends exactly the same bytes as the original. Labeler's
contract test checks every option byte for byte against a simulated USB printer; the options
are not yet tested on every printer model.

## Build

As the original: `cmake -S . -B build && cmake --build build`.

## License

GPL-3.0, the same license as ptouch-print ([COPYING](COPYING)). Copyright of ptouch-print
© 2013-2026 Dominic Radermacher; changes in this fork © 2026 Philipp Mundhenk, under the same
license.
