# Balise_Cohoma 
Projet cohoma

## Présentation du projet:

   Ce projet est en collaboration avec des deuxièmes années qui participent au projet Cohoma, pour l'armée de terre. Ce projet
  est une compétition entre différentes écoles d'ingénieurs. Il consiste en la création d'un robot autonome s'adaptant à tout type de terrains. Ce robot doit lâcher des balises sur son chemin, elles ont pour but de le localiser. C'est ce sur quoi nous avons travaillé. 
   
   Une LED RGB est utilisée afin de montrer le niveau de batterie de la balise (vert: pleine charge, jaune: à moitié chargée et rouge: déchargée). Quatre LEDs bleues sont également utilisées afin de déterminer le niveau de connexion Internet de la balise. Il y a également un capteur infrarouge qui permet de communiquer avec le rover afin d'allumer la batterie. Enfin, on utilise un convertisseur Buck-Boost, qui est une alimentation à découplage qui convertit une tension continue en une autre tension continue de plus faible ou de plus grande valeur, mais de polarité inverse.
   
   
   
## Cahier des charges :

* Rendre visible le niveau de batteries de la balise (sur la balise).
* Rendre visible le niveau de réception WIFI de la balise (sur la balise).
* Communication infrarouge entre une télécommande et la balise.
* Communication infrarouge entre le rover et la balise dans le but d'allumer la balise après lors de l'éjection.
* Alimenter la balise.

## Datasheet :

* [Battery Management System]()
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
