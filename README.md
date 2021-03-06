# AI_Genetic-Knapsack

Uses a GUI to show results from a knapsack problem solved using genetic algorithms

Open the "Graphed-Test-Results.pdf" for a visual.
PS4 Data.xlsx can also show more detail on results.
Not all results are shown and many more tests have been done with other sample data.
The testData text files show some of the data used.

As each item(gene) is read in from a file it calculates and stores a variable that I called a local fitness value which is: value/weight. This is the value my list of items gets sorted by.

In both the baseline and improved algorithms my initial population is set by randomly setting half of the bit representations in a BitSet to show what items have been selected. The difference in my improved population initialization is that I can set random bits to the significant bits with high local fitness values. In my case I used the upper half of the BitSet since that's where my high scoring local fitness items are. This starts the population in a decent direction but doesn’t necessarily guarantee things won’t get changed along the way or that these bits will be used for finding solutions.

Another improvement is when a pair of Traits(parents) are selected for breeding, one is still chosen randomly but the other is selected from the top half of the population. This may seem illogical since this would guide us to getting stuck at a local maximum sooner than later, but this is exactly what I intended. This allows me to know faster when a local maximum may have been found because the variance will be near 0. I have a variance counter that if 3 iterations result in a variance < 1 then my population will be cleared and restarted. With a large mutation percentage one could increase this variance counter’s range since hitting 0 variance is more slim. Before the population is restarted it saves the highest scoring Trait just in case this is the global maximum or the best local it could find during the algorithm.

I realize instead of restarting my population I could have from the beginning started with multiple threads of populations and work through them in unison. I know this is a great solution but I felt that this was boring and kind of a cheap way out for the assignment in my opinion.
I chose to represent results of only two test files in the graphs. The first one shows the results of a 50 item file (“testData_1.txt”) and the second one shows results of a 22 item file (“testData.txt”). These both have balanced data items. Some of my other files had worst case data but still my improved algorithm was superior to the baseline. I did not change how mutation worked since “improved” still won but results did come close when mutation was high. I could have used some kind of annealing process on high mutation. I did not show results for lowering the min fitness cap so it could be reached but my improved algorithm reached this cap faster and more often on other tests. On some results the baseline never reached the cap.
