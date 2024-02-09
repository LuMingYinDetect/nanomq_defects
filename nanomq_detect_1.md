Affected Version:
nanomq 0.21.2 74f59dee6af558ddeaac2b6882b297645b6913d0

Vulnerability Description:
This vulnerability is a UAF (Use-After-Free) vulnerability discovered in the file /nanomq/nng/src/core/socket.c. It could be maliciously exploited, leading to a denial-of-service attack.

nanomq download address:
https://github.com/nanomq/nanomq.git

Vulnerability details:

1.In the file socket.c at line 630 of /nanomq/nng/src/core/socket.c, a pointer variable named "s" is defined. At line 646, the variable "s" is passed into the function sock_destroy, as shown in the following figure:

![image](https://github.com/LuMingYinDetect/nanomq_defects/blob/main/nanomq_1.png)

2.The sock_destroy function is located in the /nanomq/nng/src/core/socket.c file. In this function, the variable "s" is passed into the nni_free function at line 542, as shown in the following figure:

![image](https://github.com/LuMingYinDetect/nanomq_defects/blob/main/nanomq_2.png)

3.The nni_free function is located in the /nanomq/nng/src/platform/posix/posix_alloc.c file. At line 33 of the nni_free function, the memory area pointed to by this pointer is released using the free function, as shown below:

![image](https://github.com/LuMingYinDetect/nanomq_defects/blob/main/nanomq_3.png)

4.After the memory area pointed to by the pointer s is released, the program accesses s->s_id at line 655, resulting in a Use-After-Free (UAF) vulnerability, as shown below:

![image](https://github.com/LuMingYinDetect/nanomq_defects/blob/main/nanomq_4.png)
