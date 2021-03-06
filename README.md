# TPG-J
This is the most up-to-date repository for TPG-J. The current version is 0.9.

API Functions:

## TPGAlgorithm

   ### getTPGLearn()

      Retrieves a TPGLearn object after the algorithm has performed its parameter setup.
  
## TPGLearn
  
  ### boolean setActions( long[] acts )
      
      Set the actions available to the Learners during execution. If actions are added 
      successfully, this returns true.
    
  ### boolean initialize()
    
    Used to set up the Team and Learner populations for the current task. Performs the 
    following functions in order:
    
      1. Initialize the Team and Learner populations. Actions are assigned from the action pool. 
      2. Create the first round of Team offspring based on the Team gap.
      3. Set every applicable Team to be a Root Team.
      4. Set the current epoch to 1.
    
    If the initialization is successfully completed, this returns true.
  
  ### int remainingTeams()
    
    Teams still waiting to act wait internally in a Team queue. This method returns the 
    number of Teams which are waiting as an int.
  
  ### long participate( double[] inputFeatures )
  
    This method returns -1 if there are no Teams left to participate. If there are Teams 
    remaining, returns the action suggested by the current participating Team based on 
    the input provided. 
    
  ### long participate( double[] inputFeatures, long[] actions )
  
    This method acts the same as participate(double[]), except after a Team processes the 
    input, it checks to ensure the Team's suggested action is valid by comparing it to the 
    provided actions array. If the Team's suggested action is not valid, this will return 
    a default action of 0. 
  
  ### boolean reward( String label, double reward )
  
    If there is no Team in the queue, this returns false. Otherwise this rewards the Team 
    based on the provided reward value against a task named by the provided label. If your 
    Teams are learning to play multiple games/scenarios, each of those games or scenarios 
    should have a different label.
    
    This method also removes the currently participating Team from the internal queue. 
    
  ### void selection()
  
    Typically called once a training generation is completed. Forces TPG to rank all of the 
    Teams available, then perform selection in order to remove the worst Teams.
    
  ### void generateNewTeams()
  
    Generates a new population of Teams using the current Root Teams. This will always 
    generate a new population, regardless of what's in the current Root Teams list, so 
    if you want only the best Teams to reproduce you should call selection() first.
    
  ### void printStats( int teamCount )
  
    Prints some simple statistics for the top number of teams as determined by the 
    teamCount value. printStats(10) will print the top 10 teams, for example.
    
  ### long nextEpoch():
  
    Advances the algorithm to the next generation of training. This process includes 
    clearing out outcome maps, resetting the Root Teams list, clearing the Team Queue, 
    and removing any Learners which are not currently attached to any Teams. This method 
    then returns the new epoch value as a long integer.
