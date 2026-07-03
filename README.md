# 🗺️ Jour 3 / 10 — Tableau : Maps & Visualisations Géographiques

> **Série : 10 Days of Tableau** · Jour 3/10  
> Concepts : Carte choroplèthe · Carte de symboles · Geocoding · Latitude/Longitude · Couches de carte

---

## 📁 Fichiers du projet

```
day-03-maps/
│
├── ventes_geo_tableau_j3.xlsx    ← 459 lignes · 16 colonnes · 12 régions françaises
└── README.md
```

---

## 📊 Les données — colonnes géographiques

| Colonne | Type Tableau | Rôle |
|---------|-------------|------|
| `Région` | Dimension géographique | Reconnue nativement par Tableau |
| `Ville` | Dimension géographique | Chef-lieu de région |
| `Latitude` | Mesure (décimal) | Pour cartes de symboles custom |
| `Longitude` | Mesure (décimal) | Pour cartes de symboles custom |
| `Montant` | Mesure | CA → taille des symboles |
| `Marge Brute` | Mesure | Marge → couleur |

---

## 🚀 Connexion des données

```
1. Ouvrir Tableau
2. Fichier → Se connecter → Microsoft Excel → ventes_geo_tableau_j3.xlsx
3. Feuille "Ventes Régions" → glisser sur le canvas
4. Vérifier :
   - Région, Ville → Abc (dimension texte)
   - Latitude, Longitude → # (mesure numérique)
   - Montant, Marge Brute → # (mesure numérique)
5. Cliquer "Feuille 1"
```

---

## 🗺️ ÉTAPE 1 — Carte Choroplèthe : CA par Région

Une carte choroplèthe remplit chaque région d'une couleur selon une valeur.

```
1. Dans le panneau Données :
   → Double-cliquer sur "Région"
   → Tableau détecte le champ géographique et crée automatiquement une carte

2. Si Tableau ne reconnaît pas Région :
   → Clic droit sur "Région" → Rôle géographique → État/Province

3. Glisser "Montant" → carte Couleur (panneau Repères)
   → Les régions se colorient selon le CA : clair = faible, foncé = élevé

4. Améliorer la palette :
   → Cliquer sur la légende Couleur → Modifier les couleurs
   → Choisir "Séquentiel" → Bleu ou Vert-Rouge

5. Ajouter les infobulles :
   → Glisser "Marge Brute" → carte Info-bulle
   → Survoler une région → le CA et la marge s'affichent

6. Renommer : "CA par Région (Choroplèthe)"
```

---

## 🔵 ÉTAPE 2 — Carte de Symboles : Bulles par Ville

Une carte de symboles place des cercles proportionnels à une valeur.

```
1. Nouvelle feuille (icône + en bas)

2. Glisser "Longitude" → Colonnes
   Glisser "Latitude"  → Lignes
   → Une carte apparaît avec un seul point au centre

3. Changer l'agrégation :
   → Clic droit sur SUM(Longitude) → Attribut
   → Clic droit sur SUM(Latitude)  → Attribut

4. Dans le panneau Repères :
   → Changer le type de "Automatique" à "Cercle"

5. Glisser "Ville" → carte Détail
   → 12 points apparaissent, un par ville

6. Glisser "Montant" → carte Taille
   → Les cercles sont proportionnels au CA

7. Glisser "Marge Brute" → carte Couleur
   → Ajouter un dégradé : rouge (marge faible) → vert (marge élevée)
   → Modifier les couleurs → Divergent → Rouge-Blanc-Vert

8. Glisser "Région" → carte Info-bulle
   → Renommer : "Carte de Symboles"
```

---

## 📊 ÉTAPE 3 — Carte Combinée : Choroplèthe + Symboles

Superposer les deux types de cartes sur la même vue.

```
1. Reprendre la feuille "CA par Région (Choroplèthe)"

2. Ajouter une couche de symboles :
   → Glisser "Latitude" (depuis le panneau Données) directement
     sur l'axe Lignes existant → une deuxième vignette apparaît

3. Dans la vignette Latitude(2) :
   → Changer le type → Cercle
   → Glisser "Montant" → Taille
   → Glisser "Ville" → Détail

4. Clic droit sur l'axe vertical → "Axe double"
   → Les deux couches se superposent sur la même carte

5. Renommer : "Carte combinée"
```

---

## 🎯 ÉTAPE 4 — Filtre Géographique

```
1. Glisser "Région" → zone Filtres
   → Cocher uniquement certaines régions
   → Clic droit → "Afficher le filtre" pour le rendre interactif

2. Filtre par Trimestre :
   → Glisser "Trimestre" → zone Filtres
   → Clic droit → "Afficher le filtre"
   → Le filtre bascule entre T1, T2, T3, T4

3. Filtre contextuel (recommandé pour les cartes) :
   → Clic droit sur le filtre Région → "Ajouter au contexte"
   → Les autres filtres s'appliquent dans la zone sélectionnée
```

---

## 📍 ÉTAPE 5 — Changer le fond de carte

```
Carte → Couches de carte :
   → Style de carte :
      - Normal (par défaut)
      - Gris clair (recommandé pour mettre les données en valeur)
      - Sombre (effet premium)
      - Rue (si tu veux les noms de rues)

Carte → Arrière-plan des cartes → Hors connexion
   → Fonctionne sans connexion internet
```

---

## 🔧 ÉTAPE 6 — Rôles géographiques (si Tableau ne reconnaît pas)

```
Si une région n'est pas reconnue automatiquement :

Clic droit sur "Région" dans le panneau Données
→ Rôle géographique → État/Province

Clic droit sur "Ville" → Rôle géographique → Ville

Pour les coordonnées :
Clic droit sur "Latitude"  → Rôle géographique → Latitude
Clic droit sur "Longitude" → Rôle géographique → Longitude
```

---

## 🚀 ÉTAPE 7 — Dashboard Géographique

```
1. Nouveau dashboard → Taille : 1400 × 900 px

2. Glisser :
   → "CA par Région" en fond (grande zone)
   → "Carte de Symboles" à côté ou en superposition

3. Ajouter un filtre global :
   → Glisser une feuille → clic sur l'icône entonnoir → filtre sur Trimestre
   → Appliquer à toutes les feuilles utilisant la source

4. Ajouter un titre :
   → Dashboard → Afficher le titre
   → Double-clic pour modifier : "Performance Commerciale par Région — 2024"

5. Sauvegarder sur Tableau Public :
   → Serveur → Enregistrer sur Tableau Public
```

---

## 💡 Astuces cartographie Tableau

| Problème | Solution |
|---|---|
| Région non reconnue | Clic droit → Rôle géographique → État/Province |
| Points au mauvais endroit | Vérifier que Latitude/Longitude sont des Mesures (pas Dimensions) |
| Carte trop zoomée | Maintenir Shift+clic pour dézoomer |
| Fond de carte manquant | Carte → Arrière-plan → Hors connexion |
| Symboles trop petits | Panneau Repères → Taille → glisser le curseur |

---

---

⭐ **Si ce projet t'aide, mets une étoile !**
