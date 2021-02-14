# douay-rheims-json

JSON representation of the Douay-Rheims Bible translation (originally taken from [Project Gutenberg](http://www.gutenberg.org/ebooks/8300)).

## Construction

These files were created by manipulating the Project Gutenberg [Plain Text Format](http://www.gutenberg.org/cache/epub/8300/pg8300.txt) with a number of regular expression find/replace operations and Perl scripts.

## Format

Each file contains a single JSON array. The schemas of the contained objects are as follows:

### books.json

* **booknumber**: number - book number identifying the book (i.e. a value from 1 to 73)
* **bookname**: string - book name as it appears at the start of the book
* **contentsname**: string - book name as it appears in the table of contents
* **shortname**: string - book name as it appears in each chapter name
* **bookdesc**: string (optional) - description at the start of book
* **chapters**: array[chapter]
    * chapter: object
        * **chapternumber**: number - chapter number identifying the chapter
        * **chaptername**: string - chapter name as it appears at the start of the chapter
        * **chapterdesc**: string (optional) - description at the start of book
        * **chapternotes**: array[string] (optional) - notes following the chapter description

### verses.json

* **booknumber**: number - book number identifying the book (i.e. a value from 1 to 73)
* **chapternumber**: number - chapter number identifying the chapter
* **versenumber**: number - verse number identifying the verse
* **text**: string - verse text
* **notes**: array[string] (optional) - notes following the verse text

## Use with MongoDB

These files can be used to populate MongoDB collections with the **mongoimport** tool. For example, to create a *books* collection and a *verses* collection in the *scripture* database:

`mongoimport --jsonArray --db=scripture --collection=books books.json`

`mongoimport --jsonArray --db=scripture --collection=verses verses.json`

## Typos, Errors, and Pull Requests

There were a number of typos and structural errors in the original Project Gutenberg text. To propose a change, please create a pull request with a brief description of the issue and some evidence supporting the correction (e.g. a link to a more accurate version).