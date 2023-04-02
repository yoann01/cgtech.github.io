---
Mots clés:
    - SOLARIS
    -Houdini
    - USD
---



## USD/SOLARIS

Et avant de commencer, un petit rappel sur l'USD.  
USD est une bibliothèque de gestion des scénographies créées par Pixar.  
C'est un format de fichier créé pour que plusieurs personnes travaillent en même temps.

La principale différence par rapport au format de fichier existant est  
Rendre plusieurs fichiers USD "procéduraux", appelés "scénographie procédurale"  
La possibilité de composer et de construire un seul scénographie.

![](https://gyazo.com/c08ab343dda8859f5b408132e8ddf508.jpg)

À partir des diapositives du séminaire de lancement.

SOLARIS supporte nativement cet USD.  
Synthétiser procéduralement le fichier USD pour gérer le SOP,  
Vous pouvez construire un scénario.

![](https://gyazo.com/0b54cdb337ab5eaa35ab5ead0e7429bc.png)

Une autre caractéristique est que les nœuds de ce SOLARIS (réseau Stage) sont  
en mémoire ou dans un fichier  
Chaque nœud est un fichier USD et traité comme une couche.

Traitement des nœuds = Traitement USD = Construction procédurale du graphe de scène

C'est le monde de SOLARIS.  
Le monde de SOLARIS est aussi le monde de l'USD lui-même.

C'est un aperçu approximatif de SOLARIS et USD.

## Télécharger le fichier USD

Nous sommes donc prêts à ouvrir.  
Pour cet échantillon, j'apporterai un fichier USD officiel de Pixar.

http://graphics.pixar.com/usd/downloads.html

Chaque fois que je télécharge le KITCHEN SET familier sur le site de téléchargement officiel.

## Ouvrir SOLARIS

Une fois téléchargé, lancez Houdini18.

![](https://gyazo.com/12c067a991b01b4c2f7ddb3398d1c0c9.png)

Une fois démarré, changez la disposition de l'écran en Solaris.

### Composition de l'écran

SOLARIS a ajouté deux nouvelles vues que Houdini n'avait pas auparavant.

![](https://gyazo.com/fbf024ed32a3bcb741cd10c7cdd239dc.png)

Le premier est l'arborescence des graphes de scène  
Ceci affiche un ``scenegraph en USD'' (appelés étapes) des étapes du nœud actuellement sélectionné.  
Ce SOLARIS signifie "USD Procedural Scene Graph"  
Un nœud est traité comme un fichier USD = couche.  
Lorsque vous connectez des nœuds, les nœuds sont composés de manière procédurale.  
et pour les nœuds qui sont actuellement sélectionnés ou dont l'indicateur d'affichage est activé  
L'étape est "le résultat de la composition des nœuds jusqu'à ce point".  
  
Le graphique de scène résultant est affiché comme  
C'est ce "Scene Graph Path".  
  
L'autre est "Scene Graph Detail".  

![](https://gyazo.com/77fcd27b285a8dbdb75b48de3ba3e258.png)

Il s'agit d'un panneau dans lequel vous pouvez centrer les attributs de la primitive actuellement sélectionnée et d'autres informations diverses.  
Quand je commence à expliquer les détails, il y a suffisamment de matière pour écrire un article ici.  
Je vais l'omettre cette fois, mais quand vous regardez chaque individu, vous pouvez voir comment ils sont composés.  
Vous pouvez voir les valeurs d'attribut actuelles, etc.  
  
Ces deux-là seront plus attachés à USD qu'aux fonctionnalités SOLARIS.  
Étant donné que le résultat de la construction d'un graphe scénique dans SOLARIS est affiché dans ces deux  
Si vous vérifiez ces deux panneaux avec la création de nœuds  
C'est facile à comprendre à bien des égards.  
  
Par conséquent, je vais montrer ces deux ensemble dans l'explication ci-dessous.

## USD, ouvrons-le

Passons donc au sujet principal.  
Ouvrez le fichier USD téléchargé avec Houdini/SOLARIS.  

![](https://gyazo.com/d33dec1b340af443fcaae9bb7d9ce326.png)

Tout d'abord, utilisez le nœud "LoadLayer" pour ouvrir le fichier USD.  
La raison pour laquelle ce n'est pas LoadUSD est  
En effet, USD fait référence aux fichiers USD en tant que couches.

Pour plus de détails à ce sujet,  
https://fereria.github.io/reincarnation_tech/11_Pipeline/01_USD/04_layer_stage/  
Voir article précédent.

![](https://gyazo.com/87d8b7fcbb7e911938c72c9112a23d0d.png)

Cependant, puisque l'ensemble de cuisine est Zup  
Comme ce sera étrange si c'est comme ça, ouvrez les fenêtres 3D,  

![](https://gyazo.com/06048f4a13b907278e50a6711a3f4e70.png)

Changez l'orientation en "Z UP".

![](https://gyazo.com/3e4def8e6db9c4f78fc37b125bda50c9.png)

J'ai pu charger avec succès.  
Je voudrais dire que ce sera OK si divers processus sont effectués à ce sujet.  
En fait, SOLARIS a différentes manières de lire l'USD.  
Jetons un coup d'œil aux autres méthodes de chargement.

## ChargerCouche
    
Tout d'abord, le LoadLayer utilisé ci-dessus "charge l'USD spécifié en tant que couche".

![](https://gyazo.com/db5e31904a121df2625dd543d1a0dfe2.png)

C'est facile à comprendre en regardant le SceneGraphPath, mais en utilisant ce nœud  
Pour root, "chargez" l'USD spécifié tel quel.  
Je n'ai rien fait d'autre.  

## Ouvrir avec le nœud d'arc de composition

Alors, quel genre de méthode existe-t-il autre que LoadLayer ?  
Divers nœuds d'arc de composition préparés comme nœuds SOLARIS  
je vais le charger.  
Lorsqu'il est chargé avec ce nœud, ainsi que la fonctionnalité des arcs de composition,  
Vous pouvez charger des fichiers USD.
S'il est lu comme ceci, le ClassPrim dans le fichier usda chargé est caché
Il ne peut plus être remplacé.
Mais si je le charge avec LoadLayer puis que je connecte ce nœud à un nœud de référence,  
Synthétisez la couche que vous souhaitez lire par référence une fois en tant que sous-couche  
Après cela \</sdfPath...\> Prim dans la scène comme celle-ci
Il sera chargé en tant que référence.

Dans ce cas, la couche n'est pas encapsulée et une autre prim dans la couche spécifiée est également chargée.
Semblable à l'héritage, vous pouvez désormais remplacer la prim de référence.
Pour plus de détails [ici](03_comp_arc_inherits.md) car la vérification est résumée
se il vous plaît se référer.

### Ouvrir dans le sous-calque

Tout d'abord, ouvrez-le dans le nœud Sous-couche.  
  
![](https://gyazo.com/65d86205563105def4a757da5fd482d9.png)

Lorsqu'il est ouvert avec une sous-couche, les bases sont les mêmes que lorsqu'il est chargé avec LoadLayer.  
  
![](https://gyazo.com/7fe464cc59894c03a62fa89d912489e2.png)

Le chemin du graphe de scène sera également le même que lorsque LoadLayer est utilisé.  
La différence avec loadlayer est que vous pouvez combiner des fichiers USD avec des sous-couches avec ce seul nœud.  
  
![](https://gyazo.com/8579995b8c8d05ed79a24f27d2c7ead4.png)

Par exemple, chargez trois fichiers comme celui-ci :  

![](https://gyazo.com/9bff0fba0911963e70b5f414ffda6280.png)

Comme une boule verte avec base.usda comme ça.  
  
![](https://gyazo.com/8616c46e18c492f7360d3be25481107a.png)

Changez la couleur en rouge avec add_color.usda  
  
![](https://gyazo.com/663563ef426f159324fc653667463a7e.png)

Essayez de le rendre carré avec final.usda.  
  
Ensuite, il sera synthétisé dans l'ordre à partir du haut, et le résultat de la synthèse de tout sera produit à la suite de ce nœud.  
  
![](https://gyazo.com/1517709aa704c16940649eed8e3ef207.png)

L'avantage de synthétiser plusieurs USD dans cette sous-couche est  
Il est possible d'activer/désactiver l'effet de l'USD en utilisant Mute Layer et Enable.  
Par exemple, désactivons "add_color.usda" parmi ces trois échantillons.  
  
![](https://gyazo.com/1f40bdf1ef7f38294768e6bb6b66b417.png)

Ensuite, ce qui se passe, c'est que seule la couche (fichier USD) appelée "Red" est muette  
Vous vous retrouverez avec un cube vert.  
De cette façon, pour activer / désactiver la couche de logiciel 2D  
C'est l'effet du noeud Sublayer qui vous permet de basculer et de vérifier facilement l'effet de calque USD.  
  
Pendant le chargement, vous pouvez l'activer et le désactiver comme un calque PhotoShop  
C'est l'avantage de lire en utilisant ce nœud.
  
### Ouvrir avec référence

![](https://gyazo.com/01bc89a88163c456fa10e185ba3085ad.png)

Essayez maintenant de le charger à l'aide du nœud de référence.  
  
![](https://gyazo.com/8e657966e5a397e2e394f6dae0af7f4b.png)

Le nœud de référence a également une fonction pour référencer le résultat d'entrée de MultiInput  

![](https://gyazo.com/00bddb25883ddc0c7803c433a9ae0830.png)
En réglant Type de référence sur Fichiers de référence,  
Vous pouvez utiliser ce nœud pour "Charger le fichier USD par référence".  
  
![](https://gyazo.com/39cab059035ce2a16e068a57bc790e86.png)

En regardant le SceneGraphPath, nous pouvons voir que les noms primitifs sont verts.  
De plus, la grande différence avec LoadLayer est que "le nom du nœud supérieur est différent".  
Lorsqu'il est chargé avec LoadLayer, la structure primitive écrite dans le fichier USD est  
Il sera chargé tel quel.  
Mais pour les références, la différence est  

![](https://gyazo.com/db1f6e2700a342d292056e2c555ea4e9.png)

Sous le nom de la primitive spécifié dans Destination Primitive  
Lit la primitive USD lue par référence.  
Puisque $OS est le nom du nœud, la primitive enfant est chargée sous reference1 qui est le nom du nœud.  
  
![](https://gyazo.com/47e20b46bcea9c6562f67f7b98b05c4e.png)

Essayez de cliquer avec le bouton droit sur le nœud de référence et d'ouvrir Actions LOP > Inspecter la couche active.

```USD
#sdf 1.4.32

def HoudiniLayerInfo "HoudiniLayerInfo" (
    donnéespersonnalisées = {
        chaîne HoudiniCreatorNode = "/stage/reference1"
        chaîne[] HoudiniEditorNodes = ["/stage/reference1"]
    }
)
{
}

def "référence1" (
    préfixer les références = @C:/pyEnv/JupyterUSD_py27/usd/Kitchen_set/Kitchen_set.usd@
)
{
}
```
Lorsque vous ouvrez ce menu, vous pouvez voir l'état actuel de l'édition du nœud (= fichier USD du nœud)  
Vous pouvez le vérifier avec un fichier ASCII.  
  
J'ai expliqué que tous les nœuds sont des couches, mais cet ActiveLayer est "USD de ce nœud"  
C'est pourquoi.  
Donc, en regardant cela, vous pouvez voir ce que fait ce nœud maintenant et ce qu'il fait en termes d'USD  
Tu peux le vérifier.  
  
Donc, d'après ce que je peux voir, vous pouvez voir qu'il est lu par référence.  

### Différence de lecture avec le nœud de référence * 2020/01/05 ajouté

Il a été trouvé plus tard lors de l'examen du comportement détaillé du nœud  
Lorsqu'il est chargé à l'aide d'un nœud de référence et après le chargement à l'aide d'un LoadLayer  
J'ai trouvé qu'il y a une grande différence entre les nœuds de connexion et de référence.  
La "différence" est **si encapsuler ou non**.

Lorsqu'il est chargé avec un nœud de référence, lorsqu'il est visualisé avec l'USDA
préfixer les références = @C:/pyEnv/JupyterUSD_py27/usd/Kitchen_set/Kitchen_set.usd@
En spécifiant le chemin du fichier comme celui-ci, le prim spécifié par USDA DefaultPrim ou SdfPath du chemin spécifié  
sera chargé par référence.


## Ouvrir avec StageManager

![](https://gyazo.com/a3cbe3fa1431c43261fd9c6e2b227f6d.png)

Enfin, comment ouvrir autre que l'arc de composition.  
C'est le noeud StageManager.  
  
Il existe de nombreux exemples d'utilisation de ce StageManager dans les vidéos de didacticiel  
Quelle est la différence entre les trois ci-dessus et ce StageManager ?  
  
Comme la grande différence est le gestionnaire "Stage", ce nœud est  
Vous pouvez construire une scène par elle-même.  
  
Une étape dans ce cas fait référence au résultat de la composition de plusieurs fichiers USD.  
  
![](https://gyazo.com/bc946750eba4166a0a9ac58e4b768464.png)

Une fois ouvert, l'écran StageManager ressemblera à la fenêtre de l'image ci-dessus.  
Cliquez sur l'icône du dossier qu'il contient.  
  
![](https://i.gyazo.com/154b283e8603f72965cb9740531eb334.gif)

Jusqu'à présent, les nœuds étaient principalement ceux qui lisaient un fichier USD avec un nœud  
Ce StageManager construit une scène (un graphe de scène résultant de la composition USD) par lui-même  
Parce que c'est un nœud qui peut le faire, chargez plusieurs USD avec des références, etc.  
Vous pouvez construire une étape tout en regroupant.

![](https://gyazo.com/d2c5c7780351d44e75f13c514d036357.png)

Ainsi, pour ce nœud StageManager seul, le ScenerGraphPath est  
Une étape terminée est construite. (Orange est chargé par l'arc de composition)  
  
## Écrivez le fichier ASCII tel quel et ouvrez-le

![](https://gyazo.com/c57bdcde55538e2b7bab3e01d50b719f.png)

Peu de gens le font, mais avec inlineusd,  
Vous pouvez écrire et lire des fichiers USD à la main au lieu de fichiers.

![](https://gyazo.com/ddc9efcb3436aa6016fb37a1d36f2349.png)

En écrivant en ASCII pour USD Source comme ceci,

![](https://gyazo.com/6e567590ef26de63133b389d93f99478.png)

Vous pouvez réellement créer une scène dans SceneGraphPath comme celle-ci.  


## Alors, comment puis-je l'ouvrir ! ! ? ?

Comme vous pouvez le voir, il existe de nombreuses façons d'ouvrir un fichier USD.  
Je ne sais pas quoi faire avec ça !  
Présentation de ma propre recommandation pour ceux qui disent.  
  
### "StageMnaager" si vous voulez placer beaucoup d'objets

![](https://gyazo.com/602c4cd806705c1680efdef7b8891968.png)

Si vous voulez faire des mises en page dans la scène, vous pourriez vous retrouver avec des centaines d'éléments.  
Vous devrez le charger et le placer.  
Dans un tel cas, il est très gênant de les lire un par un ou de les regrouper.  
  
Dans ce cas, si vous utilisez StageManager, vous pouvez charger tous ensemble par référence  
Le chargement de plusieurs actifs est facile avec le glisser-déposer
Vous pouvez facilement effectuer des opérations telles que le regroupement et la modification de la hiérarchie.  
  
En d'autres termes, la construction de la scène est terminée avec ce seul nœud.  
Par conséquent, ce nœud est recommandé pour les mises en page.

![](https://gyazo.com/f680a2f9047f6d24c24673460f2f66cb.png)

Bien sûr, si vous mettez tout cela ensemble dans un seul StageManager, cela deviendra désordonné ! ! !  
Dans ce cas, vous pouvez également connecter plusieurs StageManagers.  
Dans ce cas, ajoutez des assets avec + α au graphe de scène de la scène reçu en entrée  
devient possible.  

### "Reference" si vous souhaitez encapsuler une couche

DefaultPrim de la couche que vous souhaitez lire par référence ou autre que la prim spécifiée
Si vous souhaitez "l'encapsuler", chargez-le à l'aide d'un nœud de référence.
Lorsqu'elles sont lues avec le nœud de référence, toutes les prims autres que la prim spécifiée sont masquées.
Il ne peut plus être remplacé.
Donc, si vous voulez lire un caractère, etc.
Le chargement à l'aide d'un nœud de référence semble bon.
  
### sinon "LoadLayer"

En dehors de cela, LoadLayer + nœud d'arc de composition ou autre nœud pratique (Graft, etc.)  
est recommandé.  

Après cela, je veux construire une structure basée sur la base de nœuds de SOLARIS pour le modèle lu par LoadLayer  
(Tout en combinant des nœuds légers qui souhaitent créer des variations avec des variantes et attribuer des shaders  
Je veux construire une scène... etc.  
  
![](https://gyazo.com/65827db5367f92eb61c4d309a4d860ac.png)

Vous pouvez lire le fichier directement avec SubLayer ou Reference  
Dans ce cas, il est très difficile de remplacer l'ordre d'entrée ou de le désactiver temporairement.  
Je l'ai trouvé difficile à utiliser car la listabilité au niveau du nœud n'était pas si bonne.  
  
Si vous lisez et composez toujours avec LoadLayer,  
Il est facile de basculer et clarifie "lecture d'un fichier"  
Personnellement, je pense qu'il est préférable d'utiliser LoadLayer pour le chargement unique de fichiers USD.  
  
### Bien sûr, vous pouvez utiliser les deux

Bien entendu, les nœuds d'arc de composition StageMnaager et LoadLayer + peuvent être utilisés ensemble.  

![](https://gyazo.com/ea296ad1a04c0989d6fd3d60428d4fbc.png)

Lors de la construction collective d'une scène avec StageManager, faites des variations détaillées avec des nœuds  
Enfin, synthétisez  
En utilisant différentes manières d'ouvrir plusieurs USD dans le bon sens  
Il est également possible de construire le plus simplement possible des nœuds dans une scène complexe.  
  
## sommaire

Il s'agissait d'une introduction à l'ouverture de fichiers USD dans SOLARIS/LOP.  
Il est étonnant qu'il existe autant d'approches différentes simplement en ouvrant un seul fichier USD.  
Vous pouvez également ouvrir des scènes + SOP avec LOP et ainsi de suite.  
SOLARIS est très flexible lorsqu'il s'agit d'USD et permet la création de divers USD en fonction de la façon de penser.  
Je pensais que c'était un outil.  
  
  
Je me demande si ce genre d'article est la première étape pour écrire beaucoup d'articles SOLARIS ?  
Ensuite, il s'agit du nœud d'arc de composition que j'ai écrit brièvement cette fois  
J'aimerais écrire un peu plus à ce sujet.  
  