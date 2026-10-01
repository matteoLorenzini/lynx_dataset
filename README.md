# Description

Dataset files for cultural-heritage places, archaeological stratigraphic units, and catalogued objects. The repository contains source exports in CSV/XML format and RDF representations of selected entities and relationships.

These datasets document archaeological research promoted by the LYNX research unit at the IMT School for Advanced Studies Lucca.

## Repository structure

```text
.
├── raw_data/
│   ├── Places_and_sites/
│   │   └── places_and_sites.xml
│   ├── SAB/
│   │   └── Schede-US/
│   │       ├── US_data_SAS1.csv
│   │       ├── US_data_SAS1.xml
│   │       └── US_data_SAS1_relations.xml
│   └── SPE/
│       └── Scheda-Catalogo/
│           ├── Scheda_Catalogo_-_Scheda_Catalogo.csv
│           ├── Scheda_Catalogo_-_Scheda_Catalogo.xml
│           └── Scheda_Catalogo_-_Scheda_Catalogo_relations.xml
├── RDF/
│   ├── E18.rdf
│   ├── E18_relations.rdf
│   └── E53.rdf
└── LICENSE
```

## Contents

### Places and sites

`raw_data/Places_and_sites/places_and_sites.xml` contains the geographic hierarchy used by the dataset. Each place entry includes:

- a place identifier and name;
- coordinates for the place;
- a site identifier and name;
- coordinates for the site.

The current records include Sabaudia / Villa di Domiziano and Sperlonga / Villa di Tiberio.

### SAB: stratigraphic units

The `raw_data/SAB/Schede-US/` files describe archaeological stratigraphic units from SAS 1 at the Villa di Domiziano site in Sabaudia.

The records include identifiers, excavation context, unit type, materials, physical characteristics, stratigraphic relationships, descriptions, interpretations, dating information, documentation references, and responsible personnel. `US_data_SAS1.csv` provides a tabular export, while `US_data_SAS1.xml` stores the same records as structured XML. The relations XML file contains the corresponding relationship data.

### SPE: catalogue records

The `raw_data/SPE/Scheda-Catalogo/` files describe catalogued cultural-heritage objects, including marble fragments. Fields cover identifiers, classification, material, dimensions, preservation state, discovery and storage locations, chronology, descriptions, stylistic notes, related objects, analytical data, and photogrammetry.

`Scheda_Catalogo_-_Scheda_Catalogo.csv` is the tabular export and `Scheda_Catalogo_-_Scheda_Catalogo.xml` is its structured XML counterpart. The relations XML file contains links between catalogue records.

### RDF exports

The `RDF/` directory contains RDF/XML exports using namespaces from CIDOC CRM and related extensions:

- `E18.rdf`: descriptions of physical cultural-heritage objects, including identifiers, types, materials, dimensions, locations, dates, and other object properties.
- `E18_relations.rdf`: relationships between physical objects, such as equivalence or composition links.
- `E53.rdf`: descriptions of cultural-heritage places and sites, including names, coordinates, and place/site containment.

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