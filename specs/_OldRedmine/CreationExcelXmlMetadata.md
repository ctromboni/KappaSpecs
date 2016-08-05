Excel and XML creation of records in Kappa V3
==============================================


Serials creation via batch loading from Excel:
----------------------------------------------

In this document we use the generic word "serial" to define `collection` and `periodical` work types in Kappa.

All the metadata necessary to create the serial pyramid is given by the supplier in an excel file made of three tabs, each one corresponding to one catalogue type (`book series`, `periodical`, `journal`).

The three types are:

|    TAB              | WORK TYPE IN KAPPA | CATALOGUE TYPE        |
|---------------------|--------------------|-----------------------|
|    Book series      |    Collection      |    Book series        |
|    Periodicals      |    Periodical      |    Book periodical    |
|    Journal          |    Periodical      |    Journal            |

#### Creation of the pyramid:

Each line of the excel file contains the  metadata of one serial in one language, i.e. each line corresponds to one expression of the serial.

**Master Language**

For OECD publications the convention is to use metadata in English to create the work.
Some UN publications do not exist in English, so we need to introduce the concept of `Master Language` (=language of the metadata which generates the work).

**_Cataloguing guideline_**: Whenever English exists, it is the master language

#### Rules on how to identify Work, Expression and Manifestation

**RULE N°1** : The metadata of the master language version is used for the creation of the work. We identify the master version of the publication because the column “is translation of” is empty. Therefore:
 - if a line does not have “is translation of”, it will generate the work, expression and manifestation.
 - Otherwise the line will generate an expression (+ manifestation).


 **RULE N°2** If the master version is multilingual, then the title chosen for the work is the title in the first language declared.

**RULE N°3**: The link between expressions of the same work is made in the column `Is translation of` through the ISSN of the `master language`.

**RULE N°4**: The link between manifestations of the same expression is made in the column `other media` through the ISSN of PDF version in the `master language`.
 
#### Mapping of work metadata
This table indicates how to map the columns in the Excel file to the work metadata fields in kappa and the default values to be applied.

|    Kappa   metadata    | Mandatory |    Excel   column                            |   Rules,   Default values and comments                                |
|------------------------|-----------|----------------------------------------------|-----------------------------------------------------------------------|
|    Author              |    Y      |    AuthorID 1, AuthorID 2… AuthorID n        |  ex. organization:5595                                                    |
|    otherTheme          |    N      |    IGO Main theme 2, … IGO   Main theme n    |                                                                       |
|    Country             |    N      |    Country                                   |                                                                       |
|    Igo                 |    Y      |    IGO                                       |  igo:itu                                                              |
|    Form                |    N      |    Nature of Information                     |                                                                       |
|    creationDate        |    Y      |    NA                                        |  Generated                                                            |
|    lastUpdate          |    N      |    NA                                        |  Generated                                                            |
|    mainTheme           |    Y      |    IGO Main theme 1                          |                                                                       |
|    objectType          |    Y      |    tab name                                  |  Depending on the TAB: Collection or periodical  see above            |
|    catalogueType       |    Y      |    tab name                                  |  Depending on the TAB: Book series, Periodical Books or Journals      |
|    Region              |    N      |    Region                                    |                                                                       |
|    Title               |    Y      |    Master Main Title 1                       |                                                                       |
|    Periodicity         |    Y      |    Periodicity                               |  For periodicals and journal only                                     |
|    issuesPerYear       |    Y      |    NA                                        |  Periodicals   – calculated from periodicity                          |

#### Mapping of expression metadata

This table indicates how to map the columns in the Excel file to the expression metadata fields in kappa.

|    Kappa   metadata    | Mandatory |    Excel   column                           |    Rules   and comments                                                |
|------------------------|-----------|---------------------------------------------|------------------------------------------------------------------------|
|    doiPrefix           |    N      |    first part of DOI column (until /)       |                                                                        |
|    doiSuffix           |    N      |    second part of DOI column (from /)       |                                                                        |
|    iLibraryUrl         |    Y      |    NA                                       |                                                                        |
|    Language            |    Y      |    Master Language 1  …   Language n        |    Can be multiple                                                     |
|    creationDate        |    Y      |    NA                                       |    generated                                                           |
|    lastUpdate          |    Y      |    NA                                       |    generated                                                           |
|    iLibraryAccessType  |    Y      |    NA                                       |    Under access control by default                                     |
|    Title               |    Y      |    Master Main Title 1 ...  Main Title n    |    Each title   should be associated with its language                 |
|    Abstract            |    N      |    "Master" Marketing blurb 1               |    Each abstract should be associated with its language attribute      |
|    Issnl               |    Y      |    ISSN-L                                   |    Copy value of ISSN by default                                       |

#### Mapping of manifestation metadata
This table indicates how to map the columns in the Excel file to the manifestation metadata fields in kappa.

|    Kappa   metadata    | Mandatory  |    Excel   column    |    Rules   and comments                                                                      |
|------------------------|------------|----------------------|----------------------------------------------------------------------------------------------|
|    Availability        |    Y       |    availability      |                                                                                              |
|    FileName            |    N       |    NA                |                                                                                              |
|    FileNameAlias       |    N       |    NA                |    generated                                                                                 |
|    creationDate        |    Y       |    NA                |    generated                                                                                 |
|    lastUpdate          |    Y       |    NA                |    generated                                                                                 |
|    Medium              |    Y       |    Medium            |                                                                                              |
|    Publisher           |    Y       |    NA                |    same organization as in the author field : ex.organization:5595                           |
|    Software            |    N       |    NA                |                                                                                              |
|    Issn                |    Y       |    ISSN              |                                                                                              |
|    isIssnl             |    N       |    NA                |    YES by default                                                                            |

Creation of books from XML :
----------------------------

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

**RULE N°1** : The metadata of the master version are used for the creation of the work. We identify the master version because the XML does not have the element “is translation of”. Therefore if a file does not have “is translation of”, then it will generate the work, expression and manifestation. Otherwise it will generate an expression (+ manifestation)

**RULE N°2**: The data in the master language If the master version is multilingual, then the first declared language is the master language

**RULE N°3**: The master version XML should either exist in the base before loading the translations, or be loaded in the same ticket as its translations.

**RULE N°4**: The link between expressions of the same work is with the property “Is translation of” through the “master language”ISBN.
The following content types are linked to a series/periodical and the link is made via the ISSN

| Work | Catalogue type  | Belongs to  | Link made through |
|------|-----------------|-------------|-------------------|
| Book | Series Book     | Book Series | ISSN              |
| Book | Periodical Book | Periodical  | ISSN              |
| Book | Journal Issue   | Journal     | ISSN              |

## Mapping of work metadata
This table indicates how to map the metadata in the XML file to the work metadata fields in kappa.

|    KV3 Metadata        |    Xml field              |    Rules and Comments                                                                                                    |
|------------------------|---------------------------|--------------------------------------------------------------------------------------------------------------------------|
|    Author              |    author                 |    The id of the persons and organizations is given in the   file enumeration.xsd                                        |
|    otherTheme          |    theme                  |    Themes from the second listed (first is main)                                                                         |
|    timeRange           |    timeRange              |                                                                                                                          |
|    Country             |    country                |                                                                                                                          |
|    Form                |    natureOfInformation    |                                                                                                                          |
|    Igo                 |    igo                    |    To distinguish publications from different IGOs, the Taxonomy today   contains : OECD, UN, Norden anc Commonwealth    |
|    creationDate        |                           |    Generated at creation                                                                                                 |
|    lastUpdate          |                           |    Generated                                                                                                             |
|    mainTheme           |    Theme                  |    The first theme in the list is the main                                                                               |
|    objectType          |    Root element           |    Catalogue type                                                                                                        |
|    region              |    Region                 |    Taxonomy regions (updated with also the list of UN   regions)                                                         |
|    subTitle            |    Subtitle               |                                                                                                                          |
|    title               |    Title                  |    Work title is always in EN                                                                                            |
|    editionStatement    |    editionStatement       |                                                                                                                          |
|    editionYear         |    editionYear            |                                                                                                                          |
|    Volume              |    Volume                 |                                                                                                                          |
|    Issue               |    issueNumber            |                                                                                                                          |
|    number              |    continuousNumber       |                                                                                                                          |

#### Mapping of expression metadata
This table indicates how to map the metadata in the XML file to the expression metadata fields in kappa.

|    KV3 Metadata       |    Xml field                          |    Rules and Comments                                                                             |
|-----------------------|---------------------------------------|---------------------------------------------------------------------------------------------------|
|    doiTitle           |                                       |    Contains   the title that was registered with the DOI agency                                   |
|    doiSubTitle        |                                       |    Contains the subtitle that was registered with the   DOI agency                                |
|    language           |                                       |    Taxonomy                                                                                       |
|    creationDate       |    Creation date                      |    Generated . Creation date of the record either in   KV3 or migrated from KV2. Used for PIM.    |
|    lastUpdate         |    Last update date then generated    |    Generated                                                                                      |
|    subTitle           |    Subtitle                           |                                                                                                   |
|    abstract           |    Abstract                           |    In every language of the expression (language attribute)                                       |
|    user               |                                       |    Generated                                                                                      |
|    coverImage         |    Cover                              |    Name of the image file (this is no longer needed)                                              |
|    tableOfContents    |    tableOfContent                     |    Rich text                                                                                      |
|                       |                                       |                                                                                                   |

#### Mapping of manifestation metadata

This table indicates how to map the columns in the Excel file to the manifestation metadata fields in kappa.

|    KV3 Metadata         |    Xml field          |    Rules and Comments                                 |
|-------------------------|-----------------------|-------------------------------------------------------|
|    Availability         |    Availability       |    Set to available                                   |
|    dateOfPublication    |    publicationDate    |                                                       |
|    Filename             |    Format/filename    |                                                       |
|    creationDate         |                       |    Generated                                          |
|    lastUpdate           |                       |    Generated                                          |
|    medium               |    fomat@type         |    Taxonomy                                           |
|    publisher            |    Publisher          |    Taxonomy : link to organization                    |
|    subTitle             |    Subtitle           |                                                       |
|    title                |    Title              |                                                       |
|    pageNumber           |    numberOfPages      |    Necessary? Can we calculated on the fly for PDF    |
|    onlineBookShopUrl    |    bookShopUrl        |                                                       |
|    user                 |                       |    Generated                                          |
|    isbn13               |    Isbn13             |                                                       |

Creation of components from XML
--------------------------------

#### Creation of chapters and articles



|    KV3 Metadata              |    Xml field               |    Level    |    Rules and Comments                                                                            |
|------------------------------|----------------------------|-------------|--------------------------------------------------------------------------------------------------|
|    Title                     |    Title                   |    W        |    In the first language of the master version                                                   |
|    Subtitle                  |    Subtitle                |    W        |    In the first language of the master version                                                   |
|    Form                      |    naturefInformation      |    W        |    Taxonmy Form                                                                                  |
|    componentContentType      |    componentContentType    |    W        |    componenttype                                                                                 |
|    Author                    |    Author                  |    W        |    RULE: In the absence of a chapter AuthorID, the   chapter should inherit the book AuthorID    |
|    Maintheme, otherThemes    |    Theme                   |    W        |    the chapter should inherit the book Themes                                                    |
|    Country                   |    Country                 |    W        |                                                                                                  |
|    Region                    |    Region                  |    W        |                                                                                                  |
|    Time Range                |    timeRange               |    W        |                                                                                                  |
|    Language                  |    language                |    E        |    List of languagesof the expression                                                            |
|    Abstract                  |    Abstract                |    E        |                                                                                                  |
|    Filename                  |    Filename                |    M        |                                                                                                  |
|    startPage                 |    startPage               |    M        |                                                                                                  |
|    endPage                   |    endPage                 |    M        |                                                                                                  |
|    publisherID               |    NA                      |    M        |    RULE: The chapter should inherit the book publisherID                                         |
|    publicationDate           |    NA                      |    M        |    RULE: The chapter should inherit the book publicationDate                                     |

#### Links:

**RULE1** : The link between two chapters expression of the same work will be done in the order of the xml.
This means that is a publication in EN has two chapters 1,2, and a French version is loaded, then chapter 1FR will be the French expression of chapter1, chapter 2FR will be the French expression of chapter2. It is up to the user to verify that this is actually true, because the application cannot determine it automatically.

**RULE2** : The link between two sections expression of the same work will be done in the order of the xml.
This means that is a publication in EN has two sections 1,2, and a French version is loaded, then section 1FR will be the French expression of section1, section 2FR will be the French expression of section2. It is up to the user to verify that this is actually true, because the application cannot determine it automatically.


|    KV3 Metadata    |    Xml field    |    Level    |    Rules and Comments                                                        |
|--------------------|-----------------|-------------|------------------------------------------------------------------------------|
|    Title           |    Title        |    W-E      |    The title in the language of the master version is   used in the work.    |
|    Language        |    Language     |    E   |                |


Controls to be done at loading for the creation of a book

![](specs/BookLoading.jpg)

![](specs/Standalone.jpg)

#### Controls to be done at loading for chapter creation

•	The number of chapters and sections needs to be the same in all language versions

•	The ordered sequence of sections/chapters must be the same in all language versions
If it not the same, then a message appears at loading and the object is not created
`the sequence of components needs to be identical in all language versions and it is not, please revise the table of contents comparing it to existing language version`

**RULE**: The order of chapters and sections will not be editable in kappa, to avoid creating discrepancies in the table of contents of a book. For the moment if a user wants to change the order of the chapters, then he/she will need to reload the XML in all the languages.

#### Reloading an xml for existing records
The metadata needed for export as DOI and DOI title is preserved.
All the other metadata and links at the three levels are erased and recreated

` WARNING: All metadata for this book and its components will be recreated, and FTIs erased. are you sure you want to proceed?`

The control on chapter/section number and sequence is run again. If the number/sequence does not correspond, then the loading stops

`The sequence of components needs to be identical in all language versions and it is not, please revise the table of contents comparing it to existing language version`
