
)
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
Nous avions un probleme avec le shift register : si on considère un plan de led et qu'on veut allumer la led tout en haut à gauche et tout en bas à droite, cela allumera aussi la led tout en haut à droite et tout en bas à gauche (les 4 coins finalement). On s'est rendu compte que ce probleme n'en etait pas un, il suffit de jouer sur la persitance rétinienne.
Nous avons donc chercher à comprendre le fonctionnement d'un shift register en réalisant le schema suivant :
![shift register](http://fritzing.org/media/fritzing-repo/projects/s/shift-register-74hc595/images/multiplexing-shiftregister_Steckplatine.png)
Nous avons ensuite décider qu'on realisera d'abord un cube prototype 3x3x3 et non un 5x5x5 directement, de façon à comprendre parfaitement le fonctionnement d'un calcul et ne pas faire d'erreur lors de la realisation du 5x5x5

# Séance du 24 janvier
J'ai passé une bonne partie de la séance à ecouter les présentations de mes camarades de classe. J'ai ensuite découvert l'existence de led, les APA106, qui permettent d'éviter l'utilisation de multiplexeur en étant toutes connectés entre elles et qui ont l'avantage d'être RGB et deja polies. J'ai ensuite cherché si un cube avec ces led avait deja été fait.


On a commandé des leds ws2812D F8 (8mm de diametre)(![shift register](https://datasheet.lcsc.com/szlcsc/WS2812D-F8_C139126.pdf) qui sont des led programmables semblables aux APA106. Elles comportent 4 pattes : VDD, GND, DIN chargé de recupérer le signal d'entrée,et enfin DOUT qui est la patte par laquelle l'information quitte la led. Ces led se branchent les unes à la suite des autres de sorte à ce qu'elles se transmettent l'information. On relie le DOUT d'une led au DIN de la led suivante et ainsi de suite. On envoie un signal sur le DIN de la premiere led et elle transmet le signal à sa voisine qui elle meme transmet à sa voisine etc...



Ces led ne fonctionnent donc pas comme celles qu'on a pu utiliser en td, elles requierent une libraire arduino spéciale capable de les diriger. Nous sommes donc parti à la recherche d'un tel librairie. On trouve sur internet la libraire "adafruit neopixel" qui est dite capable de diriger les leds APA106, les notres étant semblables nous essayons d'utiliser cette libraire sur une led, l'objectif étant d'allumer une led afin de mieux s'apprivoiser le focntionnement de la led et de la librairie. Mais après moulte essais, pas moyen d'en allumer une! On repart alors chercher sur internet et on tombe sur des forums disant que les librairais controlant les APA106 ne controlent pas nécessairement les ws2812d , on tombe également sur differents montage censé faire la meme chose (en l'occurence allumer une (ou +) led). Plus on fait de recherches, plus on apprend tout et son contraire. On découvre la libraire FastLED supposée etre LA libraire des ws2812 mais encore une fois, aucun résultat. On se met alors à douter de tout, du cable USB utilisé pour relier l'arduino, de la carte arduino elle meme, on vérifie un millier de fois chaque montage avant dappliquer VDD de peur d'endommager la led.
