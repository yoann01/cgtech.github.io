### ENVIRONNEMENT VIRTUEL 

Un environnement virtuel est un environnement d'exécution isolé.

Les environnements virtuels sont utilisés afin d'isoler les paquets utilisés pour un projet.

On peut ainsi avoir sur le même ordinateur deux projets Python (ou plus) qui utilisent chacun une version différente d'un même paquet.

Pour créer un environnement virtuel, on peut utiliser le module venv qui est inclus dans la bibliothèque standard de Python :

```py
python -m venv nom_de_lenvironnement
```

L'environnement virtuel contient plusieurs dossiers et fichiers :

```py
├── bin
│   ├── Activate.ps1
│   ├── activate
│   ├── activate.csh
│   ├── activate.fish
│   ├── easy_install
│   ├── easy_install-3.8
│   ├── pip
│   ├── pip3
│   ├── pip3.8
│   ├── python -> python3
│   └── python3 -> /Library/Developer/CommandLineTools/usr/bin/python3
├── include
├── lib
│   └── python3.8
│      └── site-packages
└── pyvenv.cfg
```

Le dossier bin contient l'interpréteur Python et tous les exécutables dont vous pourriez avoir besoin (comme easy_install ou pip). C'est également dans ce dossier que vous trouverez les fichiers qui vous permettent d'activer votre environnement virtuel (activate).

Pour activer votre environnement virtuel, il suffit donc de « sourcer » le fichier activate dans votre terminal :

```sh
$ source bin/activate
```

windows
```sh
venvName/Scripts/activate.bat
```
Le dossier include ne contient par défaut aucun fichier. Ce dossier sert dans le cas de la création de bibliothèques utilisant le langage C.

Le dossier lib contient tous les paquets que vous installerez avec pip dans cet environnement virtuel (à l'intérieur du sous-dossier site-packages).

Le fichier pyvenv.cfg contient des variables qui définissent certains paramètres de votre environnement virtuel, comme le chemin vers l'interpréteur Python système ou la version de Python de votre environnement virtuel.
