# $${\color{black}Balise \space \color{black}Cohoma}$$

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

L'objectif du logiciel développé est le traitement des données du routeur et de la batterie et la commande du <em>driver</em> LED. Le code a été développé en C. Le code est implémenté sur un processeur STM32 L412KBT6. En fonction des données reçues, le logiciel commande les LEDs, en particulier en fonction du niveau de batterie disponible. Le driver de LEDs, relié à quatre LEDs bleues et une LED RGB est connecté en I2C avec le processeur STM32.

* [Architecture <em>software</em>](Software/[CoHoMa]BeaconSoftwareArchitecture.drawio) (originale, modifiée depuis)
* [Code](Software/CHMBeaconB.zip)

#### Batterie
Selon le niveau de batterie calculé, 1 à 4 Blue LEDs sont allumées
* 75% : 4 LEDs activées
* 50% : 3 LEDs activées
* 25% : 2 LEDs activées
* 10% : 1 LED activée
On utilise une connexion I²C pour lier le STM32 au <em>driver</em> LED.

#### Routeur/IR
On utilise une LED RGB pour témoigner de la qualité de la connexion.
En fonctionnement normal, on utilise 3 couleurs : rouge (signal faible), vert (signal moyen), bleu (signal fort).

#### Problèmes rencontrés lors du développement :
* Longue lecture des fiches techniques des composants utilisés
* Recherche et étude d'un algorithme pour déterminer le niveau de batterie (SOC Algorithm)
* Lien entre la partie <em>hardware</em> et <em>software</em>, en particulier le lien avec la batterie/le niveau de charge

D'un point de vue personnel, je juge avoir sous-estimé la quantité de travail à fournir dans la partie <em>software</em>, trop importante pour une seule personne.

### Hardware - PCB Leds:

La version finale de mon [PCB](Hardware/PCB_LEDs/PCB_LEDs.kicad_sch_copie.kicad_pro).

#### Composants utilisés : 

Type de produit | Empreinte | Nombre 
--- | --- | ---
Driver de LEDs | Package_STO:TSSOP-28_4.4x9.7mm_P0.65mm | 1
LED bleue | LED_SMD:LED_0603_1608Metric_Pad1.05x0.95mm_HandSolder | 4 
LED RGB | LED_SMD:LED_Avago_PLCC6_3x2.8mm | 1
Résistance (100Ω et 150Ω)| Resistor_SMD:R_0603_1608Metric_Pad0.98x0.95mm_HandSolder | 7
Connecteur 01x05 | Connector_JST:JST_XH_B5B-XH-A_1x05_P2.50mm_Vertical | 1

#### Utilité des composants :

* Driver de LEDs : pilote les LEDs.
* LEDs bleues : montrent le niveau de connexion Wifi sur la balise. Plus le nombre de LEDs allumées est important, plus la connexion internet est bonne. 
* LED RGB : montre le niveau de batterie de la balise. Si la LED est verte, la balise est entièrement chargée ; jaune, à moitié chargée ; rouge, déchargée.
* Résistances : permettent de limiter le courant qui traverse les LEDs.
* Connecteur : permet de faire communiquer le driver de LEDs avec l’extérieur. Il est composé de cinq sorties : une d'alimentation et une de masse, mais également d'une sortie SDA (Serial Data Line), d'une sortie SCL (Serial Clock Line) et d'une sortie output enable, qui permet d’activer ou de désactiver les sorties de LEDs, en fonction des besoins.


#### Choix des résistances : 

Le driver de LEDs est alimenté par une tension de 5V. La tension maximum que peuvent recevoir les LEDs est d’environ 3V. Or, puisqu’on a un courant de 25 mA qui doit traverser les LEDs, on en conclut que la résistance qui doit être ajoutée afin de limiter la tension est de 100Ω. EN ce qui concerne la LED RGB, la diode rouge supporte une tension moins importante que les diodes jaune et verte. Sa résistance doit donc être supérieure à celles des diodes jaune et verte. C’est pourquoi, on ajoute une résistance de 150Ω.


#### Problèmes rencontrés lors de la fabrication de ce PCB : 

En ce qui concerne les LEDs bleues, il n'y a pas de problème, elles s'allument correctement. En revanche, cette partie comporte un principal problème : à cause d'une mauvaise connexion des pins de la LED RGB, on s'est rendu compte que seule la diode verte s'allume, les diodes jaune et rouge ne fonctionnent pas. Il faut prendre garde à ne pas se tromper entre l'anode et la cathode des diodes, pour éviter que l'erreur ne se reproduise. 

### Hardware - PCB IR :

La version finale de mon [PCB](Hardware/PCB_IR/cohoma.kicad_pro).

#### Composants utilisés : 

Type de produit | Empreinte | Nombre 
--- | --- | ---
Décodeur | Package_SO:SOIC-14_3.9x8.7mm_P1.27mm | 1
Récepteur Infrarouge | Package_SO:TSOP753TT (empreinte que nous avons créée) | 1
Quartz | Crystal:Crystal_SMD_7050-2Pin_7.0x5.0mm | 1
Condensateur (20 pF et 100 nF)| Capacitor_SMD:C_0603_1608Metric_Pad1.08x0.95mm_HandSolder | 3
Connecteur 01x03 | Connector_PinHeader_1.27mm:PinHeader_1x03_P1.27mm_Horizontal | 1 

Ce PCB se compose de plusieurs parties:

#### Récepteur IR:
Le récepteur IR reçoit un signal provenant d'un émetteur IR. Il renvoie alors RXIR à l'encodeur/décodeur dans le but que le signal soit décodé.
Afin d'éviter les fluctuations de tensions, il était recommandé par la datasheet, lorsque Vs<2.8 V d'utiliser une résistance et un condensateur. Ce n'est ici pas le cas, cependant, afin d'éviter tout risque, un condensateur de 100 nF a tout de même été ajouté.

#### Encodeur/Décodeur:
Dans le cadre de ce projet, ce composant a été utilisé uniquement comme un décodeur. Il reçoit RXIR, le décode et renvoie UART_RX au microcontrôleur (via le connecteur).
En effet, pour être compris par le microcontrôleur, le signal doit être en UART.


Les "BAUD" permettent de modifier la vitesse de transmission. Ils sont tous les trois mis à la masse ici, ce qui équivaut à les mettre à 0.

#### Quartz:
Le quartz sert d'horloge. Il est ici accompagné de deux condensateurs qui permettent de "lisser" afin que l'horloge soit vraiment régulière.

#### Difficultés rencontrées lors de la fabrication de ce PCB :
* Trouver les schematics correspondants au projet (pour plusieurs composants, elles n'existaient pas sur Kicad: il a donc été nécessaire de les trouver, les télécharger, puis les importer sur Kicad).
* La datasheet du quartz ne permettait pas de connaître la schematic associée, il fallait effectuer d'autres recherches.
* De même pour les empreintes de certains composants, il fallait alors trouver une empreinte très proche, ou bien créer l'empreinte dans certains cas.
* Rendre le PCB le plus petit possible tout en respectant une contrainte: les deux condensateurs associés au Quartz devaient être aussi proche que possible de ce dernier.


### Hardware - PCB Buck-Boost:

La version finale de notre [PCB](Hardware/PCB_BuckBoost/pcb_v3/pcb_v3.kicad_pro).

#### Composants utilisés : 

Type de produit | Empreinte | Nombre 
--- | --- | ---
Diode| Diode_SMD:D_SOD-123F | 1
Diode| Diode_SMD:D_SOD-323F | 1
PS1| Footprints_Balise:PS1 | 1
Régulateur Buck/Boost | Package_SO:SOIC-8-1EP_3.9x4.9mm_P1.27mm_EP2.29x3mm | 2
Condensateur polarisé (330 uF)| Capacitor_SMD:CP_Elec_10x10.5 | 2
Condensateur polarisé (100 uF)| Capacitor_SMD:CP_Elec_6.3x7.7 | 1
Condensateur polarisé (22 uF)| Capacitor_SMD:CP_Elec_5x5.4 | 1
Condensateur (2.2 uF, 1 uF et 0.47 nF)| Capacitor_SMD:C_0603_1608Metric_Pad1.08x0.95mm_HandSolder | 6
LED bleue | LED_SMD:LED_0603_1608Metric_Pad1.05x0.95mm_HandSolder | 4 
Inductance (100 uH)| Inductor_SMD:L_Wuerth_WE-PD-Typ-LS | 2
Résistance | Resistor_SMD:R_0603_1608Metric_Pad0.98x0.95mm_HandSolder | 11
Diode Schottky | Footprints_Balise:Diode_Schottky (empreinte créée)| 2
Connecteur 01x02 | Connector_JST:JST_XH_B2B-XH-A_1x02_P2.50mm_Vertical | 4


#### Utilité des composants
* LEDs bleues : témoignent du bon fonctionnement de l'alimentation
* Diodes / Diode Schottky : permettent les différents états de commutation du régulateur
* Régulateur à découpage : gère le découpage (via le rapport cyclique) de la tension en fonction des différents états. Les régulateurs sont au nombre de deux, chacun est monté différemment, permettant le passage au mode Buck ou Boost.
* PS1 : régule la tension

#### Choix des composants     
Les composants (autre que ceux imposés) ont été sélectionnés en fonction des datasheets des montages Buck et Boost et des composants passifs disponibles à l'ENSEA. Pour ce qui est des condensateurs, des condensateurs classiques ou polarisés ont été choisi en fonction de la valeur des capacités indiquées sur la datasheet (au dessus de 10 uF, on choisit un condensateur polarisé).

#### Explication du fonctionnement des régulateurs à découplage  
Un régulateur de découplage est un type de régulateur de tension qui utilise des composants électroniques commutés (transistors, inductances, condensateurs) pour convertir l'énergie de manière efficace. 

Régulation de la tension d'entrée : Le régulateur de découplage commence par réguler et contrôler la tension d'entrée, celle-ci pouvant être supérieure ou inférieure à la tension de sortie souhaitée, à l'aide de composants électroniques commutés.

Conversion d'énergie : L'énergie est efficacement convertie en utilisant un interrupteur électronique, généralement un transistor, pour commuter rapidement entre les états "on" et "off". Il est possible de réduire les pertes d'énergie et d'améliorer l'efficacité globale du régulateur grâce à cette commutation.

Stockage de l'énergie : Pendant la commutation, l'énergie est stockée dans une inductance (bobine) lors de l'état "on" de l'interrupteur et est libérée lors de l'état "off". Cela permet de réguler et de maintenir la tension de sortie constante malgré les variations de la tension d'entrée ou de la charge.

Filtrage : Le régulateur de découplage utilise également des condensateurs pour filtrer les fluctuations résiduelles de la tension de sortie et pour fournir une alimentation stable et régulée.


#### Difficultés rencontrées lors de la fabrication de ce PCB : 
* Repérer sur la datasheet les montages buck et boost qui correspondaient au projet.
* Choisir des empreintes des condensateurs et des inductances adaptées à la situations (exemple : condensateurs polarisés).
* Assigner (voire créer) les bonnes empreintes car elles n'étaient pas toujours disponibles sur Kicad.  
* Agencer les composants afin d'obtenir un PCB le plus petit possible.
* Placer les composants traversés par une forte tension de manière optimale (ils devaient être proches des régulateurs à découpage).
* Il fallait imposer un courant de sortie de 100 mA, ce qui n'était possible que si la balise était complète. Or, ce n'était pas le cas, puisque nous n'avions que le PCB. Nous avons donc dû rajouter deux résistances en parallèle à un condensateur polarisé.
* Choisir une largeur de piste suffisante en fonction du courant qui traversait les différents composants. 
* Augmenter le nombre de vias car ils ne fonctionnaient pas toujours.
* Certaines pastilles de cuivres n'étaient pas connectés à la masse, une erreur lors de la conception du PCB sur Kicad.

## $${\color{black}Impact \space \color{black}environnemental}$$

### $${\color{green}Expliquer \space \color{green}les \space \color{green}{critères} \space \color{green}de \space \color{green}choix \space \color{green}du \space \color{green}mode \space \color{green}d'alimentation \space \color{green}de \space \color{green}votre \space \color{green}{projet}}$$

Notre projet exigeait déjà un cahier des charges précis à respecter. En effet, la plupart des composants, y compris l'alimentation Buck-Boost, étaient imposés. Cependant, on peut tout de même se demander pourquoi c'est une alimentation à découpage qui à été choisie plutôt qu'une alimentation linéaire. En effet, l'alimentation à découpage possède un rendement bien plus élevé (et consomme donc moins d'énergie) que l'amplificateur linéaire grâce à son fonctionnement "alterné" entre différents états de commutations. Cette meilleure efficacité énergétique est principalement due à leur principe de fonctionnement différent. Dans un régulateur linéaire, la tension excédentaire est dissipée sous forme de chaleur par un transistor de régulation. Cela signifie que la différence de tension entre l'entrée et la sortie du régulateur est convertie en chaleur, ce qui entraîne une perte d'énergie importante. Par conséquent, les régulateurs linéaires ont généralement une efficacité relativement faible, en particulier lorsque la différence de tension entre l'entrée et la sortie est importante. 

En revanche, les régulateurs de découplage utilisent des composants électroniques commutés, tels que des transistors MOSFET et des inductances, pour réguler la tension de sortie. Ces composants commutent rapidement entre les états "on" et "off", ce qui permet de minimiser les pertes d'énergie. Lorsque le transistor est en état "on", il présente une résistance très faible, ce qui réduit les pertes de puissance. Lorsque le transistor est en état "off", l'inductance stocke l'énergie et la restitue lors de l'état "on" suivant, ce qui permet de maintenir une tension de sortie constante.En conséquence, les régulateurs de découplage ont une efficacité énergétique beaucoup plus élevée que les régulateurs linéaires. Une plus grande quantité d'énergie est transférée du côté de l'entrée vers le côté de la sortie sans être dissipée sous forme de chaleur. De plus, en raison du rapport cyclique, le transformateur à l'intérieur de l'alimentation peut être très petit, réalisant ainsi la miniaturisation de la taille de l'alimentation tout en permettant également l'utilisation normale de l'alimentation. 

Il est à noter que dans certains cas (dans d'autres projets par exemple), l'utilisation des régulateurs linéaire est préférable : 
* Moins sensible aux variations de la tension d'entrée,
* Coût moins élevé,
* Meilleure performance en terme de réduction de bruit et des interférences électromagnétique, 
* Moins complexe
* Réglage plus fin de la sortie.

### $${\color{green}Votre \space \color{green}projet \space \color{green}favorise-t-il \space \color{green}une \space \color{green}utilisation \space \color{green}judicieuse \space \color{green}et \space \color{green}rationnelle \space \color{green}de \space \color{green}l'énergie, \space \color{green}en \space \color{green}minimisant \space \color{green}{les}}$$

### $${\color{green}impacts \space \color{green}de \space \color{green}sa \space \color{green}production, \space \color{green}de \space \color{green}sa \space \color{green}distribution \space \color{green}et \space \color{green}de \space \color{green}sa \space \color{green}{consommation?}}$$
 
La plupart des composants étant imposés, nous avons eu peu de marge de manoeuvre. Nous avons donc porté une attention toute particulière à la taille des PCBs conçus. En effet, ces derniers devaient être les plus petits possibles, afin de ne pas gaspiller de matériaux. De plus, les PCBs ayant été réalisés sur place, leur impact environnemental dû aux transports était minime, les composants étant déjà à l'école.
 
Pour ce qui est des LEDs présentes sur le projet, elles ne s’allument que lorsque le module qui leur est associé est sollicité. Ainsi il n'y a pas d'énergie utilisée inutilement. De plus, nous nous sommes assurés qu’aucun composant ne consomme plus d’énergie que celle nécessaire à son bon fonctionnement.

Cependant, si l’on s’intéresse au projet de manière plus large, son impact est plus important que ce que nous avons décrit précédemment. En effet, plusieurs écoles sont en compétition dans la réalisation de ce projet pour ne sélectionner que le meilleur. L’impact aurait été moins important si une seule équipe d’ingénieurs professionnels s’en était chargée. Néanmoins, cette compétition entre écoles encourage chacun des participants à réaliser le projet le plus efficace et propre possible dans l’espoir d’être sélectionnés.

## $${\color{black}Conclusion}$$

Nous avons manqué de temps pour atteindre tous nos objectifs. Cependant, si nous pouvions donner des conseils à nos successeurs, nous dirions de :
 
* Faire des groupes plus équitables entre le <em>hardware</em> et le <em>software</em>.
* Bien lire les datasheet des composants, de façon à choisir des valeurs de résistances ou de condensateurs appropriées, par exemple. 
* Faire particulièrement attention aux empreintes, quitte à en créer, de façon à n'avoir aucun problème lors de la soudure.
* Faire particulièrement attention au sens des diodes, ne pas intervertir l'anode et la cathode, dans le cas ou le PCB en comporte.
* Faire attention à la largeur des pistes, en fonction du courant qui traverse les différents composants.
