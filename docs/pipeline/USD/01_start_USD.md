---
title : Créer un environnement pour diverses opérations sur USD à partir de Python
description : Comment tirer parti de Jupyter Notebook
---

# Créer un environnement pour diverses opérations sur USD à partir de Python

Je pensais que j'expliquerais d'abord les bases autour de l'USD et l'explication autour de la structure  
Si j'écris avec une compréhension vaguement à moitié cuite~~~J'ai l'impression que je vais être légèrement gêné~~~  
On dirait que ça va semer la confusion, alors je vais méditer un peu plus dessus...

J'ai pu ouvrir USD avec usdview la dernière fois, donc  
Au lieu d'écrire directement le fichier USD tel quel, faites-le fonctionner du côté Python  
Je voudrais créer un environnement pour vérifier ce qui se passe.

## préparation

Tout d'abord, préparez-vous.  
Usdview peut vérifier le modèle, mais ce n'est qu'une visionneuse  
Vous ne pouvez pas faire des choses comme le contrôle en entrant des valeurs numériques dans AttributeEditor.

![](https://gyazo.com/c9db8ccab23266051d25085db95c77bd.png)

Cependant, si vous voulez jouer avec des nombres, PythonInterpreter est attaché, donc  
Vous pouvez le contrôler à partir de là.

Mais... c'est impossible de faire de mon mieux avec cet interprète  
J'ai décidé de créer un environnement en utilisant VSCode et Jupyter.

Tout d'abord, utilisez la série Python 3.  
Mais ici nous n'avons pas usdview  
Téléchargez séparément USD (build nvidia) pour Python2  
Ouvrez usdview à partir de là.

```
cd /d I:\jupyter_notebook_root
cahier jupyter
```

Pour le moment, créez un lot qui peut démarrer Jupyter à un emplacement fixe comme celui-ci  
Démarrer le bloc-notes en arrière-plan.  
Mais lorsque j'utilise ce notebook depuis mon navigateur,

![](https://gyazo.com/b3a8bf3a0e527f61b217b5cab8d82e9d.png)

Il peut être utilisé pour le moment, mais dans ce cas, la saisie semi-automatique ne fonctionne pas  
Comme le raccourci est difficile à utiliser, je vais essayer de le frapper du côté korewoVSCode.

![](https://gyazo.com/de2de82522cab139a46da49981bae9cc.png)

Ouvrez les paramètres URI du serveur Jupyter de Python,  
Entrez l'URL du Notebook exécuté en arrière-plan.

Cependant, il était difficile d'insérer le jeton

```
bloc-notes jupyter --generate-config
```

Tout d'abord, créez une configuration,

C:/Users/<nom d'utilisateur>/.jupyter

Ci-dessous, dans jupyter_notebook_config.py

```python
c.NotebookApp.token = ''
```

Supprimez le jeton et

```python
c.NotebookApp.password = "sha1:～～～～"
```

Tapez votre mot de passe.

Le mot de passe est

```
python -c "importer IPython; imprimer (IPython.lib.passwd())"
```

Vous pouvez le générer avec cette commande.

et.

Une fois que tout est prêt, il est temps de tester les choses côté VSCode.

## Faites quelque chose avec VSCode

![](https://gyazo.com/833bf64be619f449b049a72ce03c982b.png)

Dans la version actuelle de VSCode, lorsque j'ouvre .ipynb (au format JupyterNotebook)
Vous pouvez modifier des cahiers sur VSCode.
(Des raccourcis, etc. de VSCode peuvent également être utilisés)

## imprimer

Tout d'abord, imprimons le contenu du fichier USD avant de l'ouvrir avec usdview.

```python
print(stage.GetRootLayer().ExportToString())
```

Puisque vous voudrez le vérifier souvent, divisez-le uniquement en cellules  
J'essaierai de l'imprimer si nécessaire.

![](https://gyazo.com/67708aa3b9cd65a747f03ca9084c6a11.png)

Comme ça, le fichier USD actuel (couches pour être précis)  
peut être imprimé.

Par précaution, lors de l'impression, comme "imprimer (~~~)"  
Que vous devez utiliser la commande d'impression correctement.  
Il peut être affiché sans lui, mais dans ce cas, les sauts de ligne ne sont pas possibles.

### enregistrer

Exportez la scène lors de l'enregistrement.  
Je le ferai fréquemment, il est donc pratique de le garder dans une cellule.

```python
étape.GetRootLayer().Export(USD_PATH_ROOT + "/refTest.usda")
```

Il sortira comme ceci.

USD peut également être NewOpened et Saved lors de l'ouverture  
S'il y a déjà un fichier, ce sera une erreur, donc c'était un peu gênant

```python
# Créer un fichier une fois en mémoire
stage = Usd.Stage.CreateInMemory()
# Exporter
étape.GetRootLayer().Export("CHEMIN")
```

Il est préférable de créer une scène en mémoire comme celle-ci et de l'exporter à la fin  
Je pense qu'il est facile de tester avec une nouvelle scène à chaque fois. (peut-être)

### ouvrir avec usdview

Après l'exportation, ouvrez le fichier avec usdview.

```
usdview I :\usd_test\refTest.usda
```

Est-ce un piège lors de l'utilisation d'usdview sous Windows ?  
Le fichier usd passé en argument doit être un chemin complet et le fichier usd doit être passé en argument.
De plus, comme le démarrage de cet outil est inhabituellement lent  
Ouvrez-le avec un fichier approprié uniquement pour la première fois  
Il est recommandé d'ouvrir ou de recharger le fichier à partir du menu de l'outil.

![](https://gyazo.com/052b4430de2622643f14ae59322af78d.png)

Je viens d'ouvrir le fichier.

Si vous êtes prêt jusqu'à présent, alors en écrivant le code du côté VSCode  
Après avoir enregistré, rechargez la scène avec Ctrl + R dans usdview et les propriétés, prims et apparence  
Assurez-vous qu'il ressemble à ce que vous voulez.

https://snippets.cacher.io/snippet/e4a461c3093c7ce7929f

Après cela, le résultat du test est téléchargé sur Cacher sous forme de mémo.

## petite histoire

![](https://gyazo.com/5878a971ba83dcf4312eb3e6d1afcaae.png)

Affichage du résultat d'exécution PythonInteractive de VSCode  
Ça devient de plus en plus.  
mais peut être réinitialisé en appuyant sur le bouton X dans le coin supérieur droit d'Interactif.

Vous pouvez également le sortir sous forme de fichier Jupyter ipynb en appuyant sur l'icône de disquette.

https://snippets.cacher.io/snippet/90166b7fd86eb73d7d0e

Je peux le sortir, mais je ne pense pas que je l'utiliserai beaucoup.

Pour le moment, si vous avez fait jusqu'ici, vous pouvez jouer avec Python  
Nous avons créé un environnement sans stress.

Probablement, pour l'utiliser comme format de données avec Exporter, etc.  
Je pense que tu n'as pas besoin d'aller aussi loin.  
Après tout, pour gérer la synthèse USD, le fonctionnement avec Python ou C ++ est essentiel.  
Parce qu'il est important de gérer du côté Python en termes de compréhension de la structure des données

Je pense qu'il est important de rendre l'environnement de test sans stress.