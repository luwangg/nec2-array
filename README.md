/*
Tools for Antenna array simulation in Nec2  
Copyright (C) 2014 Bogdan Diaconescu

This program is free software; you can redistribute it and/or
modify it under the terms of the GNU General Public License
as published by the Free Software Foundation; either version 2
of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301, USA.
*/  

##Tools for Antenna array simulation in Nec2

http://yo3iiu.ro/blog/?p=1423  

![alt text][logo]
[logo]: https://github.com/BogdanDIA/nec2-array/raw/master/pictures/rootMusic.png "Root Music DOA"

**Description of the tools:**

This is a set of tools that simulate an antenna array to obtain array output which in turn is used by Matlab to run various Direction Of Arrival (DOA) algorithms. The 4Nec2 MoM program is used to simulate one or more signal sources that emmit a modulated signal toward the array. Matlab files are provided for evaluation of various DOA algorithms.

generate_one.cc - generate a {4Nec2}/models/model.bat file and corresponding model files for running under 4Nec2 based on the model defined in model.nec and parameters f1, f2, fs defined in parse_one.cc. Each generated model file has excitation modulated in amplitude according with a cos() function. For each sample one model file is created in {4Nec2}/models/a/ directory having the filename m$sample.nec where 'sample' is the sample number for which the 4Nec2 is run.

parse_one.cc - parse a set of 4Nec2 out files produced by model.bat and generate a complex matrix representing the output of the antenna array in signal.out file placed in current directory.

generate_mutual.cc - generate {4Nec2}/models/mutual.bat and corresponding model files for calculating the receiving mutual coupling impedance matrix. The model files are generated in {4Nec2}/models/m/m_i_j.nec where i, j are array elements antenna.

parse_mutual.cc - parse a set of 4Nec2 out files generated by mutual.bat and calculate the receiving mutual coupling matrix for the array in mutual.out file placed in out/ current directory.

generate_sweep.cc - generate a {4Nec2}/models/m_sweep.bat file and corresponding model files for running under 4Nec2 for an azimuth sweep and each of the sample used in the modulation and sampling with fs. The model files are generated in {4Nec2}/models/a/m_$az_$sample.nec where 'az' is the azimuth for the excitation position relative to the array and 'sample' is the sample for which the 4Nec2 is run.

parse_sweep.cc - parse the set of 4Nec2 out files produced by m_sweep.bat and generates a complex matrix representing the output of the antenna array in out/sweep_$az.out where 'az' is the azimuth for the excitation position relative to the array.

matlab/ - directory that contains .m files for executing the various DOA algorithms.

**How to build:**

 cd lib
 make all

**How to run:**

 place the nec2-array in the 4Nec2 installation directory  
 ./bootstrap.sh  

To run one simulation:

 ./generate_one  
wine cmd.exe will give windows comand prompt  
cd to ${4Nec2}/models directory  
model.bat  
 ./parse_one  

To run a full azimuth sweep:

 ./generate_sweep  
wine cmd.exe will give windows comand prompt  
cd to ${4Nec2}/models directory  
m_sweep.bat  
 ./parse_sweep  

To calculate mutual impedance matrix:

 ./generate_mutual  
wine cmd.exe will give windows comand prompt  
cd to ${4Nec2}/models directory  
mutual.bat  
 ./parse_mutual  

**Run matlab files (phased array module is needed):**
 rootMusic  
 esprit  
 wsf  
 beamscan  
 mvdr  


