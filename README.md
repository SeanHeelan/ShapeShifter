# Introduction 

ShapeShifter is a heap allocator that allows for a particular heap layout to be
selected by the user. Its purpose is to support automatic exploit generation,
and primitive discovery, by allowing such a system to *assume* a particular heap
layout holds, explore the possibilities that layout offers, and then later, if
the layout is useful, figure out how to achieve that layout.

I developed ShapeShifter for use in the system described in my CCS 2019 paper
titled *Gollum: Modular and Greybox Exploit Generation for Heap Overflows in
Interpreters*. The code in this repository is an updated version of ShapeShifter
and so some features may have been added, changed or removed.

If ShapeShifter is useful to you in your research, please cite it as follows:

```
@inproceedings{Heelan:2019:GMG:3319535.3354224,
 author = {Heelan, Sean and Melham, Tom and Kroening, Daniel},
 title = {Gollum: Modular and Greybox Exploit Generation for Heap Overflows in Interpreters},
 booktitle = {Proceedings of the 2019 ACM SIGSAC Conference on Computer and Communications Security},
 series = {CCS '19},
 year = {2019},
 isbn = {978-1-4503-6747-9},
 location = {London, United Kingdom},
 pages = {1689--1706},
 numpages = {18},
 url = {http://doi.acm.org/10.1145/3319535.3354224},
 doi = {10.1145/3319535.3354224},
 acmid = {3354224},
 publisher = {ACM},
 address = {New York, NY, USA},
 keywords = {exploit generation, greybox, primitive search},
} 
```

# Details

ShapeShifter offers two run modes, one to record all of the allocations that an
application makes up to the point of a heap overflow and to assign IDs to these
allocations, and another in which any two allocations made by the application
can be requested to be placed adjacent to each other. In both modes ShapeShifter
uses LD_PRELOAD to replace the standard memory allocation functions (malloc, 
realloc, calloc and free). 

## Allocation Recording Mode

The purpose of this mode is to generate a file describing each allocation
that the application makes. For each allocation ShapeShifter outputs an
identifier, the requested allocation size, and the offsets of any pointers
within that allocation at the point where the execution terminates. Pointers are
detected heuristically by iterating over the allocation's contents in four byte
increments, converting the data at each offset to a pointer type, and checking
if it is possible to read the memory at that address.

To see this mode in action build the `crasher` application in the `test`
sub-directory, by running `make` in that directory. Next, run the `./recalloc.py`
script as follows:

```
$ ./recalloc.py -t test/crasher -i ./test/OVERFLOW_DATA -a ./test/OVERFLOW_DATA -l ./libshapeshifter/libshapeshifter.so -w /tmp/output
[+] Using /tmp/output as the output directory
[+] Executing: test/crasher ['./test/OVERFLOW_DATA']
[+] Return code: -11
[+] SIGSEGV detected. OK to proceed.
```

`recalloc.py` takes care of LD_PRELOAD'ing `libshapeshifter.so` and setting up the 
various arguments that it requires. `libshapeshifter.so` reads its arguments from 
the environment (search for `SSR_` and `AFL_` in `libshapeshifter/libshapeshifter.c`
to find them), and you *can* set them up yourself if you wish (see `recsetup.sh` for
an example), but usually it makes sense to just use `recalloc.py`.


## Delayed Enabling of Allocation Tracking

## Saving the Crashing Processes Output




## Layout Request Mode

# Usage

## Compilation 

Compile `libshapeshifter.so` by running `make` in the `libshapeshifter` sub-directory. It depends `libunwind`. 

