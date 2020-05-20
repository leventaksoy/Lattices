This repository includes the algorithms developed for the realization of logic functions using switching lattices and the logic functions used as benchmarks. 

The LS_algos directory includes the algorithms proposed for the LS problem. JANUS is an approximate algorithm that aims to find the realization of a logic function on a switching lattice including a number of four-terminal switches close to the minimum. MEDEA is a divide&conquer method used to find a realization of a single logic function on a switching lattice using a little computational effort. MF_TOOL can realize the multiple functions in a single lattice using the solutions of JANUS or MEDEA on each single logic function.

On the other hand, the LSDC_algos directory includes the algorithms proposed for the LS_DC problem. While PHAEDRA is an approximate algorithm, TROADES is a divide&conquer method both aim to find a realization of a single logic function on a switching lattice without violating the delay constraint.

The detailed descriptions of these algorithms are given in the README files.
