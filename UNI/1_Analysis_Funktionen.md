# Funktionen
:funktionen:injektiv:surjektiv:bijektiv:inverse_abbildung:extrema:hop:tip:

## Injektivität und Surjektivität
- Injektiv: $f(x): A \to B$
	- $\iff \forall_{x,y \in A} \land x \neq  y \implies f(x) \neq f(y)$
	- $\iff f(x) = f(y) \implies x = y$ 
	- $\iff \forall_{y \in B} \big(f^{-1}\{y\} = \emptyset \lor \exists!_{x \in A} f(x) = y \big)$
- Surjektiv: $f(x): A \to B$ 
	$\forall_{y \in B} \exists_{x \in A} f(x) = y$
- Bijektiv: $\iff f \text{ injektiv} \land f \text{ surjektiv}$

## Linksinverse & rechtsinverse Abbildungen
Zur Wiederholung: $\text{Id:} A \to A \text{ ,} \text{I.d}(x) := x$, wird Identitätsfunktion genannt

- Rechtsinvers: Wenn $f: A \to B$, dann muss es $g: B \to  A$  geben, sodass $(f \circ g)(x) = f(g(x)) = \text{I.d}_B$
- Linksinvers: Wenn $f: A \to  B$, dann muss es $g: B \to A$ geben, sodass $(g \circ f)(x) = g(f(x)) = \text{I.d}_A$
- $g$ heißt *invers*, wenn $g$ rechts- und linksinvers ist

- *Rechtsinvertierbarkeit* $\iff$ *Surjektivität*
- *Linksinvertierbarkeit* $\iff$ *Injektivität*
- *Invertierbarketi* $\iff$ *Bijektivität*
- *Str. Monotonie* $\implies$ *Injektivität*


## (Streng) Monoton steigende & fallende Funktionen
- $f: A \to B$ heißt *isoton* gdw. $\forall_{x,y \in A}(x < y \implies f(x) \le f(y) \text{ bzw. } \underbrace{f(x) < f(y)}_{\text{streng isoton}})$
- $f: A \to B$ heißt *antiton* gdw. $\forall_{x,y \in A}(x < y \implies f(x) \ge f(y) \text{ bzw. } \underbrace{f(x) > f(y)}_{\text{streng antiton}})$
- $f: A \to B$ heißt *monoton*, wenn $f$ (str.) isoton oder antiton

## Max, Min, Sup, Inf
- *Obere Schranke:* $\forall_{b \in B} x \le b$
- *Untere Schranke:* $\forall_{b \in B} b \le x$

- *Maximum* $x$ heißt Maximum von $B$, wenn $x$ obere Schranke
- *Minimum* $x$ heißt Minimum von $B$, wenn $x$ untere Schranke

- *Sup* kleinste obere Schranke
- *Inf* größte untere Schranke


## Minima Maxima Extrema
- $f$ hat globales *Minimum* in $z \in M$ g.d.w:
	- $\boxed{\forall_{w \in M \backslash \{z\}} f(z) \le f(w) \text{ bzw. } \underbrace{f(z) < f(w)}_{\text{für streng}} }$
- $f$ hat globales *Maximum* in $z \in M$ g.d.w:
	- $\boxed{\forall_{w \in M \backslash \{z\}} f(z) \ge f(w) \text{ bzw. } \underbrace{f(z) > f(w)}_{\text{für streng}} }$
Wenn $f$ hat *(str.)* globales *Min/Max* $\implies f$ hat *(str)* globalen Extremwert  

- $f$ hat lokales *Min* in $z \in M$ g.d.w:
	- $\boxed{\exists_{\epsilon > 0} \forall_{w \in (B_{\epsilon}(z)\cap M) \backslash \{z\}} f(z) \le f(w) \text{ bzw. } \underbrace{f(z) < f(w)}_{\text{für streng}} }$

- $f$ hat lokales *Max* in $z \in M$ g.d.w:
	- $\boxed{\exists_{\epsilon > 0} \forall_{w \in (B_{\epsilon}(z)\cap M) \backslash \{z\}} f(z) \ge f(w) \text{ bzw. } \underbrace{f(z) > f(w)}_{\text{für streng}} }$

Wenn $f$ hat *(str.)* lokales *Min/Max* $\implies f$ hat *(str)* lokalen Extremwert  
