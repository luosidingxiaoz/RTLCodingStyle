Variable definition and naming
==============================

- **Explicitly declare the type**

verilog/system verilog will use the default type when the type is not clear

Some examples are as follows.

.. code-block:: systemverilog

    // This code does not explicitly declare the type, 
    // and the language automatically inferred it to be 1bit logic type.
    // It is equivalent to 
    // output logic valid
    output  valid,          


.. code-block:: systemverilog

    // The language infers that it is of type "integer unsigend" based on its value of "32".
    // It is equivalent to
    // parameter integer unsigned WIDTH = 32
    parameter WIDTH = 32

We should specify the variable type directly, rather than having the language do the type inference.

Because sometimes the language inference may not match our intention.



Some good examples are as follows.


.. code-block:: systemverilog

    output logic            valid,
    output logic [31:0]     payload,


.. code-block:: systemverilog

    parameter integer unsigned WIDTH = 32
    parameter integer unsigned DEPTH = 64