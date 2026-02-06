# Spécifications Techniques BidBooster

> **Statut** : Production Ready  
> **Version** : 1.2.0  
> **Dernière MÀJ** : Février 2026  
> **Classification** : Confidentiel / Interne

---

## 1. Vue d'Ensemble de l'Architecture

BidBooster repose sur une architecture **"Sovereign-First"** conçue pour garantir la confidentialité totale des données sensibles des appels d'offres. Le système utilise un pipeline d'inférence RAG (Retrieval-Augmented Generation) hébergé exclusivement sur des infrastructures européennes.

### Diagramme de Flux Cognitif

```mermaid
graph TD
    subgraph "Niveau 1 : Ingestion & Sécurité"
        A[Sources Données] -->|TLS 1.3 / Chiffrement| B(Ingestion Engine)
        B --> C{Anonymisation}
        C -->|Données Nettoyées| D[Vector Database]
        C -->|Métadonnées| E[SQL Database]
    end

    subgraph "Niveau 2 : Moteur Cognitif (Europe)"
        D --> F[RAG Controller]
        E --> F
        F -->|Contexte| G[Orchestrateur LLM]
        G --> H[Model A: Mistral Large]
        G --> I[Model B: Qwen 2.5]
        G --> J[Model C: Llama 3]
    end

    subgraph "Niveau 3 : Consensus & Validation"
        H & I & J --> K[Aggrégateur de Scores]
        K --> L[LLM-as-a-Judge]
        L -->|Verdict| M[Interface Expert]
    end

    style B fill:#e0e7ff,stroke:#4338ca
    style G fill:#f3e8ff,stroke:#7e22ce
    style L fill:#dcfce7,stroke:#15803d
```

---

## 2. Infrastructure & Souveraineté

Nous appliquons une politique de **Zéro Data Transfer** hors de l'Union Européenne.

| Composant | Technologie | Hébergeur | Localisation |
| :--- | :--- | :--- | :--- |
| **Compute / GPU** | Nvidia H100 Cluster | Scaleway | Paris (DC5) |
| **Vector DB** | Qdrant | OVHcloud | Roubaix |
| **App Server** | Node.js / Bun | Clever Cloud | Paris |
| **Stockage Fichier** | S3 Compatible | Scaleway | Amsterdam |

> [!IMPORTANT]
> **Conformité RGPD** : Toutes les données sont chiffrées au repos (AES-256) et en transit (TLS 1.3). Aucune donnée d'entraînement n'est renvoyée aux fournisseurs de modèles (Azure/OpenAI exclus).

---

## 3. Moteur d'Intelligence Artificielle

### Approche Multi-Modèles (Ensemble Learning)
Pour éviter les hallucinations et garantir la précision des analyses d'appels d'offres, BidBooster n'utilise pas un, mais **3 modèles concurrents** pour chaque tâche critique.

1.  **Mistral Large 2 (70B)** : Spécialiste de la syntaxe et du raisonnement juridique français.
2.  **Qwen 2.5 (72B)** : Excellent pour l'extraction de données structurées et de tableaux financiers.
3.  **Llama 3.3 (70B)** : Utilisé pour la synthèse et la reformulation commerciale.

### Algorithme de "Consensus Cognitif"
Le module **LLM-as-a-Judge** évalue la cohérence des trois sorties :
-   Si la variance est > 15%, une alerte "Incertitude" est levée pour l'expert humain.
-   Si la variance est < 5%, la réponse est considérée comme fiable et pré-validée.

---

## 4. Sécurité & Authentification

### Mécanismes de Défense
-   **WAF (Web Application Firewall)** : Protection contre les injections SQL et XSS.
-   **Rate Limiting** : 100 req/min par IP via Redis.
-   **Audit Logs** : Traçabilité immuable de toutes les décisions (Qui a validé Quoi et Quand).

### SSO & Gestion des Identités
L'intégration Enterprise supporte :
-   OIDC (OpenID Connect)
-   SAML 2.0 (Azure AD, Okta)
-   Visualisation des rôles via RBAC (Role-Based Access Control) :
    -   `Admin` : Configuration système & Facturation
    -   `Bid Manager` : Validation & Envoi
    -   `Analyst` : Enrichissement & Recherche

---

## 5. Workflow Métier : Le Pipeline "BidBooster"

Ce diagramme illustre l'interaction continue entre l'IA générative et l'expertise commerciale pour maximiser le taux de transformation ("Win Rate").

```mermaid
graph TD
    %% Entrée
    Start[📡 Capture Appel d'Offre]:::startNode
    
    subgraph "Phase 1 : Intelligence & Stratégie (Automatisé)"
        Analysis[🧠 Analyse Sémantique Profonde]:::aiNode
        RAG{🔍 RAG Strategique}:::ragNode
        Knowledge[(🗄️ Base de Connaissance)]:::dbNode
        
        Start --> Analysis
        Analysis --> RAG
        
        Knowledge <-->|Extraction Pricing & Argus| RAG
        Knowledge <-->|Preuves de Succès 'Même Client'| RAG
        
        Judge[⚖️ LLM-as-a-Judge]:::judgeNode
        RAG -->|Contexte Enrichi| Judge
        Judge -->|Score de Faisabilité| Gate{Verdict IA}:::decisionNode
    end
    
    subgraph "Phase 2 : Production Augmentée (Hybride)"
        Draft[📝 Génération Draft 70%]:::docNode
        Expert[👨‍💼 Expert Commercial]:::humanNode
        Refine[✨ Affinage & Styles]:::aiNode
        
        Gate -- "GO (>80%)" --> Draft
        Gate -- "A ÉVALUER (50-80%)" --> Expert
        Gate -- "NO-GO (<50%)" --> Archive((⛔ Archivage)):::stopNode
        
        Draft --> Expert
        Expert -->|Instruction de Dernier km| Refine
        Refine -->|Boucle de Correction| Expert
    end
    
    subgraph "Phase 3 : Livraison"
        Final[🚀 Dossier Finalisé]:::finalNode
    end
    
    Refine --> Final

    %% Styling Classes
    classDef startNode fill:#fef3c7,stroke:#d97706,stroke-width:2px,color:#92400e;
    classDef aiNode fill:#e0e7ff,stroke:#4338ca,stroke-width:2px,color:#3730a3;
    classDef ragNode fill:#f3e8ff,stroke:#7e22ce,stroke-width:2px,color:#6b21a8;
    classDef dbNode fill:#f3f4f6,stroke:#4b5563,stroke-width:2px,stroke-dasharray: 5 5;
    classDef judgeNode fill:#dcfce7,stroke:#15803d,stroke-width:2px,color:#166534;
    classDef decisionNode fill:#fcd34d,stroke:#b45309,stroke-width:2px,shape:rhombus;
    classDef docNode fill:#dbeafe,stroke:#1e40af,stroke-width:1px;
    classDef humanNode fill:#ffedd5,stroke:#c2410c,stroke-width:4px,color:#9a3412;
    classDef stopNode fill:#fee2e2,stroke:#991b1b,stroke-width:1px;
    classDef finalNode fill:#10b981,stroke:#064e3b,stroke-width:2px,color:#fff,font-weight:bold;
```

> **Note sur le RAG Stratégique** : L'IA ne cherche pas seulement des mots-clés, elle identifie des *patterns de succès*. Si nous avons déjà gagné chez ce client, les arguments utilisés lors de la victoire précédente sont "sur-pondérés" dans la génération du draft.

---

## 6. Intégrations API

Le système expose une API RESTful documentée (Swagger/OpenAPI 3.0) pour l'intégration avec les CRM du marché.

```json
// Exemple de Payload d'Analyse
{
  "tender_id": "AO-2026-X89",
  "files": ["cctp.pdf", "rc.pdf"],
  "options": {
    "deep_scan": true,
    "financial_extraction": true,
    "risk_level": "strict"
  }
}
```

---

> _Ce document est la propriété exclusive de BidBooster. Toute reproduction interdite._
