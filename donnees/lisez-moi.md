# Données SIG — projet AVENIR RDC

Extrait public du formulaire SIG, arrêté au **29/10/2026**.

| Contenu | Nombre |
|---|---|
| Objets observés | 106 |
| Éléments localisés | 98 |
| Objets sans géométrie | 10 |
| Points GPS | 80 |
| Tronçons (geotrace) | 13 |
| Zones (geoshape) | 5 |
| Territoires | 6 — Kenge, Kikwit, Lukula, Masimanimba, Mbanza-Ngungu, Mushie |

## Fichiers

- `sig_objets.csv` — une ligne par élément localisé, séparateur `;`,
  encodage UTF-8 avec BOM (ouvrable directement dans Excel), colonne `wkt`.
- `sig_objets.geojson` — `Point`, `LineString` et `Polygon` en WGS 84
  (EPSG:4326), directement ouvrable dans QGIS, ArcGIS, umap ou Google Earth.

## Champs

- `fiche` — identifiant KoBo de la fiche
- `territoire` — territoire (PDE)
- `secteur` — secteur déclaré
- `localite` — localité déclarée
- `type_objet` — type d'objet observé (Q6)
- `type_precis` — type précis (Q7)
- `nom_objet` — nom de l'objet relevé
- `statut` — statut de l'objet
- `source` — source de l'information
- `methode_releve` — méthode de relevé (Q17)
- `date` — date d'observation
- `enqueteur` — code de l'enquêteur
- `geom_type` — Point / LineString / Polygon
- `lat` — latitude (points)
- `lon` — longitude (points)
- `precision_m` — précision GPS annoncée (m)
- `altitude_m` — altitude (m)
- `nb_sommets` — nombre de sommets
- `longueur_km` — longueur recalculée (tronçons)
- `surface_ha` — surface recalculée (zones)
- `wkt` — géométrie WKT (QGIS, PostGIS)

## Précautions de lecture

1. **Un enregistrement = un élément localisé**, pas une fiche : une fiche peut
   décrire un marché et les routes qui y mènent.
2. `lat` et `lon` ne sont remplis que pour les points ; pour un tronçon ou une
   zone, utiliser `wkt` ou le GeoJSON.
3. Les longueurs et surfaces sont **recalculées sur les sommets GPS** ; les
   valeurs saisies dans le formulaire ne sont pas publiées (elles divergent
   fortement de la trace).
4. Au-delà de 20 m, une position est approximative.
5. Une coordonnée vide n'est pas un zéro : l'objet n'a pas de géométrie.

## Ce qui n'est pas publié

Les observations libres des enquêteurs, les identifiants internes des objets et
les noms de fichiers photos sont exclus de cet extrait : un texte libre peut
contenir des noms ou des numéros de téléphone. Les données du questionnaire
MPME (entreprises) ne sont pas publiées ; seuls des agrégats par secteur
figurent dans le tableau de bord.

## Reproduire l'extrait

```
cd CODEX-BECON-2026/Tools/kobo
python publier_donnees_sig.py
```
