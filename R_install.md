I choose the source of R offered by Duke University.
```
wget -c https://archive.linux.duke.edu/cran/src/base/R-4/R-4.2.1.tar.gz
tar -zxvf R-4.2.1.tar.gz
cd R-4.2.1/
./configure
```

if you choose ```./configure --with-x=no```
write here first about the software relied.
gcc-gfortran, gcc-c++, readline-devel 

we should install a fortran compiler, because nearly no one use fortran now, I just choose the source of YUM.

```
yum install gcc-gfortran
```

and then

```
configure: error: in `/root/icl/R-4.2.1':
configure: error: C++ preprocessor "/lib/cpp" fails sanity check
```

It means that we need a complier for c++

```
yum install gcc-c++
```

and there is still a problem.

```
configure: error: --with-readline=yes (default) and headers/libs are not available
```

to solve it

```
yum install readline-devel 
```

the last question:

```
configure: error: --with-x=yes (default) and X11 headers/libs are not available
```

although we can install R by ```./configure --with-x=no```
(I didn't try it, but I'm sure it can complete the process of configure. However, in Linux (not mac), you can't use any GUI functionality in R.)

So, I tried to install libXt-devel.

```
yum -y install libXt-devel
```

and got:

```
checking whether bzip2 support suffices... configure: error: bzip2 library and headers are required
```

It seems that this environment need bzip2, however, I found bzip2 has been already exsited.

```
(base) [root@VM-0-7-centos R-4.2.1]# bzip2 -V
bzip2, a block-sorting file compressor.  Version 1.0.8, 13-Jul-2019.
   
   Copyright (C) 1996-2019 by Julian Seward.
   
   This program is free software; you can redistribute it and/or modify
   it under the terms set out in the LICENSE file, which is included
   in the bzip2 source distribution.
   
   This program is distributed in the hope that it will be useful,
   but WITHOUT ANY WARRANTY; without even the implied warranty of
   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
   LICENSE file for more details.
   
bzip2: I won't write compressed data to a terminal.
bzip2: For help, type: `bzip2 --help'.
```

The solution is to set the LDFLAGS and the CFLAGS for bzip2 and tell to R to configure with static libs:

```
export LDFLAG="-L/usr/local/bzip2/lib"
export CFLAGS="-I/usr/local/bzip2/include"
./configure --enable-R-static-lib
```

Anyway, be PATIENT if you choose to compile somethhing by source code.
