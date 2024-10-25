############
Known Errors
############

Some known compilation errors
=============================

1. NetCDF error example::

    /usr/bin/ld: /project_shared/Libraries/netcdf-3.6.3_pgi_fortran_17.4-0//lib/libnetcdf.a(attr.o): relocation R_X86_64_32S against '.data' can not be used when making a shared object; recompile with -fPIC
    /project_shared/Libraries/netcdf-3.6.3_pgi_fortran_17.4-0//lib/libnetcdf.a: error adding symbols: Bad value

The NetCDF library is not compiled using shared library. You need to re-install NetCDF, compile it
with -fPIC, and check if libnetcdf.so file is generated.

2. Link library issue example::

    /usr/bin/ld: cannot find -lmpi_cxx

The mpi_cxx library is not available now in the current OpenMPI version. Use -lmpi instead in the
build_rule.mk file. Also, the following command can be used to check which library mlicxx depends
on::

    mpicxx -showme:libs

3. C++ library issue example::

    /usr/bin/ld: ESMCI_StringSubr.o: undefined reference to symbol '_ZNKSt5ctypeIcE13_M_widen_initEv@@GLIBCXX_3.4.11'

It seems that the location of library that ESMC_StringSubr.o depend on is not known to the system.
Check the library by using::

    strings /usr/lib64/libstdc++.so.6 | grep _ZNKSt5ctypeIcE13_M_widen_initEv_ZNKSt5ctypeIcE13_M_widen_initEv

And, add ``/usr/lib64/`` to ``LD_LIBRARY_PATH`` variable in ``~/.bashrc``

To see what a Library is linked to::

    [cpapadop@ring lib64]$ ldd libstdc++.so.6
    linux-vdso.so.1 =>  (0x00007ffd7bdf8000)
    libm.so.6 => /lib64/libm.so.6 (0x00007f569cdd9000)
    libc.so.6 => /lib64/libc.so.6 (0x00007f569ca17000)
    /lib64/ld-linux-x86-64.so.2 (0x00007f569d3f9000)
    libgcc_s.so.1 => /lib64/libgcc_s.so.1 (0x00007f569c801000)

4. NetCDF issue:: 

    ./esmf/lib/libO/Linux.pgi.64.openmpi.default/libesmf.so: undefined reference to 'netcdf_nf90_put_var_4d_eightbytereal\_'

The undefined reference issue is because the the library is not added when compiling the unit test
programs. The solution is to add “-netcdff” to the end of the compling command.

5. error: namespace "std" has no member "addressof"

This is a problem due to c++11 library.

