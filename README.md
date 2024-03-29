# Putative-iM-Searcher

Putative-iM-Searcher is commandline software designed to search putative DNA or RNA i-Motif forming sequences.

# Principle
We designed a general pattern for iM formation searching using directed graph traversal process. For one sequence, the C-tracts can be regarded as nodes, and the loops can be defined as edges. All possible C-tracts are identified as nodes in the first phase, and if the distance between two nodes (loop length) is between one and twelve nucleotides, a directed edge is added between the two nodes. After constructing the directed graph, all possible iM formations and conformations are identified via the traversal of the directed graph from every node. All possible putative iMs are represented with the sub-population containing the first four nodes and three edges of the traversing paths with at least four nodes. To choose the representative iM structures from all possible iM structures, four strategies were introduced (greedy non-overlapping, greedy overlapping, non-greedy non-overlapping, and non-greedy overlapping) maintaining the nomenclature derived from QuadBase2. Overlapping strategy selects an iM representative structure for each iM starting coordinate while the non-overlapping function has no coinciding iM representatives. The greedy strategy maximises the loop length of iM representatives with longest C-tract. For non-greedy strategies, the iM with the most extended C-tract length and the shortest loop length can be selected. One representative iM forming sequence may have many different iM conformations although they share the same sequence content. Two representative iM formations are chosen for according to their stability: (A) the structure with minimum standard deviation of loop lengths; (B) the structure with minimum length of the two side loops. We called the initial computational pipeline Putative-iM-Searcher

![putative iM search](https://github.com/YANGB1/Putative-iM-Searcher/assets/92316121/a2297cca-8e07-45fd-b8e0-71b85d813fb1)

# Installation and Usage
The dependency packages can be installed by:
``` 
pip3 install -r requirements.txt
``` 
Putative-iM-Searcher (available at https://pypi.org/project/Putative-iM-Searcher/) can be installed by:
``` 
pip3 install Putative-iM-Searcher
```
Alternatively, the python script 'Putative-iM-Searcher.py' can be downloaded directly from Github. The stored directory can be added to the ‘PATH’ environmental variable or the scripts with full path can be run alternatively using command like: 
``` 
python3 Putative-iM-Searcher.py -h. 
``` 
After intalled the package with 'pip', the help page can be checked by following command:
``` 
Putative-iM-Searcher.py -h
``` 
Parameters can be configured according to the user's own needs. Here is an example:
``` 
Putative-iM-Searcher.py --nuc_type DNA --sequence input.fa --overlapped 2 --greedy 2 --stem_short 3 --stem_long 5 --loop1_short 1 --loop1_long 12 --loop2_short 1 --loop2_long 12 --loop3_short 1 --loop3_long 12 --representative_conformation 3 --output_conformation 1 --output_folder output_path
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

# Test
We provide the 'test.fa' in zipped folder 'test'. 'test.fa' contains Chr4 and Chr5 of Arabidopsis thaliana. Besides, there are nine example output files. 

After intalled the package with 'pip', the same output files as 'Overlapped_Greedy_conformationA.txt', 'Overlapped_Greedy_conformationB.txt', and 'All_conformation.txt' can be generated with the following command:
``` 
Putative-iM-Searcher.py --sequence test.fa --overlapped 1 --greedy 1 --representative_conformation 3 --output_conformation 1
``` 
After intalled the package with 'pip', the same output files as 'Overlapped_NonGreedy_conformationA.txt', 'Overlapped_NonGreedy_conformationB.txt', and 'All_conformation.txt' can be generated with the following command:
``` 
Putative-iM-Searcher.py --sequence test.fa --overlapped 1 --greedy 2 --representative_conformation 3 --output_conformation 1
```
After intalled the package with 'pip', the same output files as 'NonOverlapped_Greedy_conformationA.txt', 'NonOverlapped_Greedy_conformationB.txt', and 'All_conformation.txt' can be generated with the following command:
``` 
Putative-iM-Searcher.py --sequence test.fa --overlapped 2 --greedy 1 --representative_conformation 3 --output_conformation 1
```
After intalled the package with 'pip', the same output files as 'NonOverlapped_NonGreedy_conformationA.txt', 'NonOverlapped_NonGreedy_conformationB.txt', and 'All_conformation.txt' can be generated with the following command:
``` 
Putative-iM-Searcher.py --sequence test.fa --overlapped 2 --greedy 2 --representative_conformation 3 --output_conformation 1
``` 
