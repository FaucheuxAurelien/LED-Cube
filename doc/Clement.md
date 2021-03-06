

# Seance du 21 décembre 
J'ai décidé de me mettre en binome avec Aurélien Faucheux pour le projet.
Pendant le reste de la séance j'ai cherché une idée de projet sur internet via les liens donnés par mail par M.Masson.
En fin de séance on était sur à 90% de partir sur la création d'un cube à led, reste à savoir quel taille

# Séance du 10 janvier
J'ai cherché différents cube de différente taille, différente maniere de réaliser un cube, comment se balader dans le plan et les étages pour sélectionner une seule led pour finalement choisir la taille du mon futur cube : un cube 5x5x5, donc 125 leds
Un cube de cette taille requiert plus d'I/O que l'arduino n'en possède, j'ai donc cherché à résoudre ce probleme et je me suis rendu compte que j'allais surement avoir besoin de composants tels que les shift register et un multiplexeur
J'ai donc cherché à savoir comment fonctionne un 74hc595 ou un unl2803 
J'ai, entre autres, consulté les liens suivant : 
https://openclassrooms.com/forum/sujet/projet-d-un-cube-a-led-75491
http://www.robot-maker.com/forum/topic/6328-leds-cube/
https://openclassrooms.com/forum/sujet/projet-cube-led?page=2
http://www.instructables.com/id/5x5x5-LED-cube-run-on-Arduino-Uno/
https://www.bing.com/images/search?view=detailV2&ccid=mDnaEv93&id=E9265543A488660AEDE4551BBB910C2AD4E86436&thid=OIP.mDnaEv93GkgXteTmqBNfBgHaM2&q=shift+rehister+matrix&simid=608039591611467589&selectedIndex=0&ajaxhist=0
https://www.bing.com/images/search?view=detailV2&ccid=KWNH1N4n&id=514DF6A93A7A626B4795A2A75069D7A43DC02D80&thid=OIP.KWNH1N4njUhnOfBRv4BZ5wHaEB&q=74hc595&simid=608042937370414697&selectedIndex=16&ajaxhist=0

# Séance du 17 janvier
Nous avions un probleme avec le shift register : si on considère un plan de led et qu'on veut allumer la led tout en haut à gauche et tout en bas à droite, cela allumera aussi la led tout en haut à droite et tout en bas à gauche

Nous avions un probleme avec le shift register : si on considère un plan de led et qu'on veut allumer la led tout en haut à gauche et tout en bas à droite, cela allumera aussi la led tout en haut à droite et tout en bas à gauche (les 4 coins finalement). On s'est rendu compte que ce probleme n'en etait pas un, il suffit de jouer sur la persitance rétinienne.
Nous avons donc chercher à comprendre le fonctionnement d'un shift register en réalisant le schema suivant :
![shift register](http://fritzing.org/media/fritzing-repo/projects/s/shift-register-74hc595/images/multiplexing-shiftregister_Steckplatine.png)
Nous avons ensuite décider qu'on realisera d'abord un cube prototype 3x3x3 et non un 5x5x5 directement, de façon à comprendre parfaitement le fonctionnement d'un calcul et ne pas faire d'erreur lors de la realisation du 5x5x5

# Séance du 24 janvier

J'ai passé une bonne partie de la séance à ecouter les présentations de mes camarades de classe. J'ai ensuite découvert l'existence de led, les APA106, qui permettent d'éviter l'utilisation de multiplexeur en étant toutes connectés entre elles et qui ont l'avantage d'être RGB et deja polies. J'ai ensuite cherché si un cube avec ces led avait deja été fait.


On a commandé des leds ws2812D F8 (8mm de diametre)(https://datasheet.lcsc.com/szlcsc/WS2812D-F8_C139126.pdf) qui sont des led programmables semblables aux APA106. Elles comportent 4 pattes : VDD, GND, DIN chargé de recupérer le signal d'entrée,et enfin DOUT qui est la patte par laquelle l'information quitte la led. Ces led se branchent les unes à la suite des autres de sorte à ce qu'elles se transmettent l'information. On relie le DOUT d'une led au DIN de la led suivante et ainsi de suite. On envoie un signal sur le DIN de la premiere led et elle transmet le signal à sa voisine qui elle meme transmet à sa voisine etc... On cherche alors des cube qui ont été fait avec ces led sans grand succès.



# Librairie
Ces led ne fonctionnent donc pas comme celles qu'on a pu utiliser en td, elles requierent une libraire arduino spéciale capable de les diriger. Nous sommes donc parti à la recherche d'un tel librairie. On trouve sur internet la libraire "adafruit neopixel" qui est dite capable de diriger les leds APA106, les notres étant semblables nous essayons d'utiliser cette libraire sur une led, l'objectif étant d'allumer une led afin de mieux s'apprivoiser le focntionnement de la led et de la librairie. Mais après moulte essais, pas moyen d'en allumer une, on en grille plusieurs! On repart alors chercher sur internet et on tombe sur des forums disant que les librairais controlant les APA106 ne controlent pas nécessairement les ws2812d , on tombe également sur differents montage censé faire la meme chose (en l'occurence allumer une (ou +) led). Plus on fait de recherches, plus on apprend tout et son contraire. On découvre la libraire FastLED supposée etre LA libraire des ws2812 mais encore une fois, aucun résultat. On se met alors à douter de tout, du cable USB utilisé pour relier l'arduino, de la carte arduino elle meme, on vérifie un millier de fois chaque montage avant dappliquer VDD de peur d'endommager la led.On a fini pas decourvir que c'etait le microprocesseur à l'interieur des leds qu'on souhaitait allumer qui etaient grillés, sans que cela se voit de l'exterieur (pas de trace marron comme lorsqu'on a grillé des led précedemment). Finalement la libarire Adafruit Neopixel fonctionne très bien pour nos led. On se docmente sur les fonctions de cette nouvelle librairie pour comprendre les programmes qu'on utilise et en réaliser nous meme. On se lance alors dans la réalisation de quelques petits programmes histoire de maitriser cette librairie.

Maintenant que l'on sait faire fonctionner nos led, on cherche à savoir comment construire notre cube, comment relier toutes les led d'un etage entre elles tout en gérant de facon efficace leurs pattes vdd et gnd. Les led ayant 4 pattes chacunes, on ne peut se permettre la présence de 4 fils par led soit 100fils juste pour un étage...Comment réduire un maxmimum le nombre de fils utilisés? On trouve très peu de page detaillé sur la réalisation d'un cube utilisant nos led, ce qui rend l'avancé du projet difficile.

Nous avions pensé à plusieurs methodes de construction mais nous avons finit pas adopter celle qui est utilisé sur ce site : http://www.instructables.com/id/Cubic-Art/
On souhaite alors s'inspirer de la façon de faire developpé sur ce site, ce qui se traduit essentiellement par le souhait de réaliser un gabarit comme celui ci : 
![shift register](https://cdn.instructables.com/F41/NXGY/JCAUOQL9/F41NXGYJCAUOQL9.LARGE.jpg)
Ce gabarit permet la construction d'un étage.
Le principe est le suivant : on met les chapeaux des 25 led dans les cylindres puis on plie les pattes DIN et DOUT comme ici : ![shift register](https://cdn.instructables.com/FMY/DROO/JCAUOPFP/FMYDROOJCAUOPFP.LARGE.jpg) 
De cette façon, toutes les leds du plan sont les unes à la suite des autres.
Pour gérer les pattes VDD et GND, on utilise des "bus" comme ici : ![shift register](https://cdn.instructables.com/F25/HG6I/JC6K020O/F25HG6IJC6K020O.LARGE.jpg)
Puis on relie les vdd et gnd des led au bus, ce qui donne ceci : ![shift register](https://cdn.instructables.com/FSA/WMC8/JCGK5VC1/FSAWMC8JCGK5VC1.LARGE.jpg)
Appliqué à tout le plan : ![shift register](https://cdn.instructables.com/F50/TPCS/JCGK9WHD/F50TPCSJCGK9WHD.LARGE.jpg)
On remarque que si 'lon réalise tous les étages comme celui ci dessus, lorsqu'on va vouloir relier le DOUT final d'un étage au DIN initial de l'étage supérieur, il va falloir un long fil qui va travserser la largeur du cube. Pour contrer ce probleme, les étages impairs se font d'une différente maniere que leurs collègues pairs.
Il suffit d'inverse le sens de circulation entre etage pair et impair.
On a alors un étage impair comme celui : ![shift register](https://cdn.instructables.com/FSW/8IJB/JCKUHGRF/FSW8IJBJCKUHGRF.LARGE.jpg?auto=webp&width=645)
et un étage pair : ![shift register](https://cdn.instructables.com/F1V/SCFA/JCKUHGN3/F1VSCFAJCKUHGN3.LARGE.jpg)
Cela permet au DOUT final d'un étage d'etre juste en dessous du DIN inital de l'etage suivant : 
![shift register](https://cdn.instructables.com/FGC/I52G/JCKUI9BG/FGCI52GJCKUI9BG.LARGE.jpg?auto=webp&width=933)


Mais les choses ne sont pas passés comme prévu,l'imprimante 3D du FabLab a totalement raté l'impression :
sur le logiciel : 
<img src="https://user-images.githubusercontent.com/35264662/40738802-cbb2ade6-6444-11e8-816e-c1128990ea4d.jpeg" alt=surLogiciel />
en réalité : 
<img src=https://user-images.githubusercontent.com/35264662/40738803-cc3d6a9e-6444-11e8-9c6e-b767ad13291b.jpeg />

Nous avons donc changé de methode. Nous avons pris une planche de bois dans laquelle nous avons fait des trous destiné à acceuillir les chapeaux des leds afin de construire une etage facilement, en suivant les meme schemas pour les bus VDD et GND.
<img src="https://user-images.githubusercontent.com/35264662/40739299-1c8844be-6446-11e8-97aa-58637874a088.jpg" />

Nous avons construit 5 étages à l'aide de cette planche de bois. Ensuite, nous avons testé chaque plans un par un pour verifier le bon fonctionnement de l'étage.
<img src="https://user-images.githubusercontent.com/35264662/40739302-1cf1f990-6446-11e8-9281-1833d4ba228f.jpg" />
Sur 5 étages, 3 ont parfaitement fonctionné , l'allumage se faisait correctemnt. Mais sur les 2 autrs étages, l'allumage est aleatoire, les 3-4premieres leds s'allument comme il faut mais les autres leds sont "bugé". La transmission de l'information entre les leds se fait tres mal. Selon nous le probleme vient de la basse qualité de l'étain utilisé pour les soudures ainsi que des tiges de fer utilisées pour les bus VDD et GND qui sont quelque peu inadaptés à la soudure. En effet, l'étain fondu glisse sur les bus comme des gouttes d'eau sur un k-way.Nous détaillerons davantage dans le rapport.
Nous avons ensuite assemblé les 3 étages fonctionnels, ils fonctionnent mais pas "aussi bien" que lorsqu'ils etaient separé, ils bug un peu de la meme maniere que les etages infonctionnels, on a malgré tout reussi à avoir tous les étages allumés en meme temps.
Nous avons assemblé les 5 étages et les 2 premiers sont fonctionnels(meme si ils ne s'allument par correctement lorsqu'on applique vdd et gnd à certains endroit sur le cube) , le 3e étage est bugué, l'allumage est aleatoire, les 2 derniers étages qui sont les 2 étages, qui ne fonctionnaient pas coreectement tout seul, ne s'allument que rarement, encore une fois cela depend des emplacement ou sont appliqués vdd et gnd sur le cube. Les 2 premiers etages s'allument meme lorsque on applique vdd et gnd sur les bus du dernier etage, on en deduit que les bus sont bien reliés, le probleme vient des liaisons entre les led. 
