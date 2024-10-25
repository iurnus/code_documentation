#############################
MITgcm test case in CA region
#############################

MITgcm example case
-------------------

Compile the code
~~~~~~~~~~~~~~~~

We have an example MITgcm case in our coupled code::

    cd $SKRIPS_DIR/coupler/L1.C1.mitgcm_case_CA2009

Here, L1 denotes "Level 1 complexity" and C1 denotes "Case 1". 

We have the following files in the test case::

    clean.sh
    input_ca_mitgcm\
    install.sh
    mitCode\
    mitRun\
    README
    utils\

To compile and run this case::

    ./install.sh

MITgcm--ESMF coupled case
-------------------------

The L2C1 case (Level 2 complexity, Case 1) is to test the interface between
MITgcm and ESMF::

    cd $SKRIPS_DIR/coupler/L2.C1.mitgcm_case_CA2009_mpiESMF_1cpu

To compile and run this case::

    ./install.sh

The results obtained from the L2C1 case should be the same as the L1C1 case.
Because L2C1 case only uses one CPU, we also have implemented the L2C2 case
that uses more CPUs to test the code in parallel using MPI.

