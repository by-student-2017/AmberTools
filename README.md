# AmberTools
- AmberTools is a free, useful standalone package and a prerequisite for installing Amber itself. The AmberTools suite is free of charge, and its components are mostly released under the GNU General Public License (GPL). A few components are included that are in the public domain or which have other, open-source, licenses. The libsander and libpbsa libraries use the LGPL license. (see https://ambermd.org/GetAmber.php#ambertools)


## Ubuntu 22.04 LTS (Related packages)
```
sudo apt update
sudo apt -y install tcsh make gcc gfortran flex bison patch bc wget xorg-dev libz-dev libbz2-dev build-essential libopenblas-dev libarpack2-dev libnetcdf-dev libnetcdff-dev
sudo apt -y install openmpi-bin libopenmpi-dev openssh-client python3-mpi4py python3-numpy python3-setuptools
```
- For Ambertools24 or later
```
sudo apt -y install swig octave-dev guile-3.0-dev libprotobuf-dev libperl-dev netcdf-bin
```
- GPU
```
sudo apt -y install g++-11
sudo apt -y install g++-10
sudo apt -y install nvidia-cuda-toolkit libnvidia-ml-dev
```


## PLUMED, Installation
```
wget https://github.com/plumed/plumed2/releases/download/v2.9.0/plumed-2.9.0.tgz
tar zxvf plumed-2.9.0.tgz
cd plumed-2.9.0
./configure --prefix=/mnt/d/plumed-2.9.0/opt
make
make install
```
- Note: "make test" is failed on gfortran and gcc, etc
### PLUMED, Environment settings
```
echo '# PLUMED, Environment settings' >> ~/.bashrc
echo 'export PATH=$PATH:/mnt/d/plumed-2.9.0/opt/bin' >> ~/.bashrc
echo 'export PATH=$PATH:/mnt/d/plumed-2.9.0/opt/lib' >> ~/.bashrc
echo 'export PATH=$PATH:/mnt/d/plumed-2.9.0/opt/include' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/mnt/d/plumed-2.9.0/src/lib' >> ~/.bashrc
bash
````


## Note for AmberTools source code
- I couldn't upload it because I didn't have enough storage space. Please download it directly from the link below.


## AmberTools24 (amber24) [AT24]
```
wget https://ambermd.org/downloads/AmberTools24_rc5.tar.bz2
```
### AmberTools24, Installation (Ubuntu 22.04 LTS (or WSL2), cmake, 1 CPU (=serial))
- Not use MPI, GPU, GUI, Quick, python, and miniconda
- This is a very simple executable file with few dependencies, suitable for basic functionality. It has also passed testing.
```
tar xvf AmberTools24_rc5.tar.bz2
cd amber24_src
./update_amber --check-updates
./update_amber --update
cd build
AMBER_PREFIX=$(dirname $(dirname `pwd`))
mkdir build_cpu_serial && cd build_cpu_serial
cmake $AMBER_PREFIX/amber24_src -DCMAKE_INSTALL_PREFIX=$AMBER_PREFIX/amber24 -DCOMPILER=GNU -DMPI=FALSE -DOPENMP=FALSE -DCUDA=FALSE -DNCCL=FALSE -DBLA_VENDOR=OpenBLAS -DBUILD_GUI=FALSE -DBUILD_QUICK=FALSE -DINSTALL_TESTS=TRUE -DBUILD_PYTHON=FALSE -DDOWNLOAD_MINICONDA=FALSE -Wno-dev 2>&1 | tee cmake.log
make -j8 && make install

source $AMBER_PREFIX/amber24/amber.sh
echo "# Ambertools24 (amber24) environment settings" >> ~/.bashrc
echo "source $AMBERHOME/amber.sh" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/bin" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/lib" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/include" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/dat" >> ~/.bashrc
bash
```
- test (about 1 hours)
```
cd $AMBERHOME/test
make test.serial && make clean.test
```
### AmberTools24, Installation (Ubuntu 22.04 LTS (or WSL2), cmake, python, quick)
- Not use MPI, GPU, and GUI
- [-- Found PythonLibs: /home/inukai/miniconda3/lib/libpython3.10.so (found suitable exact version "3.10.14")] (If miniconda3 is not installed, set "-DDOWNLOAD_MINICONDA=TRUE".)
```
tar xvf AmberTools24_rc5.tar.bz2
cd amber24_src
./update_amber --check-updates
./update_amber --update
cd build
AMBER_PREFIX=$(dirname $(dirname `pwd`))
mkdir build_serial && cd build_serial
cmake $AMBER_PREFIX/amber24_src -DCMAKE_INSTALL_PREFIX=$AMBER_PREFIX/amber24 -DCOMPILER=GNU -DMPI=FALSE -DOPENMP=TRUE -DCUDA=FALSE -DNCCL=FALSE -DBLA_VENDOR=OpenBLAS -DBUILD_GUI=FALSE -DBUILD_QUICK=TRUE -DINSTALL_TESTS=TRUE -DBUILD_PYTHON=TRUE -DDOWNLOAD_MINICONDA=FALSE -Wno-dev 2>&1 | tee cmake.log
make -j8 && make install

source $AMBER_PREFIX/amber24/amber.sh
echo "# Ambertools24 (amber24) environment settings" >> ~/.bashrc
echo "source $AMBERHOME/amber.sh" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/bin" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/lib" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/include" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/dat" >> ~/.bashrc
bash
```
- test (about 3 hours)
```
cd $AMBERHOME/test
make test.serial && make clean.test
```
### AmberTools24, Installation (Ubuntu 22.04 LTS (or WSL2), make, parallel)
- Not use GUI, GPU, and Quick
- [-- Found PythonLibs: /home/inukai/miniconda3/lib/libpython3.10.so (found suitable exact version "3.10.14")] (If miniconda3 is not installed, set "-DDOWNLOAD_MINICONDA=TRUE".)
```
tar xvf AmberTools24_rc5.tar.bz2
cd amber24_src
./update_amber --check-updates
./update_amber --update
cd build
AMBER_PREFIX=$(dirname $(dirname `pwd`))
mkdir build_cpu_parallel && cd build_cpu_parallel
cmake $AMBER_PREFIX/amber24_src -DCMAKE_INSTALL_PREFIX=$AMBER_PREFIX/amber24 -DCOMPILER=GNU -DMPI=TRUE -DOPENMP=TRUE -DCUDA=FALSE -DNCCL=FALSE -DBLA_VENDOR=OpenBLAS -DBUILD_GUI=FALSE -DBUILD_QUICK=FALSE -DINSTALL_TESTS=TRUE -DBUILD_PYTHON=TRUE -DDOWNLOAD_MINICONDA=FALSE 2>&1 | tee cmake.log
make -j8 && make install

source $AMBER_PREFIX/amber24/amber.sh
echo "# Ambertools24 (amber24) environment settings" >> ~/.bashrc
echo "source $AMBERHOME/amber.sh" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/bin" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/lib" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/include" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/dat" >> ~/.bashrc
bash
```
- test (parallel)
```
cd $AMBERHOME/test
export DO_PARALLEL="mpirun -np 8"
make test.parallel.4proc && make clean.test
unset DO_PARALLEL
```
### AmberTools24, Installation (Ubuntu 22.04 LTS (or WSL2), cmake, GPU (=CUDA), no check)
- Not use MPI
- This is a very simple executable file with few dependencies, suitable for basic functionality. It has also passed testing.
- The steps for compiling on this GPU after performing the above two compilations (single and parallel) are shown below.
- Due to an error with the GPU, it is necessary to temporarily use gcc-10 and g++-10. Compile again for the problematic GPU (stotko/stdgpu#337, NVlabs/instant-ngp#119).
```
tar xvf AmberTools24_rc5.tar.bz2
cd amber24_src
./update_amber --check-updates
./update_amber --update
cd build
AMBER_PREFIX=$(dirname $(dirname `pwd`))
CUDA_HOME="/usr/lib/cuda"
mkdir build_gpu_serial && cd build_gpu_serial

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-10 10
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-10 10
sudo update-alternatives --config gcc
sudo update-alternatives --config g++

cmake $AMBER_PREFIX/amber24_src -DCMAKE_INSTALL_PREFIX=$AMBER_PREFIX/amber24 -DCOMPILER=GNU -DMPI=FALSE -DOPENMP=FALSE -DCUDA=TRUE -DCUDA_TOOLKIT_ROOT_DIR=${CUDA_HOME} -DNCCL=FALSE -DBLA_VENDOR=OpenBLAS -DBUILD_GUI=FALSE -DBUILD_QUICK=TRUE -DINSTALL_TESTS=TRUE -DBUILD_PYTHON=TRUE -DDOWNLOAD_MINICONDA=FALSE -Bbuild -Wno-dev 2>&1 | tee cmake.log
cd build
make -j8 && make install

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 11
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 11
sudo update-alternatives --config gcc
sudo update-alternatives --config g++

source $AMBER_PREFIX/amber24/amber.sh
echo "# Ambertools24 (amber24) environment settings" >> ~/.bashrc
echo "source $AMBERHOME/amber.sh" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/bin" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/lib" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/include" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/dat" >> ~/.bashrc
bash
```
- Note (https://github.com/stotko/stdgpu/issues/337, https://github.com/NVlabs/instant-ngp/issues/119): Error: /usr/include/c++/11/bits/std_function.h:435:145: CMake Error at pbsa.cuda_generated_cuda_pb.cu.o.RELEASE.cmake:278 (message):
- test (about 3 hours)
```
cd $AMBERHOME/test
#make test.cuda.serial && make clean.test
make test.serial && make clean.test
```
- Note: sqm (=semi-empirical quantum chemistry): MNDO, MNDO/d (=MNDOD), AM1 (AM1, AM1-D* or AM1-DH+), AM1/d (=AM1D), PM3, PDDG/PM3, PDDG/MNDO, RM1, PM3CARB1, PM3-MAIS, PM6 (PM6, PM6-D, or PM6-DH+), DFTB2 (mio-1-1), DFTB3 (3ob-3-1)
- Note: quick (QUantum Interaction Computational Kernel) ab initio quantum chemistry): HF, UHF, DFT (LDA, GGA, Hybrid-GGA, e.g., e B3LYP/cc-pVDZ), UDFT, vdW (Grimme)
- Note: DFT (of quick) = B3LYP, PBE0, D3MBJ, etc [DFT = BLYP, B3LYP, BP86, B97, B](https://quick-docs.readthedocs.io/en/24.3.0/user-manual.html)
- Note: BASIS (of quick) = 6-31G**, cc-pVTZ, aug-cc-pVTZ, def2-TZVP, etc
- Note: sander (Simulated Annealing with NMR-Derived Energy Restraints)
- Note: Mechanical and electrostatic embedding: AMBER/QM, QM = ADF, Gaussian, Orca, Q-Chem, TeraChem, QUICK, MRCC, or Fireball
- Note: Mechanical embedding: ADF, GAMESS-US, NWChem
- Note: sebomd (Semi-Empirical Born-Oppenheimer Molecular Dynamics): NDDO (=AN1, PM3, RM1, etc)


## AmberTools23 (amber22) [AT23]
```
wget https://ambermd.org/downloads/AmberTools23_rc6.tar.bz2
```
### AmberTools23, Installation (Ubuntu 22.04 LTS (or WSL2), cmake, 1 CPU (=serial))
- Not use MPI, GPU, GUI, Quick, python, and miniconda
- This is a very simple executable file with few dependencies, suitable for basic functionality. It has also passed testing.
```
tar xvf AmberTools23jlmrcc.tar.bz2
cd amber22_src
./update_amber --check-updates
./update_amber --update
cd build
AMBER_PREFIX=$(dirname $(dirname `pwd`))
mkdir build_cpu_serial && cd build_cpu_serial
cmake $AMBER_PREFIX/amber22_src -DCMAKE_INSTALL_PREFIX=$AMBER_PREFIX/amber22 -DCOMPILER=GNU -DMPI=FALSE -DOPENMP=FALSE -DCUDA=FALSE -DNCCL=FALSE -DBLA_VENDOR=OpenBLAS -DBUILD_GUI=FALSE -DBUILD_QUICK=FALSE -DINSTALL_TESTS=TRUE -DBUILD_PYTHON=FALSE -DDOWNLOAD_MINICONDA=FALSE -Wno-dev 2>&1 | tee cmake.log
make -j8 && make install

source $AMBER_PREFIX/amber22/amber.sh
echo "# Ambertools23 (amber22) environment settings" >> ~/.bashrc
echo "source $AMBERHOME/amber.sh" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/bin" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/lib" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/include" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/dat" >> ~/.bashrc
bash
```
- test
```
cd $AMBERHOME/test
make test.serial && make clean.test
```
### AmberTools23, Installation (Ubuntu 22.04 LTS (or WSL2), make, parallel)
- Not use GUI, GPU, and Quick
- [-- Found PythonLibs: /home/inukai/miniconda3/lib/libpython3.10.so (found suitable exact version "3.10.14")] (If miniconda3 is not installed, set "-DDOWNLOAD_MINICONDA=TRUE".)
```
tar xvf AmberTools23jlmrcc.tar.bz2
cd amber22_src
./update_amber --check-updates
./update_amber --update
cd build
AMBER_PREFIX=$(dirname $(dirname `pwd`))
mkdir build_cpu_parallel && cd build_cpu_parallel
cmake $AMBER_PREFIX/amber22_src -DCMAKE_INSTALL_PREFIX=$AMBER_PREFIX/amber22 -DCOMPILER=GNU -DMPI=TRUE -DOPENMP=TRUE -DCUDA=FALSE -DNCCL=FALSE -DBLA_VENDOR=OpenBLAS -DBUILD_GUI=FALSE -DBUILD_QUICK=FALSE -DINSTALL_TESTS=TRUE -DBUILD_PYTHON=TRUE -DDOWNLOAD_MINICONDA=FALSE 2>&1 | tee cmake.log
make -j8 && make install

source $AMBER_PREFIX/amber22/amber.sh
echo "# Ambertools23 (amber22) environment settings" >> ~/.bashrc
echo "source $AMBERHOME/amber.sh" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/bin" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/lib" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/include" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/dat" >> ~/.bashrc
bash
```
- test (parallel)
```
cd $AMBERHOME/test
export DO_PARALLEL="mpirun -np 8"
make test.parallel.4proc && make clean.test
unset DO_PARALLEL
```
- Note: sqm (=semi-empirical quantum chemistry): MNDO, MNDO/d (=MNDOD), AM1 (AM1, AM1-D* or AM1-DH+), AM1/d (=AM1D), PM3, PDDG/PM3, PDDG/MNDO, RM1, PM3CARB1, PM3-MAIS, PM6 (PM6, PM6-D, or PM6-DH+), DFTB2 (mio-1-1), DFTB3 (3ob-3-1)
- Note: quick (QUantum Interaction Computational Kernel) ab initio quantum chemistry): HF, UHF, DFT (LDA, GGA, Hybrid-GGA, e.g., e B3LYP/cc-pVDZ), UDFT, vdW (Grimme)
- Note: DFT (of quick) = B3LYP, PBE0, D3MBJ, etc [DFT = BLYP, B3LYP, BP86, B97, B](https://quick-docs.readthedocs.io/en/24.3.0/user-manual.html)
- Note: BASIS (of quick) = 6-31G**, cc-pVTZ, aug-cc-pVTZ, def2-TZVP, etc
- Note: sander (Simulated Annealing with NMR-Derived Energy Restraints)
- Note: Mechanical and electrostatic embedding: AMBER/QM, QM = ADF, Gaussian, Orca, Q-Chem, TeraChem, QUICK, MRCC, or Fireball
- Note: Mechanical embedding: ADF, GAMESS-US, NWChem
- Note: sebomd (Semi-Empirical Born-Oppenheimer Molecular Dynamics): NDDO (=AN1, PM3, RM1, etc)


## AmberTools22 [AT22]
```
wget https://ambermd.org/downloads/AmberTools22jlmrcc.tar.bz2
```
### AmberTools22, Installation (Ubuntu 22.04 LTS (or WSL2), cmake, 1 CPU (serial))
- Not use MPI, GPU, GUI, Quick, python, and miniconda
- This is a very simple executable file with few dependencies, suitable for basic functionality. It has also passed testing.
```
tar xvf AmberTools22jlmrcc.tar.bz2
cd amber22_src
./update_amber --check-updates
./update_amber --update
cd build
AMBER_PREFIX=$(dirname $(dirname `pwd`))
mkdir build_cpu_serial && cd build_cpu_serial
cmake $AMBER_PREFIX/amber22_src -DCMAKE_INSTALL_PREFIX=$AMBER_PREFIX/amber22 -DCOMPILER=GNU -DMPI=FALSE -DOPENMP=TRUE -DCUDA=FALSE -DNCCL=FALSE -DBLA_VENDOR=OpenBLAS -DBUILD_GUI=FALSE -DBUILD_QUICK=FALSE -DINSTALL_TESTS=TRUE -DBUILD_PYTHON=FALSE -DDOWNLOAD_MINICONDA=FALSE 2>&1 | tee cmake.log
make -j8 && make install

source $AMBER_PREFIX/amber22/amber.sh
echo "# Ambertools22 (amber22) environment settings" >> ~/.bashrc
echo "source $AMBERHOME/amber.sh" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/bin" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/lib" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/include" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/dat" >> ~/.bashrc
bash
```
- test
```
cd $AMBERHOME/test
make test.serial && make clean.test
```
### AmberTools22, Installation (Ubuntu 22.04 LTS (or WSL2), make, parallel)
- Not use GUI, GPU, and Quick
- [-- Found PythonLibs: /home/inukai/miniconda3/lib/libpython3.10.so (found suitable exact version "3.10.14")] (If miniconda3 is not installed, set "-DDOWNLOAD_MINICONDA=TRUE".)
```
tar xvf AmberTools22jlmrcc.tar.bz2
cd amber22_src
./update_amber --check-updates
./update_amber --update
cd build
AMBER_PREFIX=$(dirname $(dirname `pwd`))
mkdir build_cpu_parallel && cd build_cpu_parallel
cmake $AMBER_PREFIX/amber22_src -DCMAKE_INSTALL_PREFIX=$AMBER_PREFIX/amber22 -DCOMPILER=GNU -DMPI=TRUE -DOPENMP=TRUE -DCUDA=FALSE -DNCCL=FALSE -DBLA_VENDOR=OpenBLAS -DBUILD_GUI=FALSE -DBUILD_QUICK=FALSE -DINSTALL_TESTS=TRUE -DBUILD_PYTHON=TRUE -DDOWNLOAD_MINICONDA=FALSE 2>&1 | tee cmake.log
make -j8 && make install

source $AMBER_PREFIX/amber22/amber.sh
echo "# Ambertools22 (amber22) environment settings" >> ~/.bashrc
echo "source $AMBERHOME/amber.sh" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/bin" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/lib" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/include" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/dat" >> ~/.bashrc
bash
```
- test (parallel)
```
cd $AMBERHOME/test
export DO_PARALLEL="mpirun -np 8"
make test.parallel.4proc && make clean.test
```
- Note: sqm (=semi-empirical quantum chemistry): MNDO, MNDO/d (=MNDOD), AM1 (AM1, AM1-D* or AM1-DH+), AM1/d (=AM1D), PM3, PDDG/PM3, PDDG/MNDO, RM1, PM3CARB1, PM3-MAIS, PM6 (PM6, PM6-D, or PM6-DH+), DFTB2 (mio-1-1), DFTB3 (3ob-3-1)
- Note: quick (QUantum Interaction Computational Kernel) ab initio quantum chemistry): HF, UHF, DFT (LDA, GGA, Hybrid-GGA, e.g., e B3LYP/cc-pVDZ), UDFT, vdW (Grimme)
- Note: DFT (of quick) = B3LYP, PBE0, D3MBJ, etc [DFT = BLYP, B3LYP, BP86, B97, B](https://quick-docs.readthedocs.io/en/24.3.0/user-manual.html)
- Note: BASIS (of quick) = 6-31G**, cc-pVTZ, aug-cc-pVTZ, def2-TZVP, etc
- Note: sander (Simulated Annealing with NMR-Derived Energy Restraints)
- Note: Mechanical and electrostatic embedding: AMBER/QM, QM = ADF, Gaussian, Orca, Q-Chem, TeraChem, QUICK, MRCC, or Fireball
- Note: Mechanical embedding: ADF, GAMESS-US, NWChem
- Note: sebomd (Semi-Empirical Born-Oppenheimer Molecular Dynamics): NDDO (=AN1, PM3, RM1, etc)


## AmberTools21 (amber20) [AT21]
```
wget https://ambermd.org/downloads/AmberTools21jlmrcc.tar.bz2
```
### AmberTools21, Installation (Ubuntu 22.04 LTS (or WSL2), cmake, 1 CPU (serial), failed)
- Not use MPI, GPU, GUI, Quick, and miniconda
- This is a very simple executable file with few dependencies, suitable for basic functionality. It has also passed testing.
```
tar xvf AmberTools21jlmrcc.tar.bz2
cd amber20_src
./update_amber --check-updates
./update_amber --update
cd build
AMBER_PREFIX=$(dirname $(dirname `pwd`))
cmake $AMBER_PREFIX/amber20_src -DCMAKE_INSTALL_PREFIX=$AMBER_PREFIX/amber20 -DCOMPILER=GNU -DMPI=FALSE -DOPENMP=TRUE -DCUDA=FALSE -DNCCL=FALSE -DBLA_VENDOR=OpenBLAS -DBUILD_GUI=FALSE -DBUILD_QUICK=FALSE -DINSTALL_TESTS=TRUE -DBUILD_PYTHON=TRUE -DDOWNLOAD_MINICONDA=FALSE 2>&1 | tee cmake.log
make -j8 && make install

source $AMBER_PREFIX/amber20/amber.sh
echo "# Ambertools21 (amber20) environment settings" >> ~/.bashrc
echo "source $AMBERHOME/amber.sh" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/bin" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/lib" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/include" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/dat" >> ~/.bashrc
bash
```
- test (need long time (about 2 hours))
```
cd $AMBERHOME/test
make test.serial && make clean.test
```
### AmberTools21, Installation (Ubuntu 22.04 LTS (or WSL2), make, parallel, failed)
- Not use GUI, Quick, and miniconda
```
tar xvf AmberTools21jlmrcc.tar.bz2
cd amber20_src
./update_amber --check-updates
./update_amber --update
cd build
AMBER_PREFIX=$(dirname $(dirname `pwd`))
cmake $AMBER_PREFIX/amber20_src -DCMAKE_INSTALL_PREFIX=$AMBER_PREFIX/amber20 -DCOMPILER=GNU -DMPI=TRUE -DOPENMP=TRUE -DCUDA=FALSE -DNCCL=FALSE -DBLA_VENDOR=OpenBLAS -DBUILD_GUI=FALSE -DBUILD_QUICK=FALSE -DINSTALL_TESTS=TRUE -DBUILD_PYTHON=TRUE -DDOWNLOAD_MINICONDA=FALSE 2>&1 | tee cmake.log
make -j8 && make install

source $AMBER_PREFIX/amber20/amber.sh
echo "# Ambertools21 (amber20) environment settings" >> ~/.bashrc
echo "source $AMBERHOME/amber.sh" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/bin" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/lib" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/include" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/dat" >> ~/.bashrc
bash
```
- test (parallel)
```
cd $AMBERHOME/test
export DO_PARALLEL="mpirun -np 8"
make test.parallel.4proc && make clean.test
```
### AmberTools21 (amber20), Installation (cygwin, failed)
```
tar xvf AmberTools21jlmrcc.tar.bz2
cd amber20_src
export AMBERHOME=`pwd`
export LOCALFLAGS="-lgfortran -std=legacy"
#export CUSTOMBUILDFLAGS="-fallow-argument-mismatch"
echo "N" | ./configure -cygwin -noX11 --skip-python gnu
source $AMBERHOME/amber.sh
make -j8
make install

export PATH=$AMBERHOME/bin:$PATH
make test
```


## AmberTools20 (amber20)
```
wget https://ambermd.org/downloads/AmberTools20jlmrcc.tar.bz2
```
### AmberTools20, Installation (Ubuntu 22.04 LTS (or WSL2), cmake, 1 CPU (serial), failed)
- Not use MPI, GPU, GUI, Quick, python, and miniconda
- This is a very simple executable file with few dependencies, suitable for basic functionality. It has also passed testing.
```
tar xvf AmberTools20jlmrcc.tar.bz2
cd amber20_src
./update_amber --check-updates
./update_amber --update
cd build
AMBER_PREFIX=$(dirname $(dirname `pwd`))
cmake $AMBER_PREFIX/amber20_src -DCMAKE_INSTALL_PREFIX=$AMBER_PREFIX/amber20 -DCOMPILER=GNU -DMPI=FALSE -DOPENMP=TRUE -DCUDA=FALSE -DNCCL=FALSE -DBLA_VENDOR=OpenBLAS -DBUILD_GUI=FALSE -DBUILD_QUICK=FALSE -DINSTALL_TESTS=TRUE -DBUILD_PYTHON=FALSE -DDOWNLOAD_MINICONDA=FALSE 2>&1 | tee cmake.log
make -j8 && make install

source $AMBER_PREFIX/amber20/amber.sh
echo "# Ambertools20 (amber20) environment settings" >> ~/.bashrc
echo "source $AMBERHOME/amber.sh" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/bin" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/lib" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/include" >> ~/.bashrc
echo 'export PATH=$PATH:'"$AMBERHOME/dat" >> ~/.bashrc
bash
```
- amber20_src/AmberTools/src/arpack/dnaitr.f:658:35:
- Error: Rank mismatch between actual argument at (1) and actual argument at (2) (scalar and rank-1)
### AmberTools20 (amber20), Installation (WSL2, ubuntu 22.04, failed)
```
tar xvf AmberTools20jlmrcc.tar.bz2
cd amber20_src
export AMBERHOME=`pwd`
export LOCALFLAGS="-lgfortran -std=legacy"
export GOTO="/usr/lib/x86_64-linux-gnu/libopenblas.a"
echo "Y" | ./configure -noX11 --skip-python gnu
source $AMBERHOME/amber.sh
make -j8
make install

export PATH=$AMBERHOME/bin:$PATH
make test
```
### AmberTools20 (amber20), Installation (cygwin, update "Y", failed)
```
tar xvf AmberTools20jlmrcc.tar.bz2
cd amber20_src
export AMBERHOME=`pwd`
export LOCALFLAGS="-lgfortran -std=legacy"
#export CUSTOMBUILDFLAGS="-fallow-argument-mismatch"
echo "Y" | ./configure -cygwin -noX11 --skip-python gnu
source $AMBERHOME/amber.sh
make -j8
make install

export PATH=$AMBERHOME/bin:$PATH
make test
```
### AmberTools20 (amber20), Installation (cygwin, update "N", failed)
```
tar xvf AmberTools20jlmrcc.tar.bz2
cd amber20_src
export AMBERHOME=`pwd`
export LOCALFLAGS="-lgfortran -std=legacy"
#export CUSTOMBUILDFLAGS="-fallow-argument-mismatch"
echo "N" | ./configure -cygwin -noX11 --skip-python gnu
source $AMBERHOME/amber.sh
make -j8
make install

export PATH=$AMBERHOME/bin:$PATH
make test
```


## AmberTools19 (amber18)
```
wget https://ambermd.org/downloads/AmberTools19.tar.bz2
```
### AmberTools19 (amber18), Installation (cygwin, failed)
```
tar xvf AmberTools19.tar.bz2
cd amber18
export AMBERHOME=`pwd`
export LOCALFLAGS="-lgfortran -std=legacy"
#export CUSTOMBUILDFLAGS="-fallow-argument-mismatch"
echo "N" | ./configure -cygwin -noX11 --skip-python gnu
source $AMBERHOME/amber.sh
make -j8
make install

export PATH=$AMBERHOME/bin:$PATH
make test
```


## AmberTools18 (amber18)
```
wget https://ambermd.org/downloads/AmberTools18.tar.bz2
```
### AmberTools18 (amber18), Installation (cygwin, failed)
```
tar xvf AmberTools18.tar.bz2
cd amber18
export AMBERHOME=`pwd`
export LOCALFLAGS="-lgfortran -std=legacy"
#export CUSTOMBUILDFLAGS="-fallow-argument-mismatch"
echo "N" | ./configure -cygwin -noX11 --skip-python gnu
source $AMBERHOME/amber.sh
make -j8
make install

export PATH=$AMBERHOME/bin:$PATH
make test
```


## AmberTools17 (amber16)
```
wget https://ambermd.org/downloads/AmberTools17.tar.bz2
```
### AmberTools17 (amber16), Installation (cygwin, failed)
```
tar xvf AmberTools17.tar.bz2
cd amber16
export AMBERHOME=`pwd`
export LOCALFLAGS="-lgfortran -std=legacy"
echo "N" | ./configure -cygwin -noX11 --skip-python gnu
source $AMBERHOME/amber.sh
sed -i "s/FREEFORMAT_FLAG/#FREEFORMAT_FLAG/g" $AMBERHOME/AmberTools/src/config.h
make -j8
sed -i "s/FILE \*cifpin = NULL,/\/*FILE \*cifpin = NULL,*\/ FILE/g" $AMBERHOME/AmberTools/src/cifparse/lex.cif.c
make -j8
sed -i "s/_REAL_ :: twork/_REAL_ :: twork(1)/g" $AMBERHOME/AmberTools/src/sqm/qm2_scf.F90
sed -i "s/NINT(twork)/NINT(twork(1))/g" $AMBERHOME/AmberTools/src/sqm/qm2_scf.F90
make -j8
make install

export PATH=$AMBERHOME/bin:$PATH
make test
```
- Note (error): $AMBERHOME/AmberTools/src/lib/nxtsec.F
- Note (F77 -> F90): perl f2f.pl --tab 2 --base-indent 0 *.F *.F90
- Note: multiple definition of `cifpin': cifparse.c and lex.cif.c -> (lex.cif.c: Line 327, /*FILE *cifpin = NULL,*/ FILE *cifpout = NULL;)
- Note: Openblas is fully compatible with Netlib BLAS. (https://cygwin.com/pipermail/cygwin-announce/2024-January/011501.html)
- Note: usr/bin/cygblas-0.dll (dynamic library) (https://cygwin.com/cygwin/packages/summary/libopenblas.html)
- Note: Failed: export GOTO="-L/usr/bin -lcygblas-0"
- Note: /AmberTools/src/sqm/qm2_scf.F90:2271:48:(Line 2265 & 2271) Error: Rank mismatch between actual argument at (1) and actual argument at (2) (scalar and rank-1): Line 2252 => _REAL_ :: twork(1)  ! Declare twork as an array with at least one element
- Note: /AmberTools/src/sander/sebomd_module.F90:124:34: Error: Symbol ‘hamiltonian’ in namelist ‘sebomd’ at (1) must be declared before the namelist is declared. (In subroutine read_sebomd_namelist(), the namelist follows the type declaration.)
- Note: Plumed_init.inc:8:44: Error: Type mismatch between actual argument at (1) and actual argument at (2) (REAL(8)/INTEGER(4)). etc


## AmberTools13 (amber12)
```
wget https://ambermd.org/downloads/AmberTools13.tar.bz2
```
### AmberTools13 (amber12), Installation (cygwin, failed)
```
tar xvf AmberTools13.tar.bz2
cd amber12
export AMBERHOME=`pwd`
export LOCALFLAGS="-lgfortran -std=legacy"
export CUSTOMBUILDFLAGS="-fallow-argument-mismatch -w"
./configure -cygwin -noX11 gnu
make -j8
make install

export PATH=$AMBERHOME/bin:$PATH
make test
```


## AmberTools-1.5 (amber11)
```
wget https://ambermd.org/downloads/AmberTools-1.5.tar.bz2
```
### AmberTools-1.5 (amber11), Installation (cygwin, failed)
```
tar xvf AmberTools-1.5.tar.bz2
cd amber11/AmberTools/src
export AMBERHOME=$HOME/amber11
export LOCALFLAGS="-lgfortran -std=legacy"
export CUSTOMBUILDFLAGS="-fallow-argument-mismatch -w"
./configure -cygwin -noX11 -nopython -bit64 gnu
make -j8
make install

export PATH=$AMBERHOME/bin:$PATH
make test
```


## sci-AmberTools (sci-ambertools)
```
wget https://gitweb-cdn-origin.gentoo.org/proj/sci.git/snapshot/sci-ambertools.tar.bz2
```


## Pinda [AT18Pinda]
```
pip install pinda
pinda install ambertools 18
```


## cygwin
```
gcc-fortran 12.4.0-3
libopenblas 0.3.25-1
liblapack-devel 3.12.0-1
libarpack-devel 3.9.1-1
libfftw3-devel 3.3.10-1
make 4.4.1-2
cmake 3.28.3-1
patch 2.7.6-17
wget 1.24.5-1
gcc-g++ 12.4.0-3
python3-devel 3.9.16-1
tcsh 6.24.10-1
flex 2.6.4-2
bison 3.8.2-1
bc 1.07.1-1
xorg-server-devel 21.1.12-1
zlib-devel 1.3.1-1
libbz2-devel 1.0.8-1
libopenmpi-devel 4.1.6-1
openssh 9.8p1-1
libXext-devel 1.3.6-1
perl 5.36.3-1
perl-ExtUtils-MakeMaker 7.70-1
util-linux 2.39.3-2
bzip2 1.0.8-1
libzip2 0.11.2-2
libtool 2.4.7-1
gzip 1.13-1
libboost-devel 1.66.0-1
tar 1.35-2
libc++-devel 8.0.1-1
libgfortran5 1.2.4.0-3
libssl-devel 3.0.14-1
libnetcdf-devel 4.9.2-1
libnetcdf-fortran-devel 4.5.4-1
netcdf 4.9.2-1
```

## src/config.h


# References
- [AT24] https://github.com/conda-forge/ambertools-feedstock/issues/135
- [AT23] https://github.com/conda-forge/ambertools-feedstock/issues/97
- [AT22] http://archive.ambermd.org/202306/0138.html
- [AT21] http://archive.ambermd.org/202305/0106.html
- [AT20] https://github.com/GoHypernet/Galileo-AmberTools-Framework
- [AT19] https://github.com/GoHypernet/Galileo-AmberTools-Framework
- [AT18Pinda] https://pypi.org/project/pinda/
- [ATXX] https://gitweb-cdn-origin.gentoo.org/proj/sci.git/commit/profiles?h=ambertools
- [AT22I1] https://prof.uok.ac.ir/m.irani/index_files/Page312.htm
- [AT22I2] https://www.hull1.com/linux/2022/10/20/compile-amber22.html
- [AT20I1] https://www.programmersought.com/article/70808542288/
- [AT20I2] https://www.kitasato-u.ac.jp/sci/resea/buturi/seitai/matsui/memo.html (Japanese)
- [AT20I3] https://biomodeling.co.jp/2020/05/31/%e5%88%86%e5%ad%90%e3%82%b7%e3%83%9f%e3%83%a5%e3%83%ac%e3%83%bc%e3%82%b7%e3%83%a7%e3%83%b3%e7%92%b0%e5%a2%83%e8%a8%ad%e5%ae%9a/ (Japanese)
- [AT18I1] https://winmostar.com/en/gmx4wm_en_linux.html (./configure -noX11 --skip-python gnu)
- [AT17I1] https://www.computabio.com/compilation-tutorial-of-ambertools17-under-windows.html (export AMBERHOME='pwd'; ./configure -cygwin -noX11 gnu; source amber.sh; make install)
- [AT15I1] https://topic.alibabacloud.com/a/summary-of-accelerated-installation-of-amber11--ambertools15--cuda_1_16_32529945.html
- [AT13I1] http://jswails.wikidot.com/installing-amber12-and-ambertools-13
- [TU1] https://amber.tkanai-lab.org/ (Japanese)
- [ATT1] https://amber.tkanai-lab.org/TutorialB4/index.htm, https://www.tkanai-lab.org/wp/wp-content/uploads/2017/09/antechmber-jp.pdf (Japanese)
- [ATT2] https://oosakik.hatenablog.com/entry/2019/11/19/144858
- [ATT3] https://amberhub.chpc.utah.edu/tutorials/
- 
- [acpype] https://github.com/alanwilter/acpype
- [WC1] http://jswails.wikidot.com/windows-cygwin
- [CWM1] https://github.com/X-Ability/CygwinWM/
- [f2f.pl] https://github.com/mgaitan/f2f_online/blob/master/lib/f2f.pl
- [f2f.pl] https://github.com/senooken/example/tree/master/Fortran/f77tof90/f2f


## PC specs used for test
- OS: Microsoft Windows 11 Home 64 bit
- BIOS: 1.14.0
- CPU： 12th Gen Intel(R) Core(TM) i7-12700
- Base Board：0R6PCT (A01)
- Memory：32 GB
- GPU: NVIDIA GeForce RTX3070
- WSL2: VERSION="22.04.1 LTS (Jammy Jellyfish)"
- Python 3.10.12
