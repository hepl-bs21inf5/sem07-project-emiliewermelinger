Séminaire 07 - Projet

[Emilie Wermelinger]

## Journal de bord

## Semaine 1 projet

### Tâche/ Temps estimé/ Temps réel

- installation de l'extension et création/modification des dossiers pour le projet
  temps estimé: 25 min/temps réel : 45 min

- modification du quizz/ajout de questions et de réponses
  temps estimé: 35 min/temps réel : 1h

- affichage du score/message et bouton réinitialiser à la fin du quizz
  temps estimé: 45 min/temps réel : 1h15

- modification des boutons (css)
  temps estimé: 30 min/temps réel : 40 min

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

- Créer nouveau fichier appelé QuestionRadio.vue et y ajouter le code 
  temps estimé : 10 min/temps réel 10 min

- Créer une nouvelle question en faisant appel à QuestionRadio
  temps estimé : 15 min/ temps réel 25 min

- Modifier les questions afin qu'elles fassent toutes appel au code de QuestionRadio
  temps estimé : 35 min/ temps réel 20 min

- Créer le code pour les questions QuestionText
  temps estimé : 45 min/ temps réel 1h30

- Ajouter une tab Trivia et créer de document QuizTrivia.vue
  temps estimé : 20 min/ temps réel 20 min

  ### Commentaire:
  Il faut bien faire attention à ce que l'on modifie dans quaque code, car si on modifie dans QuestionText.vue cela peut avoir un impact dans le code de QuizForm.vue ou alors sur le rendu visuel du site internet.

  ### Questions:
  #### Comment rendre la propriété placeholder optionnelle ?
  - Il faut dans les documents parents mettre comme cela placeholder:{type: String, default : ''}.
  Cela signifie que le message affiché par défault si rien n'est indiqué spécifiquement pour chaque question est vide, rien ne s'affichera.

  #### Quelle est la différence entre un prop et un modèle (v-model) ?
  - Un prop permet de transmettre certaines données d'un composant parent à un composant enfant. 
  - un v-model permet de transmettre certaines données dans les deux-sens (document parent->enfant et inverse), ils peuvent donc tous les deux modifier la donnée.

## Semaine 3 projet

### Tâche/Temps estimé/ Temps réel

- Modifier le document Questionradio.vue afin d'afficher si la réponse sélectionnée et true ou false
  temps estimé : 15 min/ temps réel 15 min

- Modifier le QuizzForm.vue afin que chaque solution soit dans la liste affichée de réponses juste ou fausse/ modifier le v-model
  temps estimé : 15 min/ temps réel: 25min


### Commentaire:
Il faut faire attention à bien modifier les v-model de chaque question. et de bien les ajouter dans le liste des correctAnswers.Il faut bien modifier l v-model dans QuestionRadio.vue afin que ce ne soit plus un model mais un value qui reprend la const value.