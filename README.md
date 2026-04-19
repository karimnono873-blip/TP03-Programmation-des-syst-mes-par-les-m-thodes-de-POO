# TP N°03 : Programmation des Systèmes (POO) - "Saute Mouton" 🐑

**Université des Sciences et de la Technologie HOUARI BOUMEDIENE (USTHB)** **Faculté de Génie Electrique (FGE) | Département d'Automatique** **Spécialité :** Master 1 AII | **Module :** TP POO 

Ce dépôt abrite l'implémentation complète, l'analyse architecturale et l'environnement d'exécution web du projet "Saute Mouton". L'objectif de ce projet dépasse la simple écriture algorithmique : il s'agit d'une application stricte des concepts de Programmation Orientée Objet (POO), d'optimisation de la mémoire dynamique et de prévention des failles logicielles en langage Java.

---

## 🎯 Définition du Système (Cahier des charges)

Le système modélise un plateau de jeu unidimensionnel. À l'état initial, des pions Noirs (à gauche) et des pions Rouges (à droite) sont séparés par une unique case vide centrale.  
**Objectif de l'algorithme :** Inverser parfaitement cette configuration (Rouges à gauche, Noirs à droite, vide au centre) en respectant les contraintes physiques du système :
* **Vecteurs de déplacement :** Les Noirs ne se déplacent que vers la droite (+), les Rouges uniquement vers la gauche (-).
* **Cinématique :** Un pion peut glisser sur une case adjacente vide ou sauter par-dessus **un seul** pion adverse si la case de réception est vide.

---

## 🧠 Architecture Logicielle & Gestion de la Mémoire

Ce code a été conçu pour être "Memory-Safe" et hautement optimisé en termes de cycles d'horloge (CPU) et de consommation RAM :

1. **Allocation Dynamique (Heap vs Stack) :** Contrairement aux tableaux statiques du C++, l'instanciation `new char[taille]` retarde l'allocation dans le Tas (Heap) jusqu'au Runtime, après la saisie utilisateur. La variable `plateau` n'est qu'une référence légère stockée dans la Pile (Stack).
2. **Prévention des Exceptions (Memory Safety) :** L'accès aux indices du tableau est sécurisé par des conditions strictes (`pos >= 0 && pos < plateau.length`), empêchant le pointeur de lire des adresses non allouées et évitant le redouté `ArrayIndexOutOfBoundsException`.
3. **Complexité Algorithmique Optimisée :** Les fonctions de scan du plateau (`estGagne()`, `estBloque()`) ont une complexité de base de **O(N)**. Elles sont optimisées via des **évaluations en court-circuit** (`return false` immédiat), détruisant la boucle dès qu'une erreur d'état est détectée pour épargner le CPU.
4. **Garbage Collection (Zero Memory Leak) :** La clôture du flux matériel via `Scanner.close()` rend l'objet d'écoute orphelin, forçant l'intervention du Ramasse-miettes (Garbage Collector) pour restituer la RAM au système d'exploitation à la fin du processus.

---

## 🌐 Environnement d'Exécution Intégré (Web)

Ce projet inclut une **interface web avancée (`index.html`)** qui sert de portfolio technique interactif :
* **Émulateur de Terminal (Runtime) :** Un émulateur natif codé en JavaScript reproduit la logique mathématique et la machine à états du Java. Il permet de tester le système en temps réel directement dans le navigateur, sans avoir à compiler la JVM.
* **Dissection Technique :** Une documentation intégrée analysant chaque instruction logicielle sous l'angle de la consommation RAM et de l'expérience utilisateur (UX).

---

## 🚀 Comment exécuter le projet

### Option 1 : Démonstration Web (Recommandé)
Ouvrez simplement le fichier `index.html` dans n'importe quel navigateur web moderne. Vous pourrez interagir avec l'émulateur de terminal en bas de page pour jouer et tester les limites de l'algorithme.

### Option 2 : Compilation Java Native
1. Assurez-vous que le JDK (Java Development Kit) est installé sur votre machine.
2. Ouvrez un terminal (Bash, CMD, PowerShell) dans le répertoire du projet.
3. Compilez le bytecode :
   ```bash
   javac SauteMouton.java
