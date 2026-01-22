# C2GBR - C to Gameboy Tile Designer Converter

A lightweight utility to convert Game Boy tile data from C array format back to `.gbr` format.

## Overview

This tool converts C  arrays (extracted from [GBTD](https://www.devrs.com/gb/hmgd/gbtd.html)) back into the native `.gbr` format.
This is useful for reverse engineering, modifying exported tile data, or regenerating `.gbr` files from C source code.

## Features

- Converts 2bpp (2 bits per pixel) Game Boy tile format to GBTD `.gbr` format
- Supports up to 512 tiles (8KB of tile data)
- Automatically unpacks compressed tile data into the 64-byte per tile format used by GBTD
- Simple command-line interface

## Building

Simply run:

```bash
git clone https://github.com/wirenux/C2GBR.git
cd C2GBR
make
```

This compiles the tool to `build/C2GBR`.

## Usage

```bash
./build/C2GBR <input.c>
```

The output file will be written to `output/output.gbr`.

### Example

```bash
./build/C2GBR examples/decompiled.c
```

Output:

```bash
Converted 80 bytes into 5 tiles in 'output.gbr'
```

## Input Format

The input C file should contain a tile array in the format exported by GBTD:

```c
unsigned char TileLabel[] =
{
    0xFF,0xFF,0xFF,0xFF,0xFF,0xFF,0xFF,0xFF,
    0xFF,0xFF,0xFF,0xFF,0xFF,0xFF,0xFF,0xFF,
    // ... more tile data (16 bytes per tile)
};
```

Each tile is represented as 16 bytes in 2bpp format (2 bytes per row, 8 rows per tile).

## GBR File Structure

The output `.gbr` file consists of:

180-byte header - GBTD 2.2 format header containing metadata and palette

Tile data - 64 bytes per tile in unpacked format

## Boring Stuff

### License

[UNLICENSE](./UNLICENSE)

### Credits

- [GBTD](https://www.devrs.com/gb/hmgd/gbtd.html) (Gameboy Tile Designer) by [Harry Mulder](https://www.devrs.com/gb/hmgd/me.html)
