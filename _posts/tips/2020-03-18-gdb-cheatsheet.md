---
title: "GDB cheatsheet"
date: 2020-03-18
categories:
 - programming tools and environments 

tags:
 - c
 - c++
 - gdb

---

Something that I need for GDB

### gdb

{% highlight c %}
#include <stdio.h>
// gdbmain.c

int main(void)
{
	int times = 10;
	for(int i = 0; i < times; i++)
	{
		printf("line #%d\n", i+1);
	} 
	
}

{% endhighlight %}


Do compile using gdb compile first
```
gcc -g -o main main.c
```

Execute gdb
```
gdb ./main
```

prompt like:
```
GNU gdb (Ubuntu 8.2-0ubuntu1~18.04) 8.2
Copyright (C) 2018 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from ./gdbmain...done.
(gdb)
```

"l" to see codes
```
(gdb) l
1	#include <stdio.h>
2	
3	int main(void)
4	{
5	  int times = 10;
6	  for(int i = 0; i < times; i++)
7	  {
8	    printf("line #%d", i+1);
9	  }
10	}

```

"info b" to see breakpoints
```
(gdb) info b
Num     Type           Disp Enb Address    What
1       breakpoint     keep n   0x80104b80 in syscall at syscall.c:144
	breakpoint already hit 158 times
2       breakpoint     keep y   0x80105a30 in sys_getnice at sysproc.c:95
3       breakpoint     keep y   0x801046b0 x86.h:126
```

"b (number)" to set breakpoint
```
(gdb) b 5
Breakpoint 1 at 0x652: file gdbmain.c, line 5.
```

"b (func)" to set breakpoint at current file's function
```
(gdb) b main
Breakpoint 1 at 0x80102fc0: file main.c, line 19.
```

"disable br (num)" to disable breakpoints
```
(gdb) disable br 1
(gdb) disable br 3
(gdb) info b
Num     Type           Disp Enb Address    What
1       breakpoint     keep n   0x80104b80 in syscall at syscall.c:144
	breakpoint already hit 158 times
2       breakpoint     keep y   0x80105a30 in sys_getnice at sysproc.c:95
3       breakpoint     keep n   0x801046b0 x86.h:126
```

"r" to run program
```
(gdb) r
Starting program: /home/dongmin/Desktop/Projects/current/dongminkim0220.github.io/_posts/2020/03/18/gdbmain 

Breakpoint 1, main () at gdbmain.c:5
5	  int times = 10;
```

"n" or "s" to proceed
"n" is for doing next line
"s" is to step into function, if any
```
(gdb) n
6	  for(int i = 0; i < times; i++)
```

"p" to see the value of a variable
```
(gdb) p times
$1 = 10
(gdb) p i
$2 = 0
```

"target remote :xxxxx" to access another gdb executing console
```
$ gdb
(gdb) target remote :26000
Remote debugging using :26000
warning: No executable has been specified and target does not support
determining executable automatically.  Try using the "file" command.
0x0000fff0 in ?? ()
```

"file kernel" to load
```
(gdb) file kernel
A program is being debugged already.
Are you sure you want to change the file? (y or n) y
Reading symbols from kernel...done.
```

"r < (input file)" for redirection
```
(gdb) r < input.txt
```


"quit" to turn off
```
(gdb) quit
```
