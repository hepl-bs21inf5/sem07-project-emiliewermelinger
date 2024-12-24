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

#### Quelle est la différence entre un prop et un modèle (v-model) ?
  - Un prop permet de transmettre certaines données d'un composant parent à un composant enfant. 
  - un v-model permet de transmettre certaines données dans les deux-sens (document parent->enfant et inverse), ils peuvent donc tous les deux modifier la donnée.

#### Comment rendre la propriété placeholder optionnelle ?
  - Il faut dans les documents parents mettre comme cela placeholder:{type: String, default : ''}.
  Cela signifie que le message affiché par défault si rien n'est indiqué spécifiquement pour chaque question est vide, rien ne s'affichera.

## Semaine 3 projet

### Tâche/Temps estimé/ Temps réel

- Modifier le document Questionradio.vue afin d'afficher si la réponse sélectionnée et true ou false
  temps estimé : 15 min/ temps réel 15 min

- Modifier le QuizzForm.vue afin que chaque solution soit dans la liste affichée de réponses juste ou fausse/ modifier le v-model
  temps estimé : 15 min/ temps réel: 25min

- Modifier le composant QuestionText.vue afin qu'il fonctionne comme QuestionRadio.vue
  temps estimé: 20 min/ temps réel: 20 min


### Questions:

#### À quoi sert l'option immediate: true dans le watch ? Que se passe-t-il si on l'enlève ou si on met immediate: false ?  
- immediate : true permet d'exécuter immédiatement ce que l'on met dans le watch. Si l'on met false ou que l'on enlève le immediate, la fonction watch fonctionnera seulement lorsque la velur changera.

#### Proposer une autre manière de calculer le score (réécrire la fonction du computed) et comparer les deux méthodes.

- Une autre manière de définir le score serait d'utiliser la fonction reduce qui permettrait d'additioner directement les bonnes réponses. Si la réponse est true on ajoute 1 et sinon 0. 

const score = computed<number>(() => correctAnswers.value.reduce((acc, value) => acc + (value ? 1 : 0), 0));

Actuellement nous utilisons la fonction filter qui utilise un tableau qui va contenir les éléments true, puis on va mesurer la taille de ce tableau et cela va nous donner le score. Cette méthode est plus facile à lire que celle avec reduce. le désavantage de cette fonction est que si le tableau contient beaucoup d'éléments cela va prendre plus de mémoire à être executée.

### Commentaire:
Il faut faire attention à bien modifier les v-model de chaque question et de bien les ajouter dans le liste des correctAnswers.Il faut bien modifier le v-model dans QuestionRadio.vue afin que ce ne soit plus un model mais un value qui reprend la const value.

## Semaine 4 projet

### Tâche/Temps estimé/ Temps réel

- Créer un nouveau fichier models.ts
  temps estimé: 5 min/ temps réel: 5 min

- Ajouter un nouveau watch sur model pour corriger l'état de la question
  temps estimé: 15 min/ temps réel: 20 min

- Adapter le watch sur value pour qu'il mette à jour le modèle
  temps estimé: 15min/ temps réel: 20 min

- Adapter QuestionText.vue comme QuestionRadio.vue
  temps estimé: 20 min/ temps réel: 20 min

- Adapter la fonction submit et reset dans QuizForm.vue
  temps estimé: 20 min/ temps réel: 45 min

- Rendre les réponses immuables
  temps estimé: 20 min/ temps réel: 35 min

### Questions:

#### Comment pourrait-on réécrire la ligne suivante sans l'opérateur ternaire (avec des if et else) ?

model.value =
  value.value === props.answer ? QuestionState.Correct : QuestionState.Wrong;

  - Si la valeur entrée est égale à la réponse attendue, alors elle devient correcte (Correct), sinon elle devient incorrecte (Wrong).
  
  if (value.value === props.answer) {
  model.value = QuestionState.Correct;
} else {
  model.value = QuestionState.Wrong;
}

#### Comment pourrait-on réécrire autrement la logique du watch sur value ?

- On pourrait utiliser des if. On vérifie si newValue est null, si oui alors model.value devient  QuestionState.Empty, sinon elle devient QuestionState.Fill.

watch(value, (newValue) => {
  model.value = newValue === null ? QuestionState.Empty : QuestionState.Fill;
}, { immediate: true });

## Semaine 5 projet

### Tâche/Temps estimé/ Temps réel

- Mettre en place les réponses détaillées
  temps estimé: 15 min/ temps réel: 25 min

- Changer les couleurs dans un composant
  temps estimé: 15 min/ temps réel: 10 min

### Questions:

#### Remplacer {{ props.answer }} par {{ answerText }} dans le template.Expliquer pourquoi on a fait ce changement ainsi que le code du computed.
- Ce changement permet permet de récupérer le texte associé à la valeur de la réponse (props.answer) parmi les options données dans props.options. Si aucune correspondance n'est trouvée, il retourne simplement la valeur de props.answer.
Cela permet de simplifier le code dans le template car au lieu d'aller chercher dans chaque utilisation de pops.answer, il va le faire une fois dans le computed.

1. props.options.find((option) => option.value === props.answer) 
Cette ligne cherche dans le tableau options l'option qui correspond à la valeur de props.answer.

2. ?.text
Si une correspondance est trouvée, cela retourne le texte associé à cette option (option.text).

3. ?? props.answer 
Si aucune correspondance n'est trouvée on affiche la valeur de props.answer.

### Que se passe-t-il lorsqu'on ne met pas de valeur à answer-detail ? Est-ce satisfaisant ? Si ce n'est pas le cas, proposer une amélioration.
- Si on ne met pas de valeur à answer-detail (comme je l'ai fait), cela reprendra la valeur définie par défaut dans nos code parents. Si comme moi, dans ces code il est défini comme '' alors il afichera seulement un petit trait.
Ce n'est pas toujours satisfaisant car parfois nous n'avons aucune information compémentaire à ajouter et nous ne voulons pas afficher la valeur définie par défaut.

### Commentaire:

La mise en placedes réponses détaillées ne prened pas enormément de temps, ce qui prend le plus de temps c'est d'écrire les réponses détaillées pour chaque question.

J'ai choisi de laisser la valeur par défaut '' comme cela j'ai pu ajouter si je voulais des answer-detail dès que je voulais et ne pas en afficher si je n'en voulais pas. Cela m'a aussi permis par la suite de créer une nouvelle page "Lausanne" et d'afficher différemment les réponses données en laissant afficher le -.


## Semaine 6 projet- améliorations

### Expliquer votre démarche pour les améliorations que vous avez choisies :

1. QuestionSelect
2. Questioncheckbox
3. Ajout images
4. Nouvelle page Lausanne

#### Pourquoi avez-vous choisi ces améliorations ?

1. J'ai choisi d'ajouter des questions de différents types (QuestionSelect et QuestionCheckbox) afin d'avoir plus de proposition d'affichage différente. 

2. J'ai choisi d'ajouter des images lors que les solutions s'affichent sur ma page Lausanne car cela aide à comprendre de quoi on parle dans la question. J'ai décidé de ne pas les afficher tant que nous n'avons pas répondu car selon la question(dependant du quiz créer), cela peut nous donner les informations de réponse et ce n'est aps ce que je voulais.

3. J'ai choisi de créer une nouvelle page Lausanne afin d'y implémenter mes nouvelles améliorations et de garder la page Quiz de la manière basique vue en cours pour le projet.


#### Comment les avez-vous implémentées ?

1. 


#### Quels problèmes avez-vous rencontrés ?
#### Quelles améliorations pourriez-vous encore apporter ?
#### Vous devoir pouvoir expliquer votre code afin de valider une amélioration.