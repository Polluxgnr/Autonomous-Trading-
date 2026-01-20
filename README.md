# 🏛️ AEGIS Institutional : Système de Trading Quantitatif à IA
**Pipeline de production Cloud pour l'arbitrage directionnel et la gestion systématique du risque.**

---

## 🎯 Philosophie et Raisonnement Quantitatif
AEGIS est conçu sur l'hypothèse que les marchés financiers présentent des **structures de probabilité exploitables** malgré le bruit court-terme. Le système ne cherche pas à "deviner" le prix, mais à identifier des **fenêtres d'opportunité à haute conviction** via une hiérarchie de filtres mathématiques.

### Pourquoi ce système est robuste :
* **Meta-Labeling (Supervision IA)** : Une stratégie Alpha génère des signaux bruts, puis une IA (Random Forest) agit comme un comité de crédit pour valider si les conditions actuelles (volatilité, régime) favorisent statistiquement le succès.
* **Segmentation par Régime (HMM)** : Utilisation d'un **Modèle de Markov Caché** pour classifier l'état latent du marché (Calme, Volatile, Baissier) et adapter les indicateurs techniques en temps réel.
* **Symbiose Multi-Indicateurs** : Fusion du RSI (momentum), de l'ATR (volatilité) et du ROC (vitesse) pour une lecture multidimensionnelle de l'action du prix.

---

## 🏗️ Architecture du Pipeline de Production
Le système est décomposé en 9 modules autonomes s'exécutant en série sur une VM Google Cloud :

### 1. Ingestion & Ingénierie (M1-M3)
* **Ingestion** : Flux de données institutionnels via Alpaca SDK.
* **Normalisation** : Transformation des prix bruts en caractéristiques stationnaires pour le Machine Learning.
* **Alpha Generation** : Détection mathématique des points d'entrée optimaux.

### 2. Intelligence Artificielle & Risque (M4-M6)
* **Filtrage ML** : Réduction du "churn" par rejet de 40% à 80% des signaux faibles pour maximiser le ratio de Sharpe.
* **Allocation VaR (Value-at-Risk)** : Dimensionnement des positions pour qu'une perte probable (95% de confiance) ne dépasse jamais une fraction fixe du capital (670$).
* **Vanguard Shield** : Filtre macro (SMA 200 sur SPY) désactivant le système lors des phases de krach systémique.

### 3. Exécution & Reporting (M7-M9)
* **Synchronisation Active** : Rééquilibrage en temps réel du portefeuille Alpaca selon les cibles de l'IA.
* **Kill Switch** : Sécurité critique liquidant tout le portefeuille en cas de baisse intraday de 5%.
* **Visualisation** : Dashboard institutionnel envoyé sur Discord incluant courbes d'équité et Drawdown.

---

## 📊 Performances & Paramètres Globaux
* **Capital de Base** : 1000$.
* **Objectif de Sharpe** : > 1.2 (Rendement ajusté au risque de haut niveau).
* **Fréquence** : Daily (Exécution automatisée via Cron à 15h45 UTC).
* **Actifs** : Univers diversifié incluant QQQ, AMD, GOOGL, NVDA et BTC/USD.

---

## 💻 Stack Technique
* **Cloud** : Google Cloud Platform (Compute Engine e2-medium).
* **Langages** : Python 3.11, Pandas, Scikit-learn, Matplotlib, Hmmlearn.
* **Connectivité** : Alpaca-py API (Trading/Data), Discord Webhooks (Alerting).

---
**Développé par Gronier Pollux.** 🏛️⚖️🚀
