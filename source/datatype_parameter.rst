Data-type Parameter
====================


Data-type parameter (paraemter type) is a very useful feature that allows you to pass a type to a parameter and use that parameter to define new variables, an example of which is as follows.


.. code-block:: systemverilog 


    module param_test #(
        parameter type DAT_TYPE = logic
    )(
        input   DAT_TYPE din  ,
        output  DAT_TYPE dout
    );

        assign dout = din;

    endmodule


The module in the above example can be instantiated as follows.


.. code-block:: systemverilog 

    //inst 1
    param_test #(
        .DAT_TYPE(logic [2:0]))
    uinst_1 (
        .din    (din_width3     ),
        .dout   (dout_width3    ));

    //inst 2
    param_test #(
        .DAT_TYPE(logic [5:0]))
    u_inst2 (
        .din    (din_width6     ),
        .dout   (dout_width6    ));

This use is no different from defining "parameter DATA_WIDTH = 3", but the parameter type can also support packages, as well as more specific types. Two more meaningful examples are as follows.

Example 1.

.. code-block:: systemverilog 

    module adder #(
        parameter DAT_TYPE = logic
    )(
        input  DAT_TYPE         din1,
        input  DAT_TYPE         din2,
        output type(din1+din2)  dout
    );

        assign dout = din1 + din2;

    endmodule

    //--------------------------------------------
    // Inst

    //unsigned_adder
    adder #(logic unsigned [7:0])
    u_uadder (
        .din1(udin1 ),
        .din2(udin2 ),
        .dout(udout ));

    //signed_adder
    adder #(logic signed [7:0])
    u_sadder (
        .din1(sdin1 ),
        .din2(sdin2 ),
        .dout(sdout ));

Example 2.

In this example, if package is added or subtracted arbitrarily, regslice, which is not concerned with package content, can be left unchanged.

.. code-block:: systemverilog 

    module reg_slice #(
        parameter PLD_TYPE = logic
    )(
        output logic    out_vld ,
        input  logic    out_rdy ,
        output PLD_TYPE out_pld ,

        input  logic    in_vld  ,
        output logic    in_rdy  ,
        input  PLD_TYPE in_pld 
    );

        assign out_vld  = in_vld    ;
        assign in_rdy   = out_rdy   ;
        assign out_pld  = in_pld    ;

    endmodule

    package PLD1;
        logic [31:0]    addr    ;
        logic [3:0]     qos     ;
    endpackage

    package PLD2;
        logic [31:0]    addr    ;
        logic [3:0]     qos     ;
        logic [4:0]     user    ;
    endpackage

    //--------------------------------------------
    // Inst

    reg_slice #(
        .PLD_TYPE(PLD1))
    u_rs1 (
        .in_vld     (in_vld1    ),
        .in_rdy     (in_rdy1    ),
        .in_pld     (in_pld1    ),
        .out_vld    (out_vld1   ),
        .out_rdy    (out_rdy1   ),
        .out_pld    (out_pld1   ));

    reg_slice #(
        .PLD_TYPE(PLD2))
    u_rs2 (
        .in_vld     (in_vld2    ),
        .in_rdy     (in_rdy2    ),
        .in_pld     (in_pld2    ),
        .out_vld    (out_vld2   ),
        .out_rdy    (out_rdy2   ),
        .out_pld    (out_pld2   ));


By using the data-type parameter, a module can be used to handle different data types.


.. attention:: 

    **This syntax is synthesizable and has been tested on leading commercial synthesis and QC tools.**