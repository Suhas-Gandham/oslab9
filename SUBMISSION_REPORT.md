Name:Suhas gandham
roll: 2401MC18
OS LAB ASSIGNMENT 9.
# xv6 Memory Management Exercises

## Page-table inspection

Added the `vmprint()` system call. It walks only page-directory entries below
`KERNBASE`, prints each present user mapping's virtual and physical addresses
and P/W/U bits, and reports the number of present user pages and user
page-table pages (excluding the page directory). `pttest` prints the map,
reserves four pages with `sbrk`, touches one byte in each page, and prints it
again. The touches are needed because the lazy allocator in Question 2 does
not map pages at `sbrk` time; the second dump should therefore contain four
additional user mappings.

## Lazy allocation and page faults

Positive `sbrk` now reserves virtual address space without allocating frames.
User-mode not-present faults below the process break allocate zero-filled
pages and increment a per-process counter exposed by `getfaults()`. Invalid
or protection faults kill only the process that caused them. `deallocuvm()`
and `copyuvm()` now accept unmapped holes. `faulttest` reserves 32 pages,
writes to five distinct pages, reports five handled faults, and then checks
that an out-of-range access terminates its child while the parent survives.

## FIFO and LRU simulation

`pagerepl` simulates both policies and shows the frame contents and hit/fault
result after every reference. Running `pagerepl` without arguments uses the
requested 20-reference sample, shows the detailed 3-frame run, and prints
fault counts and integer hit percentages for 3, 4, and 5 frames. The sample
should produce 15 FIFO faults and 12 LRU faults with 3 frames. Custom runs
accept `pagerepl frames reference [reference ...]`.

## Demonstration

After building and booting xv6, run `pttest`, `faulttest`, and `pagerepl` at
the xv6 shell prompt. Capture the terminal for each program to provide the
requested submission screenshots.
