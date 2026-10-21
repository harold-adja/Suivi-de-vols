# ✈️ SuiviVol — Application de Suivi de Vols en Temps Réel

Application web moderne construite avec **Next.js 14**, **React**, **TypeScript** et **Tailwind CSS**.

Elle permet de rechercher un vol par son numéro (ex. : `AF123`) et d'afficher les informations en temps réel :
- Compagnie aérienne et numéro de vol
- Aéroports de départ et d'arrivée (codes IATA et villes)
- Horaires prévus et réels
- Statut du vol avec badge coloré (*En vol*, *Atterri*, *Retardé*, *Annulé*, *Programmé*)

---

## 🛠️ Prérequis

Pour exécuter cette application, vous devez avoir **Node.js** installé sur votre ordinateur :
1. Téléchargez et installez Node.js (version LTS recommandée) depuis [nodejs.org](https://nodejs.org/).
2. Redémarrez votre terminal ou invite de commandes après l'installation.
3. Vérifiez l'installation en tapant :
   ```bash
   node -v
   npm -v
   ```

---

## 🚀 Lancement en local sur votre PC

### 1. Ouvrir un terminal dans le dossier du projet
Ouvrez PowerShell ou l'Invite de commandes, puis placez-vous dans le dossier :
```powershell
cd C:\Users\Harold\.gemini\antigravity\scratch\mon-site
```

### 2. Installer les dépendances
```powershell
npm install
```

### 3. Lancer le serveur de développement
```powershell
npm run dev
```

### 4. Ouvrir l'application
Ouvrez votre navigateur web et rendez-vous sur :  
👉 **http://localhost:3000**

---

## 🧪 Tester avec les données fictives (incluses)

Tant que vous n'avez pas renseigné de vraie clé API, l'application fonctionne automatiquement avec des **données de test réalistes**. Vous pouvez tester ces numéros de vol :

| Numéro | Compagnie | Trajet | Statut testé |
|--------|-----------|--------|--------------|
| **AF123** | Air France | Paris (CDG) → New York (JFK) | 🛫 **En vol** |
| **LH456** | Lufthansa | Francfort (FRA) → Barcelone (BCN) | 🛬 **Atterri** |
| **BA789** | British Airways | Londres (LHR) → Dubaï (DXB) | ⏳ **Retardé** |
| **EK999** | Emirates | Dubaï (DXB) → Tokyo (NRT) | ❌ **Annulé** |
| **VY321** | Vueling | Barcelone (BCN) → Paris (ORY) | 🕐 **Programmé** |

Si vous entrez un numéro inconnu (ex. : `XX999`), l'application affichera un message d'erreur clair en français.

---

## 🔑 Brancher la vraie API (AviationStack)

Pour suivre de **vrais vols en direct** :

1. Rendez-vous sur [aviationstack.com](https://aviationstack.com/).
2. Cliquez sur **« Get Free API Key »** et créez un compte gratuit.
3. Copiez votre clé d'accès API depuis votre tableau de bord.
4. Ouvrez le fichier [`.env.local`](.env.local) situé à la racine du projet.
5. Remplacez `VOTRE_CLE_ICI` par votre vraie clé :
   ```env
   AVIATIONSTACK_API_KEY=votre_cle_secrete_ici
   ```
6. Redémarrez le serveur (`Ctrl + C` puis `npm run dev`).

> [!NOTE]
> Le fichier `.env.local` est configuré dans le `.gitignore` : votre clé ne sera jamais exposée sur GitHub ou dans le code visible côté client. L'appel à l'API passe par une route serveur Next.js sécurisée (`/api/flight`).

---

## ☁️ Mettre en ligne gratuitement sur Vercel

Vercel est la plateforme officielle des créateurs de Next.js, 100% gratuite pour les projets personnels :

1. **Créer un dépôt GitHub :**
   - Créez un compte sur [github.com](https://github.com) si vous n'en avez pas.
   - Créez un nouveau dépôt public ou privé nommé `suivivol`.
   - Dans le dossier du projet, publiez votre code :
     ```powershell
     git init
     git add .
     git commit -m "Initial commit - SuiviVol"
     git branch -M main
     git remote add origin https://github.com/VOTRE_PSEUDO/suivivol.git
     git push -u origin main
     ```

2. **Déployer sur Vercel :**
   - Allez sur [vercel.com](https://vercel.com) et connectez-vous avec votre compte GitHub.
   - Cliquez sur **« Add New... »** puis **« Project »**.
   - Importez votre dépôt `suivivol`.
   - Dans la section **« Environment Variables »**, ajoutez :
     - **Name** : `AVIATIONSTACK_API_KEY`
     - **Value** : votre clé AviationStack (ou laissez vide pour utiliser les données de test).
   - Cliquez sur **« Deploy »**.

En moins d'une minute, votre application sera accessible mondialement via une URL en `https://suivivol.vercel.app` !

---

## 📁 Architecture du projet

```
mon-site/
├── .env.local                    # Clé API privée
├── .gitignore                    # Fichiers ignorés par Git
├── package.json                  # Dépendances du projet
├── next.config.js                # Configuration Next.js
├── tailwind.config.ts            # Configuration Tailwind CSS
├── tsconfig.json                 # Configuration TypeScript
├── src/
│   ├── app/
│   │   ├── layout.tsx            # Mise en page globale (balise html, polices)
│   │   ├── page.tsx              # Page d'accueil interactive
│   │   ├── globals.css           # Styles CSS globaux & Tailwind
│   │   └── api/
│   │       └── flight/
│   │           └── route.ts      # Proxy API serveur sécurisé (AviationStack)
│   ├── components/
│   │   ├── Header.tsx            # Barre de navigation avec icône ✈️
│   │   ├── SearchBar.tsx         # Barre de recherche avec autocomplétion suggérée
│   │   ├── FlightCard.tsx        # Carte visuelle du vol (trajet, aéroports, horaires)
│   │   ├── StatusBadge.tsx       # Badge coloré selon le statut
│   │   ├── LoadingSpinner.tsx    # Indicateur de chargement animé
│   │   └── ErrorMessage.tsx      # Messages d'erreur clairs en français
│   ├── lib/
│   │   └── mockData.ts           # Données de test réalistes
│   └── types/
│       └── flight.ts             # Types TypeScript et fonctions utilitaires
└── README.md
```
