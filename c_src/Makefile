FFTWFLAGS = -L${FFTW_PATH}/lib -I${FFTW_PATH}/include -lfftw3f

libSigPyProc32.so: libSigPyProc32.o
	gcc -Wl,--no-as-needed -shared -lgomp  -o libSigPyProc32.so libSigPyProc32.o
 
libSigPyProc32.o: libSigPyProc32.c Makefile
	gcc -O3 -lm -fopenmp -DHAVE_OPENMP -fPIC -c $< -o $@
 
libSigPyProc8.so: libSigPyProc8.o MersenneTwister.o
	gcc -Wl,--no-as-needed -shared -lgomp -o libSigPyProc8.so libSigPyProc8.o MersenneTwister.o
 
libSigPyProc8.o: libSigPyProc8.c Makefile
	gcc -O3 -lm -fopenmp -DHAVE_OPENMP -fPIC -c $< -o $@ 
 
libSigPyProc.so: libSigPyProc.o 
	gcc -Wl,--no-as-needed -shared -o libSigPyProc.so libSigPyProc.o

libSigPyProc.o: libSigPyProc.c Makefile
	gcc -O3 -lm -fPIC -c $< -o $@

libSigPyProcTim.so: libSigPyProcTim.o
	gcc -Wl,--no-as-needed -shared $(FFTWFLAGS) -lgomp  -o libSigPyProcTim.so libSigPyProcTim.o

libSigPyProcTim.o: libSigPyProcTim.c Makefile
	gcc -O3 $(FFTWFLAGS) -lm -fopenmp -DHAVE_OPENMP -fPIC -c $< -o $@

libSigPyProcSpec.so: libSigPyProcSpec.o
	gcc -Wl,--no-as-needed -shared $(FFTWFLAGS) -lgomp  -o libSigPyProcSpec.so libSigPyProcSpec.o

libSigPyProcSpec.o: libSigPyProcSpec.c Makefile
	gcc -O3 $(FFTWFLAGS) -lm -fopenmp -DHAVE_OPENMP -fPIC -c $< -o $@

MersenneTwister.o: MersenneTwister.c Makefile
	gcc -O3 -lm -fPIC -c $< -o $@

all:
	make libSigPyProc32.so
	make libSigPyProc8.so
	make libSigPyProc.so
	make libSigPyProcTim.so
	make libSigPyProcSpec.so

install:
	mv *.so ../lib/
	rm -rf *.o

.PHONY: clean
clean:
	rm -f *.o *.so*
