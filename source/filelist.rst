Filelist
===============

The following rules should be observed when defining the filelist:

1. **Keep the same prefix**

For an IP filelist, all files should use the same prefix, and this prefix needs to be guaranteed to be unique within the project.

An example is as follows:

.. code-block:: 

    sc_bus_arbiter.sv
    sc_bus_decoder.sv
    sc_bus_buffer.sv

In general, the prefix used is the abbreviation of this IP (but be aware of the uniqueness).

2. **Centralized processing of macro definitions and timely cancellation of definitions**

If an IP needs to use macro definitions, then all the defines must be grouped together in one file and placed at the beginning of the filelist.

Correspondingly, all defines must have their undefine counterparts, which are also grouped together in a single file and placed at the end of the filelist

An example is as follows:

.. code-block:: 

    sc_bus_define.sv
    sc_bus_arbiter.sv
    sc_bus_decoder.sv
    sc_bus_buffer.sv
    sc_bus_undefine.sv

.. warning::
    Do not use macro definitions unless there is no other solution to the problem at all.

    If a macro definition is defined in an IP and not cancelled after the IP filelist is completely finished, it will affect other IPs and cause the code of other IPs to be modified.

    
