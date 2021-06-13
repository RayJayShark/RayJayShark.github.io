# Enhancement Two: Algorithms and Data Structures

For the second enhancement, I focused on the algorithms and data structures aspects of the project.
I created an algorithm for scoring and comparing the poker hands using asynchronous code execution.

## Narrative

Click [here](https://rayjayshark.github.io/Narratives/AlgorithmsDataStructuresNarrative_JoshuaRay.pdf) to access the narrative I created with this enhancement.

## Code

Click [here](https://rayjayshark.github.io/Enhancements/PokerBot_AlgorithmsEnhancement.zip) to find the zip archive of the project after the enhancement.
After being extracted, the project can be openned in an IDE of your choice and compiles.
This enhancement includes a test project used to ensure the scoring algorithm works correctly.

### Important Examples

#### CalculateScore()

The calculate score method is called when a 5-card Hand object is instantiated. This uses other helper methods to give the hand a score.

```cs
  private void CalculateScore()
  {
      // Sort cards for better comparing
      cards.Sort();

      CheckFlushStraight();   // Checks for a flush, straight, or related hand

      if (scoreTierOne > 0)
      {
          return;
      }

      CheckForMatches();      // Checks for pair, three of a kind, four of a kind, and full house

  }
```

#### Async Combinations and Scoring

This snippit is the beginning of the Showdown phase where the possible hands for each player need to be found and scored.
Since the hands are scored on instantiated, finding the combinations also finds the scores for each combination.
Async tasks are used to find these more efficiently.

```cs
  var hands = new List<List<Hand>>();     // All possible hands for each player
                    
  // Tasks finding possible hands
  var handTasks = new List<Task>();
  foreach (var player in _playerList)
  {
      var cards = new List<Card>(_river);
      cards.AddRange(player.GetHand().GetCards());
      handTasks.Add(Task.Run(() => hands.Add(Combinations.FindCombinations(cards)))); // Scores are calculated in constructor
  }

  // Wait for all hands to be created and scored
  Task.WaitAll(handTasks.ToArray());
```
