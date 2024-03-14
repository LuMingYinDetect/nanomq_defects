Affected Version:
nanomq 0.21.6 572fdf5f9d79cfa8ec7f2643ecea16cd358d0cc3

Vulnerability Description:
A memory leak defect was found on line 1434 of the file /nanomq/nanomq/bridge.c.

nanomq download address:
https://github.com/nanomq/nanomq.git

Vulnerability details:

1.The pointer named 'new' is defined and a block of dynamic memory is allocated using the 'nng_alloc' function at line 1431 in the file '/nanomq/nanomq/bridge.c'. When the 'if' statement at line 1433 evaluates to true, the program returns at line 1434 without utilizing or freeing the memory pointed to by 'new', thus constituting a memory leak defect.

![image](https://github.com/LuMingYinDetect/nanomq_defects/blob/main/nanomq_6.png)
