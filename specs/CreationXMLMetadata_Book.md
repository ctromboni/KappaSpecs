Creation of book records from XML :
===================================


The batch metadata loading schema loding.xsd has been created to load UN catalogue, but it will be reused to load other IGOs metadata and to create metadata for OECD publications.
With the batch metadata schema, we can load the following types of Kappa Objects (the catalogue type is given by the root element of the XML).

| Element in XML      | Catalogue type       | Kappa SUBMODEL |
|---------------------|----------------------|----------------|
| standaloneMonograph | Standalone Monograph | 1306           |
| seriesBook          | Series Book          | 1305           |
| periodicalIssue     | Periodical book      | 1308           |
| journalIssue        | Journal Issue        | 1304           |

#### Creation of the pyramid :
The pyramid creation rules for books are very similar to those applied for serials in the excel batch loading.
Each XML file contains the necessary metadata to create one expression of the book and its corresponding manifestation.
It is necessary to understand which XML generates the work metadata and how to attach expressions to their work.

**Cataloguing guideline**: Whenever English metadata exists, it is the master language and will generate the work
Rules on how to identify Work, Expression and Manifestation

#### Rules on how to identify Work, Expression and Manifestation

1. The metadata of the master version are used for the creation of the work. We identify the master version because the XML does not have the element `is translation of`. Therefore if a file does not have `is translation of`, then it will generate the work, expression and manifestation. Otherwise it will generate an expression (+ manifestation)

2. The data in the master language If the master version is multilingual, then the first declared language is the master language

3. The master version XML should either exist in the base before loading the translations, or be loaded in the same ticket as its translations.

4. The link between expressions of the same work is with the property `Is translation of` through the `master language` ISBN.
The following content types are linked to a series/periodical and the link is made via the ISSN

| Work | Catalogue type  | Belongs to  | Link made through |
|------|-----------------|-------------|-------------------|
| Book | Series Book     | Book Series | ISSN              |
| Book | Periodical Book | Periodical  | ISSN              |
| Book | Journal Issue   | Journal     | ISSN              |

### Mapping of work metadata

This table indicates how to map the metadata in the XML file to the work metadata fields in kappa.

|    KV3 Metadata        |    Xml field              |    Rules and Comments                                                                          |
|------------------------|---------------------------|------------------------------------------------------------------------------------------------|
|    Author              |    author                 |    The id of the persons and organizations is given in the   file enumeration.xsd              |
|    otherTheme          |    theme                  |    Themes from the second listed (first is main)                                               |
|    timeRange           |    timeRange              |                                                                                                |
|    Country             |    country                |                                                                                                |
|    Form                |    natureOfInformation    |                                                                                                |
|    Igo                 |    igo                    |                                                                                                |
|    creationDate        |                           |    Generated at creation                                                                       |
|    lastUpdate          |                           |    Generated                                                                                   |
|    mainTheme           |    Theme                  |    The first theme in the list is the main                                                     |
|    objectType          |    Root element           |    Catalogue type                                                                              |
|    region              |    Region                 |    Taxonomy regions (updated with also the list of UN   regions)                               |
|    subTitle            |    Subtitle               |                                                                                                |
|    title               |    Title                  |    Work title is always in EN                                                                  |
|    editionStatement    |    editionStatement       |                                                                                                |
|    editionYear         |    editionYear            |                                                                                                |
|    Volume              |    Volume                 |                                                                                                |
|    Issue               |    issueNumber            |                                                                                                |
|    number              |    continuousNumber       |                                                                                                |

#### Mapping of expression metadata
This table indicates how to map the metadata in the XML file to the expression metadata fields in kappa.

|    KV3 Metadata       |    Xml field               |    Rules and Comments                                                                         |
|-----------------------|----------------------------|-----------------------------------------------------------------------------------------------|
|    doiTitle           |                            |    Contains   the title that was registered with the DOI agency                               |
|    doiSubTitle        |                            |    Contains the subtitle that was registered with the DOI agency                              |
|    language           |                            |    Taxonomy                                                                                   |
|    creationDate       |    Creation date           |    Generated . Creation date of the record either in   KV3 or migrated from KV2. Used for PIM |
|    lastUpdate         |                            |    Last update date then generated                                                            |
|    subTitle           |    Subtitle                |                                                                                               |
|    abstract           |    Abstract                |    In every language of the expression (language attribute)                                   |
|    user               |                            |    Generated                                                                                  |
|    coverImage         |    Cover                   |    Name of the image file (this is no longer needed)                                          |
|    tableOfContents    |    tableOfContent          |    Rich text                                                                                  |


#### Mapping of manifestation metadata

This table indicates how to map the columns in the Excel file to the manifestation metadata fields in kappa.

|    KV3 Metadata       |    Xml field              |    Rules and Comments                                 |
|-----------------------|---------------------------|-------------------------------------------------------|
|    Availability       |    Availability           |                                                       |
|    dateOfPublication  |    publicationDate        |                                                       |
|    Filename           |    Format/filename        |                                                       |
|    creationDate       |                           |    Generated                                          |
|    lastUpdate         |                           |    Generated                                          |
|    medium             |    fomat@type             |    Taxonomy                                           |
|    publisher          |    Publisher              |    Taxonomy : link to organization                    |
|    subTitle           |    Subtitle               |                                                       |
|    title              |    Title                  |                                                       |
|    pageNumber         |    numberOfPages          |                                                       |
|    onlineBookShopUrl  |    bookShopUrl            |                                                       |
|    user               |                           |    Generated                                          |
|    isbn13             |    Isbn13                 |                                                       |
