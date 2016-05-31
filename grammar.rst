Introduction
============
The present work shows the implementation of a Python to Verilog translator. The modified Python grammar is called **Verython** and was made using ANTLR4 and Java.

This code was implemented using *Visitors*, which captures every grammar rule and generates his respective code.

Lexical components
==================

The lexical components of Verthon are basically the same of the Python ones, adding the next reserved words:

::

    TOP: '@top';
    INITAL: '@initial';
    ALWAYS: '@always';
    SWITCH : 'switch';
    CASE : 'case';
    DEFAULT: 'default';
    BLOCK: 'block';

The first three ones, ``@top``, ``@initial`` and ``@always``, are decorators for realizing special operations in Verilog. ``switch``, ``case`` and ``default`` are for the implementation of the *switch* control structure, non-native in Python. Finally, ``block`` is a defined structure made for surronding with ``begin``-``end`` in Verilog code.

It was also restricted the language to use only numeric data, all this because in the silicon implementation there's no implementation of any other kind.
