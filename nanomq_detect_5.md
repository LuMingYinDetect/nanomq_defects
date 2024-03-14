Affected Version:
nanomq 0.21.6 572fdf5f9d79cfa8ec7f2643ecea16cd358d0cc3

Vulnerability Description:
A memory leak defect was found on line 874 of the file /nanomq/nng/src/supplemental/nanolib/ringbuffer/ringbuffer.c.

nanomq download address:
https://github.com/nanomq/nanomq.git

Vulnerability details:

1.In the /nanomq/nng/src/supplemental/nanolib/ringbuffer/ringbuffer.c file, on line 863, a pointer named list is defined. This pointer is then passed as a parameter to the ringBuffer_get_and_clean_msgs function on line 864, as shown in the following figure:

![image](https://github.com/LuMingYinDetect/nanomq_defects/blob/main/nanomq_8.png)

2.In the ringBuffer_get_and_clean_msg function, the variable list is passed as an argument to ringBuffer_get_msg on line 94, as shown in the following figure

![image](https://github.com/LuMingYinDetect/nanomq_defects/blob/main/nanomq_9.png)

3.On line 18 of the ringBuffer_get_ msg function, a pointer named newList is defined. On line 24, this pointer is allocated a dynamic memory region through the function nng_alloc. On line 39, the memory region pointed to by the pointer newList is assigned to list, as shown in the following figure

![image](https://github.com/LuMingYinDetect/nanomq_defects/blob/main/nanomq_10.png)

4.When the ringBuffer_get_and_clean_msgs function completes its execution, a dynamic memory region is allocated to the variable list. If the if condition on line 872 of the program is true, the program returns on line 874. During this process, the memory region pointed to by the variable list is neither used nor freed, thus constituting a memory leak defect, as shown in the following figure.

![image](https://github.com/LuMingYinDetect/nanomq_defects/blob/main/nanomq_11.png)
