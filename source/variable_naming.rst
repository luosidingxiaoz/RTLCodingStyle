Variable definition and naming
==============================

- **Explicitly declare the type**

verilog/system verilog will use the default type when the type is not clear.

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
    parameter integer unsigned DEPTH 


- **Use the same prefix for the same set of variables**


If several IOs or several signals are transmitted and processed in a bus-like manner, i.e. the signals together form a function or protocol.

An example is a channel of axi.

.. code-block:: systemverilog

    input   logic           awvalid   ,
    output  logic           awready   ,
    output  logic  [31:0]   awaddr    ,


For these signals, the same prefix name should be used, a few examples are as follows.


.. code-block:: systemverilog

    logic           in_vld  ;
    logic           in_rdy  ;
    logic [31:0]    in_data ;

.. code-block:: systemverilog

    input   logic           out_rdy ,
    output  logic           out_vld ,
    output  logic [31:0]    out_pld ,



- **Add the prefix "v_" to the vector variable**

A vector is a group of signals of the same type, but with independent functions.

For the definition of vectors, two examples are given here.

.. code-block:: systemverilog

    // This signal consists of 32 independent en's, so we consider it as a vector that needs to be prefixed.
    logic [31:0] in_v_en    ;

    // The 32 bits within this signal together form a single piece of data, so logically we do not consider this a vector that needs to be prefixed.
    logic [31:0] in_data    ;



- **Meaningful naming**

- **Appropriate use of abbreviations**
