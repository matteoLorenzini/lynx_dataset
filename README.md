# Description

Dataset files for cultural-heritage places, archaeological stratigraphic units, catalogued objects, and biographical records of scholars. The repository contains source exports in CSV/XML format and RDF representations of selected entities and relationships.

These datasets document archaeological research promoted by the LYNX research unit at the IMT School for Advanced Studies Lucca.

## Repository structure

```text
.
├── raw_data/                          # source exports, by project
│   ├── Places_and_Sites/
│   │   ├── csv/                       # empty
│   │   └── xml/                       # places_and_sites.xml
│   ├── Sabaudia_Project/              # stratigraphic units (SAS 1)
│   │   ├── raw/
│   │   │   ├── csv/
│   │   │   └── xml/
│   │   ├── rdf/3M/                    # 3M RDF exports
│   │   └── samples/                   # RDF excerpts
│   └── Sperlonga_Project/
│       ├── raw/
│       │   ├── person/                # scholar biographies
│       │   │   ├── csv/
│       │   │   └── xml/
│       │   └── scheda_catalogo/       # catalogued objects
│       │       ├── csv/
│       │       └── xml/
│       └── samples/                   # empty
├── processed_data/                    # RDF outputs, by project and version
│   ├── Places_and_Sites/E53/{v1.1,v1.2}/
│   ├── Sabaudia_Project/A8_A2/v1.1/
│   └── Sperlonga_Project/
│       ├── E18/{v1.1,v1.2}/
│       └── E21/v1.1/
└── LICENSE
```

Files ending in `_sample.xml` (and `sample_us*.rdf`) are reduced excerpts of the corresponding full exports, intended for quick inspection and testing.

## Contents

### Places and sites

`raw_data/Places_and_Sites/xml/places_and_sites.xml` contains the geographic hierarchy used by the dataset. Each place entry includes:

- a place identifier and name;
- coordinates for the place;
- a site identifier and name;
- coordinates for the site.

The current records include Sabaudia / Villa di Domiziano and Sperlonga / Villa di Tiberio.

### SAB: stratigraphic units

The `raw_data/Sabaudia_Project/` files describe archaeological stratigraphic units from SAS 1 at the Villa di Domiziano site in Sabaudia.

The records include identifiers, excavation context, unit type, materials, physical characteristics, stratigraphic relationships, descriptions, interpretations, dating information, documentation references, and responsible personnel. `raw/csv/US_data_SAS1.csv` provides a tabular export, while `raw/xml/US_data_SAS1.xml` stores the same records as structured XML. `raw/xml/US_data_SAS1_relations.xml` contains the corresponding relationship data.

### SPE: catalogue records

The `raw_data/Sperlonga_Project/raw/scheda_catalogo/` files describe catalogued cultural-heritage objects, including marble fragments. Fields cover identifiers, classification, material, dimensions, preservation state, discovery and storage locations, chronology, descriptions, stylistic notes, related objects, analytical data, and photogrammetry.

`csv/Scheda_Catalogo_-_Scheda_Catalogo.csv` is the tabular export and `xml/Scheda_Catalogo_-_Scheda_Catalogo.xml` is its structured XML counterpart. `xml/Scheda_Catalogo_-_Scheda_Catalogo_relations.xml` contains links between catalogue records.

### Person: scholar biographies

The `raw_data/Sperlonga_Project/raw/person/` files describe the scholars connected to the research, currently Bernard Andreae. Each record has `Unique_ID`, `Name_Surname`, `Birth_place`, `Birth_date`, `Death_place`, `Death_date`, `Biography`, `Role`, and `Contribution` fields (biographical text is in English).

- `csv/Person.csv` and `xml/Person.xml`: tabular and XML exports of the same records.
- `xml/Person_entities.xml`: entities extracted from the biography, role, and contribution text (persons, places, organizations, roles with start/end years, events, and works). Each entity keeps a `Source` element with the originating row, field, and text excerpt. The per-type files `persons.xml`, `places.xml`, `organizations.xml`, `roles.xml`, `events.xml`, `works.xml`, and `types.xml` sit alongside it.
- `xml/Person_timeline.xml`, `xml/Person_entities_timeline.xml`, and `xml/Person_entities_timeline_timeline.xml`: timeline exports.
- `xml/Person_relations.xml`: relations between person records; currently empty.

### RDF exports

The RDF/XML exports use namespaces from CIDOC CRM and related extensions. They are split between two folders:

- `raw_data/Sabaudia_Project/rdf/3M/`: 3M exports of the stratigraphic units (`A2_3M.rdf`, `A2_relations_3M.rdf`).
- `raw_data/Sabaudia_Project/samples/`: `sample_us.rdf` and `sample_us_relation.rdf`, reduced excerpts of the stratigraphic-unit RDF.
- `processed_data/`: versioned RDF outputs, grouped by project and dataset. Each `vX.Y` folder is one generation of the output; newer versions sit next to older ones.

Versioned outputs:

- `processed_data/Places_and_Sites/E53/v1.1/E53_new.rdf` and `v1.2/` (`E53_new_with_places.rdf`, `E53_new_test_with_places.rdf`): cultural-heritage places and sites (`crm:E53_Place`), including names, coordinates, and place/site containment.
- `processed_data/Sabaudia_Project/A8_A2/v1.1/`: `A8_A2_new.rdf` and `a8_a2_relations_new.rdf`, stratigraphic units (`A2_Stratigraphic_Volume_Unit`, `A8_Stratigraphic_Unit`) and their relations.
- `processed_data/Sperlonga_Project/E18/v1.1/E18.rdf` and `v1.2/` (`E18_new.rdf`, `E18_relations.rdf`, `e18_immagini.rdf`): physical cultural-heritage objects (`crm:E18_Physical_Thing`), their relationships, and image documentation. `e18_immagini.rdf` links each object via `crm:P70i_is_documented_in` to `crm:E31_Document` resources that reference the image file names.
- `processed_data/Sperlonga_Project/E21/v1.1/`: `E21_new.rdf` and `E21_timeline_new.rdf`, person records (`crm:E21_Person`) and their appellations/timelines.

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