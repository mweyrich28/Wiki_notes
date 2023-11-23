# MATERIAL
I) Vorlesung →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Slides/Bioinf2-Lect08-HMM.pdf)
II) Tutorium Slides: [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Tutorien/7_Ex_EiB2_hidden_markov_modelsstudents.pptx.pdf)
# Markov-Chain
:markov_chains:

Stochastic process for modeling state changes by knowing a limited history

"What came before? With this history, we can say it's very likely 'X' comes next"

![Example](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/HMM/chain_example.png)

*CHARACTERISTICS:*
- Memoryless →  only the current state matters, no matter how we got there (even if we had like 1000 x 0.001 before, it doesn't matter)
- Homogeneous = same transition probabilities for all time steps: $P_{ij} = P(X_{n+1} = j|X_{n} = i) = P(X_{1} = j| X_{0} = i)$
- Time-discrete / stationary process
- Transition matrix (stochastic matrix →  row sum = 1)

*STATE CHARACTERISTICS:*
- _Recurrent_: chain will return to the state in finite time: ![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/HMM/recurrent.png)
- _Transient_: state is reached at most once: ![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/HMM/transient.png)
- _Absorbent_: if the state is reaced it will never leave again: ![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/HMM/absorbent.png)

## Order of Markov-Chain
:order_of_markov_chains:
How many states do we consider? (1st order: only the last state, 2nd order: last two states, ...): ![1st vs 2nd order](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/HMM/2nd_order.png)
- 0th order: Position weight matrix (PWM) →  because all values are independent from each other
- 1st order: dependent on one position (last state): 
	- ![First order matrix](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/HMM/1st_order.png)
	- ![First order sequence](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/HMM/1st_order_2.png)
- 2nd order: dependent on two positions (last two states): 
- etc.
nth order: ![Exercise](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/HMM/nth_ord_ex.png)

$Y =$ Base an Pos $t$, $Q = \{A,G,C,T\}$
Transition matrix: alle möglichen Zustände die wir beschreiben können

# Hidden Markov Models
:hidden_markov_models:
- Generalization of Markov Chains
- Two types of states: 
	- _Hidden states_ (HMM states): not directly observable:
		- transition probabilities (going from S1 →  S2)
	- _Observable states_ (emission states): directly observable:
		- emission probabilities (probability of seeing a certain base in a certain state)
→  ![HMM](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/HMM/HMM.png)
- States and transitions depend on only the previous state (1st order Markov Chain)

Beispiel:
Wir haben Zustände die wir indirekt lernen müssen, wie wahrscheinlich ist es von Zustand S1 →  S2 überzugehen:
Im Genom, wenn wir uns eine Sequenz zum ersten mal sehen, wissen wir ja nicht, ob diese aus einem Gen stammt oder nicht

## Three classic HMM Problems
:three_classic_hmm_problems:hmm_problems:

### Evaluation
Wie wahrscheinlich ist es, dass eine gegebene Sequenz mit diesem Modell X generiert wurde?
![Forward Algorithm](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/HMM/forwardAlg.png)
- Consider all possible paths through the model
- Wir summieren immer beide Kanten auf 
- Das macht man für alle Knoten, am Ende steht dann, wie wahrscheinlich sind wir in S,,1,, ode S,,2,, 
- Summieren = Wie wahrscheinlich wurde die Sequenz mit diese Modell generiert 
	- *P(Sequenz|Modell)*
- kann mit Bayes zu P(Modell|Sequenz) umbeschrieben werden 
- Wenn wir mehrere HMM haben, können wir sehen, welches Modell am wahrscheinlichsten sie Sequenz generiert hat

### Learning
:foward_backward_algorithm:baum_welch_algorithm:
Wir haben ein Modell X und k viele Sequenzen: Wie tunen wir die Parameter von X, damit es mit einer hohen Wahrscheinlichkeit die k Sequenzen
generiert hat?

Mit EM Algorithm *(Forward Backward Algorithm or Baum Welch Algorithm)* 
Ein Algorithm der den Vorderen Teil betrachtet, der andere betrachtet den hinteren Teil $a_{k}(i)$ = Vorwärts, $b_{k}(i)$ = Hinterer Teil 
Das machen wir für alle Übergänge (S,,1,,→  S,,1,, , S,,1,, →  S,,2,,, ...) und vergleiche sie, dann übernehme ich den wahrscheinlichsten 
Übergang in mein neues HMM 
We need:
- Topology of HMM →  Wir brauchen ein Modell mit Zuständen (Wie kann es mein Problem beschreiben, welche Zustände machen Sinn?)
- Data
- Measuring the Fitness of our model:

*BAUM-WELCH ALGORITHM:*
1. Initialize the parameters (transition probabilities & emission probabilities) of the HMM randomly
2. E-step: Get new estimate of:
	- T(r|q) transition probabilities: by counting the number of transitions from state q to state r for all paths and sequences (weighted by the probability of the path)
	- P(x|q) emission probabilities: by counting the number of times x is aligned to the state q
3. M-step: Update the parameters of the HMM (replace old parameters with new ones)
4. Repeat steps 2 and 3 until convergence

- *ML: Maximum Likelihood* →  Given a set of sequences:
  find a model P(Sequence|Model) = $\prod_{j = 1}^{n} P(s_{j}|model)$ = max; s,,j,, = sequence j
- *Negative Log Likelihood* (NLL) score: $-\log_{10}(Sequenz|Modell)$
- *MAP: Maximum a posteriori* →  Given a set of sequences:
  find a model P(Model|Sequence) = $\frac{P(Sequence|Model) * P(Model)}{P(Sequence)}$ = max
  - P(Model) = prior probability of the model
  - P(Sequence) = probability of the sequence
  - P(Sequence|Model) = likelihood of the sequence given the model
  - P(Model|Sequence) = posterior probability of the model given the sequence

### Decoding
:viterbi_algorithm:
→  Fertiges Modell gegeben, Sequenz gegeben. Gesucht: in welchem State befinde ich mich an welcher Stelle?
   Wann befinden wir uns in Gen und wann nicht?
   *Viterbi Algorithm* →  rechnet Wahrscheinlichkeit für eine gewissen Zustand (Folie 28: LLHHHHLLL) 
   →  Dynamic Programming mit trace back matrix 
   S. 35 wäre der Zustand: HHHLLLLLL (trace back) 
   →  Wir haben versteckte Zustände in HMM, diese wollen wir vorhersagen. Input: fertiges Modell, Output: was ist die wahrscheinlichste Reihenfolge von Zuständen
   
*VITERBI ALGORITHM EXERCISE:*
- Note: Apply log2 to all probabilities →  log(x * y) = log(x) + log(y) →  we can sum instead of multiply →  not so small numbers
![Exercise](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/HMM/decoding_ex.jpg)

## HMM Applications
- Coding and non-coding regions in DNA determination
- Modeling of protein-binding sites in DNA
- Modeling of protein superfamilies
- Protein secondary structure prediction
- Gene prediction
- Chromatin states
- etc.

## HMM in Sequence analysis
- DNA binding sites
- Gene structure prediction
- Gene identification
- Protein family identification
- CpG islands
- etc.

## GENSCAN
- 27 States and 46 transitions
- Needs to be mirrored for the reverse strand
![HMM of GENESCAN with 27 States and 46 transitions](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/HMM/genescan.png)
(die grüne Achse spiegelt)

## Profile HMMs
:hmmer:
- Modelliert Motifs:
![HMMER](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/HMM/hammer.png)
Motifs sind nicht immer gleich lang, z.B. kann eine Base eingefügt/gelöscht werden 
Parameters:
- m := match state (corresponds to positions in a protein or columns in a multiple sequence alignment)
- i := insert state (corresponds to insertions in a protein or gaps in a multiple sequence alignment)
- d := delete state (corresponds to deletions in a protein or gaps in a multiple sequence alignment)
- P(x|q) := emission probabilities (probability of seeing x in state q)
- T(r|q) := transition probabilities (probability of going from state q to state r)

## HMMs for protein sequence generation
Assumtions:
- Markov assumption: the probability of a state depends only on the previous state
- Stationary assumption: the probability of a state are independent on time
- Output independence assumption: the probability of an output is independent of the previous outputs

## In Short
- Good theoretical basis
- Provides good solutions for:
	- Sequence alignment
	- Sequence generation
	- Sequence classification

## Advantages
1. Statistics:
	- HMMs are based on statistics
	- Freedom to manipulate the parameters
2. Modularity:
	- HMMs can be combined to form more complex models
3. Transparency:
	- HMMs are easy to understand
	- HMMs are easy to visualize
4. Incorporation of prior knowledge:
	- HMMs can be easily modified to incorporate prior knowledge

## Disadvantages
1. States independece:
	- States are supposed to be independent
	- This usually does not hold in reality
	- Relations can be local
2. Local maximas:
	- HMMs can get stuck in local maximas
	- This can be avoided by using multiple random initializations
3. Overfitting:
	- HMMs can overfit the data
	- This can be avoided by using regularization
4. Slow:
	- We basically always "enumerate all possible paths" →  bad time complexity
