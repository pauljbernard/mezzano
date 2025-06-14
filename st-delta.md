# Smalltalk Features Missing in Mezzano

The following list highlights capabilities commonly found in modern Smalltalk environments such as Pharo that are absent or incomplete in Mezzano.

- **Integrated Image-Based IDE.**  Pharo provides a rich graphical environment with browsers and inspectors.  Mezzano only ports McCLIM and some introspection tools, with no dedicated Smalltalk-style IDE【F:README.md†L48-L53】.
- **Robust Package Management.**  Smalltalk uses tools like Metacello for versioned packages.  Mezzano merely ports Quicklisp without a system-level manager【F:README.md†L50-L53】.
- **Cross‑Platform VM.**  Pharo runs on multiple operating systems.  Mezzano distributes only x86‑64 images and warns that AArch64 support requires code tinkering【F:README.md†L13-L17】.
- **Mature Networking Stack.**  Smalltalk environments support DHCP and bridging.  Mezzano notes that only specific NICs work and DHCP or bridging are not implemented【F:doc/manual.md†L11-L16】.
- **Foreign Function Interface.**  Pharo can call external libraries via FFI.  Searching Mezzano reveals no general FFI layer【F:sbcl-delta.md†L5-L9】.
- **Stable SMP and Threads.**  Pharo's VM is multi-threaded.  Mezzano warns that SMP support is experimental and may need to be disabled【F:doc/Dualboot.md†L188-L204】.
- **External Program Execution.**  Smalltalk systems spawn OS processes.  The Mezzano repository lacks a facility comparable to `run-program`【F:sbcl-delta.md†L13-L15】.
