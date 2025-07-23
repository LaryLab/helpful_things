# Procedures for Projects in the Lary Lab  
    
### Starting a project  
    
**Data:** Data should be stored in a location accessible to all lab members in a subdirectory of `/projects/larylab/data/`. Then individual lab members can use absolute paths to read in the data in their scripts.  
  
**GitHub integration:** Before starting any analysis, lab members should create a GitHub repository (just one per project), then create a project and subdirectory in their space in `/projects/larylab/` and link them together.  
    
**Collaboration within the lab:** If multiple lab members are working on different parts of the same project, they should each have a subdirectory in their space in `/projects/larylab/` (preferrably called the same thing) that is linked to the GitHub repo. These will be duplicates for as long as the project is ongoing. Lab members should pull from GitHub when they start work, and push periodically to make sure everyone is working with the most up-to-date version of the project.  
    
**Analysis:** Create scripts, subdirectories, and results files as necessary. Try to keep things relatively organized as you go along! And remember that you don't need to create multiple versions of the same code - we have git for version control.  
    
**README:** This can be pretty general while the project is ongoing, but make it more informative as you get closer to publication. Info about what each file and script is and is for would be great. Include: purpose of the script, what input files it needs, and what output files will be produced.      
**Ending a project:** When we are totally done with the project, we should move the project subdirectory out into the `/projects/larylab/` directory so that it can be found easily by everyone. If multiple lab members were working on it in independent (but identical) subdirectories, one member should move it into the larylab space and one should delete theirs.  
