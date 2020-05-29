## Artifact evaluation for ICCAD2020. PLEASE KEEP IT CONFIDENTIAL


AIG Opt : iccad2020/aig_opt/ and execute "run.sh" for all results. Or you can execute the command in run.sh individually.

LUT Opt : iccad2020/fpga_opt/ and execute "run.sh" for all results. Or you can execute the command in run.sh individually.

CNF Opt : iccad2020/cnf_opt/ and execute "run.sh" for all results. Or you can execute the command in run.sh individually.

STD Opt : iccad2020/std_map_opt/ and execute "run.sh" for all results. Or you can execute the command in run.sh individually. Additional README provided in that folder.

Vivado results: ftune-fpga-xilinx/vivado/ and execute "vivado_ftune.sh"

## Required Packages:
	- readline: sudo apt-get install libreadline6 libreadline6-dev (Ubuntu)
	- readline: sudo yum install readline-devel (CentOS 7)
	- -stdc++11 
	- OpenMP (https://www.openmp.org/resources/openmp-compilers-tools/)
		- wget https://download.open-mpi.org/release/open-mpi/v4.0/openmpi-4.0.1.tar.gz; tar -xvf openmpi-4.0.1.tar.gz
		- cd openmpi-4.0.1; ./configure; make -j12 all install
	- export ./abc PATH TO .bashrc
		For example: echo "export PATH=$(pwd):\${PATH}" >> ~/.bashrc; source ~/.bashrc
	
## "ftune" implemented in ABC

	abc 01> ftune -h
	usage: ftune [drtfpihSL]
		flowtune(ftune): Multi-Armed Bandit (MAB) synthesis flow tuning for Logic Minimization
	-t    : Targeted metric (default = 0, i.e., AIG Minization targeting number of AIG nodes)
	      : t=0 AIG Minization - Minimizing AIG nodes                       :  ftune -d i10.aig -r 4 -t 0 -p 1 -i 10 -s 5 -L [other options]
	      : t=1 AIG Minization - minimizing AIG levels                      :  ftune -d i10.aig -r 4 -t 1 -p 1 -i 10 -s 5 -L [other options]
	      : t=2 Technology mapping (w Gate Sizing + STA) Min STA-Delay      :  ftune -d i10.aig -r 4 -t 2 -p 1 -i 10 -s 5 -L your.lib(Liberty) [other options]
	      : t=3 Technology mapping (w Gate Sizing + STA) Min Area           :  ftune -d i10.aig -r 4 -t 3 -p 1 -i 10 -s 5 -L your.lib(Liberty) [other options]
	      : t=4 FPGA Mapping - Miniziming Number of 6-input LUTs            :  ftune -d i10.aig -r 4 -t 4 -p 1 -i 10 -s 5 [other options]
	      : t=5 FPGA Mapping - Miniziming Levels of 6-input LUT network     :  ftune -d i10.aig -r 4 -t 5 -p 1 -i 10 -s 5 [other options]
	      : t=6 SAT (CNF) Minization - Miniziming Number of Clauses         :  ftune -d cnf.aig -r 4 -t 6 -p 1 -i 10 -s 5 [other options]
	      : t=7 SAT (CNF) Minization - Miniziming Number of literals        :  ftune -d cnf.aig -r 4 -t 7 -p 1 -i 10 -s 5 [other options]
	      : t=8 Regular Technology mapping using GENLIB (map) Min Delay     :  ftune -d i10.aig -r 4 -t 8 -p 1 -i 10 -s 5 -L your.genlib(GENLIB) [other options]
	      : t=9 Regular Technology mapping using GENLIB (map) Min Area      :  ftune -d i10.aig -r 4 -t 9 -p 1 -i 10 -s 5 -L your.genlib(GENLIB) [other options]
	-h    : Print the command usage
	-r    : Number of appearances of each synthesis command (default = 3)
	-p    : Factor of number of Arms (default = 1)
	-i    : Number of MAB iterations (default = 10)
	-s    : Number of MAB sampling for each iteration per Arm (default = 5)
	-f    : Toggle using long-short-term memory for probability matching (default=FALSE)
	-C    : Customize the logic transformations (commands) for tuning instead of default commands. 
		 Example 1:  -C b;rw;rwz;rf (your flow will use these 4 opts).
 			
		 Example 2: -C b;rw;rwz;rf;your_cmd (You can define your new command in abc.rc namely your_cmd and tunes for these 4 opts + your_cmd).
	-S    : Toggle using Softmax() or LogSoftmax() for finalizing samples at each iteration (default=FALSE)
		    -S 0 : Using winning rate Pr
		    -S 1 : Using Softmax()
		    -S 2 : Using LogSoftmax()
	-L    : Liberty or GENLIB file. Required for Technology mapping tuning (t=2,3,8,9) 
