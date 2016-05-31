Introduction
============
The present work shows how to use the **Verython** language, in order to simplify and enrich the development of hardware.

For those that were users of hardware description languages like Verilog know the complexity of the language and they also know that even for simple tasks a lot of code is required. **Verython** is an alternative that allows to use all the Python sugar to improve the time spended in a hardware development task.

Decorators
==========

- ``@top``: It's used before the function definition for the corresponding Verilog's principal module. This function should be the first one, so ``@top`` should be the first functional line in a Verython code.
- ``@initial``: It's used to define a block that will be executed only one time.
- ``@always``: It's used to define a block that will be executed when any of the parameters change in a sequential logic module. When the parameters list is empty, the block will be a combinational logic module.

Control sentences
=================

The loop structures ``for`` and ``while`` are implemented in the same way that in Python. This also happens with the conditional structure ``if``-``elif``-``else``.

The ``switch`` sentence only receives a simple statement for each case and the notation is as follows::

    switch(sel):
	case 0: return A
	case 1: return B
	case 2: return C
	default: return 0

Functions
=========

Each function it's defined in a Python way, but the arguments has two parts, before the *;* should be entered the inputs of the system, in a notation very similar to the Verilog's one, and after the *;* it's going to be expected the output signals with their respective name.

It's also possible to comunicate several modules using this notation, because every function will be a diferent Verilog's module. It's posible then to have several functions defined, but the ``@top`` function will be the first and mandatory.

Example
=======

A very common case and basic case is the multiplexor module. In this code you should like to have something like tihs in Verilog::

    `timescale 1ns/1ps
    module mux(A, B, C, sel, O,)
        input wire [23:0]A;
        input wire [23:0]B;
        input wire [23:0]C;
        input wire [1:0]sel;
        output reg [23:0]O;
        always @(sel or A or B or C)
        begin
            case(sel)
                'd0: O <= 'b10101;
                'd1: O <= B;
                'd2: O <= A;
                default: O <= 'd0;
            endcase
        end
    endmodule

The idea is to acomplish this module in the same way, so the proposed code in Verython will be::

    @top
    def mux ([23:0]A, [23:0]B, [23:0]C, [1:0]sel; [23:0]O):
        @always(sel, A, B, C)
        block:
            switch(sel):
                case 0:  return 0b10101
                case 1:  return B
                case 2:  return A
                default: return 0

As can be seen, the Verython code isn't only shorter, but it also removes some confusing and unusefull code that could lead to mistakes.
