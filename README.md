# Harmonies en ligne

Le jeu Harmonies jouable à plusieurs dans le navigateur, chacun sur son appareil.
La page est hébergée gratuitement par **GitHub Pages**, et les parties sont synchronisées par **Firebase** (formule gratuite Spark, sans carte bancaire).

Contenu du dossier :

| Fichier | Rôle |
|---|---|
| `index.html` | Le jeu complet |
| `firebase-config.js` | La configuration de ton projet Firebase, à remplir à l'étape 4 |
| `database.rules.json` | Les règles de sécurité de la base, à coller à l'étape 3 |

Compte environ 20 minutes.

---

## 1. Créer le projet Firebase

1. Va sur <https://console.firebase.google.com> et connecte-toi avec ton compte Google.
2. Clique sur **Créer un projet**, nomme-le par exemple `harmonies`.
3. Google Analytics n'est pas utile : tu peux le désactiver. Clique sur **Créer le projet**.

## 2. Activer la connexion anonyme

Les joueurs n'ont pas besoin de compte : le jeu leur donne un identifiant anonyme.

1. Dans le menu de gauche : **Créer** → **Authentication** → **Commencer**.
2. Onglet **Mode de connexion** (Sign-in method) → choisis **Anonyme** → active-le → **Enregistrer**.

## 3. Créer la base de données

1. Menu de gauche : **Créer** → **Realtime Database** → **Créer une base de données**.
2. Emplacement : **Belgique (europe-west1)**.
3. Mode : choisis **Démarrer en mode verrouillé**, puis **Activer**.
4. Ouvre l'onglet **Règles**, efface tout, colle le contenu du fichier `database.rules.json`, puis clique sur **Publier**.

Attention : ne choisis pas Firestore, le jeu utilise Realtime Database.

## 4. Récupérer la configuration du jeu

1. Clique sur la roue dentée en haut à gauche → **Paramètres du projet**.
2. En bas de la page, section **Vos applications**, clique sur l'icône **`</>`** (Web).
3. Nomme l'application `harmonies`. Ne coche pas Firebase Hosting. Clique sur **Enregistrer l'application**.
4. Firebase affiche un bloc `const firebaseConfig = { ... }`. Copie les valeurs dans `firebase-config.js`, à la place des valeurs d'exemple. Le résultat ressemble à ceci :

```js
window.FIREBASE_CONFIG = {
  apiKey: "AIzaSy...",
  authDomain: "harmonies-xxxx.firebaseapp.com",
  databaseURL: "https://harmonies-xxxx-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "harmonies-xxxx",
  storageBucket: "harmonies-xxxx.appspot.com",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abcdef"
};
```

Vérifie que la ligne **`databaseURL`** est bien présente. Si elle manque, recopie l'adresse affichée en haut de la page Realtime Database (elle commence par `https://` et finit par `firebasedatabase.app`).

Ces valeurs ne sont pas des mots de passe : elles peuvent être publiées sur GitHub sans risque. La sécurité vient des règles de l'étape 3.

## 5. Mettre le jeu sur GitHub Pages

1. Sur <https://github.com/new>, crée un dépôt **public** nommé `harmonies`.
2. Sur la page du dépôt, clique sur **uploading an existing file** (ou **Add file** → **Upload files**).
3. Glisse les fichiers `index.html`, `firebase-config.js`, `database.rules.json` et `README.md`, puis clique sur **Commit changes**.
4. Va dans **Settings** → **Pages**. Sous **Branch**, choisis `main` et `/ (root)`, puis **Save**.
5. Après une à deux minutes, le jeu est en ligne à l'adresse `https://TON-PSEUDO.github.io/harmonies/`.

## 6. Autoriser ton site dans Firebase

Cette étape est une précaution : elle déclare ton site auprès de Firebase et évite des refus de connexion sur certains réglages.

1. Firebase → **Authentication** → onglet **Paramètres** → **Domaines autorisés**.
2. **Ajouter un domaine** : `TON-PSEUDO.github.io` (sans `https://` ni `/harmonies`).

---

## Jouer

1. Ouvre ton adresse GitHub Pages → **Nouvelle partie** → **En ligne** → **Créer une partie**.
2. Choisis le nombre de joueurs, et pour chaque place si c'est un ami ou un bot.
3. Envoie le lien (ou le code à 5 lettres) à tes copains. Ils indiquent leur nom et rejoignent.
4. Quand toutes les places sont prises, clique sur **Lancer la partie**.

Bon à savoir :

- Un joueur qui ferme sa page retrouve sa place en rouvrant le lien, à condition d'utiliser le même navigateur.
- Si un joueur est parti, l'hôte peut le remplacer par un bot à son tour, avec le bouton **Faire jouer un bot à sa place**.
- Les bots tournent sur l'appareil de l'hôte : il doit garder la page ouverte pendant la partie.
- Le mode **Sur cet appareil** fonctionne toujours, même sans Firebase.

## En cas de problème

| Message ou symptôme | Cause probable |
|---|---|
| « Le jeu en ligne n'est pas encore configuré » | `firebase-config.js` contient encore les valeurs d'exemple |
| « Connexion à Firebase impossible » | Connexion anonyme non activée (étape 2) ou domaine non autorisé (étape 6) |
| « La base de données a refusé l'écriture » | Règles non publiées (étape 3) |
| Rien ne se passe après « Créer la partie » | `databaseURL` absent de `firebase-config.js` |
| L'ancienne version s'affiche après une mise à jour | Recharge la page en vidant le cache (Ctrl+Maj+R) |

Pour voir les parties en cours, ouvre Firebase → Realtime Database → onglet **Données**. Tu peux supprimer le nœud `games` de temps en temps pour faire le ménage.
