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

Changement de plan :
On va utiliser des led programmables RBG, les WS812D-F8. Ces led ont l'avantage d'avoir une résitance intégrée, et se transmettent l'information d'une led à la suivante. Ces led ont 4 pattes : Dout, Vdd, gnd, Din. On donne l'information à la 1ere led par la patte Din qui sortira par Dout qui est relié au Din de la led suivante.
Pour pragrammer ces led on utilise une la librairie Arduino **Adafruit neo-pixel** 

![Shift Register](https://user-images.githubusercontent.com/34739496/40749791-7e43b124-6465-11e8-86cf-8e2671006f6c.png)
![Shift Register](https://user-images.githubusercontent.com/34739496/40749800-8212b714-6465-11e8-8667-2113e03961ed.png)
Construction du cube : 
2 méthodes : 
  - une consistant à créer 25 colonnes de 5 leds chacune. Chaque colonne est consititué de deux tiges, une étant relié à Vdd et l'autre à GND. J'avais envisagé de faire fonctionner les 5 plans independament et ainsi avoir 5 résistances avec 5 Din, chaque led d'un plan étant rélié à la suivante sur la colonne voisine à la même hauteur. Les distances sont regles grace à la création d'un gabarit, constistué de 25 trous equidistant. **Problemes** : précision du cube ( plan droit , led espacé autant en longueur qu'en hauteur) soudure, et les toutes les led sauf celles du derniere étage auraient des toges sur les bords nuisant à la diffusion.
  - construction de chaque  plan selon une méthode plus simple trouvé sur internet (plan pair et impair)
  
Création d'un gabarit à la decoupeuse laser après l'échec de l'imprimante 3D.
Fabrication des 5 plans avec le gabarit pour un total d'à peu près 300 soudures.
Test des plans de led : 3 fonctionnent bien tandis que les 2 autres s'allument un peu aléatoirement. on refait donc quelques soudures et quelques remplacements de led. Le résultat reste inchangé...
Empilement des 5 étages : les 2 premiers plans en partant du bas fonctionnent bien ensemble malgré quelques beug (selon l'endroit on l'applique vdd cela marche plus ou moins bien)
![Shift Register]()
Création de nouveau pattern impossible tant que le cube n'est pas **stable** et **fonctionnel**.
Absence de connectivit bluetooth.
