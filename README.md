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


## AmberTools21 [AT21]
```
wget https://ambermd.org/downloads/AmberTools21jlmrcc.tar.bz2
```


## AmberTools20
```
wget https://ambermd.org/downloads/AmberTools20jlmrcc.tar.bz2
```


## AmberTools19
```
wget https://ambermd.org/downloads/AmberTools19.tar.bz2
```


## AmberTools18
```
wget https://ambermd.org/downloads/AmberTools18.tar.bz2
```
### AmberTools18 (amber18), Installation (cygwin, failed)
```
tar xvf AmberTools18.tar.bz2
cd amber18
export AMBERHOME=`pwd`
export LOCALFLAGS="-lgfortran -std=legacy"
./configure -cygwin -noX11 --skip-python gnu
N
source $AMBERHOME/amber.sh
make install
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
./configure -cygwin -noX11 --skip-python gnu
N
source $AMBERHOME/amber.sh
make install
```


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
./configure -cygwin -noX11 gnu
make install
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
./configure -nopython -nobintraj -nosleap -nocpptraj -nomtkpp -bit64 -cygwin -noX11 gnu
make install
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
- [AT13I1] http://jswails.wikidot.com/installing-amber12-and-ambertools-13
- [AT18I1] https://winmostar.com/en/gmx4wm_en_linux.html (./configure -noX11 --skip-python gnu)
- [AT17I1] https://www.computabio.com/compilation-tutorial-of-ambertools17-under-windows.html (export AMBERHOME='pwd'; ./configure-cygwin-noX11 gnu; source amber.sh; make install)
- [AT15I1] https://topic.alibabacloud.com/a/summary-of-accelerated-installation-of-amber11--ambertools15--cuda_1_16_32529945.html
- [TU1] https://amber.tkanai-lab.org/ (Japanese)
- [ATT1] https://amber.tkanai-lab.org/TutorialB4/index.htm, https://www.tkanai-lab.org/wp/wp-content/uploads/2017/09/antechmber-jp.pdf (Japanese)
- [ATT2] https://oosakik.hatenablog.com/entry/2019/11/19/144858
- [acpype] https://github.com/alanwilter/acpype
