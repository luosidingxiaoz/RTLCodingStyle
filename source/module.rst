Module
===============

Module name and file name must be the same
-------------------------------------------------

- **Each time a new module is defined, a new file with the same name must be created.**

In this way, we can know the contents of the file directly by its name.

Also, you can check if there are duplicate modules directly by checking if there are renamed files in the filelist.

- **The file suffix must correspond to the actual syntax used.**

For example, if system verilog syntax is used in a file, then a suffix of v is wrong and must be sv.

This is because some compilers determine the code parsing rules by the suffix name.

Since verilog is a subset of system verilog, sv is always applicable.

Module definition
--------------------

An example of a module definition is shown below.

.. code-block:: systemverilog 

    module sc_cmn_vr_dec
        // import package
        import scc_param_pkg::*;
    #(
        // parameter define
        parameter integer unsigned A = 1
    )(
        // IO define
        input         clk    ,
        output logic  data
    );

        // RTL code
        // ...

    endmodule

The module definition contains four parts.

1. **The imported package**
   
The scope of the package imported immediately after the module is limited to the internal scope of the module (excluding submodules).

2. **parameter definition**
3. **IO definition**
4. **Description of the internal circuit**

For the sake of uniformity, please try to follow the template above for line breaks, i.e. brackets on a separate line.
