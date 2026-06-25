# 📊 RetailPulse Analytics Platform - NordRetail

Bienvenue sur le dépôt officiel du projet **RetailPulse**, la plateforme de Business Intelligence conçue pour l'enseigne paneuropéenne **NordRetail**.

**Développeuse principale :** Tracy

---

## 🏗️ 1. Architecture & Modélisation des Données

Afin d'optimiser les performances du moteur VertiPaq de Power BI et de garantir la cohérence des indicateurs, j'ai implémenté une **modélisation en étoile (Star Schema)**.

*   **FactSales** : Centralise l'ensemble des transactions de ventes (Chiffre d'affaires, quantités, marges).
*   **FactInventory** : Suivi des niveaux de stocks et flux logistiques.
*   **FactCustomerEvents** : Enregistrement des interactions et de la fidélité des clients.
*   **DimProduct** : Catalogue complet des produits (Catégories, sous-catégories).
*   **DimCustomer** : Profils de segmentation et données démographiques des clients.
*   **DimStore** : Configuration du réseau de points de vente physiques par pays et régions.
*   **DimDate** : Table temporelle générée dynamiquement en DAX (période 2022-2026), marquée comme table de dates officielle.

---

## 🔒 2. Sécurité au Niveau des Lignes (RLS)

Pour respecter les politiques de confidentialité de NordRetail, une couche de sécurité étanche a été configurée :

*   **Rôle Implémenté :** `Directeur France`
*   **Règle DAX appliquée :** `[Country] = "France"` sur la dimension `DimStore`.
*   **Fonctionnement :** Dès qu'un utilisateur disposant de ce rôle ouvre le rapport, les filtres se propagent en cascade vers les tables de faits, isolant exclusivement les données géographiques françaises et masquant le reste de l'Europe.

---

## 📈 3. Structure du Rapport (5 Pages)

Le rapport Power BI est découpé en **5 pages thématiques** spécialisées pour répondre aux besoins de chaque département :
1.  **Executive Dashboard** : Indicateurs macro de performance (CA, Marge %, Évolution YoY %, Clients actifs).
2.  **Analyse Catégories** : Exploration granulaire du catalogue produit exploitant des *Field Parameters* pour basculer dynamiquement d'une métrique à l'autre.
3.  **Performance Magasins** : Cartographie interactive du réseau commercial avec fonctionnalités de *Drill-through*.
4.  **Gestion des Stocks** : Tableau de bord logistique mettant en avant les alertes de couverture (produits à moins de 10 jours de stock).
5.  **Analyse Client & Rétention** : Suivi de la fidélité, du taux de churn et de la valeur de vie client.

---

## ⚙️ 4. Approche DevOps & Versioning

Ce projet intègre les bonnes pratiques d'ingénierie logicielle :
*   **Format .pbip (Power BI Project)** : Le rapport est découpé en fichiers de métadonnées textuels clairs (TMDL/BIM) pour permettre un suivi de modifications ligne par ligne dans Git.
*   **Gestion Git** : Utilisation d'un fichier `.gitignore` personnalisé pour exclure les caches locaux.