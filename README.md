# MonteCarlo
Monte Carlo module with classes for Die, Game, and Analyzer for simulating dice rolls and analyzing results. Built for DS5100 Final Project

Metadata:

  Project Name: Monte Carlo Simulator
  
  Author: Matthew Lang
  
  Version: 1.0
  
  License: MIT

Synopsis:
  The Monte Carlo Simulator for this project allows people to roll dice and analyze the results of a dice game. Below is an example of how to install, use, and analyze a simple game with the various classes built: Die, Game, and Analyzer.

  Steps for Github:
    git clone https://github.com/mattlang108/MonteCarlo.git #review to get accurate link
    cd montecarlo
    pip install .

  1. Import the Information
    import numpy as np
    from montecarlo import Die, Game, Analyzer
  
  2. Create a Die object
    die_faces = np.array([1, 2, 3, 4, 5, 6])
    die = Die(die_faces)
  
  3. Change the weight of a specific face
    die.change_weight(3, 2.0)
  
  4. Create a Game object with multiple dice
    game = Game([die])
  
  5. Play the game by rolling the dice multiple times
    results = game.play(10)
    print("Game Results:\n", results)
  
  6. Analyze the results using the Analyzer
    analyzer = Analyzer(game)
    jackpot_count = analyzer.jackpot()
    print(f"Number of jackpots: {jackpot_count}")
    face_counts = analyzer.face_counts_per_roll()
    print("Face counts per roll:\n", face_counts)


API: #Review to ensure accuracy
  Die class
    Attributes:
      faces (numpy.ndarray): The faces of the die.
      weights (numpy.ndarray): The weights associated with each face. Defaults to 1.
      df (pandas.DataFrame): DataFrame containing the faces and their associated weights.
    Methods:
      __init__(self, faces: np.ndarray)
        Description: Initializes the Die object with a set of faces and default weights.
        Arguments:
          faces (np.ndarray): A NumPy array containing the faces of the die.
        Raises:
          TypeError: If faces is not a NumPy array.
          ValueError: If the faces are not unique.
  change_weight(self, face, new_weight)
    Description: Changes the weight of a specific face on the die.
    Arguments:
      face (str or int): The face whose weight is to be changed.
      new_weight (float): The new weight for the face.
    Raises:
      IndexError: If the face is not found.
      TypeError: If new_weight is not numeric.
  roll(self, times=1)
    Description: Rolls the die a specified number of times and returns the outcome.
    Arguments:
      times (int): The number of times to roll the die.
    Returns:
      list: A list of rolled outcomes.
  show(self)
    Description: Shows the current faces and their associated weights.
    Returns:
      pandas.DataFrame: A DataFrame showing the faces and weights of the die.
      
Game class
  Attributes:
    dice (list): A list of Die objects.
    play_data (pandas.DataFrame): Stores the results of the rolls.
  Methods:
    __init__(self, dice: list)
      Description: Initializes the game with a list of dice.
      Arguments:
        dice (list): A list of Die objects.
      Raises:
        TypeError: If any element in dice is not a Die object.
        ValueError: If the dice do not have the same faces.
  play(self, num_rolls)
    Description: Rolls all dice a specified number of times and stores the results.
    Arguments:
      num_rolls (int): The number of times to roll all dice.
    Returns:
      pandas.DataFrame: DataFrame of the roll outcomes.
  show_results(self, format='wide')
    Description: Returns the results of the rolls in either wide or narrow format.
    Arguments:
      format (str): The format of the result, either 'wide' or 'narrow' (default is 'wide').
    Returns:
      pandas.DataFrame: DataFrame with the results in the specified format.
    Raises:
    ValueError: If an invalid format is specified.
    
Analyzer class
  Attributes:
    game (Game): The Game object that stores the results to analyze.
    results (pandas.DataFrame): Stores the results of the game rolls.
  Methods:
    __init__(self, game: Game)
      Description: Initializes the analyzer with a game.
      Arguments:
        game (Game): A Game object.
      Raises:
        ValueError: If the input is not a Game object.
  jackpot(self)
    Description: Computes the number of jackpots (all faces the same).
    Returns:
      int: The number of jackpots.
  face_counts_per_roll(self)
    Description: Computes how many times each face is rolled in each event.
    Returns:
      pandas.DataFrame: A DataFrame with face counts for each roll in wide format.
  combo_count(self)
    Description: Computes distinct combinations of faces rolled and their counts.
    Returns:
      pandas.DataFrame: A DataFrame with combinations and counts, MultiIndex format.
  permutation_count(self)
    Description: Computes distinct permutations of faces rolled and their counts.
    Returns:
      pandas.DataFrame: A DataFrame with permutations and counts, MultiIndex format.

