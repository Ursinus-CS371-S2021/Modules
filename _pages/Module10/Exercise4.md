---
layout: exercise_pyodide
permalink: "Module10/Exercise4"
title: "CS 371: Module 10: Exercise 4"
excerpt: "CS 371: Module 10: Exercise 4"
canvasasmtid: "113876"
canvaspoints: "2"
canvashalftries: 5

info:
  comments: "true"
  prev: "./Video4"
  points: 2
  instructions: "Fill in the code to complete the memoization table for string edit distance."
  packages: "numpy"
  goals:
    - To use memoization/dynamic programming to solve the string edit distance efficiently
    
processor:  
  correctfeedback: "Correct!!" 
  incorrectfeedback: "Try again"
  submitformlink: false
  feedbackprocess: | 
    feedback.setValue(pyodide.globals.res);
  correctcheck: |
    pyodide.globals.res == "3.4.5"
  incorrectchecks:
    - incorrectcheck: |
        pyodide.globals.res == "0.0.0"
      feedback: "Try again.  It looks like you're not filling in all of the costs"
    - incorrectcheck: |
        pyodide.globals.res == "5.6.10"
      feedback: "Try again.  Be careful to only add 1 to the case where both are chopped off the end if they don't match"

files:
  - filename: "Student Code"
    name: driver
    ismain: false
    isreadonly: false
    isvisible: true
    height: 600
    code: | 
          import numpy as np

          def edit(s1, s2):
              """
              Parameters
              ----------
              s1: string of length M
                  A string with M characters
              s2: string of length N
                  A string with N characters
                  
              Returns
              -------
              int: The optimal number of add/delete/match/swap
                  operations needed to turn s1 into s2 or vice versa
              """
              M = len(s1)
              N = len(s2)
              table = np.zeros((M+1, N+1))
              # Fill in the base cases
              table[0, :] = np.arange(N+1)
              table[:, 0] = np.arange(M+1)
              for i in range(1, M+1):
                  for j in range(1, N+1):
                      cost1 = table[i, j-1] + 1
                      cost2 = 0 # Check table[i-1, j] + 1
                      cost3 = 0 # Check table[i-1, j-1] (+ 1 if s1[i-1] != s2[j-1])
                      # Store table[i, j] as the min of the above possibilities
              return int(table[-1, -1])



  - filename: "Test Code Block"
    ismain: true
    name: main
    isreadonly: true
    isvisible: true
    code: |
        res = "{}.".format(edit("chris", "chase"))
        res += "{}.".format(edit("school", "fools"))
        res += "{}".format(edit("topology", "topography"))
        print(res)
        
---
