# Multiclass CNN
- Multiclass classification:
	- Einander ausschließende Klassen
- Softmax benutzen für multiclass classification
- Loss function for multy class classification:
	- Cross entropy = $- \sum_{c=1}^{M} y_{i,o} \log(p_{i,o})$
- $y$ = True label
- $a$ = predicted label
- $z$ = w * x + b
- $a$ = f(z)
- learning rate = the step size in the gradient descent, we can start with big steps and then make them smaller and smaller
- backpropagation = Wird verwendet um den Fehlerbeitrag jedes einzelnen Neurons nach Verarbeitung eines Trainingsbeispiels zu berechnen und dann die Gewichte anzupassen
- $z^{L} = w^{L} a^{L-1} + b^{L}$; $a^{L} = f(z^{L})$; $C_{0}(\dots) = (a^{L}-y)^{2}$