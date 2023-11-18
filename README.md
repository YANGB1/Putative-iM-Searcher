# Putative-iM-Searcher

Putative-iM-Searcher is commandline software designed to search putative DNA or RNA i-Motif forming sequences.

# Principle
We designed a general pattern for iM formation searching using directed graph traversal process. For one sequence, the C-tracts can be regarded as nodes, and the loops can be defined as edges. All possible C-tracts are identified as nodes in the first phase, and if the distance between two nodes (loop length) is between one and twelve nucleotides, a directed edge is added between the two nodes. After constructing the directed graph, all possible iM formations and conformations are identified via the traversal of the directed graph from every node. All possible putative iMs are represented with the sub-population containing the first four nodes and three edges of the traversing paths with at least four nodes. To choose the representative iM structures from all possible iM structures, four strategies were introduced (greedy non-overlapping, greedy overlapping, non-greedy non-overlapping, and non-greedy overlapping) maintaining the nomenclature derived from QuadBase2. For the overlapping strategy, all possible iM formations are displayed while the non-overlapping function has no coinciding iM representatives. The greedy strategy maximises the length of iM representatives. For non-greedy strategies, the shortest iM can be adjusted and selected (e.g., “CCCCTCCCCTCCCCTCCCCTCCC”, the shortest potential iM forming sequence is “CCCCTCCCCTCCCCTCCC” with three cytosines while “adjusted” selects “CCCCTCCCCTCCCCTCCCC” with four cytosines in the C-tract). One representative iM forming sequence may have many different iM conformations although they share the same sequence content. Two representative iM formations are chosen for according to their stability: (A) the structure with the most extended C-tract length and minimum standard deviation of loop lengths; (B) the structure with the most extended C-tract length and minimum length of the two side loops.

![putative iM search](https://github.com/YANGB1/Putative-iM-Searcher/assets/92316121/a2297cca-8e07-45fd-b8e0-71b85d813fb1)

# Requirement
The software is developed on Python 3.9. And four Python packages are needed:
  
  os
  
  argparse (developed on v1.1)
  
  regex (developed on v2.5.109)
  
  numpy (developed on v1.22.4)

# Usage
The python script 'Putative-iM-Searcher.py' can be downloaded directly. The stored directory can be added to the ‘PATH’ environmental variable or the scripts with full path can be run alternatively. The help page can be checked by following command:
``` 
python3 Putative-iM-Searcher.py -h
``` 
Parameters can be configured according to the user's own needs.Here is an example:
``` 
python3 Putative-iM-Searcher.py --nuc_type DNA --sequence input.fa --overlapped 2 --greedy 2 --stem_short 3 --stem_long 5 --loop1_short 1 --loop1_long 12 --loop2_short 1 --loop2_long 12 --loop3_short 1 --loop3_long 12 --representative_conformation 3 --output_conformation 1 --output_folder output_path
``` 

# Input and output
The input sequences should be in fasta formation, for instance:

\>test1

CCCTCCCCCTCCCCTCCCTCCCCCCCCTCCCCTCCCTCCCTCCCCCCCCTCCCTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTCCCCCCCCCTCCTCCCCTCCCCCTCCCCTCCCTCCCTCC

\>test2

CCCCCTCCCCCTCCCCCTCCCCCTCCCCC

\>test3

CCCTAACCCTAACCCTAACCCTAACCCTAACCCTAACCC

\>test4

CCCCGACCCCAACCCCTCCCCCAACCCCTCCCC

The output files are stored in the pre-set output folder.

If --representative_conformation is set as 1, 'Putative_iM_Searcher_result_average_conformation.txt' includes conformation A of pre-set iM structures. 

If --representative_conformation is set as 2, 'Putative_iM_Searcher_result_side_shorter_conformation.txt' includes conformation B of pre-set iM structures. 

If --representative_conformation is set as 3, 'Putative_iM_Searcher_result_average_conformation.txt' and 'Putative_iM_Searcher_result_side_shorter_conformation.txt' include conformation A and B of pre-set iM structures, respectively. 

If --output_conformation is set as 1, 'Putative_iM_Searcher_result_all_conformation.txt' includes all putative iMs.


