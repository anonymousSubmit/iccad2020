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
	

