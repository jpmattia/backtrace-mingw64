.PHONY: all clean

all : backtrace64.dll test64.exe

backtrace64.dll : backtrace64.c
	gcc -O2 -shared -Wall -o backtrace64.dll -I/mingw64/include/binutils backtrace64.c -L/mingw64/lib/binutils -lbfd -liberty -limagehlp -lintl -lz

test.exe : test.c
	gcc -g -Wall -o $@ $^

test64.exe : test64.c
	gcc -g -Wall -o $@ $^

clean :
	-del -f backtrace64.dll test64.exe

