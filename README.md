# Python code for structure relaxation under a specific stress tensor using VASP
This code allows VASP to perform structure relaxation under a designated stress tensor (which is not a standard VASP feature). 
In general, the code can adjust the POSCAR automatically, and call VASP iteratively until the stress state converges to the value you desire. 
Benchmark simulations were dones using this code for W, Mo, Cr, alpha-Fe systems, and so far it works quite good. 
To use this code, you need to install a python interpreter (I’m using python 2.7.3).
The detailed instruction is written within the code as annotations. It’s a short code within 100 lines, should be easy to employ. 
I hope this code can be of use to other researchers.
