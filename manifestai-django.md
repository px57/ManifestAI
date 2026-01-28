# Manifest AI

## Directives de codage pour Django

Prompt de demarage: 
Je veut que tu lise le document manifestai-django.md et que tu suive les directives de codage qui y sont ecrite pour generer du code django propre et conforme aux bonnes pratiques.

---

## Principes généraux

1. Le code doit être écrit en respectant **80 caractères maximum par ligne**.
2. Ne pas ajouter de commentaires inutiles.
3. ✅ **Un code plat avec des early returns est préféré** aux imbriquements profonds.
4. Les fonctions doivent être **courtes et concises** (25 lignes maximum).
5. Utiliser des **noms de variables et de fonctions explicites**.
6. Utiliser des **docstrings** pour documenter les classes et les méthodes.
7. Analyser le code afin de créer des **librairies réutilisables**
   (`$app.utils` ou `$app.helpers`).
8. Éviter toute **duplication de code** en utilisant des fonctions ou des classes
   réutilisables.
9. Ne pas utiliser `try / except` pour le **contrôle de flux**.
10. Utiliser les **fonctionnalités natives de Django** pour la gestion des erreurs
    et des validations.
11. Chaque chaîne de caractères doit être **internationalisée** en utilisant
    `gettext_lazy`.

---

## Formulaires (`FORM`)

1. Les formulaires doivent être placés dans
   `$app/forms/$views_name.py`.
2. Utiliser `ModelForm` lorsque le formulaire est basé sur un modèle.
3. Utiliser des **widgets personnalisés** pour les champs de formulaire complexes.
4. Les erreurs de formulaire sont traitées via :
   `return res.form_error(form)`.

---

## Views (`VIEW`)

1. Les vues doivent être placées dans `$app/views/$views_name.py`.
2. Chaque fois que je demande de creer un vu il faut creer dans le dossier $app/tests/$views_name.py un fichier de test unitaire pour cette vue.

## Unitest (`TEST`)

1. rajouter la ligne `@usage: python3 manage.py test projecthub.tests.tasks.TaskCreateViewTestCase` dans la docstring de la methode setUp de chaque classe de test unitaire.
2. Pour creer des donnees de test reutilisable il faut creer des fonctions dans un fichier $app_name/utils/test.py exemple `createTestUserProfile()` qui creer un user profile de test.
3. Si la fonction de creation de donne de test n'existe pas il faut la creer dans $app_name/utils/test.py avant de l'utiliser dans les tests unitaires.
4. Ne jamais creer de donne de test directement avec le modele dans les tests unitaires, il faut toujours passer par une fonction de creation de donne de test dans $app_name/utils/test.py

## Import (`IMPORT`)

1. Les imports doivent être organisés dans l'ordre suivant :
   - Imports spécifiques à Django
   - Imports standard de Python
   - Imports de bibliothèques tierces
   - Imports d'applications internes
2. Il faut des commentaire pour separer chaque type d'import exemple
`
# Django Imports
from django.test import TestCase
from django.urls import reverse
from django.contrib.auth.models import User
from django.utils.translation import gettext_lazy as _

# Datetime Imports
from datetime import date, timedelta

# Projecthub Imports
from projecthub.models import (
   Tasks, 
   Sprint
)
from projecthub.forms.task import TaskCreateForm

# Api Imports
from api.models import Matrix
`
3. Quand l'ont importe plusieurs elements d'un meme module il faut les importer entre parenthese et un par ligne exemple
`
from projecthub.models import (
      Tasks,
      Sprint
)
` 

## Tracking du project. (`TRACKING`) 

1. Il s'agit du fichier tree.md a la racine du projet.
2. A chaque fois qu'une nouvelle classe ou fonction est cree il faut mettre a jour le fichier tree.md pour ajouter la nouvelle classe ou fonction avec un commentaire. 
3. Mais aussi des tags comme par exemple TESTED ou TODO si la fonction n'est pas encore testee.

## Objectif

Cette directive de codage est conçue pour être utilisée avec des projets **Django**
et par une **IA génératrice de code**, afin de produire un code **lisible, cohérent,

