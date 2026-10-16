# QCM — NOAA Niño 3.4, Pandas, NumPy et mathématiques

**50 questions — Une seule réponse correcte par question.**

> **Corrigé** : la bonne réponse de chaque question est marquée ✅ et écrite en gras.

Pour chaque question, cochez une seule proposition parmi A, B, C, D ou E. Les extraits de code sont indépendants ; supposez les bibliothèques importées (`import numpy as np`, `import pandas as pd`) et les variables mentionnées déjà définies lorsque nécessaire.

## Question 1 — Import et inspection

Que fait cette instruction ?

```python
brut = pd.read_csv("nina34.anom.csv")
```

- ✅ **A. Elle charge un CSV dans un DataFrame Pandas.**
- **B.** Elle supprime les lignes manquantes.
- **C.** Elle crée un tableau de zéros.
- **D.** Elle calcule la moyenne.
- **E.** Elle exporte un CSV.

## Question 2 — Import et inspection

Que retourne `brut.shape` pour un tableau de 564 lignes et 2 colonnes ?

```python
print(brut.shape)
```

- **A.** (563, 2)
- **B.** 564
- ✅ **C. (564, 2)**
- **D.** (2, 564)
- **E.** 2

## Question 3 — Import et inspection

À quoi sert ce code ?

```python
display(brut.head())
```

- **A.** Afficher les cinq dernières lignes.
- **B.** Afficher cinq lignes aléatoires.
- ✅ **C. Afficher les cinq premières lignes.**
- **D.** Afficher les colonnes numériques uniquement.
- **E.** Afficher tous les doublons.

## Question 4 — Import et inspection

Que compte cette instruction ?

```python
brut.isna().sum()
```

- **A.** Les données égales à zéro.
- **B.** Les lignes uniques.
- **C.** Les valeurs négatives.
- **D.** Les écarts-types.
- ✅ **E. Les valeurs manquantes, colonne par colonne.**

## Question 5 — Nettoyage

Pourquoi remplacer un code sentinelle `-9999.0` ?

```python
df["anomalie"] = df["anomalie"].replace(-9999.0, np.nan)
```

- ✅ **A. Parce qu’il désigne une absence et fausserait les calculs.**
- **B.** Parce que toute anomalie négative est fausse.
- **C.** Pour changer les unités en kelvins.
- **D.** Pour créer une date.
- **E.** Pour transformer toutes les valeurs en zéro.

## Question 6 — Nettoyage

Que repère `duplicated()` sans argument ?

```python
df.duplicated().sum()
```

- **A.** Toutes les lignes avec NaN.
- ✅ **B. Les lignes identiques sur toutes les colonnes.**
- **C.** Uniquement les dates répétées.
- **D.** Les valeurs positives.
- **E.** Les mois absents de l’index.

## Question 7 — Nettoyage

Quel code cherche les dates présentes plusieurs fois ?

```python
df["date"].duplicated().sum()
```

- **A.** La différence entre dates.
- ✅ **B. La répétition des valeurs de la colonne date.**
- **C.** Les doublons de toutes les colonnes.
- **D.** Le nombre d’années.
- **E.** Les mois avec température négative.

## Question 8 — Nettoyage

Que fait `pd.to_datetime` ?

```python
df["date"] = pd.to_datetime(df["date"])
```

- **A.** Supprimer les dates futures.
- ✅ **B. Convertir la colonne en dates reconnues par Pandas.**
- **C.** Trier automatiquement toutes les colonnes.
- **D.** Calculer une durée moyenne.
- **E.** Remplacer les NaN.

## Question 9 — Nettoyage

Pourquoi trier les dates avant une analyse mensuelle ?

```python
df = df.sort_values("date")
```

- ✅ **A. Pour respecter l’ordre chronologique des calculs.**
- **B.** Pour déplacer tous les NaN à zéro.
- **C.** Pour créer des données supplémentaires.
- **D.** Pour supprimer automatiquement les doublons.
- **E.** Pour calculer la corrélation.

## Question 10 — Index temporel

Que fait `set_index("date")` ?

```python
df = df.set_index("date")
```

- **A.** Créer une colonne de dates aléatoires.
- ✅ **B. Utiliser les dates comme index du DataFrame.**
- **C.** Remplacer les dates par la moyenne.
- **D.** Convertir la date en température.
- **E.** Effacer la date.

## Question 11 — Index temporel

À quoi sert `asfreq("MS")` ?

```python
mensuel = df.set_index("date").asfreq("MS")
```

- **A.** Supprimer tous les mois vides.
- **B.** Garder une mesure par seconde.
- **C.** Interpoler automatiquement chaque mois absent.
- **D.** Calculer une moyenne annuelle.
- ✅ **E. Créer une grille au début de chaque mois, avec NaN si un mois manque.**

## Question 12 — Index temporel

Quelle différence existe entre un mois absent et une mesure absente ?

```python
mensuel["mois_absent_source"] = ...
```

- **A.** Ils sont toujours identiques.
- **B.** Une mesure absente signifie El Niño.
- **C.** Un mois absent correspond à une année bissextile.
- **D.** Un mois absent vaut forcément 0 °C.
- ✅ **E. Un mois absent n’a pas de ligne source ; une mesure absente peut avoir une ligne sans valeur valide.**

## Question 13 — Index temporel

Que garde cet intervalle ?

```python
serie = mensuel.loc[debut_valide:fin_valide]
```

- ✅ **A. Tous les mois entre les limites, y compris les NaN intérieurs.**
- **B.** Uniquement les anomalies positives.
- **C.** Les mois postérieurs à la dernière mesure.
- **D.** Uniquement les deux dates extrêmes.
- **E.** Seulement les valeurs non manquantes.

## Question 14 — Index temporel

Dans la série validée NOAA du TP, combien de mois exploitables y a-t-il ?

```python
print(len(serie_analyse))
```

- **A.** 12
- **B.** 0
- **C.** 564
- **D.** 365
- ✅ **E. 535**

## Question 15 — Validation

Que vérifie cette assertion ?

```python
assert not serie_analyse["anomalie"].isna().any()
```

- **A.** Que toutes les valeurs sont différentes.
- **B.** Que toutes les anomalies sont positives.
- **C.** Que la moyenne vaut zéro.
- **D.** Que les dates sont triées.
- ✅ **E. Qu’aucune anomalie n’est manquante dans cette série.**

## Question 16 — Validation

Quel est l’effet de `.copy()` ?

```python
travail = brut.copy()
```

- **A.** Créer des données aléatoires.
- **B.** Remplacer les NaN par zéro.
- **C.** Télécharger le CSV.
- **D.** Trier les données.
- ✅ **E. Créer une copie indépendante pour travailler sans modifier l’objet d’origine.**

## Question 17 — Validation

Que teste cette instruction ?

```python
assert not df["date"].duplicated().any()
```

- **A.** Que df est vide.
- ✅ **B. Qu’aucune date n’apparaît deux fois.**
- **C.** Que chaque valeur est supérieure à zéro.
- **D.** Que chaque mois est observé.
- **E.** Que toutes les dates sont mensuelles.

## Question 18 — Variation

Quelle est la variation de mars si février vaut 0,4 et mars 0,9 ?

```python
variation = s.diff()
```

- **A.** 0 °C
- ✅ **B. +0,5 °C**
- **C.** 0,36 °C
- **D.** +1,3 °C
- **E.** −0,5 °C

## Question 19 — Variation

Que renvoie `.diff()` sur la première observation ?

```python
pd.Series([2, 5, 4]).diff()
```

- **A.** 3
- ✅ **B. NaN, car aucune valeur précédente n’est disponible.**
- **C.** 0
- **D.** False
- **E.** 2

## Question 20 — Variation

Une anomalie passe de −1,5 à −0,8 °C. Quel constat est correct ?

```python
variation = -0.8 - (-1.5)
```

- ✅ **A. La variation est +0,7 °C malgré une anomalie finale négative.**
- **B.** Les deux anomalies sont identiques.
- **C.** Le mois final correspond automatiquement à El Niño.
- **D.** La variation vaut −2,3 °C.
- **E.** La variation est −0,7 °C.

## Question 21 — Interprétation

Que représente une anomalie de +0,8 °C dans Niño 3.4 ?

```python
anomalie = 0.8
```

- **A.** Une erreur de capteur.
- ✅ **B. Une température de surface supérieure de 0,8 °C à la référence utilisée.**
- **C.** Une hausse de 0,8 °C depuis le mois dernier.
- **D.** La preuve d’un épisode El Niño officiel.
- **E.** Une eau mesurée à 0,8 °C.

## Question 22 — Interprétation

Un pic négatif sur la courbe des variations indique :

```python
serie_analyse["anomalie"].diff()
```

- **A.** Une forte augmentation de l’anomalie.
- **B.** Que la température de l’eau est nécessairement sous zéro.
- ✅ **C. Une baisse rapide de l’anomalie par rapport au mois précédent.**
- **D.** Que La Niña est officiellement déclarée.
- **E.** Une absence de données.

## Question 23 — Histogramme

Que signifie `bins=25` ?

```python
ax.hist(s.dropna(), bins=25)
```

- **A.** Supprimer 25 valeurs extrêmes.
- **B.** Afficher 25 mois seulement.
- **C.** Calculer 25 moyennes mobiles.
- ✅ **D. Découper les valeurs en 25 intervalles pour compter leur fréquence.**
- **E.** Tracer 25 courbes.

## Question 24 — Histogramme

Quel est l’axe horizontal d’un histogramme des anomalies ?

```python
ax.hist(s, bins=20)
```

- **A.** Le nom du fichier.
- **B.** Le numéro de ligne.
- **C.** Les années par ordre chronologique.
- ✅ **D. Les plages de valeurs d’anomalie en °C.**
- **E.** Le nombre de mois.

## Question 25 — Statistiques

Que calcule cette expression ?

```python
s.median()
```

- **A.** La moyenne arithmétique.
- ✅ **B. La valeur centrale de la distribution triée.**
- **C.** La variation mensuelle.
- **D.** L’étendue.
- **E.** Le dernier mois.

## Question 26 — Moyenne mobile

Quelle est la première moyenne d’une fenêtre [2,4,6] ?

```python
pd.Series([2, 4, 6, 8]).rolling(3).mean()
```

- **A.** 3
- **B.** 12
- **C.** NaN à la troisième position
- **D.** 6
- ✅ **E. 4**

## Question 27 — Moyenne mobile

Combien de fenêtres complètes de taille 3 dans 12 valeurs ?

```python
len(x) - 3 + 1
```

- **A.** 36
- **B.** 9
- **C.** 4
- ✅ **D. 10**
- **E.** 12

## Question 28 — Moyenne mobile

Combien de fenêtres de taille 4 dans 12 valeurs ?

```python
len(x) - 4 + 1
```

- **A.** 12
- **B.** 3
- **C.** 10
- **D.** 8
- ✅ **E. 9**

## Question 29 — Moyenne mobile

Pourquoi les deux premières valeurs sont-elles NaN ?

```python
pd.Series(x).rolling(window=3, min_periods=3).mean()
```

- **A.** La moyenne est négative.
- **B.** Les deux premières valeurs doivent être zéro.
- **C.** Pandas supprime deux mois.
- ✅ **D. Il manque encore trois observations pour former une fenêtre complète.**
- **E.** La série est forcément mal triée.

## Question 30 — Moyenne mobile

Quelle est la moyenne mobile à 3 termes à la position 4 (index 3) ?

```python
x = np.array([2, 4, 6, 8, 7])
```

- ✅ **A. 6**
- **B.** 5
- **C.** 7
- **D.** 4
- **E.** 8

## Question 31 — Moyenne mobile

Quel effet a une fenêtre de 12 mois comparée à 3 mois ?

```python
s.rolling(12).mean()
```

- **A.** La conservation de tous les pics identiques.
- **B.** La suppression des anomalies négatives.
- ✅ **C. Un lissage généralement plus fort, mais une réaction plus lente.**
- **D.** Une prédiction certaine des 12 mois futurs.
- **E.** Un lissage moins important.

## Question 32 — Moyenne mobile

À quoi sert `.dropna()` après `.rolling(3).mean()` ?

```python
m = pd.Series(x).rolling(3).mean().dropna()
```

- **A.** À créer un index mensuel.
- **B.** À calculer la variance.
- **C.** À remplir les trous par zéro.
- **D.** À classer les valeurs par taille.
- ✅ **E. À retirer les résultats manquants produits en début de série.**

## Question 33 — NumPy

Comment retirer les NaN d’un tableau NumPy numérique ?

```python
x = np.array([1., np.nan, 3.])
```

- **A.** np.zeros(x)
- **B.** x == np.nan
- ✅ **C. x[~np.isnan(x)]**
- **D.** x.dropna()
- **E.** x[np.isnan(x)]

## Question 34 — NumPy

Quel est le résultat de cette sélection ?

```python
x = np.array([2, 4, 6, 8]); print(x[1:3])
```

- ✅ **A. [4, 6]**
- **B.** [6, 8]
- **C.** [2, 4]
- **D.** [4, 6, 8]
- **E.** [2, 4, 6]

## Question 35 — NumPy

Que retourne cette instruction ?

```python
np.zeros(4)
```

- **A.** Une matrice identité 4×4.
- **B.** Un tableau de quatre NaN.
- **C.** Le nombre 4.
- ✅ **D. Un tableau de quatre zéros.**
- **E.** Un tableau sans élément.

## Question 36 — Matrices

Quelles dimensions a cette matrice ?

```python
A = np.array([[1, 2, 3], [4, 5, 6]])
```

- **A.** 3 lignes et 2 colonnes.
- **B.** 3 lignes et 3 colonnes.
- **C.** 6 lignes et 1 colonne.
- ✅ **D. 2 lignes et 3 colonnes.**
- **E.** 2 lignes et 2 colonnes.

## Question 37 — Matrices

Quelle valeur fournit l’indexation ?

```python
A = np.array([[1, 2, 3], [4, 5, 6]]); A[1, 2]
```

- **A.** 3
- **B.** 2
- **C.** 5
- **D.** 4
- ✅ **E. 6**

## Question 38 — Matrices

Que calcule `axis=0` ?

```python
A = np.array([[1, 3], [5, 7]]); A.mean(axis=0)
```

- ✅ **A. Les moyennes par colonne : [3, 5].**
- **B.** La moyenne globale : 4.
- **C.** Une matrice de zéros.
- **D.** Une somme égale à 16.
- **E.** Les moyennes par ligne : [2, 6].

## Question 39 — Matrices

Que calcule `axis=1` ?

```python
A = np.array([[1, 3], [5, 7]]); A.mean(axis=1)
```

- ✅ **A. Les moyennes par ligne : [2, 6].**
- **B.** Le produit matriciel.
- **C.** Les moyennes par colonne : [3, 5].
- **D.** Les valeurs diagonales.
- **E.** La moyenne globale : 4.

## Question 40 — Matrices

Que signifie `A.T` ?

```python
A = np.array([[1, 2, 3], [4, 5, 6]])
```

- ✅ **A. La transposée : les lignes deviennent des colonnes.**
- **B.** La somme des éléments.
- **C.** Le tri des lignes.
- **D.** L’inverse de la matrice.
- **E.** La suppression des valeurs manquantes.

## Question 41 — Matrices

Quelle condition faut-il pour calculer `A @ B` ?

```python
A.shape == (2, 3); B.shape == (3, 4)
```

- **A.** Elles doivent avoir les mêmes valeurs.
- ✅ **B. Le nombre de colonnes de A doit égaler le nombre de lignes de B.**
- **C.** Les matrices doivent être carrées.
- **D.** Elles doivent avoir le même nombre de lignes.
- **E.** Les deux matrices doivent être 2×2.

## Question 42 — Corrélation

Une corrélation de Pearson proche de +1 indique :

```python
r = 0.94
```

- **A.** Une erreur de calcul.
- ✅ **B. Une forte relation linéaire positive.**
- **C.** L’absence de relation linéaire.
- **D.** Une forte relation linéaire négative.
- **E.** La preuve que X cause Y.

## Question 43 — Corrélation

Une corrélation proche de −1 indique :

```python
r = -0.91
```

- ✅ **A. Une forte relation linéaire négative.**
- **B.** Une covariance forcément nulle.
- **C.** Une faible relation positive.
- **D.** Deux séries nécessairement égales.
- **E.** Une causalité démontrée.

## Question 44 — Corrélation

Que peut-on conclure de `r ≈ 0` ?

```python
r = 0.02
```

- **A.** La relation est parfaitement décroissante.
- **B.** Les variables sont identiques.
- **C.** Les variables sont forcément indépendantes.
- ✅ **D. Il existe peu ou pas de relation linéaire détectable.**
- **E.** Une variable cause l’autre.

## Question 45 — Corrélation

Quel code calcule la matrice de corrélation des colonnes numériques ?

```python
df[["anomalie", "variation", "moyenne_mobile_3"]]
```

- **A.** df.sort_values("date")
- **B.** df.shape
- **C.** df.head()
- ✅ **D. df[["anomalie", "variation", "moyenne_mobile_3"]].corr()**
- **E.** df.isna()

## Question 46 — Corrélation

Que trouve-t-on sur la diagonale d’une matrice de corrélation pour des variables non constantes ?

```python
df[["x", "y"]].corr()
```

- **A.** Des coefficients égaux à 0.
- **B.** Des coefficients égaux à −1.
- **C.** Les effectifs mensuels.
- ✅ **D. Des coefficients égaux à 1.**
- **E.** Les moyennes de chaque colonne.

## Question 47 — Corrélation

Quelle propriété possède une matrice de corrélation ?

```python
C = df[["x", "y", "z"]].corr()
```

- **A.** Elle est toujours triangulaire.
- **B.** Tous ses coefficients sont positifs.
- **C.** Elle ne comporte jamais de NaN.
- ✅ **D. Elle est symétrique : corr(X,Y) = corr(Y,X).**
- **E.** Toutes ses lignes ont une somme égale à 1.

## Question 48 — Corrélation

Quelle opération est réalisée par `np.corrcoef(x, y)[0,1]` ?

```python
np.corrcoef(x, y)[0, 1]
```

- **A.** Calculer la moyenne de x.
- **B.** Calculer leur produit scalaire brut.
- **C.** Calculer la différence entre x et y.
- **D.** Calculer la médiane commune.
- ✅ **E. Calculer le coefficient de corrélation de Pearson entre x et y.**

## Question 49 — Corrélation

Pourquoi corrélation ne signifie-t-elle pas causalité ?

```python
r = 0.85
```

- ✅ **A. Une relation statistique ne prouve pas que l’une des variables provoque l’autre.**
- **B.** Parce que r vaut toujours zéro.
- **C.** Parce que seule une matrice carrée peut prouver une cause.
- **D.** Parce que Pearson mesure une unité en °C.
- **E.** Parce que les deux variables sont identiques.

## Question 50 — Synthèse NOAA

Quelle conclusion est justifiée si la moyenne mobile reste élevée plusieurs mois ?

```python
s.rolling(3).mean()
```

- **A.** Il est certain qu’El Niño est officiellement déclaré.
- **B.** Tous les mois individuels sont identiques.
- **C.** L’anomalie du mois prochain est connue.
- **D.** La température réelle de la mer dépasse 0,5 °C.
- ✅ **E. La tendance récente des anomalies est durablement élevée sur les fenêtres observées, sans établir à elle seule un épisode officiel.**
