# basic overview of the competition 

competition page: https://www.kaggle.com/competitions/AI4Code

"The goal of this competition is to understand the relationship between code and comments in Python notebooks. You are challenged to reconstruct the order of markdown cells in a given notebook based on the order of the code cells, demonstrating comprehension of which natural language references which code."

JSON files were given to be used for training, and "each file contains the code and markdown cells of a Kaggle notebook. The code cells are in their original (correct) order. The markdown cells have been shuffled and placed after the code cells." The aim is to figure out the correct positioning of the markdown cells amongst the code cells.

# basic overview of how the model works 

took a pairwise approach: 
- there were as many pairs as there were markdown cells 
- the pair contained the features of one markdown cell and one code cell 
- the pairs were determined using jaccard similarity 
  - for each markdown cell, the jaccard similarity was computed with all given code cells in the notebook 
  - the code cell that resulted in the highest jaccard similarity was paired with the markdown cell 
  - note that one code cell may be paired with multiple markdown cells 

determinging the order:
- "labels" were given to both markdown and code cells 
- code cells labels were determined with a formula, using only their cumcount values (this information was guaranteed to be in the test set)
- markdown labels were determined by a formula (this depended on multiple variables that would not be there in the test set)
- these markdown labels were also what the model needed to predict
- after prediction, all cells were ordered in ascending order of their "labels"

additional details:
- of the given training examples, of which 1000 were used for training and validation, and 500 were used for testing (there is no overlap in these sets)
- predictions from the test set were scored using the kendall tau metric, accuracy obtained was 0.666
