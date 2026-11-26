# Description

Dataset files for cultural-heritage places, archaeological stratigraphic units, catalogued objects, and biographical records of scholars. The repository contains source exports in CSV/XML format and RDF representations of selected entities and relationships.

These datasets document archaeological research promoted by the LYNX research unit at the IMT School for Advanced Studies Lucca.

## Repository structure

```text
.
├── datasets/
│   ├── person/              # scholar biographies
│   │   ├── raw/             # source exports and entity extractions
│   │   ├── rdf/             # RDF exports (E21), 3M/ subfolder
│   │   └── samples/         # reduced excerpts
│   ├── places_and_sites/    # geographic hierarchy
│   │   ├── raw/
│   │   ├── rdf/             # RDF exports (E53), 3M/ subfolder
│   │   └── samples/
│   ├── sab/                 # stratigraphic units (SAS 1)
│   │   ├── raw/
│   │   ├── rdf/             # RDF exports (A2/A8), 3M/ subfolder
│   │   └── samples/
│   └── spe/                 # catalogued objects
│       ├── raw/
│       ├── rdf/             # RDF exports (E18), 3M/ subfolder
│       └── samples/
└── LICENSE
```

Files ending in `_sample.xml` are reduced excerpts of the corresponding full exports, intended for quick inspection and testing.

## Contents

### Places and sites

`datasets/places_and_sites/raw/places_and_sites.xml` contains the geographic hierarchy used by the dataset. Each place entry includes:

- a place identifier and name;
- coordinates for the place;
- a site identifier and name;
- coordinates for the site.

The current records include Sabaudia / Villa di Domiziano and Sperlonga / Villa di Tiberio.

### SAB: stratigraphic units

The `datasets/sab/` files describe archaeological stratigraphic units from SAS 1 at the Villa di Domiziano site in Sabaudia.

The records include identifiers, excavation context, unit type, materials, physical characteristics, stratigraphic relationships, descriptions, interpretations, dating information, documentation references, and responsible personnel. `US_data_SAS1.csv` provides a tabular export, while `US_data_SAS1.xml` stores the same records as structured XML. The relations XML file contains the corresponding relationship data.

### SPE: catalogue records

The `datasets/spe/` files describe catalogued cultural-heritage objects, including marble fragments. Fields cover identifiers, classification, material, dimensions, preservation state, discovery and storage locations, chronology, descriptions, stylistic notes, related objects, analytical data, and photogrammetry.

`Scheda_Catalogo_-_Scheda_Catalogo.csv` is the tabular export and `Scheda_Catalogo_-_Scheda_Catalogo.xml` is its structured XML counterpart. The relations XML file contains links between catalogue records.

### Person: scholar biographies

The `datasets/person/` files describe the scholars connected to the research, currently Bernard Andreae. Each record has `Unique_ID`, `Name_Surname`, `Birth_place`, `Birth_date`, `Death_place`, `Death_date`, `Biography`, `Role`, and `Contribution` fields (biographical text is in English).

- `Person.xlsx`: the original spreadsheet.
- `raw/XML/Person.csv` and `raw/XML/Person.xml`: tabular and XML exports of the same records.
- `raw/XML/Person_entities.xml`: entities extracted from the biography, role, and contribution text (persons, places, organizations, roles with start/end years, events, and works). Each entity keeps a `Source` element with the originating row, field, and text excerpt.
- `Person_entities.json`: the raw entity-extraction output, generated with a language model (`qwen2.5:7b`) and keyed by a hash of the source text. As automatically extracted data, it should be reviewed before being used as authoritative.
- `raw/XML/Person_relations.xml`: relations between person records; currently empty.

### RDF exports

Each dataset folder has an `rdf/` directory with RDF/XML exports using namespaces from CIDOC CRM and related extensions. Superseded variants (e.g. `*_new.rdf`) are kept alongside the current files, and `rdf/3M/` holds the 3M exports:

- `spe/rdf/E18.rdf`: descriptions of physical cultural-heritage objects, including identifiers, types, materials, dimensions, locations, dates, and other object properties.
- `spe/rdf/E18_relations.rdf`: relationships between physical objects, such as equivalence or composition links.
- `spe/rdf/e18_immagini.rdf`: image documentation for physical objects; each object is linked via `crm:P70i_is_documented_in` to `crm:E31_Document` resources that reference the image file names.
- `places_and_sites/rdf/E53.rdf`: descriptions of cultural-heritage places and sites, including names, coordinates, and place/site containment.
- `person/rdf/E21` and `person/rdf/E21_timeline`: person records (`crm:E21_Person`) and their appellations/timelines. These files have no extension in the source and are kept as-is.
- `sab/rdf/A8_A2_new.rdf` and `sab/rdf/a8_a2_relations_new.rdf`: stratigraphic units (`A2_Stratigraphic_Volume_Unit`, `A8_Stratigraphic_Unit`) and their relations.

The RDF resources use the `http://www.lynx.com/resource/` namespace. Object resources are identified by their catalogue identifiers, while place and site resources are identified by their place or site IDs.

## File formats

- **CSV**: comma-separated tabular exports with a header row. Some values contain commas, quotes, or empty fields and should be read with a CSV parser.
- **XML**: structured records and relation data. Record fields are represented as XML elements; fields with multiple values may occur as repeated `<value>` elements.
- **RDF/XML**: semantic representations of entities and relationships, using RDF/XML syntax and CIDOC CRM classes and properties.

## Identifiers and links

The source exports use several identifier types, including `Unique_ID`, `US_ID`, `Project_ID`, `Inventory_ID`, `place_id`, and `site_id`. Relations in the source and RDF files connect records through these identifiers. Empty fields and values such as `N/A` are preserved from the source data and should not automatically be treated as equivalent without checking the field context.

## Notes

- The dataset contains multilingual field names and values, with most descriptive content in Italian.
- Coordinate values are represented as latitude/longitude pairs in the source XML and RDF exports.
- The CSV and XML files should be treated as paired exports of the same source records; verify identifiers before joining them.