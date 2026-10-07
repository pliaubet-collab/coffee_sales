# Suivi de performance commerciale : Réel vs Budget

Dashboard Power BI interactif analysant la performance commerciale d'un réseau de distribution de café (1 000 magasins, 10 enseignes, 10 villes françaises, 2023 à 2025), avec comparaison du réalisé face aux objectifs budgétaires et à l'année précédente.

> **Dataset** : données de formation anonymisées, sans lien avec une entreprise réelle. Le projet porte sur la méthode (préparation, modélisation, restitution), transposable à tout contexte retail ou distribution. Certains indicateurs sont très homogènes, ce qui s'explique probablement par la génération du jeu de données.

---

## Problématique

Comment suivre la performance commerciale d'un réseau multi-enseignes face à ses objectifs, et identifier où se situent les vrais leviers d'action (produit, point de vente) derrière des indicateurs globaux parfois trompeurs ?

## Démarche

**1. Préparation des données (Power Query)**
- Connexion et combinaison de 3 sources (ventes, clients, produits)
- Nettoyage des valeurs nulles, typage, création de la colonne de chiffre d'affaires
- Chaque étape est enregistrée dans une requête rejouable : lorsque les fichiers sources sont mis à jour, un clic sur « Actualiser » relance tout le traitement sans reprise manuelle

**2. Modélisation**
- Modèle en étoile et table calendrier dédiée au time intelligence
- Mesures DAX organisées par dossiers (CA par période, écarts, évolution N/N-1, volumétrie, classements)

**3. DAX**
- Comparaisons N / N-1 avec `DATEADD`
- Écarts et taux d'atteinte du budget, avec `DIVIDE` pour éviter les divisions par zéro
- Classements dynamiques (`RANKX`, `ALL`, `FILTER`) pour isoler les 10 meilleurs et 10 moins bons magasins dans le contexte de filtre actif (une enseigne survolée, par exemple). Un piège a été identifié et corrigé : les combinaisons vides (`BLANK`) faussaient le classement croissant

**4. Visualisation et interactivité**
- Cartes de synthèse (CA réel, CA budget, écarts, évolution N/N-1) et filtres par période, enseigne, segment et marque
- Graphique de tendance Réel / Budget / N-1 par mois
- Treemap du mix produit (segment puis marque)
- Waterfall budget vers réel, avec signets et boutons pour basculer entre segment, marque et format
- Infobulles personnalisées : le survol d'une enseigne affiche ses 10 meilleurs et 10 moins bons magasins

## Insights clés

1. **L'écart se joue entre magasins.** Sur 1 000 magasins, le CA réel varie d'environ 2,1 à 6,3 M€ (moyenne 3,6 M€). Les magasins les plus faibles se répartissent entre plusieurs enseignes et villes : le levier est le point de vente, pas le canal ni la zone géographique.
2. **La croissance s'est arrêtée en 2025.** Le CA réel annuel passe d'environ 1,10 Md€ (2023) à 1,24 Md€ (2024), puis reste stable en 2025.
3. **Grand Mère est la première marque en CA réel** (931 M€) avec le prix moyen le plus bas du portefeuille : sa position vient du volume plutôt que du prix.
4. **Capsules pèse environ 37 % du CA.** Les trois autres segments sont proches entre eux, et le dépassement du budget se répartit au prorata du poids de chaque segment.
5. **Un dépassement du budget quasi identique partout (environ +4 % sur la période).** Cette homogénéité ne permet pas de repérer un canal en difficulté, ce qui explique le choix de descendre au niveau magasin.
   

## Ce que ce projet illustre côté entreprise

| Compétence | Bénéfice |
|---|---|
| Pipeline Power Query rejouable | Moins de retraitement manuel à chaque mise à jour, et moins de risque d'erreur de copier-coller |
| Mesures Réel vs Budget | Suivi des écarts actualisable sans consolidation manuelle |
| Classements dynamiques par magasin | Repérage rapide des points de vente à accompagner |
| Infobulles contextuelles | Les équipes métier consultent elles-mêmes le détail de leur enseigne |
| Contrôles qualité sur les données | Des conclusions fiabilisées avant diffusion |

## Compétences

`Power Query` `Modélisation de données` `DAX (CALCULATE, DATEADD, RANKX, FILTER)` `Time intelligence` `Signets et infobulles Power BI` `Contrôle qualité des données` `Restitution des résultats`

## Contenu du dépôt

- `cafe.pbix` : fichier Power BI source
- `cafe.pdf` : export statique du rapport
- Captures d'écran du dashboard

---

Pierre Liaubet · [LinkedIn](https://www.linkedin.com/in/pierre-liaubet-tourisme-data/) · [GitHub](https://github.com/pliaubet-collab)
