Affected Version:
nanomq 0.21.6 572fdf5f9d79cfa8ec7f2643ecea16cd358d0cc3

Vulnerability Description:
A memory leak defect was found on line 994 of the file /nanomq/nng/src/mqtt/protocol/exchange/exchange_server.c.

nanomq download address:
https://github.com/nanomq/nanomq.git

Vulnerability details:

1.On line 921 of the /nanomq/nng/src/mqtt/protocol/exchange/exchange_server.c file, a pointer named obj is defined and a dynamic memory area is allocated. When the if condition on line 992 is true, the program returns on line 994. During this process, the dynamic memory area pointed to by variable obj is neither used nor released, thus constituting a memory leak vulnerability, as shown in the following figure

![image](https://github.com/LuMingYinDetect/nanomq_defects/blob/main/nanomq_7.png)
