# 🎮 Cub3D

## 💡 1. Introduction

Cub3D est un projet de l’école 42 qui consiste à réaliser un moteur de pseudo 3D minimaliste en ray-casting, inspiré du jeu Wolfenstein 3D, à partir d’une map 2D en utilisant la librairie graphique MiniLibX.

## 🎯 2. Objectifs

- Afficher un environnement pseudo 3D interactif à partir d’une map 2D au format .cub.
- Permettre les déplacements du joueur (avancer, reculer, strafe, rotation).
- Charger et valider les textures et couleurs définies dans le fichier .cub.
- Respecter les contraintes du sujet Cub3D de 42 (gestion d’erreurs, leaks, norme, etc.).

## 📌 3. Objectifs bonus

- Gérer les collisions avec les murs et les limites de la map.​
- Création d'une minimap 
- Permettre les déplacement de la rotation de la caméra avec la souris.
- Gérer les sprites animées.
- Implémenter un système de portes.

## ✨ 4. Fonctionnalités réalisées

- Parsing des parametres, de la map et gestion des erreurs : fichier manquant, map invalide, textures introuvables, paramètres incorrects.
- Rendu 3D basique par ray-casting.
- Support des textures .xpm pour les différants orientations des murs (Nord, Sud, Est, Ouest).
- Couleurs configurables pour le sol et le plafond (RGB).​
- Déplacement fluide du joueur dans le labyrinthe par clavier. (et souris en bonus)
- Minimap pour visualiser la map 2D et la position du joueur.​ (bonus)
- Système de porte, ouverte par pressions d'une touche (F) avec une animation pour chaques ouvertures et fermetures. (bonus)

## 📜 5. Prérequis

- OS : Linux.
- gcc
- make
- X11 includes files
- XShm extension must be present (package libxext-dev)
- Utility functions from BSD systems - development files (package libbsd-dev)
- **e.g. sudo apt-get install gcc make xorg libxext-dev libbsd-dev (Debian/Ubuntu)**

## 🤖 6. Installation

### Cloner le dépôt :

	git clone https://github.com/Sellith/Cub3d.git
	cd Cub3d

### Compilation

Depuis la racine du projet :

	make

La règle "all" du Makefile permet le clonage et la compilation de la MiniLibX, et de la libft les fichiers binaires seront automatiquement copiés dans le dossier bin/archives/ situé à la racine du projet.

L’exécutable généré dans le dossier bin/ et sera typiquement nommé :

	bin/cub3D

## ⚙️ 7. Règles du Makefile :

Le makefile a été confectionné de sorte que presque tout peut-etre contrôlé à partir de ses règles :

### Règles générales

- all : Compile la Libft, la MiniLibX, et les fichiers sources. 
- clean : Supprime tous les fichiers objets existants (libft, et sources).
- fclean : Supprime tous les fichiers objets et binaires existant (libft et sources).
- re : Supprime tous les fichiers objets et binaires et recompile l'ensemble du code.

### Règles des dépendences

- libft : Clone la libft de mon repo github, la compile, copies les fichiers headers dans include/ et le fichier binaire dans bin/archives/.
- rmlib : Supprime tous les fichiers de la libft.
- udlib : Supprime tous les fichiers de la libft et la reclone.

- mlx : Clone la MiniLibX et la compile, copies les fichiers headers dans include/ et le fichier binaire dans bin/archives/.
- rmmlx : supprime tous les fichiers de la MiniLibX.

- cleandep : Supprime tous les fichiers objets de la libft.
- fcleandep : Supprime tous les fichiers objets et binaires de la libft.
- mkdep : Compile la libft.
- redep : Supprime tous les fichiers de la libft objets et binaires et la recompile.

### Règle des fichiers sources

- cleansrc : Supprime tous les fichiers objets du code sources.
- fcleansrc : Supprime tous les fichiers objets et binaires du code source.
- resrc : Supprime tous les fichiers objets et binaires du code source et recompile .

### Règle de normes et de tests

- normy : Lance la norminette avec les flags et fait un diff.

## 💎 8. Utilisation

Cub3d doit etre executé avec comme argument une map valide.

### Exemple d’exécution avec une map :

	bin/cub3D maps/big_maze.cub

### Touches utilisées :

- W / S : avancer / reculer.
- A / D : déplassement gauche / droite.
- Flèches gauche / droite / souris: tourner la caméra.
- ESC ou bouton de fermeture de la fenêtre : quitter le jeu, cette action permet un exit sans leaks.
- M : affichage de la minimap.
- F : ouvrir les portes.
- E : mode debug.

## 🤝 9. Format valide des maps

Une map valide est en format .cub

> il est important de respecter un modele précis pour que la map soit valide.

### Un fichier .cub contient généralement :

- Chemins vers les textures :
	- NO path_to_north_texture.xpm
	- SO path_to_south_texture.xpm
	- WE path_to_west_texture.xpm
	- EA path_to_east_texture.xpm

- Couleurs du plafond et du sol :
	- F R,G,B
	- C R,G,B

- La map 2D fermée, utilisant par exemple :
	- 1 pour les murs
	- 0 pour l’espace vide
	- N / S / E / W pour la position et l’orientation initiale du joueur

### Exemple minimal :


	NO textures/north.xpm
	SO textures/south.xpm
	WE textures/west.xpm
	EA textures/east.xpm
	F 220,100,0
	C 225,30,0

	111111
	100001
	1000N1
	111111

## 🤔 10. Structure du projet

	Minishell/
	├── Dependencies	   # Contient ma libft ameliorée et la MiniLibX
	├── includes/		   # Headers (cub3d.h)
	├── maps/			   
	│	├──	bad/		   # Maps non valides
	│	└── good/		   # Maps valides
	├── assets			   # Contient les assets pouvant etre utilisés
	├── bin/			   # Fichiers binaires du projet (libft.a, cub3d)
	├── build/			   # Fichiers objets du projet une fois compilé 
	├── src/
	│	├── parsing/	   # Vérification des paramètres, parsing de la map.
	│	├── display/	   # Contiens les fonction d'affichage
	│	│	└──	raycasting # Contiens les fonction implémentant le raycasting
	│	└── events		   # Contiens les fonctions implémentatnt les evenements du jeu (déplacement, ouvertures des portes).
	├── Makefile
	└── README.md

## 📩 11. Améliorations possibles

- Optimisation des performances lorsque les portes sont ouvertes.
- Ajout d'un objectif, d'ennemis, 
- Ajout d’animations, de sprites et d’objets interactifs.
- Ajout d'un menu de jeux / menu pause avec parametrage de la taille de l'écran et les touches du client.