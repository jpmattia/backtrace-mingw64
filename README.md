# backtrace library for mingw64 and mingw32 

This library produces backtraces for program crashes.
- For 64 bit compilations under an x86_64 architecture, use backtrace64.c in the "64bit" directory. 
- For 32 bit compilations under an i386 architecture, use backtrace.c in the "32bit" directory. 

## Usage
For the 64 bit x86_64 architectures, compile the library like the following:

    gcc -O2 -shared -Wall -o backtrace64.dll -I/mingw64/include/binutils backtrace64.c -L/mingw64/lib/binutils -lbfd -liberty -limagehlp -lintl -lz

and at the beginning of your program, load the library:

    LoadLibraryA("backtrace64.dll");

Similarly for 32 bit i386 architectures, compile like so:

    gcc -O2 -shared -Wall -o backtrace.dll backtrace.c -lbfd -liberty -limagehlp 

and load the library at the beginning of your program

    LoadLibraryA("backtrace.dll");

## Example

An example program is included for both 64 and 32 bit architectures.  Go to the directory for the machine architecture and type "make".  An executable file will be produced, and when the test file is executed, a crash will occur invoking the backtrace libary.  Here is the output for test64.exe

    0x401574 : C:\workspaces\backtrace-mingw64\64bit\test64.exe : C:\workspaces\backtrace-mingw64\64bit/test64.c (7) : in function (foo)
    0x40158e : C:\workspaces\backtrace-mingw64\64bit\test64.exe : C:\workspaces\backtrace-mingw64\64bit/test64.c (14) : in function (bar)
    0x4015b7 : C:\workspaces\backtrace-mingw64\64bit\test64.exe : C:\workspaces\backtrace-mingw64\64bit/test64.c (22) : in function (main)
    0x4013a5 : C:\workspaces\backtrace-mingw64\64bit\test64.exe : E:/mingwbuild/mingw-w64-crt-git/src/mingw-w64/mingw-w64-crt/crt/crtexe.c (341) : in function (__tmainCRTStartup)
    0x40150b : C:\workspaces\backtrace-mingw64\64bit\test64.exe : E:/mingwbuild/mingw-w64-crt-git/src/mingw-w64/mingw-w64-crt/crt/crtexe.c (225) : in function (mainCRTStartup)
    0xfcfa7974 : C:\WINDOWS\System32\KERNEL32.DLL : BaseThreadInitThunk (0) : in function ([unknown func])
    0xff2da271 : C:\WINDOWS\SYSTEM32\ntdll.dll : RtlUserThreadStart (0) : in function ([unknown func])

## History

Clone of 32 bit version from this [backtrace-mingw](https://github.com/cloudwu/backtrace-mingw) repo, which was exported from code.google.com/p/backtrace-mingw

64 bit version made the necessary minor tweaks to get the library working under x86_64 architecture