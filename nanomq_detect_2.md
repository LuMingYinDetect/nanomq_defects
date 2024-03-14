Affected Version:
nanomq 0.21.6 572fdf5f9d79cfa8ec7f2643ecea16cd358d0cc3

Vulnerability Description:
A memory leak defect was found on line 509 of the file bridge.c in nanomq/nanomq.

nanomq download address:
https://github.com/nanomq/nanomq.git

Vulnerability details:

1.A pointer named 'new' is defined on line 498 of the file bridge.c in nanomq/nanomq. It allocates a block of dynamic memory using the nng_alloc function. When the if statement on line 507 evaluates to true, the program returns on line 509 without freeing the memory pointed to by the 'new' pointer, resulting in a memory leak defect, as illustrated in the following figure:

![image](https://github.com/LuMingYinDetect/nanomq_defects/blob/main/nanomq_5.png)
