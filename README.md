# 🚀 BidBooster — Démo SaaS IA pour la Réponse aux Appels d'Offres

> **Projet vibe-codé en ~2h avec [Claude](https://claude.ai)** dans le cadre du Mastère Spécialisé MSIT (Mines Paris - PSL)

![BidBooster Demo](https://img.shields.io/badge/Status-Demo-blue) ![Made with Claude](https://img.shields.io/badge/Vibe%20Coded-with%20Claude-orange) ![MSIT](https://img.shields.io/badge/MSIT-Mines%20Paris-purple)

## 📋 À propos

BidBooster est une **démo fonctionnelle** d'un SaaS IA dédié à l'automatisation de la réponse aux appels d'offres. Ce prototype illustre comment l'intelligence artificielle peut transformer l'avant-vente des ESN et cabinets de conseil.

⚠️ **Disclaimer** : Il s'agit d'une démo de démonstration. Toutes les données, clients et chiffres présentés sont **100% fictifs**.

## Consultation
Le temps de la foramtion, le site restera visible ici : https://msit-bid-booster.pages.dev/

## ✨ Fonctionnalités Démontrées

### Landing Page (`index.html`)
- Value proposition claire
- Calculateur ROI interactif
- SSO entreprise (simulation)

### Dashboard (`dashboard.html`)
- Vue pipeline des AO en cours
- Scores LLM-as-a-Judge (4 modèles open source)
- Panel détail AO avec métriques

### Pipeline (`pipeline.html`)
- Gestion des appels d'offres
- Filtres et tri dynamiques
- Statuts GO/NO-GO/À qualifier

### Technologie (`technologie.html`)
- Flow métier en 6 étapes
- Architecture souveraine européenne
- Human-in-the-Loop mis en valeur

## 🛠️ Stack Technique

```
HTML5 + Tailwind CSS (CDN) + Vanilla JS
├── Lucide Icons
├── Google Fonts (Outfit, Plus Jakarta Sans)
└── Hébergement statique (Cloudflare Pages)
```

**Philosophie "No-Build"** : Stack volontairement simple pour un prototypage ultra-rapide. Aucune dépendance npm, aucun bundler.

## 🚀 Lancer en Local

```bash
# Cloner le repo
git clone https://github.com/francois-hacktion/MSIT-Bid-Booster.git
cd MSIT-Bid-Booster

# Serveur local Python
python3 -m http.server 8080

# Ou avec Node
npx serve .
```

Puis ouvrir http://localhost:8080

## 📁 Structure

```
MSIT-Bid-Booster/
├── index.html          # Landing page
├── dashboard.html      # Dashboard principal
├── pipeline.html       # Gestion pipeline AO
├── technologie.html    # Page architecture technique
├── logos/              # Assets visuels
│   └── BidBooster.png
└── README.md
```

## 🎯 Contexte MSIT

Ce prototype a été réalisé dans le cadre du **Mastère Spécialisé Management des Systèmes d'Information et des Technologies** (MSIT) de Mines Paris - PSL, pour illustrer les concepts de :

- Product Management & Prototypage rapide
- IA Générative appliquée au métier
- Architecture souveraine & Open Source
- Human-in-the-Loop design

## 👤 Auteur

**François Pannecoucke**
- 🌐 [hacktion.fr](https://hacktion.fr)
- 💼 Consultant en Transformation Digitale

---

*Vibe-coded with Claude (Anthropic) — Février 2026*
