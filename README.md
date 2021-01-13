# Prisoner's-Dilemma
This project was to look at the strategies of the repeated prisoner's dilemma, and how they functioned not only in a population but how that population changed over time if new automata (representing the agents) were added in to replace less successful automata.

The prisoner's dilemma is a non zero-sum 2 player game, where each player is trying to maximise the points they have by playing either Cooperate (C), or Defect (D) with the points they get dependent on the same action performed by the other player. 

![normal form](https://github.com/nebnebben/Prisoner-s-Dilemma/blob/main/images/prisoners-dilemmaquad.jpg)

This means that an optimal choice will change depending on what the opponent will play. Defecting will guarantee points, but it will get almost nothing if the opponent also defects. However cooperating will only be successful is the other player also cooperates.

Furthermore the decisions might change over time if both agents play against each other multiple times, instead of just once. In this scenario they will have knowledge (up to a certain point) of the other agent's past actions so that can be used to inform their decisions. An agent can be represented by a finite state automata like this:

![fsa](https://github.com/nebnebben/Prisoner-s-Dilemma/blob/main/images/prisonersdilemmafsaexample.png)

It has different states containing actions, with the connections between the states being the choices made depending on the opponent's actions. To get a sense of how each finite state automaton (FSA) performs against each other, generally around 100 moves are simulated and then the total scores are output for each FSA. But since success depends on the other FSA's strategies, it becomes more interesting when looked at when in a population with many FSAs.

To get a bit deeper I looked at populations of FSA, composed of several different FSA that all competed against each other in a round-robin tournament and determining their individual fitness by averaging the points they gained through this. So FSA 1 played FSA 2...50, FSA 2 played 1, 3...50 and so on with the points gained being averaged. This showed how successful each FSA was withinin their specific population, as the success of an FSA depends entirely on how other strategies respond to it. 

Then I started to look at what happened when a population of FSAs changed over time, examining how different strategies emerged depdendent on the actions of other FSAs. That's what I did below, representing each FSA population (with 50 FSAs) as a dot, going from blue as the first generation to dark red as the last. Each FSA was randomly generated, and once each FSA had been played against each other I discarded the lowest 5% scoring FSAs and replaced them with random new ones. While I did so, I mapped the average population score of the FSAs (which could range from 100 to 300) and the average percentage of cooperative states in each FSA to see how the population make up and strategies would change over time. These were the results:

![Image of Results](https://github.com/nebnebben/Prisoner-s-Dilemma/blob/main/images/prisonersdilemma1.png)

As can be seen, defect heavy FSAs dominate early against the initial FSAs which all have random strategies as randomness means you cannot 'punish' your opponent for defecting and against any single action defecting will always get a higher score. Early cooperative strategies lose out entirely. However, over time cooperative strategies start to emerge as they are more reliably effective if the other FSA is also cooperative. This starts to push out the defect heavy FSAs as the less random new FSAs punish them for defecting and gain more points overall by cooperating with similar FSAs. However this cooperative nature is conditional, as successful cooperative agents cooperate by default but punish defecting by defecting in turn. Amazingly, through purely random sampling of agents, cooperative strategies start to emerge and dominate. Meaning that towards the last generations, though each FSA is still entirely self interested, the average population score gets close to the optimum (300) as cooperative strategies within the population just become more effective. With any new defect heavy FSAs still being punished to keep them out of the population. 

However, this wasn't a given as in some tests populations that became too defect heavy meant that cooperative states never got a chance to get a foothold. As each point there weren't enough cooperative FSAs within the population for it to be worth cooperating at all. 
