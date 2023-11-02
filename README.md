This repository includes the algorithms developed for the realization of logic functions using switching lattices and the logic functions used as benchmarks. 

The LS_algos directory includes the algorithms proposed for the lattice synthesis (LS) problem which is defined as finding a realization of a logic function on a lattice which has the minimum number of switches. JANUS is an approximate algorithm that aims to find the realization of a logic function on a switching lattice including a number of four-terminal switches close to the minimum. MEDEA is a divide&conquer method used to find a realization of a single logic function on a switching lattice using a little computational effort. MF_TOOL can realize multiple functions in a single lattice using the solutions of JANUS or MEDEA on each single logic function.

On the other hand, the LSDC_algos directory includes the algorithms proposed for the lattice synthesis under a delay constraint (LS_DC) problem which is defined as finding a realization of a logic function on a lattice which has the minimum number of switches without violating the delay constraint given in terms of the number of switches in the critical path. While PHAEDRA is an approximate algorithm, TROADES is a divide&conquer method similar to JANUS and MEDEA, respectively.

The detailed descriptions of these algorithms are given in the README files.

For citation please use the following:

@ARTICLE{aksoy21,
  author={Aksoy, Levent and Akkan, Nihat and Sedef, Herman and Altun, Mustafa},
  journal={IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems}, 
  title={Realization of Logic Functions Using Switching Lattices Under a Delay Constraint}, 
  year={2021},
  volume={40},
  number={10},
  pages={2036-2048},
  doi={10.1109/TCAD.2020.3035629}
}

@ARTICLE{aksoy20,
  author={Aksoy, Levent and Altun, Mustafa},
  journal={IEEE Transactions on Computers}, 
  title={Novel Methods for Efficient Realization of Logic Functions Using Switching Lattices}, 
  year={2020},
  volume={69},
  number={3},
  pages={427-440},
  doi={10.1109/TC.2019.2950663}
}
