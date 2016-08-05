Serials creation via batch loading from Excel:
==============================================

In this document we use the generic word `serial` to define `collection` and `periodical` work types in Kappa.

All the metadata necessary to create the serial pyramid is given by the supplier in an excel file made of three tabs, each one corresponding to one catalogue type (`book series`, `periodical`, `journal`).

The three types are:

|    TAB              | WORK TYPE IN KAPPA | CATALOGUE TYPE        |
|---------------------|--------------------|-----------------------|
|    Book series      |    Collection      |    Book series        |
|    Periodicals      |    Periodical      |    Book periodical    |
|    Journal          |    Periodical      |    Journal            |



Each line of the excel file contains the  metadata of one serial in one language, i.e. each line corresponds to one expression of the serial.

#### Master Language

For OECD publications the convention is to use metadata in English to create the work.
Some UN publications do not exist in English, so we need to introduce the concept of `Master Language` (=language of the metadata which generates the work).

*Cataloguing guideline* : Whenever English exists, it is the `Master Language`

#### Rules on how to identify Work, Expression and Manifestation

1. The metadata of the master language version is used for the creation of the work. We identify the master version of the publication because the column `is translation of` is empty. Therefore:
 - if a line does not have `is translation of`, it will generate the work, expression and manifestation.
 - Otherwise the line will generate an expression (+ manifestation).

2. If the master version is multilingual, then the title chosen for the work is the title in the first language declared.

3. The link between expressions of the same work is made in the column `Is translation of` through the ISSN of the `master language`.

4. The link between manifestations of the same expression is made in the column `other media` through the ISSN of PDF version in the `master language`.


Metadata Mapping
----------------

#### Work

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

#### Expression


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
|    Abstract            |    N      |    Master Marketing blurb 1               |    Each abstract should be associated with its language attribute      |
|    Issnl               |    Y      |    ISSN-L                                   |    Copy value of ISSN by default                                       |

#### Manifestation

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
