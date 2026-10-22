# Comparatif des approches - projet fraude (TP04)

Documentation cloud consultee le 22/10/2026. F1 mesures sur le jeu de test (25 %, random_state=42).

| Approche | F1 test | Temps humain | Temps machine | Cout estime (source, date) | Explicabilite | Export / reversibilite |
|---|---|---|---|---|---|---|
| Logistique (ref.) | 0.7407 | ~5 min (script) | 0.09 s | 0 (poste local) | Maximale | Total |
| Manuel (TP2) | 0.8669 | ~1 h (essais au TP2) | 1.13 s (re-entrainement) | 0 (poste local) | Moyenne/Bonne | Total |
| FLAML 60 s | 0.8561 | ~10 min (script) | 60.2 s | 0 (poste local) | Moyenne/Basse | Total |
| Vertex AI AutoML | non mesure | ... | ... | ~21,25 $/heure de noeud (tabulaire), page Vertex AI pricing, 22/10/2026 | Bonne (Explainable AI) | A verifier dans la doc |
| SageMaker Autopilot | non mesure | ... | ... | Selon instances utilisees (exemple AWS : ~6,72 $/h d'entrainement), re:Post, 22/10/2026 | Bonne (rapport Clarify) | A verifier dans la doc |
| Azure Automated ML | non mesure | ... | ... | Calcul sous-jacent seulement, pas de surcout AutoML, 22/10/2026 | Bonne (Responsible AI) | Export ONNX possible |

## Resultats FLAML par budget

| Budget | F1 test | F1 validation | Duree (s) |
|---|---|---|---|
| 10 s | 0.8409 | 0.8262 | 10.1 |
| 30 s | 0.8582 | 0.8277 | 30.3 |
| 60 s | 0.8561 | 0.8317 | 60.2 |
| 120 s | 0.8473 | 0.8332 | 120.2 |

## Commentaire (5 lignes)

1. Logistique : la bonne reference de depart (F1 0.7407 en 0.09 s) et la plus facile a expliquer, utile en audit ou en secteur regule.
2. Reglage manuel : le meilleur F1 de mes mesures (0.8669), pour une equipe qui connait ses donnees, mais au prix de plus de temps humain.
3. FLAML : F1 0.8561 en 60 s sans effort, proche du manuel (-0.011), donc ideal pour obtenir vite un bon modele sans cout cloud.
4. Cloud manage : pertinent sans infrastructure ou avec de gros volumes et besoin de deploiement/monitoring, mais cout a l'usage et risque de verrouillage.
5. L'AutoML ne remplace pas la verification humaine : au bloc D, il a atteint F1 = 1.0 sur une colonne piegee, puis 0.0 en production.