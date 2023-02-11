Parameter
==========

The parameter definition should take the following form:

.. code-block:: systemverilog 

    parameter integer unsigned    EXAMPLE1 = 1,
    parameter logic [31:0]        EXAMPLE2 = 32'b0

- **When defining, the specific data type should be explicitly declared.**


- **Parameter should be in all capital letters to show the difference from other variables.**
- **Define only one parameter per line**
- **When using parameter for circuit assignment, you need to pay attention to whether it can be synthesys**