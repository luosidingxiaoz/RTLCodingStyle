Sync FIFO
============
.. code-block:: systemverilog

    `timescale 1ns / 1ps
    //////////////////////////////////////////////////////////////////////////////////
    // Company: URBADASS.LTD
    // Engineer: zick
    // 
    // Create Date: 02/26/2023 09:01:54 PM
    // Design Name: sync fifo handshake
    // Module Name: sync_fifo
    // Project Name: sync fifo
    // Description: 
    //              a handshake based sync fifo for serialized data
    // Dependencies: 
    // 
    // Revision:
    //              Revision 0.01 - File Created
    // Additional Comments:
    // 
    //////////////////////////////////////////////////////////////////////////////////
    module sync_fifo
        #(
            parameter int unsigned DEPTH    = 8             ,
            parameter int unsigned DWIDTH   = 32            ,
            parameter int unsigned AWIDTH   = $clog2(DEPTH)   
        )(
            input                       clk     ,
            input                       rst_n   ,
            // Req
            input                       req_vld ,
            output  logic               req_rdy ,
            input   logic [DWIDTH-1:0]  req_data,
            // ACK
            output  logic               ack_vld ,
            input                       ack_rdy ,
            output  logic [DWIDTH-1:0]  ack_data
        );

    //=================================================================
    // Internal Signal
    //=================================================================
        logic [DWIDTH-1:0]  data_mem [DEPTH-1:0];
        logic [AWIDTH  :0]  wr_ptr              ;
        logic [AWIDTH  :0]  rd_ptr              ;
        logic               rd_en               ;
        logic               wr_en               ;
        logic               fifo_full           ;
        logic               fifo_empty          ;

        logic               dummy_wire1;
        logic               dummy_wire2;

    //=================================================================
    // WR/RD enable
    //=================================================================
        assign wr_en = req_vld && req_rdy;
        assign rd_en = ack_vld && ack_rdy;

    //=================================================================
    // Empty & Full
    //=================================================================
        assign fifo_empty = wr_ptr == rd_ptr;
        assign fifo_full  = {~wr_ptr[AWIDTH], wr_ptr[AWIDTH-1:0]} == rd_ptr;

    //=================================================================
    // Handshake
    //=================================================================
        assign ack_vld = ~fifo_empty;
        assign req_rdy = ~fifo_full;

    //=================================================================
    // WR/RD control
    //=================================================================
        always_ff @(posedge clk or negedge rst_n) begin
            if (~rst_n) begin
                wr_ptr <= {AWIDTH+1{1'b0}};
                rd_ptr <= {AWIDTH+1{1'b0}};
            end
            else begin
                if (rd_en) {dummy_wire1, rd_ptr} <= rd_ptr + 1'b1;
                if (wr_en) {dummy_wire2, wr_ptr} <= wr_ptr + 1'b1;
            end
        end

    //=================================================================
    // Mem access
    //=================================================================
        always_ff @(posedge clk or negedge rst_n) begin
            if (~rst_n) begin
                for (int i=0; i<DEPTH; i=i+1) begin
                    data_mem[i] <= {DWIDTH{1'b0}};
                end
            end
            else begin
                if (wr_en) data_mem[wr_ptr[AWIDTH-1:0]] <= req_data;
            end
        end
        
        assign ack_data = data_mem[rd_ptr[AWIDTH-1:0]];

    endmodule