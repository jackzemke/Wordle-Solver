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
    - generously provided by github user dracos at [this repo](https://gist.github.com/dracos/dd0668f281e685bad51479e5acaadb93)
  - weight.py - weighs and sorts the words. takes in words.txt as an arg and returns words in top down weight ranking. 
    - __TODO:__ will look into recursive sorting algos. shouldnt be an issue, just need to investigate.
     - need to obtain number of appearances of each character before calling sorting algo. best way? looking at 70,000 chars. __TODO: investigate such__
       - more parallelization will likely best solution here. return a list? dict? maybe dict. parallelization will be best key here. just need to figure out how to merge returns from each parallel process. extremely feasible
  - elim.py - takes in weight.py's weighted list and string containing wordle feedback. Iterate through list eliminating words using wordle feedback. 
    - first thought is to use nested for loops, will be very slow with input list of >14,000 rows at 5 words each. looking at 70,000 comparisons. any way to do this recursively? __TODO: investigate.__
    - UPDATE: thinking of parallelizing elimination. recursively split list into smaller lists, then iteratively eliminate. will still utilize nested for loops, but will run in parallel cutting down processing time. What is most efficient number of parallel processes based on input size n? __TODO: investigate.__ 
        - how merge eliminated lists back together making sure to preserve sorted list? resorting may be expensive. some kind of flag system to ensure sorting is preserved.
  - main.py - calls weight.py and contains the functions that render gui, fetches best guess from weight.py, appropriately calls and passes arguments to elim.py

# GUI Layout
 - Don't know much about python gui's other than tkinter. want to ship on xcode. 
  - Will be biggest "new" skill of this project.
   - __TODO: investigate most fitting gui for this application, investigate usage of gui in xcode, will this be shippable on app store? is possible to ship xcode application not through app store? best way to make this a cohesive "package"__