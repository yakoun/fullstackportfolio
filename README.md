# Full Stack Portfolio - Yakoun

Portfolio complet avec panel d'administration et site web public, construit avec Next.js et Firebase.

## 🎯 Vue d'ensemble

Ce projet comprend deux applications interconnectées:

1. **[Admin Panel](./admin-panel)** - Panel d'administration pour gérer tout le contenu
2. **[Website](./website)** - Site web public portfolio avec blog

Les deux applications partagent la même base de données Firebase pour une synchronisation en temps réel.

## 🚀 Quick Start

### Prérequis
- Node.js 18+ and npm
- Compte Firebase
- (Optionnel) Compte EmailJS pour le formulaire de contact

### Installation Complète

```bash
# Cloner le repository
git clone https://github.com/yakoun/fullstackportfolio.git
cd fullstackportfolio

# Installer les dépendances de l'Admin Panel
cd admin-panel
npm install
cp .env.local.example .env.local
# Éditer .env.local avec vos credentials Firebase

# Installer les dépendances du Website
cd ../website
npm install
cp .env.local.example .env.local
# Éditer .env.local avec vos credentials Firebase + EmailJS
```

### Démarrage

```bash
# Terminal 1 - Admin Panel
cd admin-panel
npm run dev
# → http://localhost:3000

# Terminal 2 - Website
cd website
npm run dev
# → http://localhost:3000 (ou 3001 si 3000 occupé)
```

## 📦 Structure du Projet

```
fullstackportfolio/
├── admin-panel/          # Panel d'administration Next.js
│   ├── src/
│   │   ├── app/         # Pages (Dashboard, Posts, Projects, etc.)
│   │   ├── components/  # Composants réutilisables
│   │   └── lib/         # Configuration Firebase
│   └── README.md        # Documentation Admin Panel
│
├── website/             # Site web public Next.js
│   ├── src/
│   │   ├── app/        # Pages (Home, About, Blog, Contact)
│   │   ├── components/ # Composants UI et sections
│   │   ├── hooks/      # Custom hooks Firebase
│   │   └── lib/        # Configuration Firebase
│   └── README.md       # Documentation Website
│
└── README.md           # Ce fichier
```

## 🛠️ Technologies

### Frontend & Backend
- **Framework**: Next.js 15 (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS v4
- **Animations**: Framer Motion
- **Icons**: Lucide React

### Services
- **Database**: Firebase Firestore
- **Storage**: Firebase Storage
- **Auth**: Firebase Authentication
- **Email**: EmailJS
- **Hosting**: Vercel (recommandé)

## 📚 Documentation Détaillée

- **[Admin Panel Documentation](./admin-panel/README.md)** - Guide complet pour l'administration
- **[Website Documentation](./website/README.md)** - Guide complet pour le site public

## 🔐 Configuration Firebase

### 1. Créer un Projet Firebase
1. Aller sur [Firebase Console](https://console.firebase.google.com/)
2. Créer un nouveau projet
3. Activer Firestore Database
4. Activer Firebase Storage
5. Activer Authentication (Email/Password)

### 2. Obtenir les Credentials
Dans Firebase Console → Project Settings → General:
- Copier la configuration web
- Ajouter dans les fichiers `.env.local` des deux projets

### 3. Configurer les Règles de Sécurité

**Firestore Rules** (exemple pour production):
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Public read, admin write
    match /{document=**} {
      allow read: if true;
      allow write: if request.auth != null;
    }
    
    // Comments - public write
    match /comments/{comment} {
      allow read: if true;
      allow create: if true;
      allow update, delete: if request.auth != null;
    }
  }
}
```

**Storage Rules**:
```javascript
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

### 4. Créer les Index Composites
Pour les commentaires, créer un index sur:
- Collection: `comments`
- Champs: `approved` (ASC), `postId` (ASC), `createdAt` (DESC)

## 🎨 Features Principales

### Admin Panel
- ✅ Gestion complète du contenu (CRUD)
- ✅ Éditeur WYSIWYG pour les articles
- ✅ Upload d'images avec compression
- ✅ Gestion des commentaires
- ✅ Statistiques (likes, commentaires)
- ✅ Publication programmée
- ✅ Drag & Drop pour réorganiser

### Website
- ✅ Design "Quantum Light" moderne
- ✅ Blog avec likes et commentaires
- ✅ Galeries d'images
- ✅ Formulaire de contact
- ✅ Pages dynamiques (About, Projects, Services)
- ✅ SEO optimisé
- ✅ 100% Responsive

## 🚀 Déploiement

### Option 1: Vercel (Recommandé)

```bash
# Admin Panel
cd admin-panel
vercel --prod

# Website
cd website
vercel --prod
```

### Option 2: Firebase Hosting

```bash
# Build
npm run build

# Deploy
firebase deploy
```

### Variables d'Environnement
N'oubliez pas d'ajouter toutes les variables d'environnement dans votre plateforme de déploiement!

## 📊 Workflow de Développement

1. **Gérer le contenu** dans Admin Panel
2. **Le contenu apparaît automatiquement** sur le Website (sync Firebase)
3. **Pas de rebuild nécessaire** grâce à Firestore

## 🐛 Problèmes Courants

**Port déjà utilisé?**
```bash
# Changer le port
npm run dev -- -p 3001
```

**Firebase init échoue?**
- Vérifiez vos credentials dans `.env.local`
- Vérifiez que les services sont activés dans Firebase Console

**Images ne chargent pas?**
- Vérifiez `next.config.ts` → `images.remotePatterns`
- Ajoutez `firebasestorage.googleapis.com`

## 📝 TODO / Améliorations Futures

- [ ] Mode sombre
- [ ] Système de tags pour le blog
- [ ] Recherche globale
- [ ] Analytics dashboard dans Admin Panel
- [ ] Export de données
- [ ] Multi-langue i18n
- [ ] PWA support

## 📄 Licence

MIT License - Vous êtes libre d'utiliser ce projet pour vos propres portfolios!

## 👤 Auteur

**Yakoun**
- GitHub: [@yakoun](https://github.com/yakoun)
- Portfolio: [Votre URL]

## 🙏 Contribution

Les contributions sont les bienvenues! N'hésitez pas à:
1. Fork le projet
2. Créer une branche (`git checkout -b feature/AmazingFeature`)
3. Commit vos changements (`git commit -m 'Add some AmazingFeature'`)
4. Push (`git push origin feature/AmazingFeature`)
5. Ouvrir une Pull Request

## ⭐ Support

Si ce projet vous aide, donnez-lui une ⭐ sur GitHub!

---

Made with ❤️ using Next.js and Firebase
