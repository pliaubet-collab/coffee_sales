# ☕ Suivi de Performance Commerciale — Réel vs Budget

Dashboard Power BI interactif analysant la performance commerciale d'un réseau de distribution de café (1 000 magasins, 10 enseignes, 10 villes françaises, 2023–2025), avec comparaison systématique du réalisé face aux objectifs budgétaires.

> 📌 **Dataset** : données de formation anonymisées (aucune donnée réelle d'entreprise). Le projet se concentre sur la méthodologie, la modélisation et la restitution transférables à tout contexte retail/distribution.

---

## 🎯 Problématique

Comment suivre la performance commerciale d'un réseau multi-enseignes face aux objectifs fixés, et identifier les leviers d'action réels (produit, point de vente) derrière des indicateurs globaux souvent trompeurs ?

## 🔍 Démarche

**1. Préparation et automatisation des données (Power Query)**
- Connexion et fusion de 3 sources (ventes, clients, produits) via un pipeline ETL reproductible
- Nettoyage (valeurs nulles, typage)
- Fractionnement et catégorisation géographique d'une colonne adresse composite, pour un géocodage fiable
- **Pipeline entièrement automatisé** : chaque étape de nettoyage/transformation est enregistrée comme une requête Power Query rejouable, un simple clic sur "Actualiser" recharge et retraite l'intégralité des données sources, sans aucune reprise manuelle. Ce qui a demandé plusieurs heures de préparation la première fois devient un rafraîchissement de quelques secondes à chaque nouvelle période

**2. Modélisation**
- Relations en étoile, table calendrier dédiée au time intelligence
- Mesures DAX organisées par dossiers logiques (CA par période, Écarts, Évolution N/N-1, Volumétrie, Classements)

**3. DAX avancé**
- Time intelligence (`DATEADD`) pour les comparaisons N / N-1
- Mesures d'écart et de taux d'atteinte budget (`DIVIDE` défensif)
- Classements dynamiques (`RANKX` + `ALL` + `FILTER`) pour isoler les meilleurs/pires points de vente **à l'intérieur d'un contexte de filtre donné** (par enseigne, via les infobulles) — avec gestion explicite des pièges de contexte de filtre (valeurs `BLANK` faussant un classement croissant)
- Formats de nombre dynamiques (expression de chaîne de format conditionnelle : affichage automatique en M€ ou Md€ selon l'ordre de grandeur)

**4. Dataviz & interactivité**
- Cartes KPI avec code couleur conditionnel (Réel vs Budget)
- Waterfall interactif avec signets et boutons (bascule Segment / Marque / Format)
- Infobulles personnalisées et **dynamiques** : survol d'une enseigne → Top 10 / Bottom 10 de ses magasins, avec le nom de l'enseigne affiché en temps réel
- Carte géographique avec dégradé de couleur (plutôt que taille de bulle, pour refléter honnêtement un écart territorial modéré)

## 💡 Insights clés

- Le réseau dépasse systématiquement son budget (**+4,2 %**), de façon homogène sur tous les canaux — signal de stabilité plus que de disparité
- La marque leader (**Grand Mère**, 931 k€... en volume) doit sa première place à son **prix moyen le plus bas** du portefeuille, pas à un positionnement premium — lecture croisée prix/volume
- La vraie disparité de performance se joue au niveau du **magasin individuel** (écart-type ~16 % de la moyenne, facteur ~3x entre meilleur et pire point de vente), **sans corrélation avec l'enseigne ou la zone géographique** → implique un accompagnement terrain ciblé plutôt qu'une politique uniforme par canal
- Un contrôle qualité des données a révélé que l'identifiant magasin n'était fiable qu'en combinant nom + ville + enseigne (1000 magasins réels, contre une fausse lecture à 776 en ne se fiant qu'au nom) — corrigé avant toute conclusion

## 💼 Valeur business concrète

Au-delà de la technique, ce que ce type de projet apporte une fois déployé en entreprise :

| Compétence | Bénéfice concret pour l'entreprise |
|---|---|
| Pipeline Power Query automatisé | Fin des reportings Excel reconstruits à la main chaque mois — gain de temps récurrent et suppression du risque d'erreur de copier-coller sur un fichier critique |
| Mesures DAX Réel vs Budget en temps réel | Pilotage budgétaire actualisable à tout moment, sans attendre une consolidation manuelle en fin de mois |
| Classements dynamiques par magasin (RANKX) | Détection immédiate des points de vente à accompagner, sans extraction ni tri manuel dans Excel |
| Infobulles contextuelles par enseigne | Les managers terrain explorent eux-mêmes le détail qui les concerne, sans solliciter un rapport sur-mesure à chaque demande — autonomie des équipes métier |
| Contrôle qualité des données (détection de doublons d'identifiants) | Fiabilise les décisions prises sur ces chiffres — une erreur de granularité non détectée peut fausser durablement un pilotage |

## 🛠️ Compétences démontrées

`Power Query (ETL & automatisation)` `Modélisation de données` `DAX avancé (RANKX, CALCULATE, DATEADD, FILTER, format dynamique)` `Time Intelligence` `UX de dashboard (signets, infobulles dynamiques)` `Rigueur analytique & contrôle qualité des données` `Storytelling data`

## 📁 Contenu du repo

- `Dashboard.pbix` — fichier Power BI source
- `Dashboard.pdf` — export statique du rapport
- Captures d'écran du dashboard

---

📬 Pierre Liaubet — [LinkedIn](https://www.linkedin.com/in/pierre-liaubet-tourisme-data/) · [GitHub](https://github.com/pliaubet-collab)
