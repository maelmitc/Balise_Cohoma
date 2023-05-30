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



