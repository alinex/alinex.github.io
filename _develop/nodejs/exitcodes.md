---
title: Exit Codes
layout: develop
---

Status Code for Success
------------------------------------------------------

In general a zero exit status indicates that a command succeeded, a non-zero exit status indicates failure.


C/C++ Linux Codes
------------------------------------------------------
The exit codes in C/C++ which are in the kernel can be also found in:

    /usr/include/asm-generic/errno-base.h
    /usr/include/asm-generic/errno.h

    cat /usr/include/asm-generic/errno-base.h /usr/include/asm-generic/errno.h | grep define | sed -r 's/.*\t([0-9]+)\t\/\* (.*) \*\//| \1 | \2 |/g'

| Code | Description                             |
| ----:| --------------------------------------- |
|    0 | OK - no error            |
| 1	| Operation not permitted |
| 2	| No such file or directory |
| 3	| No such process |
| 4	| Interrupted system call |
| 5 | I/O error |
| 6	| No such device or address |
| 7	| Argument list too long |
| 8	| Exec format error |
| 9	| Bad file number |
| 10 | No child processes |
| 11 | Try again |
| 12 | Out of memory |
| 13 | Permission denied |
| 14 | Bad address |
| 15 | Block device required |
| 16 | Device or resource busy |
| 17 | File exists |
| 18 | Cross-device link |
| 19 | No such device |
| 20 | Not a directory |
| 21 | Is a directory |
| 22 | Invalid argument |
| 23 | File table overflow |
| 24 | Too many open files |
| 25 | Not a typewriter |
| 26 | Text file busy |
| 27 | File too large |
| 28 | No space left on device |
| 29 | Illegal seek |
| 30 | Read-only file system |
| 31 | Too many links |
| 32 | Broken pipe |
| 33 | Math argument out of domain of func |
| 34 | Math result not representable |
| 35 | Resource deadlock would occur |
| 36 | File name too long |
| 37 | No record locks available |
| 38 | Function not implemented |
| 39 | Directory not empty |
| 40 | Too many symbolic links encountered |
| 41 | Operation would block |
| 42 | No message of desired type |
| 43 | Identifier removed |
| 44 | Channel number out of range |
| 45 | Level 2 not synchronized |
| 46 | Level 3 halted |
| 47 | Level 3 reset |
| 48 | Link number out of range |
| 49 | Protocol driver not attached |
| 50 | No CSI structure available |
| 51 | Level 2 halted |
| 52 | Invalid exchange |
| 53 | Invalid request descriptor |
| 54 | Exchange full |
| 55 | No anode |
| 56 | Invalid request code |
| 57 | Invalid slot |
| 58 | EDEADLOCK EDEADLK |
| 59 | Bad font file format |
| 60 | Device not a stream |
| 61 | No data available |
| 62 | Timer expired |
| 63 | Out of streams resources |
| 64 | Machine is not on the network |
| 65 | Package not installed |
| 66 | Object is remote |
| 67 | Link has been severed |
| 68 | Advertise error |
| 69 | Srmount error |
| 70 | Communication error on send |
| 71 | Protocol error |
| 72 | Multihop attempted |
| 73 | RFS specific error |
| 74 | Not a data message |
| 75 | Value too large for defined data type |
| 76 | Name not unique on network |
| 77 | File descriptor in bad state |
| 78 | Remote address changed |
| 79 | Can not access a needed shared library |
| 80 | Accessing a corrupted shared library |
| 81 | .lib section in a.out corrupted |
| 82 | Attempting to link in too many shared libraries |
| 83 | Cannot exec a shared library directly |
| 84 | Illegal byte sequence |
| 85 | Interrupted system call should be restarted |
| 86 | Streams pipe error |
| 87 | Too many users |
| 88 | Socket operation on non-socket |
| 89 | Destination address required |
| 90 | Message too long |
| 91 | Protocol wrong type for socket |
| 92 | Protocol not available |
| 93 | Protocol not supported |
| 94 | Socket type not supported |
| 95 | Operation not supported on transport endpoint |
| 96 | Protocol family not supported |
| 97 | Address family not supported by protocol |
| 98 | Address already in use |
| 99 | Cannot assign requested address |
| 100 | Network is down |
| 101 | Network is unreachable |
| 102 | Network dropped connection because of reset |
| 103 | Software caused connection abort |
| 104 | Connection reset by peer |
| 105 | No buffer space available |
| 106 | Transport endpoint is already connected |
| 107 | Transport endpoint is not connected |
| 108 | Cannot send after transport endpoint shutdown |
| 109 | Too many references: cannot splice |
| 110 | Connection timed out |
| 111 | Connection refused |
| 112 | Host is down |
| 113 | No route to host |
| 114 | Operation already in progress |
| 115 | Operation now in progress |
| 116 | Stale file handle |
| 117 | Structure needs cleaning |
| 118 | Not a XENIX named type file |
| 119 | No XENIX semaphores available |
| 120 | Is a named type file |
| 121 | Remote I/O error |
| 122 | Quota exceeded |
| 123 | No medium found |
| 124 | Wrong medium type |
| 125 | Operation Canceled |
| 126 | Required key not available |
| 127 | Key has expired |
| 128 | Key has been revoked |
| 129 | Key was rejected by service |
| 130 | Owner died |
| 131 | State not recoverable |
| 132 | Operation not possible due to RF-kill |
| 133 | Memory page has hardware error |
| ---- | --------------------------------------- |


Unix Bash
------------------------------------------------------

The exit codes are arranged alongside the UNIX default:


| ---- | --------------------------------------- |
| Code | Description                             |
| ----:| --------------------------------------- |
|    0 | OK - no error                           |
|    1 | General error which should not occur    |
|  124 | command times out                       |
|  125 | if a command itself fails               |
|  126 | Command invoked cannot execute          |
|  127 | "command not found"                     |
|  128 | Invalid argument to exit                |
|  129 | SIGHUP (Signal 1)                       |
|  130 | SIGINT like through Ctrl + C (Signal 2) |
|  131 | SIGQUIT (Signal 3)                      |
|  134 | SIGABRT or SIGIOT (Signal 6)            |
|  143 | SIGTERM (Signal 15)                     |
|  255 | Exit status out of range                |
| ---- | --------------------------------------- |

The codes from 2 - 125 are command specific, here you should look into the
manpage for an explanation. But some have a most common use.


Alinex Generals
------------------------------------------------------

The alinex tools are based on the bash exit codes. In addition to the above
some alinex common codes are set in the range 16-120 like:

| ---- | --------------------------------------- |
| Code | Description                             |
| ----:| --------------------------------------- |
|    2 | Command parameter problem               |
|    3 | File system access problem              |
|    4 | Network problems                        |
|    5 | Service or system access problem        |
|    6 | No such service or address              |
| ---- | --------------------------------------- |
