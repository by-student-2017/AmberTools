# AmberTools
- AmberTools is a free, useful standalone package and a prerequisite for installing Amber itself. The AmberTools suite is free of charge, and its components are mostly released under the GNU General Public License (GPL). A few components are included that are in the public domain or which have other, open-source, licenses. The libsander and libpbsa libraries use the LGPL license. (see https://ambermd.org/GetAmber.php#ambertools)


## Note
- I couldn't upload it because I didn't have enough storage space. Please download it directly from the link below.


## AmberTools24 [AT24]
```
wget https://ambermd.org/downloads/AmberTools24_rc5.tar.bz2
```


## AmberTools23 [AT23]
```
wget https://ambermd.org/downloads/AmberTools23_rc6.tar.bz2
```


## AmberTools22 [AT22]
```
wget https://ambermd.org/downloads/AmberTools22jlmrcc.tar.bz2
```
### AmberTools22 (amber22), Installation (WSL2, ubuntu 22.04, cmake)
```
tar xvf AmberTools22jlmrcc.tar.bz2
cd amber22_src
./update_amber --check-updates
./update_amber --update
cd build
AMBERHOME=$(dirname $(dirname `pwd`))
cmake $AMBERHOME/amber22_src -DCMAKE_INSTALL_PREFIX=$AMBERHOME/amber22 -DCOMPILER=GNU -DMPI=FALSE -DOPENMP=FALSE -DBUILD_GUI=FALSE -DNCCL=FALSE -DCUDA=FALSE -DBUILD_QUICK=FALSE -DINSTALL_TESTS=TRUE -DTEST_PARALLEL=FALSE -DDOWNLOAD_MINICONDA=FALSE -DBUILD_PYTHON=FALSE -DBLA_VENDOR=OpenBLAS 2>&1 | tee cmake.log
make -j8 && make install

AMBERHOME=$(dirname $(dirname `pwd`))
source $AMBERHOME/amber22/amber.sh
export PATH=$AMBERHOME/amber22/bin:$PATH
bash

#make test.serial && make clean.test
```
- Memo: cmake $AMBERHOME/amber22_src -DCMAKE_INSTALL_PREFIX=$AMBERHOME/amber22 -DCOMPILER=GNU -DMPI=FALSE -DOPENMP=FALSE -DBUILD_GUI=FALSE -DCUDA=FALSE -DOPENACC=FALSE -DOPENMM=FALSE -DBUILD_QUICK=FALSE -DINSTALL_TESTS=TRUE -DTEST_PARALLEL=FALSE -DDOWNLOAD_MINICONDA=FALSE -DBUILD_PYTHON=FALSE -DOPENCL=FALSE -DROCM=FALSE -DNOX11=FALSE -DHDF5=FALSE -DCP2K=FALSE -DPLUMED=FALSE -DQUIP=FALSE -DLAPACK=FALSE -DSCALAPACK=FALSE -DBLA_VENDOR=OpenBLAS -DOpenBLAS_DIR="/usr/lib/x86_64-linux-gnu/libopenblas.a" -DFFTW=FALSE -DFFTW3=FALSE -DFFTW3_ROOT="/usr/lib/x86_64-linux-gnu/libfftw3.a" -DNETCDF=TRUE -DNETCDF_ROOT="/usr/lib/x86_64-linux-gnu/libnetcdff.a" -DFORCE_INTERNAL_LIBS="arpack" -DCHECK_UPDATES=TRUE -DCUDA_TOOLKIT_ROOT_DIR=${CUDA_HOME}  -Wno-dev 2>&1 | tee cmake.log

## AmberTools21 [AT21]
```
wget https://ambermd.org/downloads/AmberTools21jlmrcc.tar.bz2
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
### AmberTools20 (amber20), Installation (WSL2, ubuntu 22.04, cmake failed)
```
tar xvf AmberTools20jlmrcc.tar.bz2
cd amber20_src
./update_amber --check-updates
./update_amber --update
cd build
AMBERHOME=$(dirname $(dirname `pwd`))
cmake $AMBERHOME/amber20_src -DCMAKE_INSTALL_PREFIX=$AMBERHOME/amber20 -DCOMPILER=GNU -DMPI=FALSE -DOPENMP=FALSE -DBUILD_GUI=FALSE -DCUDA=FALSE -DINSTALL_TESTS=TRUE -DTEST_PARALLEL=FALSE -DDOWNLOAD_MINICONDA=FALSE -DBUILD_PYTHON=FALSE -Wno-dev
source $AMBERHOME/amber20_src/amber.sh
make -j8
make install

#export PATH=$AMBERHOME/amber20/bin:$PATH
#make test
```
- Memo: cmake $AMBERHOME/amber20_src -DCMAKE_INSTALL_PREFIX=$AMBERHOME/amber22 -DCOMPILER=GNU -DMPI=FALSE -DOPENMP=FALSE -DBUILD_GUI=FALSE -DCUDA=FALSE -DOPENACC=FALSE -DOPENMM=FALSE -DBUILD_QUICK=FALSE -DINSTALL_TESTS=TRUE -DTEST_PARALLEL=FALSE -DDOWNLOAD_MINICONDA=FALSE -DBUILD_PYTHON=FALSE -DOPENCL=FALSE -DROCM=FALSE -DNOX11=FALSE -DHDF5=FALSE -DCP2K=FALSE -DPLUMED=FALSE -DQUIP=FALSE -DLAPACK=FALSE -DSCALAPACK=FALSE -DBLA_VENDOR=OpenBLAS -DOpenBLAS_DIR="/usr/lib/x86_64-linux-gnu/libopenblas.a" -DFFTW=FALSE -DFFTW3=FALSE -DFFTW3_ROOT="/usr/lib/x86_64-linux-gnu/libfftw3.a" -DNETCDF=TRUE -DNETCDF_ROOT="/usr/lib/x86_64-linux-gnu/libnetcdff.a" -Wno-dev
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

## Ubuntu 22.04 LTS
```
sudo apt update
sudo apt -y install tcsh make gcc gfortran flex bison patch bc wget xorg-dev libz-dev libbz2-dev libopenblas-dev libnetcdf-dev libnetcdff-dev
sudo apt -y install openmpi-bin libopenmpi-dev openssh-client python3-mpi4py　
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
- [acpype] https://github.com/alanwilter/acpype
- [WC1] http://jswails.wikidot.com/windows-cygwin
- [CWM1] https://github.com/X-Ability/CygwinWM/
- [f2f.pl] https://github.com/mgaitan/f2f_online/blob/master/lib/f2f.pl
- [f2f.pl] https://github.com/senooken/example/tree/master/Fortran/f77tof90/f2f
