mupi
====

MUltiple Platform Interpreter. X86 and SPARC interpreters in bash


Background
==========

Back in 2006 I had the rather dubious idea of writing an x86 interpreter in bash.
The idea was that, as bash will run on any Linux system,
then my x86 interpreter would be universally portable across any hardware.
Also, it seems completely ridiculous idea.

Eventually, after making some progress with x86, I switched to SPARC.
Here the reasoning was that everyone already has an x86 box, so SPARC was more useful.
And SPARC seemed marginally easier to decode.

Running
=======

Try:

xumpi samples/helloworld.x86
xmupi samples/greenbottles.x86
sumpi samples/helloworld.sparcsol

For assembler debug add a -d
For stracing output add a -s


Implementation details
======================

The main idea is to use multiarch objdump to read each line as required for decoding.

This is then interpreted into a simpler format of a function name and arguments,
which can just be called.
This format is then cached for later reuse.
This caching increased the speed of greenbottles tenfold.


Memory values are stored as variables.
For example, memory location 0xffff1234 is stored in $MEMORY_ffff1234

Heavy use is made of ${!x}

