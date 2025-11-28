# 📧 Configuration EmailJS - Guide Complet

## 🎯 Objectif
Permettre aux visiteurs de votre site de vous envoyer des messages via un formulaire de contact fonctionnel.

---

## 📝 Étape 1 : Créer un Compte EmailJS

1. Allez sur [https://www.emailjs.com/](https://www.emailjs.com/)
2. Cliquez sur **"Sign Up"** (Inscription gratuite)
3. Créez votre compte avec votre email

**Plan Gratuit:**
- ✅ 200 emails/mois
- ✅ Parfait pour un portfolio
- ✅ Pas de carte bancaire requise

---

## ⚙️ Étape 2 : Configurer le Service Email

### 2.1 Ajouter un Service Email

1. Connectez-vous à [EmailJS Dashboard](https://dashboard.emailjs.com/)
2. Cliquez sur **"Add New Service"**
3. Choisissez votre fournisseur d'email :
   - **Gmail** (recommandé pour débuter)
   - Outlook
   - Yahoo
   - Ou autre

### 2.2 Configurer Gmail (Exemple)

1. Sélectionnez **Gmail**
2. Cliquez sur **"Connect Account"**
3. Autorisez EmailJS à accéder à votre Gmail
4. Donnez un nom au service (ex: "Portfolio Contact")
5. Copiez le **Service ID** (ex: `service_abc123`)

📝 **Note:** Gardez ce Service ID, vous en aurez besoin !

---

## 📬 Étape 3 : Créer un Template d'Email

### 3.1 Créer le Template

1. Allez dans **"Email Templates"**
2. Cliquez sur **"Create New Template"**
3. Donnez un nom : "Contact Form"

### 3.2 Configurer le Template

Utilisez ce template HTML :

```html
Nouveau message depuis votre portfolio!

De: {{from_name}}
Email: {{from_email}}
Téléphone: {{phone}}

Message:
{{message}}

---
Envoyé depuis votre site portfolio
```

**Variables disponibles:**
- `{{from_name}}` - Nom du visiteur
- `{{from_email}}` - Email du visiteur
- `{{phone}}` - Téléphone (optionnel)
- `{{message}}` - Message du visiteur
- `{{to_name}}` - Votre nom (configurable)

### 3.3 Paramètres du Template

**Email de destination:** Votre email où vous recevrez les messages

**Sujet:** `Nouveau message de {{from_name}} - Portfolio`

**From Name:** `{{from_name}}`

**From Email:** Utilisez l'email configuré dans le service

**Reply To:** `{{from_email}}` (pour répondre directement au visiteur)

### 3.4 Sauvegarder

1. Cliquez sur **"Save"**
2. Copiez le **Template ID** (ex: `template_xyz789`)

📝 **Note:** Gardez ce Template ID !

---

## 🔑 Étape 4 : Obtenir votre Public Key

1. Allez dans **"Account"** → **"General"**
2. Trouvez **"Public Key"** (ex: `aBcDeFgHiJkLmNoPqRs`)
3. Copiez cette clé

---

## 🚀 Étape 5 : Configurer dans votre Site

### 5.1 Créer le fichier .env.local

Dans votre projet `website`, créez un fichier `.env.local` :

```bash
# EmailJS Configuration
NEXT_PUBLIC_EMAILJS_SERVICE_ID=service_abc123
NEXT_PUBLIC_EMAILJS_TEMPLATE_ID=template_xyz789
NEXT_PUBLIC_EMAILJS_PUBLIC_KEY=aBcDeFgHiJkLmNoPqRs
```

⚠️ **Remplacez** les valeurs par vos vraies clés obtenues aux étapes précédentes !

### 5.2 Redémarrer le serveur

```bash
# Arrêtez le serveur (Ctrl+C) puis relancez
npm run dev
```

---

## ✅ Étape 6 : Tester le Formulaire

1. Allez sur votre site
2. Trouvez la section "Contact"
3. Remplissez le formulaire :
   - Nom
   - Email
   - Téléphone (optionnel)
   - Message
4. Cliquez sur "Envoyer"
5. Vérifiez votre boîte email !

---

## 📊 Étape 7 : Ajouter un Auto-Répondeur (Optionnel)

### 7.1 Créer un 2ème Template

1. Créez un nouveau template : "Auto Response"
2. Template pour le visiteur :

```html
Bonjour {{from_name}},

Merci pour votre message ! J'ai bien reçu votre demande et je vous répondrai dans les plus brefs délais.

Votre message:
{{message}}

Cordialement,
Votre Nom
Électrotechnicien & Expert IT

---
Ceci est un message automatique, merci de ne pas y répondre.
```

3. Configurez :
   - **To Email:** `{{from_email}}` (l'email du visiteur)
   - **Subject:** "Merci pour votre message !"

4. Copiez le Template ID

### 7.2 Ajouter dans .env.local

```bash
NEXT_PUBLIC_EMAILJS_AUTO_REPLY_TEMPLATE_ID=template_autoresponse123
```

---

## 🔧 Dépannage

### Problème : Les emails n'arrivent pas

**Solutions:**
1. **Vérifiez les spam/courrier indésirable**
2. **Vérifiez les clés** dans `.env.local`
3. **Quota dépassé ?** Gratuit = 200 emails/mois
4. **Service non actif** dans le dashboard EmailJS
5. **Mauvais email de destination** dans le template

### Problème : Erreur CORS

**Solution:** EmailJS gère automatiquement CORS. Si erreur :
1. Vérifiez que vous utilisez la bonne Public Key
2. Assurez-vous que le service est actif

### Problème : Variables non remplacées

**Solution:**
1. Les noms doivent correspondre exactement : `{{from_name}}` dans template = `from_name` dans le code
2. Utilisez des doubles accolades : `{{variable}}`

---

## 📈 Monitoring & Analytics

Dans le dashboard EmailJS, vous pouvez voir :
- ✅ Nombre d'emails envoyés
- ✅ Taux de succès/échec
- ✅ Quota restant
- ✅ Historique des 30 derniers jours

---

## 🎨 Personnalisation Avancée

### Template HTML Riche

Vous pouvez utiliser du HTML complet dans vos templates :

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body { font-family: Arial, sans-serif; }
    .header { background: #00d4ff; color: white; padding: 20px; }
    .content { padding: 20px; }
    .footer { background: #f5f5f5; padding: 10px; text-align: center; }
  </style>
</head>
<body>
  <div class="header">
    <h1>Nouveau Message Portfolio</h1>
  </div>
  <div class="content">
    <p><strong>De:</strong> {{from_name}}</p>
    <p><strong>Email:</strong> {{from_email}}</p>
    <p><strong>Message:</strong></p>
    <p>{{message}}</p>
  </div>
  <div class="footer">
    <p>Envoyé depuis votre portfolio</p>
  </div>
</body>
</html>
```

---

## 🔐 Sécurité & Bonnes Pratiques

### ✅ À FAIRE
- Utiliser reCAPTCHA (voir guide séparé)
- Valider les champs côté client ET serveur
- Limiter la longueur des messages
- Ne jamais exposer vos clés privées

### ❌ À ÉVITER
- Mettre les clés EmailJS dans le code source
- Accepter des pièces jointes sans validation
- Permettre des messages trop longs
- Ne pas valider les emails

---

## 💡 Améliorations Futures

1. **reCAPTCHA v3** - Protection contre spam
2. **Webhook Slack/Discord** - Notifications instantanées
3. **Base de données** - Sauvegarder les messages
4. **Dashboard admin** - Gérer les messages reçus
5. **Templates dynamiques** - Personnalisation par type de demande

---

## 📞 Support

- Documentation EmailJS : https://www.emailjs.com/docs/
- Exemples : https://www.emailjs.com/docs/examples/
- Support : support@emailjs.com

---

✅ **Configuration terminée !** Votre formulaire de contact est maintenant opérationnel ! 🎉
