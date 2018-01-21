# Séance du 21 décembre :
Mon binôme (Clément) est moi avons cherché des idées de projet Arduino sur internet.
L'idée de faire un cube à LED nous a plu et nous avons commencé à nous renseigner sur le sujet.
# Séance du 10 janvier :
On a cherché des informations sur la construction du cube pour connaitre le matériel nécessaire, notamment le nombre de LED selon
la taille du cube, et sa complexité.
On pensait partir sur un cube 5x5x5 ou 6x6x6 mais cette taille demande beaucoup d'I/O sur la carte Arduino. On peut 
réduire ce nombre ce nombre en utilisant des shift register pour "matricer" un étage de LED.

![Shift Register](https://i.pinimg.com/236x/af/ba/fc/afbafc49a383502bb2e3017b994b4432--electronic-engineering-electronic-circuit.jpg)

Cependant ce système ne permet pas de faire tous les schémas de led souhaités

# Séance du 19 janvier :
On a trouvé une solution pour le problème des shift register : le problème n'en était pas réellement un car on peut jouer sur 
la persistance rétinienne pour allumer les led voulus.
On a également décidé de créer d'abord un prototype 3x3x3 pour comprendre les fonctionnements du cube et ne pas avoir à faire des tonnes de soudure pour se rendre compte qu'on a fait une erreur.
Pour comprendre le fonctionnement du shift register nous avons réalisé un circuit simple composé de 8 LED
http://www.zem.fr/decouverte-du-composant-74hc595-8-bit-shift-register/
