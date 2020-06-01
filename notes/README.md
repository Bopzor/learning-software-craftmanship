# Software craftsmanship - TDD

## Table des matières

- [Méthodologie](#méthodologie-)
  - [Agile](#agile-)
    - [SCRUM](#scrum-)
    - [Kanban](#kanban-)
  - [Software Craftmanship](#software-scrafmanship-)
    - [Extrem Programming (XP)](#extrem-programming-(xp)-)
- [Clean code et Test Driven Development (TDD)](#clean-code-et-test-driven-development-(tdd)-)
  - [Clean code](#clean-code-)
  - [TDD](#tdd-)

## Méthodologies [↟](#table-des-matières)

### Agile [↟](#table-des-matières)

> vs : Cycle en V et Waterfall

La méthodologie agile met l'accent sur :

**Les personnes et la communication.**  
Auto-organisation  
Faire confiance à l'équipe  
Amélioration continue  

**Des logiciels opérationnels.**  
Livrez régulièrement un logiciel opérationnel

**La collaboration avec le client.**  
Intégrer le client pendant toute la durée du projet (pas uniquement au début et à la fin)  
Livraison régulière de fonctionnalité à grande valeur ajoutée  

**L'adaptation au changement.**  
Accueillir le changement positivement  
Encourage un rythme soutenable pour les développeurs  

Livrer rapidement et régulièrement des fonctionnalités à grande valeur ajoutée

> ex : site de vente en ligne de chaussettes, 1er rendu avec un site static photos, prix, contact

Pouvoir mettre ces fonctionnalités en production dès les premiers jours.  
Plus il y a de mise en production, plus la mise en production est connue.

Dès que l'on peut automatiser quelque chose, il faut le faire.

Iron Triangle :

```
       ___
      /   \
     /     \
    / cost  \
   -----------
  / \quality/  \
 /   \     /    \
/time \   /scope \
-------------------
```

La méthodologie agile :

- Temps fixe
- Prix fixe
- Scope / feature variable

#### SCRUM [↟](#table-des-matières)

Découpe le temps et le produit  
Product backlog,  
Retrospectives,  
Sprint

#### Kanban [↟](#table-des-matières)

Flux continue => sortir en production le plus rapidement, feature commencée = feature en production avant le début d'une autre.

### Software Craftmanship [↟](#table-des-matières)

Remet l'humain au premier plan

#### Extrem Programming (XP) [↟](#table-des-matières)

Réduire le temps de feedback :  
Tests unitaire,  
Pair programming,  
Code review,  
Tests fonctionnel,  
Partage de connaissance,  
Connaissance du code,  

Planning Game : Estimer de façon relative la valeur des features (ne pas parler en temps)

## Clean code et Test Driven Development (TDD) [↟](#table-des-matières)

### Clean code [↟](#table-des-matières)

#### Simple Design code [↟](#table-des-matières)

- testé
- révèle son intention
- sans duplication de connaissance (!== contexte)
- facile / simple à lire

#### Commentaires à exclure sauf pour [↟](#table-des-matières)

- expliquer pourquoi
- documenter une API publique

#### Refactoring [↟](#table-des-matières)

Ne jamais faire un refactoring sans raison (ajout de feature, résolution de bug...) et si le code n'est pas testé.

Technique de refactoring :
Golden master - prendre le code existant comme référence.
Pour éviter de devoir se plonger dans le code et le comprendre, s'il n'y a pas de test, écrire un / des tests qui passe.

Utiliser le code coverage pour écrire des tests qui passe dans tout le code, afin de s'assurer que la majorité des cas ont été couvert par les tests.

Utiliser des Approvals Tests pour obtenir des snapshots afin de voir les différences entres les résultats du tests de référence (appoved) et du test reçu (received).

Passer par une étape de "remise à plat" du code, en explicitant les cas, pour mettre en évidence les duplications et les incohérences.

#### Code smells [↟](#table-des-matières)

**S**ingleton  
**T**ight coupling  
**U**ntestable  
**P**remature optimisation  
**I**ndescriptive naming  
**D**uplicate  

#### Pair-programming [↟](#table-des-matières)

Deux personnes devant un seul ordinateur, un seul clavier, une seule souris.
Travaillent sur la même feature, ensemble.

- Driver : écrit le code en faisant confiance. Peut être dans l'incertitude
- Navigator : guide. Il a la vision à long terme, fait de la review de code

Switch techniques :

- chess clock : Période de temps, changement toutes les x minutes
- ping pong : en TDD, changement après l'écriture d'un test rouge. En cycle

Le pair-programming est fatiguant. Il est préférable de commencer par 1 ou 2 heures maximum sur une journée et de prendre des pauses.

La technique du _pomodoro_ peut facilement s'appliquer ici :  
Définir une période (25min) pendant laquelle on travail, en coupant les notifications.
Au bout de cette période, prendre une pause (5min), puis recommencer. Il est recommandé de noter la liste des tâches à réaliser pendant ce cycle.  
En cas d'interruption par quelqu'un, **finir** la période ( _pause comprise_ ), avant de prendre le temps nécessaire.

En cas de désaccord pendant le pair-programming, il est possible de séparer le binôme pendant 10-20min afin d'écrire une solution chacun de son côté.
Cela permet de revenir discuter avec du code fait.

### TDD [↟](#table-des-matières)

Les tests sont le filet de sécurité du code.
Un test doit réaliser _une_ assertion, être lisible et permet de documenter le code.

#### Tests unitaires [↟](#table-des-matières)

- prouvent que le code fait ce qu'il est supposé faire
- plus on trouve le problème tôt, moins sa résolution coûte cher
- donnent confiance lorsque l'on fait des modifications
- rendre un code testable et testé conduit à un meilleur design
- le test explique ce que fait le code

Un test doit avoir au moins ces 5 qualités :  
**F**ast  
**I**solated (ne pas dépendre les uns des autres)  
**R**peatable (pas de random : avec la même entrée, doit toujours donner la même sortie)  
**S**elf-validating (ne pas nécessiter de manipulation extérieure)  
**T**imely (écrit au bon moment)  

Le mantrat du TDD :

Red ----> Green ----> Refactor ⤶ _loop_

Faire un test rouge (qui failed) le plus simple possible.
Faire l'implémentation la plus simple possible qui permet de fait passer le test au vert.
Refactorer le code et le test si nécessaire (révèle son intention ? pas de duplication ? facile à lire ?)

Il est préférable de continuer les tests dans la même directions (si on a commencé avec des cas simples, ne pas partir sur les cas particuliers tant que ces premiers ne sont pas couverts et implémentés).

Fake it (mock)  
Obvious implementation (si l'implémentation est évidente, on peut écrire le code sous ça n'est pas la plus simple)  
Triangulation (tester plus de cas spécifique)  
