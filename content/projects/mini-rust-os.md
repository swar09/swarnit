+++
title = "MicroKernel in Rust"
description = "A minimal 64-bit x86 operating system kernel with cooperative multitasking, memory paging, and VGA text driver."
date = 2026-02-15
weight = 1

[extra]
tech_stack = ["Rust", "x86_64", "QEMU", "Assembly", "Linker Scripts"]
github = "https://github.com/yourusername/microkernel-rust"
demo = ""
featured = true
+++

## Overview

A standalone bare-metal operating system kernel written in **Rust** for the `x86_64` architecture. The kernel operates without standard library dependencies (`#![no_std]`) and boots directly via a custom bootloader into 64-bit long mode.

### Highlights & Key Features

* **VGA Buffer Driver**: Implemented safe, volatile memory writes to the VGA text buffer (`0xb8000`) with color styling and text wrapping.
* **Interrupt Descriptor Table (IDT)**: Handled CPU exceptions, page faults, double faults, and hardware interrupts via the 8259 PIC.
* **Memory Paging**: Configured 4-level page tables for virtual-to-physical memory translation with recursive paging.
* **Heap Allocator**: Custom linked-list and fixed-size block memory allocators enabling dynamic Rust data structures (`Vec`, `Box`, `String`).

```rust
#![no_std]
#![no_main]

use core::panic::PanicInfo;

#[no_mangle]
pub extern "C" fn _start() -> ! {
    println!("Hello from bare-metal Rust!");
    
    microkernel::init();
    
    println!("Kernel initialized successfully.");
    microkernel::hlt_loop();
}

#[panic_handler]
fn panic(info: &PanicInfo) -> ! {
    println!("{}", info);
    microkernel::hlt_loop();
}
```

### Challenges Overcome

Preventing kernel stack overflow during recursive double faults was resolved by setting up an **Interrupt Stack Table (IST)** in the Task State Segment (TSS) with an isolated emergency stack.
