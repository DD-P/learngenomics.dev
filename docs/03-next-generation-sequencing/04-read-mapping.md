---
title: Read Mapping
track: Next-Generation Sequencing
---

During the next generation sequencing portion of our workflow, it's as if a box
of puzzle pieces were dumped out onto a table. To get a full picture of an
individual's genome, we need to put that puzzle back together through a process
called **read mapping**. As with any puzzle, you need the picture on the front
of the box that describes what the puzzle should look like. In genomics, this
proverbial "picture on the front of the box" is called the **reference genome**.
You can learn more about the reference genome [here](/docs/02-genomic-variation/01-baselines-for-variation.md).

Before starting your analysis, you'll need to decide on which reference genome
you will use as the baseline for your project. Once a reference genome is
decided, the next step is to choose a mapping software (frequently referred to
as a mapper or aligner) to align the reads to that reference genome. The mapping
software generates a special data structure from a reference genome and then
goes through each read pair in the FASTQ files to see if and where they fit in
the reference genome. 

At the time of writing, the most popular aligner for each type of data
is [BWA](https://github.com/lh3/bwa) for DNA sequencing
and [STAR](https://github.com/alexdobin/STAR) for RNA sequencing. Each program
provides many parameters that can be tweaked depending on the characteristics of
the data to achieve the "best" alignment. Once the alignment program has
completed, it creates
a [SAM/BAM](https://samtools.github.io/hts-specs/SAMv1.pdf) file containing all
of the read pairs, where the aligner believes they live in the reference genome
(if anywhere), and many other fields that the aligner computes. This file is
widely considered the basis of most modern computational genomic analyses. The
specifics of each file type are discussed in the next chapter.

:::info

As an implementation note, the entire analysis is based off of the reference
genome used. Generally speaking, analyses that use two different reference
genomes are not compatible because the positions of genes and other important
biomarkers are updated with each genome build. Once an end-to-end analysis
pipeline is decided on, it is a significant task to update analysis pipelines to
a new reference genome. As such, at the time of writing, many labs are still
using the GRCh37 version of the human genome, which was released in
2009.

:::
