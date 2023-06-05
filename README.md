# Balise_Cohoma 

* CHARBONNIER Maëna
* MITCHEL Maël
* NGUYEN Denis
* SALOT Robin
* TESTUZ Lauriane

## $${\color{black}Présentation \space \color{black}du \space \color{black}{projet}}$$


   Ce projet est en collaboration avec des deuxièmes années qui participent au projet Cohoma, pour l'armée de terre. Ce projet
  est une compétition entre différentes écoles d'ingénieurs. Il consiste en la création d'un robot autonome s'adaptant à tout type de terrains. Ce robot doit lâcher des balises sur son chemin, elles ont pour but de le localiser. C'est ce sur quoi nous avons travaillé. 
   
   Une LED RGB est utilisée afin de montrer le niveau de batterie de la balise (vert: pleine charge, jaune: à moitié chargée et rouge: déchargée). Quatre LEDs bleues sont également utilisées afin de déterminer le niveau de connexion Internet de la balise. Il y a également un capteur infrarouge qui permet de communiquer avec le rover afin d'allumer la batterie. Enfin, on utilise un convertisseur Buck-Boost, qui est une alimentation à découplage qui convertit une tension continue en une autre tension continue de plus faible ou de plus grande valeur, mais de polarité inverse.
   
   
   
## $${\color{black}Cahier \space \color{black}des \space \color{black}{charges}}$$

* Rendre visible le niveau de batteries de la balise (sur la balise).
* Rendre visible le niveau de réception WIFI de la balise (sur la balise).
* Communication infrarouge entre une télécommande et la balise.
* Communication infrarouge entre le rover et la balise dans le but d'allumer la balise après lors de l'éjection.
* Alimenter la balise.

## $${\color{black}Datasheet}$$

* [Buck / Boost ](https://www.farnell.com/datasheets/1999134.pdf)
* [Diode (Buck) (1N4148)](https://4donline.ihs.com/images/VipMasterIC/IC/DIOD/DIOD-S-A0001754954/DIOD-S-A0001754954-1.pdf?hkey=6D3A4C79FDBF58556ACFDE234799DDF0)
* [Diode Schottky (FSV340AF)](https://www.mouser.fr/datasheet/2/308/FSV340AF_D-1810142.pdf)
* [Capteur IR TFBS4650](https://www.vishay.com/docs/84672/tfbs4650.pdf)
* [Interface USB/UART(CY7C64225-28PVXCT)](https://www.mouser.fr/datasheet/2/196/CYPR_S_A0003298042_1-3003715.pdf)
* [Encodeur/Decodeur IrDA MCP2120-I/SL ](https://docs.rs-online.com/4edb/0900766b814ada76.pdf)
* [Quartz pour Encodeur/Decodeur IrDA ABLS-7.3728MHZ-20-B-3-H-T ](https://www.mouser.fr/datasheet/2/3/abls-1664338.pdf)
* [Récepteur IrDA TSOP75338TT](https://www.mouser.fr/datasheet/2/427/tsop753-1767096.pdf)
* [Emetteur IrDA VSML3710-GS18](https://www.mouser.fr/datasheet/2/427/vsml3710-1766511.pdf)
* [Processeur STM32L412KBT6](https://www.mouser.fr/datasheet/2/389/stm32l412c8-1851177.pdf)
* [Quartz pour STM32 ABLS-16.000MHZ-20-B-3-H-T:](https://www.mouser.fr/datasheet/2/3/abls-1664338.pdf)
* [Led bleu (niveau de réception) : MP008276]( https://www.farnell.com/datasheets/3497873.pdf)
* [Led RGB (niveau batterie) : 5988G10313F ](https://www.mouser.fr/datasheet/2/109/C18481B-2944388.pdf)
* [Driver de LED I2C : PCA9685PW,118 ]( https://www.mouser.fr/datasheet/2/302/PCA9685-1127478.pdf)

## $${\color{black}Déroulement \space \color{black}du \space \color{black}{projet}}$$

### Software :

### Hardware - PCB Leds:

La version finale de mon [PCB](Hardware/PCB_LEDs/PCB LEDs.kicad_sch_copie.kicad_pro).


Ce PCB est composé d'une diode RGB qui montre le niveau de batterie de la balise et de quatre LEDs bleues qui déterminent le niveau de connexion Internet. Des résistances de 100Ω sont ajoutées afin de limiter le courant qui traverse les LEDs. 

En ce qui concerne les LEDs bleues, il n'y a pas de problème, elles s'allument correctement. En revanche, cette partie comporte un principal problème : à cause d'une mauvaise connexion des pins de la LED RGB, on s'est rendu compte que seule la diode verte s'allume, les diodes jaune et rouge ne fonctionnent pas. Il faut prendre garde à ne pas se tromper entre l'anode et la cathode des diodes, pour éviter que l'erreur ne se reproduise. 

### Hardware - PCB IR :

La version finale de mon [PCB](Hardware/PCB_IR/cohoma.kicad_pro).

Voici les difficultés rencontrées lors du projet:
* Trouver les schematics correspondants au projet (pour plusieurs composants, elle n'existait pas sur Kicad: il a donc été nécéssaire de les trouvées, les téléchargées, puis les importées sur Kicad).
* De même pour les empreintes de certains composants, il fallait alors trouver une empreinte très proche, ou bien créer l'empreinte dans certains cas.
* Rendre le PCB le plus petit possible tout en respectant une contrainte: les deux condensateurs associés au Quartz devianet être aussi proche que possible de ce dernier.
* 



### Hardware - PCB Buck-Boost:

La version finale de notre [PCB](Hardware/PCB_BuckBoost/pcb_v3/pcb_v3.kicad_pro).

Ce PCB est composé d'un régulateur monté en deux modes différents (Buck et boost) et quatre LEDs qui témoignent du bon fonctionnement de l'alimentation. 

Le projet nous a posé plusieurs difficultés : 
* Repérer sur la datasheet les montages buck et boost qui correspondaient au projet.
* Choisir des empreintes des condensateurs et des inductances adaptées à la situations (exemple : condensateurs polarisés).
* Assigner (voire créer) les bonnes empreintes car elles n'étaient pas toujours disponibles sur Kicad.  
* Agencer les composants afin d'obtenir un PCB le plus petit possible.
* Placer les composants traversés par une forte tension de manière optimale (ils devaient être proches des "switching regulator").
* Il fallait imposer un courant de sortie de 100 mA, ce qui n'était possible que si la balise était complète. Or, ce n'était pas le cas, puisque nous n'avions que le PCB. Nous avons donc dû rajouter deux résistances en parallèle à un condensateur polarisé.
* Choisir une largeur de piste suffisante en fonction du courant qui traversait les différents composants. 
* Augmenter le nombre de vias car ils ne fonctionnaient pas toujours.
* Certaines pastilles de cuivres n'étaient pas connectés à la masse, une erreur lors de la conception du PCB sur Kicad.

## $${\color{black}Impact \space \color{black}environnemental}$$

### $${\color{green}Expliquer \space \color{green}les \space \color{green}{critères} \space \color{green}de \space \color{green}choix \space \color{green}du \space \color{green}mode \space \color{green}d'alimentation \space \color{green}de \space \color{green}votre \space \color{green}{projet}}$$

Notre projet exigeait déjà un cahier des charges précis à respecter. En effet, la plupart des composants, y compris l'alimentation Buck-Boost, étaient imposés. N'ayant que peu de marge de manoeuvre, nous avons porté une attention toute particulière à la taille des PCBs conçus. En effet, ces derniers devaient être les plus petits possibles, afin de ne pas gaspiller des matériaux. De plus, les PCBs ayant été réalisés sur place, leur impact environnemental dû aux transports était minime, les composants étant déjà à l'école.

### $${\color{green}Votre \space \color{green}projet \space \color{green}favorise-t-il \space \color{green}une \space \color{green}utilisation \space \color{green}judicieuse \space \color{green}et \space \color{green}rationnelle \space \color{green}de \space \color{green}l'énergie, \space \color{green}en \space \color{green}minimisant \space \color{green}{les}}$$

### $${\color{green}impacts \space \color{green}de \space \color{green}sa \space \color{green}production, \space \color{green}de \space \color{green}sa \space \color{green}distribution \space \color{green}et \space \color{green}de \space \color{green}sa \space \color{green}{consommation?}}$$

Les LEDs présentes sur le projet ne s’allument que lorsque le module qui leur est associé est sollicité. Ainsi il n'y a pas d'énergie utilisée inutilement. De plus, nous nous sommes assurés qu’aucun composant ne consomme plus d’énergie que celle nécessaire à son bon fonctionnement.


Cependant, si l’on s’intéresse au projet de manière plus large, son impact est plus important que ce que nous avons décrit précédemment. En effet, plusieurs écoles sont en compétition dans la réalisation de ce projet pour ne sélectionner que le meilleur. L’impact aurait été moins important si une seule équipe d’ingénieurs professionnels s’en était chargée. Néanmoins, cette compétition entre écoles encourage chacun des participants à réaliser le projet le plus efficace et propre possible dans l’espoir d’être sélectionnés.

