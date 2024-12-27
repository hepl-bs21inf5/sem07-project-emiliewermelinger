Projet

[Emilie Wermelinger]

## Journal de bord

## Semaine 1 projet

### Tâche/ Temps estimé/ Temps réel

- installation de l'extension et création/modification des dossiers pour le projet
  - temps estimé: 25 min/temps réel : 45 min

- modification du quizz/ajout de questions et de réponses
  - temps estimé: 35 min/temps réel : 1h

- affichage du score/message et bouton réinitialiser à la fin du quizz
  - temps estimé: 45 min/temps réel : 1h15

- modification des boutons (css)
  - temps estimé: 30 min/temps réel : 40 min

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
  - temps estimé : 10 min/temps réel 10 min

- Créer une nouvelle question en faisant appel à QuestionRadio
  - temps estimé : 15 min/ temps réel 25 min

- Modifier les questions afin qu'elles fassent toutes appel au code de QuestionRadio
  - temps estimé : 35 min/ temps réel 20 min

- Créer le code pour les questions QuestionText
  - temps estimé : 45 min/ temps réel 1h30

- Ajouter une tab Trivia et créer de document QuizTrivia.vue
  - temps estimé : 20 min/ temps réel 20 min

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
  - temps estimé : 15 min/ temps réel 15 min

- Modifier le QuizzForm.vue afin que chaque solution soit dans la liste affichée de réponses juste ou fausse/ modifier le v-model
  - temps estimé : 15 min/ temps réel: 25min

- Modifier le composant QuestionText.vue afin qu'il fonctionne comme QuestionRadio.vue
  - temps estimé: 20 min/ temps réel: 20 min


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
  - temps estimé: 5 min/ temps réel: 5 min

- Ajouter un nouveau watch sur model pour corriger l'état de la question
  - temps estimé: 15 min/ temps réel: 20 min

- Adapter le watch sur value pour qu'il mette à jour le modèle
  - temps estimé: 15min/ temps réel: 20 min

- Adapter QuestionText.vue comme QuestionRadio.vue
 -  temps estimé: 20 min/ temps réel: 20 min

- Adapter la fonction submit et reset dans QuizForm.vue
  - temps estimé: 20 min/ temps réel: 45 min

- Rendre les réponses immuables
  - temps estimé: 20 min/ temps réel: 35 min

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
  - temps estimé: 15 min/ temps réel: 25 min

- Changer les couleurs dans un composant
  - temps estimé: 15 min/ temps réel: 10 min

### Questions:

#### Remplacer {{ props.answer }} par {{ answerText }} dans le template.Expliquer pourquoi on a fait ce changement ainsi que le code du computed.
- Ce changement permet permet de récupérer le texte associé à la valeur de la réponse (props.answer) parmi les options données dans props.options. Si aucune correspondance n'est trouvée, il retourne simplement la valeur de props.answer.
Cela permet de simplifier le code dans le template car au lieu d'aller chercher dans chaque utilisation de pops.answer, il va le faire une fois dans le computed.

1. props.options.find((option) => option.value === props.answer) :
Cette ligne cherche dans le tableau options l'option qui correspond à la valeur de props.answer.

2. ?.text :
Si une correspondance est trouvée, cela retourne le texte associé à cette option (option.text).

3. ?? props.answer :
Si aucune correspondance n'est trouvée on affiche la valeur de props.answer.

### Que se passe-t-il lorsqu'on ne met pas de valeur à answer-detail ? Est-ce satisfaisant ? Si ce n'est pas le cas, proposer une amélioration.
- Si on ne met pas de valeur à answer-detail (comme je l'ai fait), cela reprendra la valeur définie par défaut dans nos code parents. Si comme moi, dans ces code il est défini comme '' alors il afichera seulement un petit trait.
Ce n'est pas toujours satisfaisant car parfois nous n'avons aucune information compémentaire à ajouter et nous ne voulons pas afficher la valeur définie par défaut.
Nous pourrions supprimer tous les answerdetail et se besoin afficher seulement une solution via une autre fonction.

### Commentaire:

La mise en placedes réponses détaillées ne prened pas enormément de temps, ce qui prend le plus de temps c'est d'écrire les réponses détaillées pour chaque question.

J'ai choisi de laisser la valeur par défaut '' comme cela j'ai pu ajouter si je voulais des answer-detail dès que je voulais et ne pas en afficher si je n'en voulais pas. Cela m'a aussi permis par la suite de créer une nouvelle page "Lausanne" et d'afficher différemment les réponses données en laissant afficher le -.


## Semaine 6 projet - améliorations

### Expliquer votre démarche pour les améliorations que vous avez choisies :

1. QuestionSelect
2. Questioncheckbox
3. Ajout images
4. Nouvelle page Lausanne
5. Ordre aléatoire des questions
6. Ordre aléatoire des options de réponse pour les QuestionRadio
7. Plusieurs réponses possibles pour les QuestionText

#### Pourquoi avez-vous choisi ces améliorations ?

1. QuestionSelect et QuestionCheckbox:
 J'ai choisi d'ajouter des questions de différents types (QuestionSelect et QuestionCheckbox) afin d'avoir plus de proposition d'affichage différente. 

2.  Ajout images:
 J'ai choisi d'ajouter des images lors que les solutions s'affichent sur ma page Lausanne car cela aide à comprendre de quoi on parle dans la question. J'ai décidé de ne pas les afficher tant que nous n'avons pas répondu car selon la question(dependant du quiz créer), cela peut nous donner les informations de réponse et ce n'est aps ce que je voulais.

3.  Nouvelle page Lausanne:
 J'ai choisi de créer une nouvelle page Lausanne afin d'y implémenter mes nouvelles améliorations et de garder la page Quiz de la manière basique vue en cours pour le projet.

4.  Ordre aléatoire des questions et options:
 L'ordre aléatoire des questions et des options de réponses est très utile pour l'apprentissage car cela évite que les personnes apprennent par coeur les réponses et leur emplacement. 

5.  Plusieurs réponses possibles pour les QuestionText:
 Avoir la possiblité de répondre de plusieurs manière aux QuestionText est très important. L'orthographe n'a pas besoin d'être parfaite et les personnes peuvent répondre de plusieurs manières possibles sans que cela les pénalises dans leur score.

#### Comment les avez-vous implémentées ?

1. QuestionSelect et QuestionCheckbox:
    
    J'ai repris le code de QuestionRadio que j'ai modifié afin qu'il fonctionne de différentes manières.

    - QuestionSelect: J'ai dû modifier la class ainsi que les balises des questions.
                  J'ai ajouté le fait que la première ligne dans la liste déroulante soit une option par défault qui affiche le text "Choisissez une réponse".
                  Je l'ai mise comme cela :value=disabled ce qui signifie qu'elle n'est pas sélectionnable.

    - QuestionCheckbox: J'ai dû modifier la class ainsi que les balises des questions.
                    J'ai du faire en sorte que values soit un tableau qui stocke plusieurs réponses sélectionnées.
                    :value="option.value permet d'ajouter au tableau la valeur associée à la case sélectionée

    J'ai ensuite importé mes deux nouveaux documents dans QuizForm et j'ai ajouter les questions.


2. Ajout images (seuelement dans QuizLausanne):
    
    J'ai défini les images souhaitées dans questionDetail pour chaque question.
  
    J'ai utilisé la fonction getQuestionDetails pour récupérer les détails de chaque questions y compris les images.

3. Nouvelle page Lausanne:

    J'ai copier-coller la page QuizForm que j'ai par la suite modifiée en y ajoutant les photos.

    J'ai aussi ajouter " v-for="(id, idx) in questionIndices" :key="id"> "afin de créer un tableau contenant les identifiants des différentes questions afin de pouvoir ensuite le réutiliser dans le titre.

4. Ordre aléatoire des questions:

    J'ai implémenté l'ordre aléatoire des questions grâce à la méthode shuffleQuestions.

    J'ai ajouteé les indices des questions dans une variable questionIndices qui sera par la suite réutilisée dans ma fonction onMounted qui permet de mélanger les questions à chaque fois que le code est relancé.

    J'ai ajouté cette ligne de code "questionIndices.value = shuffleQuestions([...questionIndices.value])" dans ma fonction reset afin que les questions soient remélangées à chaque fois que l'on réinitialise le quiz.

5. Ordre aléatoire des options:

    Comme l'odre aléatoire des options de réponse ne concernent que les QuestionRadio, je l'ai directement implémenté dans QuestionRadio.vue.

    J'ai utilisé la fonction shuffleoptions afin de mélnager les options en reprenant les value et les text. Cette fonction retourne ensuite un tableau mélangé.

    Je réutilise un onMounted en faisant appel à shuffleoptions pour que les options de réponses soient mélangées à chawue lancement du quiz.

6. Plusieurs réponses possibles pour les QuestionText:

    J'ai modifié le script dans QuestionText afin que answer deviennent un tableau et plus une chaîne de caractère. Pour se faire je lui ai modifié le style de answer et dans QuizForm et QuizLausanne, j'ai ajouté : avant chaque answer pour que cela soit un tableau de réponses. 


#### Quels problèmes avez-vous rencontrés ?

1. QuestionSelect: 

  - J'ai du faire attention de bien utiliser les balises select pour chaque option afin que cela  s'affiche comme liste déroulante.

2. QuestionCheckbox:

  - J'ai eu du mal à trouvr la fonction qui permettait de sélectionner plusieurs réponses et que  les réponses soient prises en compte correctement.

3. Ajout d'images:

 - J'ai eu du mal à ajouter des images car je ne prenais pas le lien direct de l'image, j'ai      d'abord essayé avec le lien de la page web, puis en ajoutant l'image dans un dossier du projet  mais cela ne fonctionnait pas. J'ai finalement réussi à trouver les bon liens.

4. Nouvelle page Lausanne:

 - Je n'ai pas eu trop de soucis à créer cette nouvelle page. Le seul inconvénients était de modifier les questions comme souhaitées, puis de coder le résultat voulu après avoir appuyer sur le bouton terminer.

5. Ordre aléatoire des questions:

 - J'ai du créer une nouvelle fonction qui permet de prendre chaque sorte de questions et de les mélanger. 

6. Ordre aléatoire des options : 

 - J'ai du ajouter une nouvelle fonction qui s'applique uniquement à questionRadio dans QuestionRadio et pas dans QuizForm.
 J'ai donc du modifier les "id" afin que cela ne soit plus des nombres mais des identifiants en mots et rajouter les index en chiffres pour les questionRadio afin que seule celles-ci soient prises pour le mélange.

7. Plusieurs réponses possibles pour les QuestionText: 

  - J'ai du modifier answer afin qu'il puisse recevoir un tableau pour les réponses et non plus une chaîne de caractère. Il a fallu aussi que je le modifie dans QuizForm et dans QuizLausanne.

#### Quelles améliorations pourriez-vous encore apporter ?

1. Je pourrai ajouter des images pour chaque questions

2. Je pourrai adapter encore plus mon code en bootstrap afin de lui dire exactement comment s'afficher (je ne l'ai asp fait car mon site me convient comme il est et il s'adapte déjà aux smartphones)