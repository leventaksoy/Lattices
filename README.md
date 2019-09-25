PURPOSE:
-------
The aim of codes described below is to realize given logic function(s) using a switching lattice including four-terminal switches. This README explains the functionality and usage of these tools in detail.

JANUS:
------
JANUS is an approximate algorithm that aims to find the realization of a logic function on a switching lattice including a number of four-terminal switches close to the minimum. JANUS is developed in Perl and can run on Windows and Linux operating systems. For Windows and Linux, it was tested under the Strawberry Perl (http://strawberryperl.com/) and Perl v5.13.6, respectively. 

Dependicies:
------------
JANUS uses espresso to find the irredundant sum of products form of a logic function and its dual, a 0-1 ILP solver to solve the partitioning problem, and a SAT solver to solve the lattice mapping (LM) problem. Below, you can find the list where you can find these tools.

Espresso - logic minimization tool - (https://ptolemy.berkeley.edu/projects/embedded/Alumni/pchong/sis.html)
Scip - integer programming solver - (https://scip.zib.de/)
Glucose - SAT solver - (http://www.labri.fr/perso/lsimon/glucose/) 
Lingeling - SAT solver - (http://fmv.jku.at/lingeling/)
Cryptominisat - SAT solver - (https://github.com/msoos/cryptominisat/releases)

SCIP version 2.1.1 was used in our algorithms and glucose was found to be more efficient than other SAT solvers while finding a solution to the LM problem. Since its output format is a little bit different than others, please keep the name "glucose" in the executable file.

The location of all these tools should be given in the paths.pl file.

For the Windows 64-bit operating system, these tools can be found under the solvers_win directory. 

Input:
------
The input to JANUS is a single logic function defined in the PLA format. More details on this format can be found in http://www.ecs.umass.edu/ece/labs/vlsicad/ece667/links/espresso.5.html

Below, you can find an example realizing a two input XOR gate.

.i 2
.o 1
.ilb a b
.ob f
.p 4
00 0
01 1
10 1
11 0
.e

This input can be too simple to just include the prime implicants of the logic function as given below, which is the format of the latsynth method (https://people.eng.unimelb.edu.au/gkgange/synth/index.html).

01 1
10 1

Note that the single logic function should be written in a file whose extension is "pla".

Usage:
------
The usage of JANUS is given below which can be obtained after running the "perl janus.pl -h" command.

Usage:       perl janus.pl <File_Name> -verb=0/1/2 -cpu_lim=<int> -sat_lim=<int> -set_row=<int> -set_col=<int> -no_ub6                       
File_Name:   Name of the file including a single target function given in PLA format                                                         
-verb:       Level of verbosity (0: full, 1: medium, 2: none), by default it is full                                                         
-cpu_lim:    CPU time limit in seconds, by default it is 21600                                                                               
-sat_lim:    CPU time limit for the SAT algorithm in seconds, by default it is 1200                                                          
-set_row:    Search for a solution on the given number of rows. By default it is 0, meaning that no special lattice matrix is considered     
-set_col:    Search for a solution on the given number of columns. By default it is 0, meaning that no special lattice matrix is considered  
-no_ub6:     Turn off the DS method that may find an upper bound better than the others using more computational effort, by default it is on 
Description: Finds the realization of a single logic function in a lattice including four-terminal switches                                  

Auxiliaries:
------------
JANUS uses the following codes which can also work as a standalone code.

genlatfunc_rec.pl - finds all the irredundant four-connected paths between the top and bottom plates, i.e., the lattice function itself written in a file called lmxn where m and n denotes the number of rows and columns, respectively.

genlatfunc_dual_rec.pl - finds all the irredundant eight-connected paths between the left and right plates, i.e., the dual of the lattice function itself written in a file called dmxn where m and n denotes the number of rows and columns, respectively.

janus_dc.pl - finds an initial upper bound using the DS method

Output:
-------
The realization of a logic function defined in a "file_name.pla" on a lattice is given in a "file_name.sol" with more details.

MEDEA:
------
MEDEA is a divide and conquer method used to find a realization of a single logic function on a switching lattice using a little computational effort. Its dependicies and input format are the same as JANUS. 

Usage:
------
The usage of MEDEA is given below which can be obtained after running the "perl medea.pl -h" command.

Usage:       perl medea.pl <File_Name> -verb=0/1/2 -cpu_lim=<int> -sat_lim=<int> -ulbd=<int>              
File_Name:   Name of the file including a single target function given in PLA format                        
-verb:       Level of verbosity (0: full, 1: medium, 2: none), by default it is full                        
-cpu_lim:    CPU time limit in seconds, by default it is 21600                                              
-sat_lim:    CPU time limit for the SAT algorithm in seconds, by default it is 300                          
-ubld:       Difference between the upper and lower bounds greater than 0, by default it is 31              
Description: Finds the realization of a single logic function in a lattice including four-terminal switches 

MEDEA uses JANUS to find the realization of sub-functions on a switching lattice. Thus, JANUS and its auxilaries are also required.

Output:
-------
The realization of a logic function defined in a "file_name.pla" on a lattice is given in a "file_name_dc.sol" with more details.

MULTIPLE FUNCTIONS:
-------------------
MF_TOOL can realize the multiple functions in a single lattice. Its dependicies are the same as JANUS. Its input format is again a PLA format.

Below, the description of a full adder circuit is given as an example.

.i 3
.o 2
.ilb a b cin
.ob s cout
.p 8
000 00
001 10
010 10
011 01
100 10
101 01
011 01
111 11
.e

Usage:
------
The usage of MF_TOOL is given below which can be obtained after running the "perl janus_multi.pl -h" command.

Usage:       perl mf_tool.pl <File_Name> -verb=0/1/2 -cpu_lim=<int> -sat_lim=<int> -algo=janus/medea -tech=<int>            
File_Name:   Name of the file including multiple logic functions given in PLA format                                            
-verb:       Level of verbosity (0: full, 1: medium, 2: none), by default it is full                                            
-cpu_lim:    CPU time limit in seconds, by default it is 21600                                                                  
-sat_lim:    CPU time limit for the SAT algorithm in seconds, by default it is 1200                                             
-algo:       The algorithm used to optimize the switching lattice in the first and second techniques, by default it is janus    
-tech:       The design technique, by default it is 2                                                                           
               1: Realizes each output at a time using janus/medea to find the optimized solution and merge these lattices      
               2: Initially, apply the first technique and then, checks if the #rows and #columns in each output can be reduced 
               3: Aims to implement each output with the minimum number of rows, starting from 3                                
Description: Finds the realization of multiple logic functions in a lattice including four-terminal switches                    

Output:
-------
The realization of logic functions defined in a "file_name.pla" on a lattice is given in a "file_name_multi_tech_n.sol" with more details, where n denotes the number of the design technique given above.

NOTES:
------
All the algorithms generate additional files which are stored in the temp file.

REFERENCE:
----------
The details in JANUS and MF_TOOL can be found in the following paper.

Levent Aksoy, Mustafa Altun, "A Satisfiability-Based Approximate Algorithm for Logic Synthesis Using Switching Lattices", DATE, pp.1637-1642, 2019. (http://www.ecc.itu.edu.tr/images/f/fe/Aksoy_Altun_SAT_based_Synthesis_of_Switching_Lattices.pdf)

CONTACT:
--------
Please contact Levent Aksoy (aksoyl@itu.edu.tr) if you have any trouble running the codes and suggestions and/or comments.
