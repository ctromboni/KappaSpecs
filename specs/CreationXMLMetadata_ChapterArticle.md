Creation of chapters and articles records from XML Metadata
===========================================================

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
