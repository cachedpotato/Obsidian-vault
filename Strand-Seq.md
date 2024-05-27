---
tags:
---
# Strand-Seq
Strand-seq is a sequencing method that aims to preserve template strand data. When mitosis occur, Chromosomes are split evenly (1 paternal, 1 maternal). By normal sequencing methods, it's impossible to figure out which was the template strand used during the cloning process. Strand-seq overcomes this problem by incorporating Uracil into the nascent strands during the very first cloning phase.
![[스크린샷 2024-05-27 150118.png|400]]

The Uracil-annotated strands will not be able to replicate in the following replication steps, leaving only the template strands. This way, we can exactly figure out which template strands were inherited from the parent cell.
![[스크린샷 2024-05-27 151556 1.png|800]]
As we can see above, we can exactly see which strand has been inherited by which cell. the 3'->5' direction of strand is called the Watson Strand, and the Opposite Clark Strand. There are 3 possibilities assuming no mutations/altercations have occurred:
- 2 Watson Strands 
- 1 Watson, 1 Clark
- 2 Clark Strands
The Horizontal bars in the rightmost image represent read count of DNA fragment within a given bin (~200kb). Of course, Life is not this simple. Various alterations can occur during the mitosis, leading to results like below:
![[스크린샷 2024-05-27 152505.png]]
SCE stands for Sister Cell Exchange. We can see that for those labeled SCE have parts of Watson strand reads moved to Clark strand, and vice versa. WE can also see mis-orientations in Chromosome 10 and 14.

Sequencing is done by first going through MNase, which cleaves open chromatin spots, then using left splices for replication.


---
Categories: [[Biotechnology]], [[Sequencing Method]]
References:
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3791154/
https://www.nature.com/articles/nprot.2017.029/figures/1
https://www.youtube.com/watch?v=wfsauCLU4lk
Created: 2024-05-27
