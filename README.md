# Balise_Cohoma 
Projet cohoma

# Présentation du projet:

   Ce projet est en collaboration avec des deuxièmes années qui participent au projet Cohoma, pour l'armée de terre. Il consiste en la création d'un robot autonome s'adaptant à tout type de terrains. Ce robot doit lâcher des balises sur son chemin, elles ont pour but de le localiser. C'est ce sur quoi nous avons travaillé. 
   Une LED RGB est utilisée afin de montrer le niveau de batterie de la balise (vert: pleine charge, jaune: à moitié chargée et rouge: déchargée). Quatre LEDs bleues sont également utilisées afin de déterminer le niveau de connexion Internet de la balise. Il y a également un capteur infrarouge qui permet de communiquer avec le rover afin d'allumer la batterie.
   
   
   
# Cahier des charges :

-> Rendre visible le niveau de batteries de la balise (sur la balise)
-> Rendre visible le niveau de réception WIFI de la balise (sur la balise)
-> Communication infrarouge entre une télécommande et la balise
-> Communication infrarouge entre le rover et la balise dans le but d'allumer la balise après lors de l'éjection.


Capteur/émetteur avec le rover pour l'allumage des batteries : - Partie émission rover ( le prof ) - Partie reception : le capteur reçoit un signal bizarre, il faut le convertir en UART pour que le CPU comprenne

