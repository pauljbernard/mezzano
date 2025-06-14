# Project Overview

This document summarizes the inferred requirements and architecture of **Mezzano**, a Common Lisp operating system. The notes below are compiled from the existing repository documentation and code.

## Functional Requirements

- Provide a bootable operating system written mostly in Common Lisp.
- Run on x86‑64 and ARM64 hardware with virtual machine support (VirtualBox, QEMU).
- Offer a graphical environment with a compositor, desktop, basic REPL and system applications.
- Include essential device drivers such as:
  - Virtio and RTL8168 network interfaces.
  - Intel HDA audio hardware.
  - Intel GMA950 display controller and Virgl 3D acceleration.
- Support modern file systems including FAT32 and EXT2/3/4.
- Provide networking capabilities with TCP/IP stack, server support and DHCP.
- Expose USB stack, async APIs, and multicore/SMP support.
- Offer development tools including Swank server, disassembler and editor.

## Non‑Functional Requirements

- Recommended virtual machine settings: 2 GB RAM, virtio‑net NIC and Intel HDA controller【F:README.md†L13-L18】.
- System snapshot capability for persistent state【F:doc/quickstart.md†L148-L160】.
- Only RTL8168 and virtio‑net NICs are supported; bridging to real networks is unsupported【F:doc/manual.md†L7-L11】.
- Designed primarily for use in VirtualBox/QEMU environments; running on physical hardware may require code modifications【F:README.md†L19-L21】.

## User Experience

- Window management allows dragging title bars or holding Alt while dragging.【F:doc/quickstart.md†L11-L13】
- Global shortcuts for REPL access, debugging and keymap switching【F:doc/quickstart.md†L15-L26】.
- Built‑in line editor and Emacs‑like editor controls for text manipulation【F:doc/quickstart.md†L28-L58】【F:doc/quickstart.md†L87-L153】.
- On‑screen status lights show disk, GC and network activity with colour coding【F:doc/quickstart.md†L162-L182】.
- Memory monitor provides virtual and physical memory visualization【F:doc/quickstart.md†L184-L216】.
- Swank server runs on port 4005 and requires VM port forwarding for IDE integration【F:doc/quickstart.md†L229-L235】.

## Architecture and System Design

- Memory layout for x86‑64 defines wired, pinned and function areas along with GC mark bits and stack regions【F:doc/internals/memory-layout.md†L1-L31】.
- All memory below 0x8000000000 is assumed wired to simplify GC and supervisor logic【F:doc/internals/memory-layout.md†L32-L33】.
- The function area lies across wired and pinned zones so that wired and normal functions can reach each other via direct calls within ±2 GB【F:doc/internals/memory-layout.md†L35-L46】.
- Objects are represented using "instances" with layouts describing slot locations. Obsolete layouts can redirect old instances to new ones during class redefinition【F:doc/internals/instances.md†L1-L32】【F:doc/internals/instances.md†L33-L68】.
- Supervisor code running in interrupts must avoid allocation, floating point, and access to non‑wired memory【F:doc/internals/supervisor-restrictions.md†L1-L28】.

## Build Requirements

- Building from source requires the separate MBuild repository【F:README.md†L23-L24】【F:doc/manual.md†L7-L9】.
- Host configuration is stored in `config.lisp` with the file server IP and paths to the source and home directories【F:config.lisp†L5-L11】【F:config.lisp†L13-L16】.
- The `lispos.asd` system defines compilation components for the cross compiler, runtime and tools【F:lispos.asd†L1-L32】【F:lispos.asd†L33-L67】.

## Run Instructions

1. Obtain a pre‑built image from the [GitHub releases](https://github.com/froggey/Mezzano/releases) or build one with MBuild.
2. Create a virtual machine with 2 GB RAM, virtio‑net NIC and Intel HDA audio.
3. Boot the image in VirtualBox or QEMU. The system will load drivers, configure the network and start the desktop environment.
4. Use keyboard shortcuts such as `M‑F10` for a REPL and `M‑F12` to change keymap【F:doc/quickstart.md†L15-L26】.
5. To enable remote development, forward port 4005 to access the Swank server【F:doc/quickstart.md†L229-L235】.

For dual‑boot installation or image creation on real hardware, see `doc/Dualboot.md` which describes preparing a partition and using `qemu-img` or `build-native-image` to deploy the snapshot image【F:doc/Dualboot.md†L120-L145】.

## Technical Notes

- The runtime supports unboxed 64‑bit arithmetic, short floats and generational GC【F:README.md†L31-L40】.
- USB stack and improved filesystem support were added after Demo 4 along with SMP and 3D acceleration via Virgl【F:README.md†L25-L40】.
- Network activity indicators, asynchronous APIs and improved atomic operations are built into the supervisor and networking layers【F:README.md†L32-L38】.

