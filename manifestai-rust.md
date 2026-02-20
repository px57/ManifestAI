# Manifest AI - Rust

## Directives de codage pour Rust

Prompt de démarrage:
Je veux que tu lises le document manifestai-rust.md et que tu suives les
directives de codage qui y sont écrites pour générer du code Rust propre
et conforme aux bonnes pratiques.

---

## Principes généraux

1. Le code doit être écrit en respectant **80 caractères maximum par ligne**.
2. Ne pas ajouter de commentaires inutiles.
3. ✅ **Un code plat avec des early returns est préféré** aux imbriquements
   profonds.
4. Les fonctions doivent être **courtes et concises** (25 lignes maximum).
5. Utiliser des **noms de variables et de fonctions explicites** en snake_case.
6. Utiliser des **docstrings** (`///`) pour documenter les fonctions publiques.
7. Analyser le code afin de créer des **modules réutilisables** dans `src/`.
8. Éviter toute **duplication de code** en utilisant des fonctions ou des traits.
9. Utiliser `Result<T, E>` pour la gestion des erreurs, pas de `unwrap()` en
   production.
10. Préférer les **early returns** avec `?` pour la propagation des erreurs.

---

## Structure du projet (`STRUCTURE`)

```
src/
├── main.rs              # Point d'entrée
├── config.rs            # Configuration (constantes, env vars)
├── centrifugo/          # Module Centrifugo
│   ├── mod.rs
│   ├── client.rs        # Client WebSocket
│   ├── messages.rs      # Structs de messages
│   └── handlers.rs      # Handlers de messages
├── utils/               # Utilitaires réutilisables
│   └── mod.rs
└── error.rs             # Types d'erreurs custom
```

---

## Modules (`MODULE`)

1. Chaque module doit avoir un fichier `mod.rs` qui exporte les éléments
   publics.
2. Les structs de données doivent être dans des fichiers séparés.
3. Utiliser `pub(crate)` pour limiter la visibilité interne.

---

## Gestion des erreurs (`ERROR`)

1. Créer un type d'erreur custom avec `thiserror` ou manuel.
2. Ne jamais utiliser `unwrap()` ou `expect()` en production.
3. Utiliser `?` pour propager les erreurs.
4. Logger les erreurs avec `eprintln!` ou une lib de logging.

```rust
// ✅ Bon
let data = fetch_data().await?;

// ❌ Mauvais
let data = fetch_data().await.unwrap();
```

---

## Async (`ASYNC`)

1. Utiliser `tokio` comme runtime async.
2. Les fonctions async doivent retourner `Result<T, E>`.
3. Utiliser `tokio::spawn` pour les tâches concurrentes.

---

## Imports (`IMPORT`)

1. Les imports doivent être organisés dans l'ordre suivant :
   - Imports de la bibliothèque standard (`std::`)
   - Imports de crates externes
   - Imports du crate courant (`crate::`)

```rust
// Std Imports
use std::collections::HashMap;

// External Crate Imports
use serde::{Deserialize, Serialize};
use tokio_tungstenite::tungstenite::Message;

// Crate Imports
use crate::config::WS_URL;
use crate::centrifugo::client::CentrifugoClient;
```

---

## Configuration (`CONFIG`)

1. Les constantes de configuration doivent être dans `src/config.rs`.
2. Utiliser des variables d'environnement pour les valeurs sensibles.
3. Préfixer les constantes avec le module concerné si nécessaire.

```rust
// src/config.rs
pub const API_BASE_URL: &str = "http://localhost:5757";
pub const WS_URL: &str = "ws://localhost:5754/connection/websocket";
pub const CHANNEL: &str = "playroom:stream";
```

---

## Tests (`TEST`)

1. Les tests unitaires doivent être dans le même fichier avec `#[cfg(test)]`.
2. Les tests d'intégration dans `tests/`.
3. Utiliser `#[tokio::test]` pour les tests async.

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[tokio::test]
    async fn test_get_token() {
        // ...
    }
}
```

---

## Objectif

Cette directive de codage est conçue pour être utilisée avec des projets
**Rust** et par une **IA génératrice de code**, afin de produire un code
**lisible, cohérent et maintenable**.


