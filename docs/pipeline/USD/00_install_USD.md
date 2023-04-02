---
titre : Commencez avec l'USD
Mots clés:
    - USD
description : Comment construire des USD
---

# Essayez d'utiliser USD

SIGGRAPH2019 a constaté que l'USD est très chaud, donc  
Je vais télécharger un article de synthèse tout en vérifiant diverses choses.

Tout d'abord, nous allons télécharger et configurer USD.

## Construire

Construisez d'abord l'USD.
Auparavant, il fallait beaucoup de travail pour créer et utiliser USD, mais maintenant, créez des scripts
Il est préparé et peut être construit relativement facilement.

### Installez ce dont vous avez besoin

-   https://git-scm.com/
-   https://visualstudio.microsoft.com/ja/downloads/
-   https://www.python.org/downloads/release/python-3712/

Tout d'abord, téléchargez et installez VisualStudio nécessaire à la construction, Git pour obtenir le code source et Python.

Une fois Python installé
![](https://gyazo.com/b9e01b33a2198d006d082dbe6c43320e.png)

Ajoutez Python37 directement en dessous et Scripts à la variable d'environnement PATH.
De plus, installez PySide2 et PyOpenGL, qui sont requis lors de l'utilisation d'USDView.

```
pip installer PyOpenGL PyOpenGL_accelerate PySide2
```

Les préparatifs sont maintenant terminés.

### Cloner le dépôt

Une fois installé, clonez le référentiel à partir du Github d'USD.

À l'invite de commande, accédez au répertoire dans lequel vous avez téléchargé

```
git clone https://github.com/PixarAnimationStudios/USD.git
```

Cloner

Une fois cloné, ouvrez l'invite de commande du développeur de VisualStudio.

![](https://gyazo.com/ecddefa1fda425ead85330b083d05044.png)

Une fois ouvert, accédez au dossier dans lequel vous avez cloné le référentiel et exécutez la construction.

```
python build_scripts\build_usd.py <destination de sortie des artefacts de construction>
```

## à travers le chemin

Une fois le téléchargement terminé, placez-le dans le PATH requis.  
tu as besoin de deux

| nom de la variable | CHEMIN |
| ---------- | ------------------------------------------------------------------------ |
| PYTHONPATH | <racine du dossier téléchargé>/lib/python |
| PATH | <racine du dossier téléchargé>/bin <br> <racine du dossier téléchargé>/lib |

!!! Info

    Si votre PATH n'est pas sous lib,
    Notez qu'une erreur se produira lors de l'importation d'un fichier pyd.

Passez par ces deux et vous êtes prêt à partir

## essayez d'ouvrir des exemples de données

Lorsque vous êtes prêt, téléchargez l'exemple d'USD et ouvrez-le dans votre visionneuse.

http://graphics.pixar.com/usd/downloads.html

Des exemples de données sont disponibles sur le site officiel de PIXAR, alors téléchargez ce KitchenSet.

Après le téléchargement, décompressez et ouvrez l'invite de commande.

```lot
usdview Kitchen_set.usd
```

Ouvrez Kitchen_set.usd avec usdview.

![](https://gyazo.com/85f886a67bcafe10082f3e1e178848eb.png)

Utilisez USDView pour voir les graphiques de scène, les couches, les propriétés, etc. des fichiers USD  
boîte.  
Il est également livré avec une console Python, donc  
Il est facile de comprendre (semble) d'utiliser cet usdview pour tester diverses choses.

## Créer un fichier USD à partir de Python

Lorsque vous êtes prêt, essayez d'exécuter le didacticiel officiel.  
https://graphics.pixar.com/usd/docs/Hello-World---Creating-Your-First-USD-Stage.html

```python
depuis l'importation pxr Usd, UsdGeom
stage = Usd.Stage.CreateNew('HelloWorld.usda')
xformPrim = UsdGeom.Xform.Define(étape, '/hello')
spherePrim = UsdGeom.Sphere.Define(stage, '/hello/world')
étape.GetRootLayer().Save()
```

Une fois exécuté, un fichier HelloWorld.usda sera généré dans le dossier spécifié.

```USD
#usda 1.0

def Xform "bonjour"
{
    def Sphère "monde"
    {
    }
}
```

À l'intérieur se trouve un simple fichier USD (vide).

![](https://gyazo.com/56dcb8770dbbd7053dd164a261f19fbe.png)

Quand je l'ai ouvert dans usdeview, il a montré une simple sphère.

Pour le moment, nous avons maintenant un environnement où nous pouvons toucher l'USD.  
Comme petite précision, car je n'ai pas mis PATH dans le dossier lib  
J'ai une erreur DLL introuvable  
Erreur d'autorisation lors de la spécification d'un dossier sur le NAS de Synology comme destination de sauvegarde  
où il ne pouvait pas être écrit.

Maintenant que nous sommes prêts, tout en explorant la structure de base de l'USD  
Je voudrais résumer comment l'utiliser.