# Neural_Coreference_Resolution

![Intro_Ex1](/Images/Coref2.png)
![Intro_Ex2](/Images/Coref1.png)
** Files Used:**
* train.conll: training dataset containing 94,720 tokens (https://www.aclweb.org/anthology/D18-1016/)
* dev.conll: development dataset containing 94,336 tokens to evaluate your coref system’s performance

**B3**
We will be using B3 score to evaluate our model.

n ranges over all mentions in gold and system output
![B3](/Images/B3.png)


b3 takes in two Python dictionaries with identical keys; each dictionary maps the key to its cluster ID. It returns a tuple of three values: (precision, recall, F-score). The helper function b3_test will give you one piece of information for knowing whether your implementation is correct.

**Neural coref**
The neural coreference system that we’ll be using here is a mention-ranking model: for each mention mi in a document, the system looks to all previous mentions M = {m<sub>1</sub>, ...., m<sub>i-1</sub>} and makes a decision to either link m<sub>i</sub> to a single mention m<sub>j</sub> to leave it unlinked (in which case mi starts a new coreference chain). An entity cluster is the transitive closure of all such pairwise links (all mentions within an entity cluster are coreferent with each other). The core machinery in a mention-ranking model is a scoring function between two mentions:
<p style="text-align: center;">s(m<sub>i</sub>;m<sub>j</sub>)</p>
When making a decision to link mention mi to any of its antecedents, a mention-ranking model selects the argmax of this score over all candidate antecedents:
<p style="text-align: center;">m<sub>max</sub> = argmax s(m<sub>i</sub>;m<sub>j</sub>)</p>

If this max score is greater than 0, a link is created between mi and mmax; if, however, this max score is negative, then mi is not linked at all (and creates a new coreference chain).

![Neural_representation](/Images/Coref3.png)
