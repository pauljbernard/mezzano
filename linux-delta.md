# Desktop Linux Features Missing in Mezzano

The following features are commonly available on desktop Linux distributions such as Ubuntu but are absent or limited in Mezzano.

- **Broad Hardware Compatibility.**  Linux supports a large variety of devices out of the box.  Mezzano only publishes x86‑64 images and getting it running on other hardware typically requires digging into the code【F:README.md†L13-L17】.
- **Comprehensive Networking.**  Linux systems offer DHCP and bridging for many network adapters.  Mezzano supports only RTL8168 and virtio-net NICs and lacks DHCP and network bridging【F:doc/manual.md†L10-L16】.
- **Stable Multi-Core Support.**  Linux kernels provide robust SMP on multi‑processor systems.  Mezzano warns that SMP is experimental and may fail when multiple CPUs are detected【F:doc/Dualboot.md†L188-L204】.
- **Rich Package Management.**  Linux distributions include package managers like APT with extensive software repositories.  Mezzano merely ports Quicklisp for Lisp packages without a system-level package manager【F:README.md†L50-L53】.
- **Extensive Graphics Drivers.**  Linux offers GPU drivers for diverse hardware, whereas Mezzano only lists a GMA950 driver and Virgl-based 3D acceleration for QEMU【F:README.md†L28-L32】.
- **External Program Execution.**  Linux can spawn arbitrary processes.  Mezzano lacks this capability, as noted in `sbcl-delta.md` describing the absence of `run-program` support【F:sbcl-delta.md†L13-L15】.
