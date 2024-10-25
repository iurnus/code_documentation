############################
Install the model components
############################

SKRIPS v2.01 is available from Github::

  https://github.com/iurnus/scripps_kaust_model/releases/tag/v2.01

I am using my Linux machine kala as an example. To install the SKRIPS model (for
example, in ``$HOME/scripps_kaust_model/``), we have to download the SKRIPS
model and set up the bashrc file.

Install step 1.1: Download SKRIPS version from Github::

  # I am using my work folder as an example
  cd
  wget https://github.com/iurnus/scripps_kaust_model/archive/v2.01.zip
  unzip v2.01.zip
  mv scripps_kaust_model-2.01 scripps_kaust_model
  cd scripps_kaust_model
  ls -l

You will see the following items::
  
  drwxr-xr-x 12 rus043 mazloff-lab   13 Aug 29 15:01 coupler
  drwxr-xr-x  4 rus043 mazloff-lab    4 Aug 29 15:01 esmf_test
  drwxr-xr-x  2 rus043 mazloff-lab    5 Aug 29 15:01 license_statements
  -rw-r--r--  1 rus043 mazloff-lab 4239 Aug 29 15:01 README.md
  drwxr-xr-x  6 rus043 mazloff-lab    6 Aug 29 15:01 scripts

Install step 1.2: Create a bashrc file for SKRIPS model::

  cp ./scripts/bashrc/bashrc_kala ~/.bashrc_skrips
  
Here I am copying the bashrc file that I used for EXPANSE. There are also bashrc
files for other machines that can be used in *scripts* folder.

Then, add the following line to ``~/.bashrc`` file (you can use ``vim``, ``emacs``,
or ``gedit``)::
  
  alias load_skrips="source ~/.bashrc_skrips" 
  
Save your changes in ``~/.bashrc``, run the following command in your terminal::

  source ~/.bashrc
  load_skrips

Now activate the bashrc setups in the command line. Because the changes are
added to ``~/.bashrc``, when you open a new terminal window, you only need to
type ``load_skrips`` to activate all the changes.

.. note::
  Make sure that you activate the bachrc setups every time when you want to
  run SKRIPS model, otherwise the Linux system will not remember what you did.

When the bashrc file is successfully loaded, you can see the following message::

  Setting up the bashrc for SKRIPS model...
  SKRIPS_DIR is: /home/rus043/scripps_kaust_model/

In the ``~/.bashrc_skrips`` file, we have::

  # Location of the modules
  export SKRIPS_DIR=$HOME/scripps_kaust_model/
  export ESMF_DIR=$SKRIPS_DIR/esmf/
  export MITGCM_DIR=$SKRIPS_DIR/MITgcm_c68r/
  export WRF_DIR=$SKRIPS_DIR/WRFV452_AO/
  export WPS_DIR=$SKRIPS_DIR/WPSV45/
  export PWRF_DIR=$SKRIPS_DIR/PWRFV452_AO/
  export WW3_DIR=$SKRIPS_DIR/ww3_607/

  # This value is 1 when installing WRF with ESMF
  export WRF_ESMF=1
  
  # Other libraries
  export ZDIR=/home/rus043/libraries/zlib-1.3-build
  export H5DIR=/home/rus043/libraries/hdf5-1.14.3-build
  export NCDIR=/home/rus043/libraries/netcdf-build
  export NFDIR=/home/rus043/libraries/netcdf-build-fortran
  export OPENMPI=/home/rus043/libraries/openmpi-build
  export CMAKEDIR=/home/rus043/libraries/cmake-build
  
  export NETCDF=$NFDIR
  export NETCDF_classic=1
  export LD_LIBRARY_PATH=$ZDIR/lib:$LD_LIBRARY_PATH
  export LD_LIBRARY_PATH=$H5DIR/lib:$LD_LIBRARY_PATH
  export LD_LIBRARY_PATH=$NCDIR/lib:$LD_LIBRARY_PATH
  export LD_LIBRARY_PATH=$NFDIR/lib:$LD_LIBRARY_PATH
  export LD_LIBRARY_PATH=$OPENMPI/lib:$LD_LIBRARY_PATH
  
  export PATH=$NCDIR/bin:$NFDIR/bin:$OPENMPI/bin:$CMAKEDIR/bin:$WPS_DIR:$PATH
  export PROJ_LIB=/home/rus043/anaconda2/share/proj/
  
  # For ESMF
  export ESMF_OS=Linux
  export ESMF_COMM=openmpi
  export ESMF_NETCDF=nc-config
  export ESMF_OPENMP=OFF
  export ESMF_LAPACK=internal
  export ESMF_BOPT=g
  export ESMF_ABI=64
  export ESMF_COMPILER=gfortran
  export ESMF_SITE=default
  export ESMF_PIO=internal
  
  export ESMF_LIB=$ESMF_DIR/lib/lib$ESMF_BOPT/$ESMF_OS.$ESMF_COMPILER.$ESMF_ABI.$ESMF_COMM.default/
  export ESMF_MOD=$ESMF_DIR/mod/mod$ESMF_BOPT/$ESMF_OS.$ESMF_COMPILER.$ESMF_ABI.$ESMF_COMM.default/
  export ESMFMKFILE=$ESMF_LIB/esmf.mk
  export ESMF_TESTEXHAUSTIVE=ON
  export ESMF_TESTMPMD=OFF
  export ESMF_TESTHARNESS_ARRAY=RUN_ESMF_TestHarnessArray_default
  export ESMF_TESTHARNESS_FIELD=RUN_ESMF_TestHarnessField_default
  export ESMF_TESTWITHTHREADS=OFF
  
  # For coupled model
  export SKRIPS_NETCDF_INCLUDE="-I${NCDIR}/include -I${NFDIR}/include"
  export SKRIPS_NETCDF_LIB="-L${NCDIR}/lib -L${NFDIR}/lib"
  export SKRIPS_MPI_DIR=$OPENMPI
  export SKRIPS_MPI_INC=$OPENMPI/include/
  export SKRIPS_MPI_LIB=$OPENMPI/lib/
  
  export LD_LIBRARY_PATH=$ESMF_LIB/:$LD_LIBRARY_PATH
  
  # For WW3
  export PATH=$WW3_DIR/model/bin:${PATH}
  export PATH=$WW3_DIR/model/exe:${PATH}
  export WWATCH3_ENV=$WW3_DIR/wwatch3.env
  export WWATCH3_NETCDF=NC4
  export NETCDF_CONFIG=${NCDIR}/bin/nc-config
  # export NETCDF_CONFIG_C=${NFDIR}/bin/ncxx4-config
  export NETCDF_CONFIG_F=${NFDIR}/bin/nf-config
  
.. note:: Before you want to install the SKRIPS model on another machine:

  #. Please install NetCDF and MPI.
  #. Please update the paths for the model components (NetCDF, MPI, WW3, and ESMF).
  #. WW3 is not necessary for running the coupled model. 
  #. To install the coupled model on SDSC expanse, please use scripts/bashrc\_expanse.
  #. To install the coupled model on SHAHEEN III, please use scripts/bashrc\_shaheen.

Now we can start to install the module components and compile the coupled
model:

.. toctree::
   :maxdepth: 1
   :titlesonly:

   Install and test ESMF<esmf/index>
   Install and test MITgcm<mitgcm/index>
   Install and test WRF<wrf/index>
   Install and test WW3<ww3/index>
   Install and test coupled code<coupled/index>
