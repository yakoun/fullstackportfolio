# 🚀 GUIDE DE DÉPLOIEMENT SUR VERCEL

Ce guide vous accompagne pour mettre en ligne votre **Portfolio** (Site Public) et votre **Panneau d'Administration**.

---

## 📋 PRÉREQUIS

1.  Avoir un compte sur [Vercel.com](https://vercel.com) (connexion via GitHub recommandée).
2.  Avoir le projet poussé sur votre GitHub.

---

## 1️⃣ DÉPLOYER LE SITE PUBLIC (`website`)

### Étape 1 : Créer le projet sur Vercel
1.  Allez sur le Dashboard Vercel.
2.  Cliquez sur **"Add New..."** > **"Project"**.
3.  Importez votre dépôt GitHub `portfolio`.
4.  **IMPORTANT** : Dans "Root Directory", cliquez sur "Edit" et sélectionnez le dossier `website`.

### Étape 2 : Configurer les Variables d'Environnement
Dans la section **"Environment Variables"**, ajoutez les clés suivantes (copiez-les depuis votre fichier `.env.local` du dossier `website`) :

| Nom de la variable | Valeur (Exemple) |
|-------------------|------------------|
| `NEXT_PUBLIC_FIREBASE_API_KEY` | `AIzaSy...` |
| `NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN` | `votre-projet.firebaseapp.com` |
| `NEXT_PUBLIC_FIREBASE_PROJECT_ID` | `votre-projet` |
| `NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET` | `votre-projet.firebasestorage.app` |
| `NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID` | `123456...` |
| `NEXT_PUBLIC_FIREBASE_APP_ID` | `1:123456...` |
| `NEXT_PUBLIC_FIREBASE_MEASUREMENT_ID` | `G-XXXXXX` |

### Étape 3 : Lancer le déploiement
1.  Cliquez sur **"Deploy"**.
2.  Attendez que la construction se termine (environ 1-2 minutes).
3.  🎉 Votre site est en ligne ! Notez l'URL (ex: `portfolio-website.vercel.app`).

---

## 2️⃣ DÉPLOYER LE PANNEAU D'ADMIN (`admin-panel`)

### Étape 1 : Créer le projet sur Vercel
1.  Retournez sur le Dashboard Vercel.
2.  Cliquez sur **"Add New..."** > **"Project"**.
3.  Importez le **MÊME** dépôt GitHub `portfolio`.
4.  **IMPORTANT** : Dans "Root Directory", cliquez sur "Edit" et sélectionnez le dossier `admin-panel`.

### Étape 2 : Configurer les Variables d'Environnement
Ajoutez les mêmes variables que pour le site web (copiez-les depuis `.env.local` du dossier `admin-panel`).

### Étape 3 : Lancer le déploiement
1.  Cliquez sur **"Deploy"**.
2.  Une fois terminé, votre admin panel est accessible (ex: `portfolio-admin.vercel.app`).

---

## 3️⃣ CONFIGURATION FINALE (Domaines)

Si vous avez un nom de domaine (ex: `mon-nom.com`) :

1.  Allez dans les **Settings** du projet `website` sur Vercel.
2.  Section **Domains**.
3.  Ajoutez `mon-nom.com`.
4.  Suivez les instructions DNS (ajouter un enregistrement A ou CNAME chez votre registrar).

Pour l'admin, vous pouvez utiliser un sous-domaine :
1.  Allez dans les **Settings** du projet `admin-panel`.
2.  Ajoutez `admin.mon-nom.com`.

---

## 🚨 DÉPANNAGE COURANT

- **Erreur de Build** : Vérifiez que vous avez bien sélectionné le bon "Root Directory" (`website` ou `admin-panel`).
- **Écran blanc / Erreur Firebase** : Vérifiez que vous avez bien copié TOUTES les variables d'environnement sans espaces en trop.
- **Images ne chargent pas** : Vérifiez que le domaine de vos images (ex: `firebasestorage.googleapis.com`) est autorisé dans `next.config.ts` (déjà configuré normalement).

---

**Besoin d'aide ?** Demandez à votre assistant IA ! 🤖
