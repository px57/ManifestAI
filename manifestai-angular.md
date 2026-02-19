# Manifest AI

## Directives de codage pour Angular

**Prompt de démarrage :**

> Je veux que tu lises le document manifestai-angular.md et que tu
> suives les directives de codage qui y sont écrites pour générer du
> code Angular propre et conforme aux bonnes pratiques.

---

# Principes généraux

* Le code doit respecter **80 caractères maximum par ligne**.
* Ne pas ajouter de commentaires inutiles.
* ✅ Un code plat avec des **early returns** est préféré aux
  imbriquements profonds.
* Les fonctions doivent être **courtes et concises (25 lignes max)**.
* Utiliser des **noms explicites** pour variables, fonctions et classes.
* Utiliser des **JSDoc** pour documenter classes et méthodes.
* Factoriser la logique réutilisable dans :

  * `$app/shared/utils`
  * `$app/shared/helpers`
  * `$app/shared/services`
* ❌ Éviter la duplication de code.
* ❌ Ne pas utiliser try/catch pour le contrôle de flux.
* Utiliser les mécanismes Angular/RxJS pour la gestion des erreurs.
* Toutes les chaînes visibles doivent être **internationalisées**
  via i18n Angular (`$localize` ou ngx-translate selon projet).

---

# Composants (COMPONENT)

* Les composants doivent être placés dans :

  ```
  $app/features/$feature_name/components/
  ```
* Chaque composant doit :

  * utiliser `ChangeDetectionStrategy.OnPush`
  * avoir des **inputs/outputs typés**
  * être **présentational** si possible
* Séparer :

  * logique → service ou facade
  * template → HTML
  * styles → SCSS

✅ Structure recommandée :

```
task-create/
  task-create.component.ts
  task-create.component.html
  task-create.component.scss
  task-create.component.spec.ts
```

---

# Services (SERVICE)

* Les services doivent être placés dans :

  ```
  $app/features/$feature_name/services/
  ```
* Toujours utiliser `providedIn: 'root'` sauf cas particulier.
* Les appels HTTP doivent être centralisés dans des services API.
* Les services doivent retourner des **Observable typés**.
* ❌ Ne jamais s’abonner dans un service.
* Gérer les erreurs avec `catchError`.

---

# Formulaires (FORM)

* Utiliser **Reactive Forms** uniquement.
* Les formulaires doivent être dans :

  ```
  $app/features/$feature_name/forms/
  ```
* Créer une interface de type :

```ts
export interface TaskCreateFormValue { ... }
```

* Utiliser des **validators personnalisés réutilisables**.
* Les erreurs de formulaire doivent être gérées côté composant.

---

# State management (STATE)

Si utilisé :

* Placer dans :

  ```
  $app/features/$feature_name/store/
  ```
* Séparer clairement :

  * actions
  * reducers
  * effects
  * selectors
* Les composants ne doivent pas contenir de logique métier lourde.

---

# Tests unitaires (TEST)

⚠️ Règle stricte.

* Chaque composant/service créé doit avoir son test.
* Les tests sont placés dans le même dossier que le fichier testé.
* Utiliser **Jasmine + TestBed**.

---

## setUp des tests

Dans chaque `beforeEach` principal, ajouter dans le JSDoc :

```ts
/**
 * @usage: npm run test
 */
```

---

## Données de test réutilisables

Créer des factories dans :

```
$app/shared/testing/factories/
```

Exemple :

```ts
createTestUser()
createTestTask()
```

### ❗ Règles importantes

* ❌ Ne jamais créer de données mock directement dans les tests.
* ✅ Toujours passer par une factory.
* Si la factory n'existe pas → la créer avant usage.

---

# Imports (IMPORT)

Les imports doivent suivre cet ordre strict :

1. Angular imports
2. RxJS imports
3. Third-party imports
4. Application imports

---

## Exemple

```ts
// Angular Imports
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup } from '@angular/forms';

// RxJS Imports
import { Observable } from 'rxjs';
import { map } from 'rxjs/operators';

// Third-party Imports
import { TranslateService } from '@ngx-translate/core';

// App Imports
import { TaskService } from '@/app/features/tasks/services/task.service';
import { Task } from '@/app/features/tasks/models/task.model';
```

---

## Import multiple

Toujours entre parenthèses, un par ligne :

```ts
import {
  Task,
  TaskStatus,
} from '@/app/features/tasks/models/task.model';
```

---

# Tracking du projet (TRACKING)

Fichier concerné : **tree.md** à la racine.

---

## Règles

À chaque création de :

* composant
* service
* helper
* util
* store
* test

👉 Mettre à jour `tree.md` avec :

* nom de la classe/fonction
* commentaire court
* tag :

  * `TESTED`
  * `TODO`
  * `DEPRECATED`

---

## Objectif du tracking

* éviter la duplication de code
* aider l’IA à se repérer
* documenter l’architecture

---

# Objectif

Cette directive de codage est conçue pour être utilisée avec des
projets Angular et par une IA génératrice de code afin de produire un
code :

* lisible
* cohérent
* maintenable
* testable
* scalable

