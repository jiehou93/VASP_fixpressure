# Python code for structure relaxation under a specific stress tensor using VASP
This code allows VASP to perform structure relaxation to reach a designated stress tensor (which is not a standard VASP feature).
In general, the code can adjust the POSCAR automatically, and call VASP iteratively until the stress state converges to the value you desire. 
Note isotropic linear elastic theory is used to adjust POSCAR. For anisotropic materials, this might slow down the convegency. I performed some benchmark simulations were dones using this code for W, Mo, Cr, alpha-Fe systems, so far it works fine. 
However, for highly anisotropic materials, you might encounter some convergency problem. A possible solution is to modify the code by including a full stifiness tensor (Cijkl).

Instructions for usage:
1. Input the pressure (stress) tensor in the script
2. Input estimated elastic modulus in the script
3. Set ISIF=2 in the INCAR
4. Copy POSCAR to poscar.0
5. Configurate mpiexec commands in the script according to your VASP directory and job management system
6. cd to job directory and use 'qsub fixpressure.py' (assuming you are using pbs job system) to submit your job 

Suggestions for accurate force calculation:
Use a high ECUT and k-points density (from my experience, force converges very slowly against k-points in VASP)
Use LREAL=.FALSE., real space calculation sometimes return ridiculous forces.
Use PREC=Accurate

Suggestions for better computational efficiency:
Use LWAVE=.T. and default ISTART and ICHARG, this allows VASP to read WAVECAR from previous interation, instead of starting from scratch

General algorithm:
1. run vasp with ISIF=2 to get current pressure tensor
2. using generalized Hooke's law and elastic modulus you input, estimate the POSCAR modification required to get target pressure
3. repeat 1-2 until the current pressure  - target pressure is within convergency criteria
