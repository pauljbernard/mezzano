# SBCL Features Missing in Mezzano

The following list summarises notable SBCL capabilities that do not appear in the current Mezzano code base.

- **Foreign Function Interface (FFI).**  SBCL provides the `sb-alien` interface and supports third-party libraries such as CFFI for calling C code.  Searching the repository shows no implementation of `sb-alien` or a general FFI layer.

- **Stable OS Threading.**  SBCL's `sb-thread` library offers POSIX threads and mature synchronisation primitives.  Mezzano implements its own SMP support, but it is still described as experimental and unreliable:
  ```
  Multiple CPUs detected. SMP support is currently experimental and unreliable.
  ```
  This message comes from the boot process and is mentioned in the documentation【F:doc/Dualboot.md†L188-L203】.

- **Wide Platform Support.**  SBCL runs on many host architectures.  Mezzano only publishes x86‑64 images and states that AArch64 works on limited hardware, making hardware support a hands‑on effort【F:README.md†L13-L18】.

- **External Program Execution.**  SBCL exposes `sb-ext:run-program` to launch other operating system processes.  The Mezzano source tree lacks an equivalent facility—`grep` of the system directory returns no occurrences of "run-program"【487b2f†L1-L2】.

These differences highlight areas where SBCL functionality goes beyond what is currently implemented in Mezzano.
