+++
title = "Microkernel in Rust"
description = "A small 64-bit x86 kernel with memory paging, an interrupt table, and a VGA text driver."
date = 2026-02-15
weight = 1

[extra]
tech_stack = ["Rust", "x86_64", "QEMU"]
github = "https://github.com/yourusername/microkernel-rust"
demo = ""
featured = true
+++

This is a bare-metal kernel written in Rust for the x86_64 architecture. It runs without the standard library (`#![no_std]`) and boots directly into 64-bit long mode.

### What it does

* Writes text to the VGA buffer at memory address `0xb8000`.
* Sets up an Interrupt Descriptor Table (IDT) to catch CPU exceptions like page faults and divide-by-zero errors.
* Maps virtual to physical addresses through 4-level page tables.
* Implements a simple heap allocator so the code can use collections like `Vec` and `String`.

```rust
#![no_std]
#![no_main]

use core::panic::PanicInfo;

#[no_mangle]
pub extern "C" fn _start() -> ! {
    println!("Kernel booted.");
    microkernel::init();
    microkernel::hlt_loop();
}

#[panic_handler]
fn panic(info: &PanicInfo) -> ! {
    println!("{}", info);
    microkernel::hlt_loop();
}
```

Handling double faults was one of the harder parts: if a stack overflow happens, the CPU tries to push the exception frame to an already-broken stack, causing a triple fault and an immediate reboot. Setting up a dedicated stack in the Interrupt Stack Table fixed that.
