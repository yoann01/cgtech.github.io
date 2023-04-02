---
title: Hpyer-V で仮想デスクトップを作成する
---

# Créer un bureau virtuel avec Hyper-V

## Activation d'Hyper-V

Tout d'abord, activez Hyper-V pour pouvoir utiliser des bureaux virtuels.

![](https://gyazo.com/30cf582edce07f8943019ef6b067de27.png)

Dans Windows Search, sélectionnez Activer ou désactiver les fonctionnalités Windows.
2
![](https://gyazo.com/d3e44f062bf954fc2ee57aef7ecf5f48.png)

Sélectionnez "hyper-V" dans la liste.
Après avoir sélectionné, Windows sera (probablement) redémarré.

![](https://gyazo.com/439070bb455a1178cff8c6f9d7359302.png)

Dans la barre de recherche saisissez "Hyper-V Manager" et exécutez-le..

!!! Note
    Si Hyper-V n'est pas activé dans les fonctionnalités Windows, Hyper-V Manager ne s'affichera pas.

## Créer un pc virtuel

Sélectionnez Actions → Cliquez sur Créer....

![](https://gyazo.com/5494adf458e0f5e0bd08ef894b570dcf.png)

Définissez le système d'exploitation sur Windows 10 DevEnviroment. Une fois que vous l'avez exécuté, tout ce que vous avez à faire est d'attendre
 et un environnement PC virtuel sera créé pour vous.

![](https://gyazo.com/16e28445b59f4b49b9ccde1bad693394.png)

Cliquez sur "Connecter" lorsque vous avez terminé.

## Setup

Tout d'abord, démarrez l'environnement virtuel créé et avant les paramètres initiaux de Windows, 
configurez la mise en réseau de votre environnement virtuel.


Exécutez Action → Gestionnaire de commutateur virtuel.

![](https://gyazo.com/840e7b4b953cdc50c092c0caf9bd5cda.png)

Sélectionnez le nouveau commutateur de réseau virtuel, sélectionnez "Externe" → Créer un commutateur virtuel.

![](https://gyazo.com/516f1a041ab3232c6a4d9336da760795.png)

Sélectionnez le système d'exploitation de gestion "Réseau externe". Cochez ON et "Appliquer". Connectez-vous ensuite à la machine virtuelle créée. Sélectionnez Paramètres de la machine virtuelle pour ouvrir l'écran des paramètres de l'environnement virtuel.

![](https://gyazo.com/1a803c6ae305a6a1ed4a697359c98938.png)

Depuis l'adaptateur réseau, remplacez le commutateur virtuel par celui créé en ↑.
Si ce réglage n'a pas été effectué, le réglage LAN d'Internet ne s'affichera pas. 
Internet n'était pas disponible dans l'environnement virtuel.

## Créer un point de contrôle

La bonne chose à propos des environnements virtuels est que vous pouvez créer des "points de contrôle".
Vous pouvez enregistrer les paramètres actuels de l'environnement virtuel.

Comme cette fois, je veux vérifier le test de l'outil dans un état complètement nu 
(autre que mon propre environnement avec certains paramètres) 
Donc, créez un "état initial" avec seulement l'installation minimale
Je veux revenir à ce moment si nécessaire.
  

![](https://gyazo.com/da8c8d0d1838011b6b5da8cf7177b5e5.png)

"Opération" → "Point de contrôle" sur l'écran de connexion de la machine virtuelle Choisir.
  
![](https://gyazo.com/d90cbd215d71c8ed180c4a1f79054929.png)

Donnez-lui un nom et cliquez sur "oui".

![](https://gyazo.com/08384cb96f73225a7f581ae3c0d5c56c.png)

Un arbre est créé pour chaque point de contrôle. Donc, créez un point de contrôle au moment où vous voulez ramifier le travail dans une certaine mesure Ce faisant, vous pouvez retourner tout l'environnement ou changer jusqu'à un certain point. Puisqu'il est possible de rebrancher à partir de la synchronisation modifiée Vous pouvez reproduire la situation dans divers modèles et environnements.
  
De plus, lorsque vous créez un point de contrôle, non seulement l'environnement de réglage du PC À ce moment-là, "l'état de l'application en cours d'exécution" est enregistré.
Par exemple, même si vous créez un "point de contrôle" avec Maya en cours d'exécution Maya sera sauvegardée comme elle a commencé.
![](https://gyazo.com/6769b487e83a630a0f3f9cc76af8745c.png)
La création de l'environnement est maintenant terminée. Travailler avec Maya sur une machine virtuelle était comme travailler sur un PC normal. L'atmosphère est comme l'utilisation de Maya via un bureau à distance.

L'environnement Python a été séparé dans une certaine mesure avec pipenv etc. Je voulais tester l'environnement autour de Maya complètement séparément, y compris les paramètres Windows. Il peut être assez bon de construire avec une machine virtuelle simple et performante.

## 参考

- https://qiita.com/nomurasan/items/3c58b964943a24751802
- https://fereria.github.io/reincarnation_tech/10_Programming/00_Settings/hyper-v/