Introduction
============
The present work shows how to use the **Verython** language, in order to simplify and enrich the development of hardware.

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
