# TP El Niño — NOAA Niño 3.4 (Nexa Digital School)

Diagnostic, nettoyage et préparation de la série mensuelle des anomalies de température Niño 3.4.

| Fichier | Contenu |
|---|---|
| `tp_noaa.ipynb` | Notebook exécuté : diagnostics, nettoyage, graphiques, assertions, réponses aux questions et conclusion |
| `noaa_nino34_propre.csv` | Données nettoyées : `date`, `anomalie`, `variation`, `moyenne_mobile_3`, `interpole` |
| `data/extrait_noaa_1997_1999.csv` | Extrait NOAA fourni (1997-01 → 1999-12), utilisé si l'URL officielle est inaccessible |

Exécution : `pip install numpy pandas matplotlib jupyter` puis `jupyter nbconvert --to notebook --execute tp_noaa.ipynb`
(ou ouvrir le notebook et « Run All »). Le notebook lit d'abord `https://psl.noaa.gov/data/correlation/nina34.anom.csv`.
