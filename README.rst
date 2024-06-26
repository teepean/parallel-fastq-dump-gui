
parallel-fastq-dump-gui
===================
parallel ``fastq-dump`` wrapper with a claude.ai created GUI. 

The GUI version requires PyQt5

Why & How
---------
NCBI ``fastq-dump`` can be very slow sometimes, even if you have the resources (network, IO, CPU) to go faster, even if you already downloaded the sra file (see the protip below). This tool speeds up the process by dividing the work into multiple threads.

This is possible because ``fastq-dump`` have options (``-N`` and ``-X``) to query specific ranges of the sra file, this tool works by dividing the work into the requested number of threads, running multiple ``fastq-dump`` in parallel and concatenating the results back together, as if you had just executed a plain ``fastq-dump`` call.

Protips
-------
* Downloading with ``fastq-dump`` is slow, even with multiple threads, it is recommended to use ``prefetch`` to download the target sra file before using ``fastq-dump``, that way ``fastq-dump`` will only need to do the dumping.
* All extra arguments will be passed directly to ``fastq-dump``, ``--gzip``, ``--split-files`` and filters works as expected.
* This tool is **not** a replacement, you still need ``fastq-dump`` and ``sra-stat`` on your ``PATH`` for it to work properly.
* Speed improvements are better with bigger files, think at least 200k reads/pairs for each thread used.

Micro Benchmark
---------------

.. figure:: https://cloud.githubusercontent.com/assets/6310472/23962085/bdefef44-098b-11e7-825f-1da53d6568d6.png
