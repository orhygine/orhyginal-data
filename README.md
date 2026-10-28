orhyginal-data
==============

Some JSON and GeoJSON hosted on github pages : 

http://orhygine.github.io/orhyginal-data/

Catalogue des liens (`osm-links.yaml`)
--------------------------------------

`osm-links.yaml` recense des liens vers des services cartographiques externes. Les URL
peuvent contenir des variables remplacées par la position de la carte au moment du clic.
Ce catalogue est exploité sur le site [map.orhyginal.fr](https://map.orhyginal.fr).

### Sections

Le fichier est un dictionnaire dont chaque clé est une liste d'entrées :

| Section     | Rôle                                                   |
|-------------|--------------------------------------------------------|
| `link`      | Liens principaux, classés par catégorie                |
| `edit`      | Éditeurs OpenStreetMap (JOSM, iD, …)                   |
| `check`     | Outils de contrôle qualité OSM (Osmose, notes, …)      |
| `reference` | Documentation OSM (wiki, Taginfo, …)                   |

### Champs d'une entrée

| Champ         | Requis | Description                                                  |
|---------------|--------------------|--------------------------------------------------------------|
| `label`       | oui                | Nom affiché                                                  |
| `url`         | oui                | URL, éventuellement avec variables (voir ci-dessous)         |
| `description` | oui                | Description courte, en français                              |
| `tags`        | oui                | Liste de mots-clés en minuscules (`fond-de-carte`, `osm`, …) |
| `checked`     | oui                | Date de dernière vérification du lien (`AAAA-MM-JJ`)         |
| `category`    | `link` uniquement  | Catégorie d'affichage (voir liste ci-dessous)                |
| `created`     | `link` uniquement  | Date d'ajout (`AAAA-MM-JJ`)                                  |
| `updated`     | `link` uniquement  | Date de dernière modification (`AAAA-MM-JJ`)                 |
| `favorite`    | non                | `true` pour mettre le lien en favori                         |
| `comment`     | non                | Note libre                                                   |

Exemple :

```yaml
link:
- label: CyclOSM
  url: https://www.cyclosm.org/#map={z}/{lat}/{lon}/cyclosm
  description: Carte vélo basée sur OpenStreetMap mettant en avant pistes cyclables, stationnements et services vélo.
  category: Cartes OSM
  favorite: true
  tags:
  - vélo
  - osm
  created: 2025-01-01
  updated: 2025-01-01
  checked: 2026-10-27
```

### Variables d'URL

| Variable                                       | Valeur                                                     |
|------------------------------------------------|------------------------------------------------------------|
| `{lat}`, `{lon}`                               | Centre de la carte (WGS84, degrés)                         |
| `{z}`                                          | Niveau de zoom (accepte un décalage, ex. `{z-9}`)          |
| `{xmin}`, `{ymin}`, `{xmax}`, `{ymax}`         | Emprise de la carte (WGS84)                                |
| `{x_3857}`, `{y_3857}`                         | Centre en Web Mercator (EPSG:3857)                         |
| `{xmin_3857}`, `{ymin_3857}`, `{xmax_3857}`, `{ymax_3857}` | Emprise en Web Mercator (EPSG:3857)            |
| `{x_23031}`, `{y_23031}`                       | Centre en ED50 / UTM 31N (EPSG:23031)                      |
| `{res}`                                        | Rayon / résolution de la vue                               |
| `{date}`, `{time}`                             | Date et heure courantes                                    |

### Catégories de la section `link`

Cartes OSM, Cartes 3D OSM, Cartes thématiques, Contribution OSM, Données OSM,
Géocodage OSM, Téléchargement OSM, Services cartographiques, Outils cartographiques,
Géoportails, Données géographiques, Références géographiques, Itinéraires, Transport,
Plein air, Ski et montagne, Météo, Soleil et astronomie, Espace, Photo et imagerie,
Webcams, Histoire et patrimoine, Art et visualisation, Jeux et découvertes, Communication.

### Automatisation

Chaque push sur `gh-pages` modifiant `osm-links.yaml` déclenche le workflow
[`trigger-favicon-dl.yml`](.github/workflows/trigger-favicon-dl.yml), qui demande au dépôt
`orhygine/orhyginal-map` de retélécharger les favicons des liens.
