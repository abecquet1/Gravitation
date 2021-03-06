##################################
### SIMULATEUR SYSTEME SOLAIRE ###
##################################



### DEMARRAGE ###

Pour lancer le logiciel, double-cliquer sur "main.py"



### FONCTIONNALITÉS ###

+ OK pour lancer la simulation 
+ Modifier la valeur de "Unit of time" puis OK pour accélérer / ralentir la simulation		[1]
+ Cliquer sur l'astre voulu dans "Planet Frame" pour passer dans son référentiel
+ Molette de la souris pour zoomer / dézoomer
+ Cliquer sur la molette pour réinitialiser le zoom
+ Maj+molette pour modifier l'échelle des astres (garde les distances mais augmente les rayons)
+ Maj+cliquer sur la molette pour réinitialiser l'échelle des astres
+ Cliquer dans le ciel pour bouger le point de vue (translation du référentiel) 		[2]



### BUGS ###

[1] Unit of time représente le DT de la simulation : plus il est grand plus les erreurs sont grandes
    passer à 36000s (x10) perturbe immédiatement les lunes des géantes gazeuses, le reste semble bien tourner
[2] N'est pas réinitialisé lors d'un changement de référentiel : à éviter



### FONCTIONNEMENT ### 

GRAV.PY

Dans le fichier grav.py, on définit les planettes (astres en général) et les systèmes (ensemble de planettes)

Les astres ont :
+ des caractéristiques esthétiques (name, radius, color)
+ des caractéristiques physiques (mass, x, y, vx, vy)

On peut : 
+ les faire accélérer (accelerate) selon un vecteur accélération a donné : v = v + a*dt
+ les faire bouger (move) selon leur vitesse : x = x + v*dt 
+ calculer le champs gravitationel qu'elles génèrent (field) -r*G/d^3 (r vecteur position)


Un système est un énsemble de planettes permettant l'intéraction et l'affichage de celles-ci.

Un système a, entre autres : 
+ une liste de planettes (planet_list) et une planette de référence (p_ref)
+ une valeur fixe de dt servant à simuler des mouvements infinitésimaux

On peut, entre autres :
+ générer le champs gravitationnel global du système (field) par somme des champ de ses planettes 
+ faire bouger toutes les planettes (move)


MAIN.PY

Le fichier main.py récupère les données du fichier ss.csv comportant les caractéristiques d'objets du système solaire (source : wikipedia https://fr.wikipedia.org/wiki/Liste_d%27objets_du_Syst%C3%A8me_solaire)
Puis il génère pour chaque objet hors soleil une position initiale aléatoire autour de son objet parent et calcule une vitesse initiale correspondant à l'excentricité des trajectoires (chaque objet commence à son periastre)
Il lance enfin la simulation
