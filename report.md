Séminaire 07 - Projet

[Emilie Wermelinger]

## Temps passé

## Semaine 1 projet

### Tâche/ Temps estimé/ Temps réel

- installation de l'extension et création/modification des dossiers pour le projet
  estimé: 25 min/temps réel : 45 min
- modification du quizz/ajout de questions et de réponses
  estimé: 35 min/temps réel : 1h
- affichage du score/message et bouton réinitialiser à la fin du quizz
  estimé: 45 min/temps réel : 1h15
- modification des boutons (css)
  estimé: 30 min/temps réel : 40 min

### Commentaire:

Au début, il n'est pas simple de comprendre le fonctionnement de chaque commande mais à force de travaille avec, cela devient logique.
Commentaires ajoutés dans le code src->components->QuizForm.vue qui aide à comprendre et se rappeler de quelques détails importants pour le fonctionnement du code.

### Questions:

#### Expliquer le rôle des fichiers suivants

1. main.ts : permet à main.css d'aller chercher les infos sur un autre site (bootstrap). C'est aussi la page principale de notre application.
2. main.css : permet de coder le style visuel utilisé dans notre code (personnalisation des boutons)
3. App.vue : permet de choisir la forme de la page (émoticone)
4. router/index.ts : permet de créer un lien entre toutes les pages de notre site internet.
5. AboutView.vue : permet d'afficher le message voulu lorsque l'on clique sur le "à propos" dans la nav-barre
6. HomeView.vue : permet de créer la page où s'affichera notre quizz et de l'afficher en faisant référence à notre document appelé QuizForm
7. QuizForm.vue : Ce fichier est le fichier où nous codons notre quiz (questions, réponses, score). Il est repris par HomeView afin de l'afficher.

#### Quelles sont les similarités et les différences entre ref et computed ?

- ref et computed permettent de modifier des valeurs.
  Ref permet de modifier des valeurs directement alors que computed peut être modifié via le changement d'une autre valeur.

#### Que se passe-t-il lorsqu'on clique sur le bouton "Terminer" ?

- Lorsque l'on appuie sur le bouton "terminer" un "pop-up" s'ouvre et nous indique notre score.

#### Qu'est-ce qu'un v-model ?

- Le v-model permet une fois qu'il est défini (par question) d'y faire référence pour calculer le score et reset le quizz

#### À quoi sert le :class="{ disabled: !filled }" ?

- :class="{ disabled: !filled }" permet de vérifier que nous avons répondu à toutes les questions. Si ce n'est pas le cas, alors nous ne pouvons pas appuyer sur le bouton.

## Semaine 2 projet

### Tâche/ Temps estimé/ Temps réel

- Créer nouveau fichier appelé QuestionRadio.vue et y ajouter le code estimé : 10 min/temps réel 10 min
- Créer une nouvelle question en faisant appel à QuestionRadio
  estimé : 15 min/ temps réel 25 min
- Modifier les questions afin qu'elles fassent toutes appel au code de QuestionRadio
  estimé : 35 min/ temps réel 20 min
