# AVE ROX — Landing Page

> Brief complet pour Bolt.new

## Contexte
Landing page pour **AVE ROX**, compétition fitness inspirée de HYROX (format français).
Le fichier `index.html` contient le design complet. Les images sont dans `images/`.

---

## Ce qu'il faut faire

### 1. Animations visuelles
- Animer l'image hero (`images/poster.jpg`) : léger effet **parallax** au scroll + fade-in au chargement
- Animer l'entrée de chaque section avec un **slide-up** fluide (déjà partiellement en place avec `.reveal`)
- Ajouter un effet **Ken Burns** (zoom lent) sur l'image hero en fond
- Le ticker doré animé doit rester tel quel
- Le curseur custom doré doit rester tel quel

### 2. Formulaire d'inscription → Base de données
**Remplacer le localStorage actuel par une vraie base de données.**

Utiliser **Supabase** (gratuit) :
- Créer une table `inscriptions` avec les champs : `id, prenom, nom, email, tel, format, categorie, club, message, created_at`
- Chaque soumission du formulaire insère une ligne dans Supabase
- Afficher un toast de confirmation après soumission

Variables d'environnement à prévoir :
```
VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=
```

### 3. Email automatique à chaque inscription
**À chaque nouvelle inscription**, envoyer un email à :
**julien.martinez@evelyne.fr**

Utiliser **Resend** (gratuit jusqu'à 3000 emails/mois) ou **EmailJS** :
- Objet : `Nouvelle inscription AVE ROX — [Prénom] [Nom]`
- Corps : récapitulatif complet de l'inscription (tous les champs)
- Format HTML avec le style AVE ROX (fond noir, or #e3ac00)

Variables d'environnement :
```
VITE_RESEND_API_KEY=
NOTIFICATION_EMAIL=julien.martinez@evelyne.fr
```

### 4. Rapport hebdomadaire CSV par email
**Chaque lundi matin à 8h**, envoyer automatiquement un email à **julien.martinez@evelyne.fr** avec :
- Objet : `📊 Rapport hebdo AVE ROX — Semaine du [date]`
- Pièce jointe : fichier CSV `inscriptions_averox_semaine_XX.csv`
- Colonnes CSV : `ID, Prénom, Nom, Email, Téléphone, Format, Catégorie, Club, Message, Date inscription, Statut`
- La colonne **Statut** doit afficher `🆕 NOUVEAU` pour les inscrits de la semaine en cours, `Ancien` pour les autres
- Le CSV doit contenir **TOUTES** les inscriptions (pas seulement les nouvelles)

Implémenter avec un **Cron Job** (Supabase Edge Functions + pg_cron, ou Vercel Cron + API Route).

---

## Stack recommandée
- **Frontend** : HTML/CSS/JS vanilla (conserver le design existant) ou React si nécessaire
- **BDD** : Supabase (PostgreSQL)
- **Emails transactionnels** : Resend
- **Cron** : Supabase Edge Functions + pg_cron
- **Hébergement** : Vercel ou Netlify

---

## Design — Ne pas modifier
- Couleurs : `#e3ac00` (or), `#070707` (noir), `#ffffff` (blanc)
- Typographies : `Audiowide` + `Barlow Condensed` + `Barlow`
- Conserver TOUS les effets existants (curseur, ticker, scroll reveal, clip-path sur les boutons)
- Le formulaire garde sa structure et son style

---

## Fichiers
```
index.html     — Landing page complète (design final)
images/
  logo.png     — Logo AVE ROX (blanc + or, fond transparent)
  poster.jpg   — Affiche officielle avec les athlètes
```
