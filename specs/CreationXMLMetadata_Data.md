Loading process for databases, dataset groups and datasets via XML metadata
============================================================================

Introduction and Use Cases
------------------------------------------------

The schema contains all the necessary metadata to create a database and its components (Dataset Group and/ Or Datasets)

**Warning:** Handling the updates with reloading is not possible.
 If you wish to update metadata, you need to do it through the edit button in the interface

The Use cases are the following:
1. Creation of the whole structure Database/Dataset Group/Dataset:
this is the batch creation of a database with all of its components dataset groups and Datasets (editions and updating)

2. Add datasets to an existing database: we propose for this use case to reload the whole XML containing the structure,
or to add them manually via the interface.


XML loading model and mapping to OECD Kappa XML
------------------------------------------------

The structure of the loading schema is the following:
- first the database (with all the work related elements)
- then, grouped by <version> the different expressions to create, containing themselves the children structure (datasetgroup & dataset) for the current language.

This is very close to the FRBR final structure and the mapping to Kappa XML elements is evident.


### Databases

| Loading Schema metadata | Level |  card  | Kappa XML metadata   | Exemples                                  |
|-------------------------|-------|--------|----------------------|-------------------------------------------|
| igo                     | W     | 1      | igo                  | igo:oecd  igo:ncm                         |
| theme                   | W     | 1-n    | mainTheme,otherTheme | theme:30 (OECD) or theme:disarmament (UN) |
| author                  | W     | 1      | author               | person:1688 or organization:9612          |
| editor                  | W     | 0-1    | editor               | person:1688                               |
| country                 | W     | 0-n    | country              | country:aus                               |
| region                  | W     | 0-n    | region               | region:africa                             |
| imprint                 | W     | 0-1    | imprint              | imprint:9                                 |
| directorate             | W     | 0-1    | directorate          | directorate:env                           |
| webtopic                | W     | 0-n    | webtopic             | webtopic:agriculture                      |
| timeRange               | W     | 0-1    | timeRange            | 2016 ****                                 |
| OECD.statBanner         | W     | 0-1    | OECD.statBanner      | banner-oil.jpg                            |
| version                 |       |        | Expression wrapper   |                                           |
| language                | E     | 1-n    | language             | language:de                               |
| title                   | E     | 1-n    | title                |                                           |
| subtitle                | E     | 0-1    | subtitle             |                                           |
| shortTitle              | E     | 0-1    | shortTitle           |                                           |
| doi                     | E     | 0-1    | doi                  | Full DOI URL                              |
| abstract                | E     | 0-n    | abstract             |                                           |
| keyword                 | E     | 0-n    | keyword              |                                           |
| format                  |       |        | Manifestation wrapper|                                           |
| medium                  | M     | 1      | medium               | medium:x                                  |
| publisher               | M     | 0-1    | publisher            | organization:9612                         |
| issn                    | M     | 1      | issn                 | 20798342                                  |
| publicationDate         | M     | 0-1    | publicationDate      | 12-05-2016                                |
| onlineUrl               | M     | 0-1    | onlineUrl            |                                           |
| filename                | M     | 0-1    | filename             |                                           ||                                 

**** WARNING: timeRange will soon be modified into two fields (Start and End)

### Dataset Groups


| Loading Schema metadata | Level | card  | Kappa XML metadata   | Comments/ Exemples                        |
|-------------------------|-------|-------|----------------------|-------------------------------------------|
| parentWork              | W     | 0-1   | WorkId of parent     | exemple work:g1g1054c                     |
| theme                   | W     | 0-1   | mainTheme,otherTheme | theme:30 (OECD) or theme:disarmament (UN) |
| author                  | W     | 1     | author               | person:1688 or organization:9612          |
| editor                  | W     | 0-1   | editor               | person:1688                               |
| country                 | W     | 0-n   | country              | country:aus                               |
| region                  | W     | 0-n   | region               | region:africa                             |
| imprint                 | W     | 0-1   | imprint              | imprint:9                                 |
| directorate             | W     | 0-1   | directorate          | directorate:env                           |
| webtopic                | W     | 0-n   | webtopic             | webtopic:agriculture                      |
| timeRange               | W     | 0-1   | timeRange            | 2016 ****                                 |
| version                 |       |       | Expression wrapper   |                                           |
| language                | E     | 1-n   | language             |language:de                                |
| title                   | E     | 1-n   | title                |                                           |
| subtitle                | E     | 0-1   | subtitle             |                                           |
| shortTitle              | E     | 0-1   | shortTitle           |                                           |
| doi                     | E     | 0-1   | doi                  | Full DOI URL                              |
| abstract                | E     | 0-n   | abstract             |                                           |
| keyword                 | E     | 0-n   | keyword              |                                           ||

**** WARNING: timeRange will soon be modified into two fields (Start and End)


### Datasets


| Loading Schema metadata | Level | card | Kappa XML metadata   | Comments/ Exemples                        |
|-------------------------|-------|------|----------------------|-------------------------------------------|
| parentWork              | W     | 0-1  | WorkId of parent     | exemple work:g1g1054c                     |
| theme                   | W     | 0-1  | mainTheme,otherTheme | theme:30 (OECD) or theme:disarmament (UN) |
| author                  | W     | 1    | author               | person:1688 or organization:9612          |
| editor                  | W     | 0-1  | editor               | person:1688                               |
| country                 | W     | 0-n  | country              | country:aus                               |
| region                  | W     | 0-n  | region               | region:africa                             |
| imprint                 | W     | 0-1  | imprint              | imprint:9                                 |
| directorate             | W     | 0-1  | directorate          | directorate:env                           |
| webtopic                | W     | 0-n  | webtopic             | webtopic:agriculture                      |
| timeRange               | W     | 0-1  | timeRange            | 2016 ****                                 |
| queryId                 | W     | 0-n  |                      |                                           |
| version                 |       |      | Expression wrapper   |                                           |
| language                | E     | 1-n  | language             |language:de                                |
| title                   | E     | 1-n  | title                |                                           |
| subtitle                | E     | 0-1  | subtitle             |                                           |
| shortTitle              | E     | 0-1  | shortTitle           |                                           |
| doi                     | E     | 0-1  | doi                  | Full DOI URL                              |
| abstract                | E     | 0-n  | abstract             |                                           |
| keyword                 | E     | 0-n  | keyword              |                                           |
| format                  |       |      | Manifestation wrapper|                                           |
| medium                  | M     | 1    | medium               | medium:x                                  |
| publisher               | M     | 0-1  | publisher            | organization:9612                         |
| publicationDate         | M     | 0-1  | publicationDate      | 12-05-2016                                |
| onlineUrl               | M     | 0-1  | onlineUrl            |                                           |
| filename                | M     | 0-1  | filename             |                                           ||                   

**** WARNING: timeRange will soon be modified into two fields (Start and End)

Metadata and Process Rules for Editors
------------------

1. This process is only for batch creating once and not for updating or adding datasets: the ideal way to proceed is to load a whole database with all of its children into the nightly, test that everything is correct and then load into Kappa Live. You can add datasets and sataset groups at a later stage, but only at the end of the list of children, you will not be able to modify the structure.
2. If a dataset or a dataset group is loaded alone (use case 2):
    - the parent database must exist
    - the Workid of the parent database has to be in the XML (element : parentWork,exemple work:g1g1054c)
3. The first theme in the XML will be the main theme in Kappa.
4. Elements referring to taxonomies have to be entered using the id of the taxonomy as shown in the exemples . We can deliver a file listing all the elements of the taxonomy to the external suppliers.
5. Title, subtitle and abstracts must exist in the language of the expression, but they can also exist in other languages (for example if metadata in German exist for an obect in English)
6. DOI should be entered only if it is already existing and active. A normal procedure to generate DOIs will be applied for those objects which are not loaded with a pre-existing DOI.
7. The dataset type= edition, updating or archive is an attribute of the element "dataset" and shoul be filled in the XML

NOTE: we need to add an attribute "isDefaultChild" to the schema. In the mean time it can be added via the Kappa interface


Loading Rules
------------------
1. All objects are loaded with status = published
2. The first theme in the XML will be the main theme in Kappa.
3. If a dataset or a dataset group is loaded on its own with the reference to its parent database, it will be appended at the end of the list of children of the database already present in Kappa.
4. At loading the XML will generate the whole pyramid for the three types of objects (WEM for database, WEM for datasets, WE for dataset groups)
5. The follwing links will be created "has data" from database to datasets ang from dataset Groups to datasets, "hasGrouping" from Database to dataset Groups
