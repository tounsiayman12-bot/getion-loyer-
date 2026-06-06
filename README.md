# 🏘️ Système de Gestion Locative — Guide d'installation

## Prérequis
- XAMPP v3.3.0 ou supérieur (Apache + MySQL + PHP 8.x)
- Navigateur moderne (Chrome, Firefox, Edge)

---

## ⚡ Installation en 4 étapes

### 1. Copier les fichiers
Copiez le dossier **`gestion_loyer/`** dans :
```
C:\xampp\htdocs\gestion_loyer\
```

### 2. Démarrer XAMPP
Ouvrez le **XAMPP Control Panel** et démarrez :
- ✅ **Apache**
- ✅ **MySQL**

### 3. Créer la base de données
1. Ouvrez votre navigateur → http://localhost/phpmyadmin
2. Cliquez sur **"Importer"**
3. Sélectionnez le fichier : `sql/schema.sql`
4. Cliquez sur **"Exécuter"**

> La base `gestion_loyer` sera créée automatiquement avec les données de démonstration.

### 4. Accéder à l'application
Ouvrez votre navigateur :
```
http://localhost/gestion_loyer/
```

---

## 🗂️ Structure des fichiers

```
gestion_loyer/
├── index.php              → Tableau de bord
├── locaux.php             → Liste et gestion des locaux
├── loyer.php              → Génération des reçus arabes
├── config/
│   └── db.php             → Connexion MySQL (modifiez ici si besoin)
├── modules/
│   ├── layout.php         → En-tête HTML partagé
│   ├── layout_footer.php  → Pied HTML partagé
│   ├── local_detail.php   → Détail local (3 onglets)
│   ├── locataire_archive.php → Archives des contrats
│   ├── locataire_form.php → Formulaire locataire
│   └── recu_generate.php  → Reçu standalone (impression)
├── assets/
│   ├── css/style.css      → Styles globaux
│   ├── js/main.js         → UI helpers
│   └── js/recu_calc.js    → Moteur calcul reçu arabe
├── uploads/
│   ├── contrats/          → Contrats uploadés
│   └── documents_locaux/  → Docs des locaux
└── sql/
    └── schema.sql         → Structure + données démo
```

---

## ⚙️ Configuration base de données

Si votre MySQL a un mot de passe différent, modifiez `config/db.php` :

```php
define('DB_HOST', 'localhost');
define('DB_NAME', 'gestion_loyer');
define('DB_USER', 'root');
define('DB_PASS', '');  // ← votre mot de passe ici
```

---

## 📋 Fonctionnalités

### 🏠 Tableau de bord
- KPIs : nb locaux, locataires actifs, total loyers du mois
- Alertes d'augmentation dans les 30 jours
- Accès rapide aux locaux et génération de reçus

### 🏢 Locaux
- Liste complète avec statut Occupé / Vacant
- Ajout de local avec upload de document
- Vue détail avec 3 onglets :
  - **Archive** : historique des anciens locataires
  - **Locataire actuel** : fiche complète + téléchargement contrat
  - **Nouveau locataire** : formulaire d'onboarding complet

### 💰 Loyer / Reçus
- Navigation mois par mois (← →)
- Filtrage automatique : seuls les locataires dont le loyer est **dû ce mois-ci** s'affichent
- Reçu arabe complet (وصل تسويغ محل) avec :
  - Tous les champs modifiables en temps réel
  - Calcul automatique retenue / net
  - Montant en lettres arabes (dinars + millimes)
  - Période calculée selon fréquence (mois/trimestre/semestre)
  - Zone signature + timbre fiscal
  - Impression propre @media print

---

## 🔒 Sécurité
- PDO + requêtes préparées (anti SQL injection)
- Validation uploads (types + taille)
- htmlspecialchars sur toutes les sorties

---

## 📞 Données de démonstration incluses

| Local | Locataire | Fréquence | Montant |
|-------|-----------|-----------|---------|
| Magasin Centre-Ville | SARL TechStore | Mensuel | 850,000 TND |
| Appartement Lac | Karim Mansouri | Mensuel | 650,000 TND |
| Garage Ariana | Entreprise AutoPieces | Trimestriel | 300,000 TND |
| Bureau Menzah | Dr. Leila Bouzid | Semestriel | 900,000 TND |
