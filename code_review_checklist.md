# Code Review Checklist  
  
In the process of code review, this checklist should be used first by the primary author of the code. Once they have gone through it for each script, they can hand it off to another member of the lab or the whole lab group for final review.  
  
  
## Scripting  

A good way to check each script is to clear your workspace and run it top to bottom. If there is any code you're not sure you need anymore, comment it out and do this again. Make sure that the names of the scripts are a good indication of what they are for.  
  
At the top of each script, include this information:  
- author name(s)  
- what the goal of the script is  
- the date that it was last modified  
  
In the body of the script:  
- set up the environment and/or working directory  
- load all packages necessary to run the script (and no others) at the top  
- read in all data files at the top  
  - original data files should have absolute paths  
  - all other paths (such as intermediate data files and results) should be relative  
- use consistent spacing throughout  
- separate sections clearly  
- comment every major process (and include more comments for dense/complicated sections)  
- use variable and column names that are logical and informative  
- only include the code that is necessary to achieve the goal (other code that you want to keep can be moved elsewhere)  


## Organization  
  
- original data files should be in a totally separate directory under `/projects/larylab/data/`.  
- 1 main project directory that contains everything generated for the project  
- 3 directories inside the project directory  
  - some variation is okay - if the project is especially expansive it might make more sense to have directories under the project directory that represent datasets or traits, and then each of these three directories inside each of those  
  - `scripts` should hold all scripts used to analyze and plot data (including slurm scripts)  
    - all scripts necessary to replicate your analysis  
    - 1 script for generating an analytic file - should wrangle data, combine it with other necessary information, and get it into a useable format  
    - other scripts for doing stats and other analyses and making tables and figures  
    - slurm scripts get included here, but it's fine to upload representative samples of these to GitHub if there are many similar ones  
  - `data` should hold intermediate data files generated during the analysis  
    - files don't necessarily need to be read out at every stage, so check that these will be necessary later in the analysis or visualization process  
  - `results` should hold all results files, especially tables and figures  
    - these should be end point files - if they are used in another script, the data directory is more appropriate


## ReadMe File  

- list scripts in the order that they are needed to reproduce the analysis  
- give a brief description (one sentence is fine) of what the script does  
- note the files necessary to run the script  
- note the files that will be produced by the script  
