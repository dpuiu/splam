User Manual 
=======================

splam
---------------------------------

.. code-block:: text

   usage: splam [-h] [-v] [-c] {extract,score,clean} ...

   splice junction predictor to improve alignment files (BAM / CRAM)

   optional arguments:
   -h, --help            show this help message and exit
   -v, --version
   -c, --citation

   Commands:
   {extract,score,clean}
      extract             Extracting all splice junctions from an alignment or annotation file
      score               Scoring all splice junctions
      clean               Cleaning up spurious splice alignment


|

splam extract
-----------------------------------

.. code-block:: text

   usage: splam extract [-h] [-V] [-F TYPES] [-P] [-n] [-f FILE_FORMAT]
                        [-d DATABASE] [-o DIR] [-M DIST] [-g GAP] [--fr] [--rf]
                        INPUT

   positional arguments:
   INPUT                 target alignment file in BAM format or annotation file in GFF format.

   optional arguments:
   -h, --help            show this help message and exit
   -V, --verbose         running splam in verbose mode.
   -F TYPES, --features TYPES
                           text file listing parent feature types from which to extract introns
   -P, --paired          bundling alignments in "paired-end" mode.
   -n, --write-junctions-only
                           writing out splice junction BED file only without other temporary files.
   -f FILE_FORMAT, --file-format FILE_FORMAT
                           the file type for Splam to process: "BAM", "GFF", or "GTF"
   -d DATABASE, --database DATABASE
                           path to an existing gffutils annotation database
   -o DIR, --outdir DIR  output directory; the default is "tmp_out"
   -M DIST, --max-splice DIST
                           maximum splice junction length
   -g GAP, --bundle-gap GAP
                           minimum gap between bundles
   --fr                    assume a stranded fr-secondstrand library
   --rf                    assume a stranded rf-firststrand library

|

splam score 
-----------------------------------

.. code-block:: text

   usage: splam score [-h] [-V] [-o DIR] [-b BATCH] [-d pytorch_dev] -G REF.fasta -m MODEL.pt junction_BED

   positional arguments:
   junction_BED          target splice junctions in bed files.

   optional arguments:
   -h, --help            show this help message and exit
   -V, --verbose
   -o DIR, --outdir DIR  the directory where the output file is written to. Default output filename is "junction_score.bed"
   -b BATCH, --batch-size BATCH
                           the number of samples that will be propagated through the network. By default, the batch size is set to 10.
   -d pytorch_dev, --device pytorch_dev
                           the computing device that is used to perform computations on tensors and execute operations in the PyTorch framework. By
                           default, this parameter is detected automatically.
   -G REF.fasta, --reference-genome REF.fasta
                           the path to the reference genome.
   -m MODEL.pt, --model MODEL.pt
                           the path to the Splam model

|                     

splam clean 
-----------------------------------

.. code-block:: text

   usage: splam clean [-h] [-@ threads] [-t threshold] [-n bad intron num]
                      [-P] -o DIR

   optional arguments:
   -h, --help            show this help message and exit
   -@ threads, --threads threads
                           set the number of sorting, compression, and merging threads; the default is 1
   -t threshold, --threshold threshold
                           cutoff for identifying spurious splice junctions; the default is 0.1
   -n bad intron num, --bad-intron-num bad intron num
                           number of spurious introns used to classify a transcript as bad; the default is 8
   -P, --paired          clean an alignment file in paired-end mode
   -o DIR, --outdir DIR  required directory containing the extract and score outputs



|
|
|
|
|


.. image:: ../_images/jhu-logo-dark.png
   :alt: My Logo
   :class: logo, header-image only-light
   :align: center

.. image:: ../_images/jhu-logo-white.png
   :alt: My Logo
   :class: logo, header-image only-dark
   :align: center
