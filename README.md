# Wordle-Solver
Welcome to my first personal project, wordle solver. 

# Layout
 - First cache all words
  - assign a weight to each word, based on the weight of each letter contained 
    - done by scanning all words and determining number of occurances of each letter. If "e" occurs 12 times in the word bank, it will have a weight of 12. word's weight is sum of all letter weights
 - suggest highest weighted word 
 - prompt user for word they used to input. does not need to be the word suggested
- prompt user to input the wordle feedback
- based on feedback, eliminate the correct words
- suggest new best word until guessed.

# Dependencies
 - words.txt - provides the word list
  - weight.py - weighs and sorts the words. takes in words.txt as an arg and returns words in top down weight ranking. 
    - will look into recursive sorting algos. shouldnt be an issue, just need to investigate
  - elim.py - takes in weight.py's weighted list and string containing wordle feedback. Iterate through list eliminating words using wordle feedback. 
    - first thought is to use nested for loops, will be very slow with input list of >14,000 rows at 5 words each. looking at 70,000 comparisons. any way to do this recursively? will investigate.
    - UPDATE: thinking of parallelizing elimination. recursively split list into smaller lists, then iteratively eliminate. will still utilize nested for loops, but will run in parallel cutting down processing time. What is most efficient number of parallel processes based on input size n? must investigate. 
  - main.py - calls weight.py and contains the functions that render gui, fetches best guess from weight.py, appropriately calls and passes arguments to elim.py
