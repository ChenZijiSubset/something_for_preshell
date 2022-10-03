my environmrnt:

```
(base) [root@VM-0-7-centos nano-6.4]# uname -r
4.18.0-348.7.1.el8_5.x86_64
(base) [root@VM-0-7-centos nano-6.4]# uname
Linux
```

First, I have to remove the orginal nano

```
(base) [root@VM-0-7-centos nano-6.4]# nano --version
 GNU nano, version 2.9.8
 (C) 1999-2011, 2013-2018 Free Software Foundation, Inc.
 (C) 2014-2018 the contributors to nano
 Email: nano@nano-editor.org	Web: https://nano-editor.org/
 Compiled options: --enable-utf8
```

```
(base) [root@VM-0-7-centos nano-6.4]# yum remove nano
Dependencies resolved.
===================================================================================================
 Package            Architecture         Version                     Repository               Size
===================================================================================================
Removing:
 nano               x86_64               2.9.8-1.el8                 @anaconda               2.2 M

Transaction Summary
===================================================================================================
Remove  1 Package

Freed space: 2.2 M
Is this ok [y/N]: y
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                           1/1 
  Running scriptlet: nano-2.9.8-1.el8.x86_64                                                   1/1 
  Erasing          : nano-2.9.8-1.el8.x86_64                                                   1/1 
  Running scriptlet: nano-2.9.8-1.el8.x86_64                                                   1/1 
  Verifying        : nano-2.9.8-1.el8.x86_64                                                   1/1 

Removed:
  nano-2.9.8-1.el8.x86_64                                                                          

Complete!
```

```
wget - c https://www.nano-editor.org/dist/v6/nano-6.4.tar.gz
tar -zxvf nano-6.4.tar.gz
cd nano-6.4/
./configure
```

While there is a small question:

```
checking for initscr in -lcurses... no
configure: error: 
  *** No curses lib was found.  Please install the curses header files
  *** from libncurses-dev (Debian), ncurses-devel (Fedora), or similar.
  *** (Or install ncurses from https://ftp.gnu.org/gnu/ncurses/.)
```

so remember to install ncurses-devel before configure.

```
yum install ncurses-devel
```

and then

```
./configure
make
make install
```

and there is still a problem:

```
(base) [root@VM-0-7-centos nano-6.4]# nano --version
-bash: /usr/bin/nano: No such file or directory
```

We need create a Symbolic Link.

```
ln -s /usr/local/bin/nano /usr/bin/nano
```

and success!

```
(base) [root@VM-0-7-centos nano-6.4]# nano -V
 GNU nano, version 6.4
 (C) 2022 the Free Software Foundation and various contributors
 Compiled options: --disable-libmagic --enable-utf8
```






