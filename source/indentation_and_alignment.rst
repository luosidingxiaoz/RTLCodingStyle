Indentation and alignment
============================


Indentation
------------


- **All indents must be in 4 space increments.**


An example is shown below.

.. code-block:: systemverilog

    always_comb begin
        if(enable_1) 
            if(enable_2)
                data = 1'b1;
            else
                data = 1'b0;
        else
            if(enable_3)
                data = 1'b0;
            else
                data = 1'b1;
    end


.. warning:: 

    "tab" and "4 spaces" look very similar, but don't use tab instead of 4 spaces.

    Some editors have automatically replaced the tab key with 4 spaces.


- **Each sub code block must be indented one level.**


These are a few examples.

.. code-block:: systemverilog

    module pipe (
        // IO is a sub code block for module
        input           clk     ,
        input           rst_n   ,
        input           din0    ,
        input           din1    ,
        output logic    dout0   ,
        output logic    dout1
    );
        // RTL content is a sub code block for module
        always_ff @(posedge clk or negedge rst_n) begin

            //if-else is a sub code block for always
            if(rst_n) begin
        
                // this is a sub code block for if-else
                dout0 <= 1'b0;
                dout1 <= 1'b0;
            end
            else begin
                dout0 <= din0;
                dout1 <= din1;
            end
        end

        // In fact, begin ... end form a sub block, but by convention, 
        // "begin" can be left alone, "end" is new but not indented, 
        // and the rest of the sub block code must be new and indented.

    endmodule

Alignment
----------------

In general, variable names, operators, keywords, etc. should be aligned in several lines with similar functions, as shown in the following examples.

.. code-block:: systemverilog

    assign res0  = din0  + din1    ;
    assign res32 = din45 + din235  ;


.. code-block:: systemverilog


    always_comb begin
        out_en  = in_en  ;
        out_pld = in_pld ;
    end

.. code-block:: systemverilog

    input               out_ready   ,
    output logic        out_valid   ,
    output logic [31:0] out_payload ,

.. code-block:: systemverilog

    reg_slice u_rs (
        .clk         (clk         ),  
        .rst_n       (rst_n       ),  
        .in_valid    (in_valid    ),      
        .in_ready    (in_ready    ),      
        .in_payload  (in_payload  ),      
        .out_valid   (out_valid   ),      
        .out_ready   (out_ready   ),      
        .out_payload (out_payload )          
    );