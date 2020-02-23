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