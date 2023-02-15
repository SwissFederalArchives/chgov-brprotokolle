# chgov-brprotokolle
The “Minutes of the Federal Council” page, includes 4 repositories.

- **[chgov-brprotokolle](https://github.com/SwissFederalArchives/chgov-brprotokolle)** :triangular_flag_on_post:
  - [chgov-brprotokolle-server](https://github.com/SwissFederalArchives/chgov-brprotokolle-server)
  - [chgov-brprotokolle-markdown](https://github.com/SwissFederalArchives/chgov-brprotokolle-markdown)
  - [chgov-brprotokolle-frontend](https://github.com/SwissFederalArchives/chgov-brprotokolle-frontend)
  - [chgov-brprotokolle-ocr](https://github.com/SwissFederalArchives/chgov-brprotokolle-ocr)

# Introduction

The “Minutes of the Federal Council (1848–1963)” page allows full-text searches of the handwritten minutes from 1848 to 1903 and the typewritten minutes up to 1963.

The site is comprised of the following features:

- Browsing handwritten and typewritten minutes of the Federal Council from 1848-1963 in a chronological manner
- Fulltext search all minutes including highlighted search results snippets
- Search options and filters include timespan restrictions and fuzzy search
- Fulltext search within a chosen minutes document
- Parallel display of the digitised original and the automatically read text

# Overview

The complete solution includes 4 code repositories.

The repository chgov-brprotokolle-server is the backend for the ingestion of minutes and the interface for SOLR search requests. The repository chgov-brprotokolle-frontend 
is the public facing site to browse and search the minutes. The repository chgov-brprotokolle-mirador-ocr-helper is plugin for the Mirador IIIF viewer that enables a parallel 
display of the digitised original and the automatically read text. The repository chgov-brprotokolle-markdown is a set of info and help pages in markdown format.

## Data access

Structural data as well as the content of the minutes of the Federal Council can be accessed in a strcutured format. That data is available as IIIF Collections and IIIF Manifests. That endpoint can be accessed by the public and can be crawled as needed to extract data.

### Endpoint

The following IIIF collection acts as a "root" collection [https://api.chgov.bar.admin.ch/manifests/root.json](https://api.chgov.bar.admin.ch/manifests/root.json)

This collection holds references to sub-collection for every year from 1848 to 1963 in the `items` object:

| Property | Description |
|---|---|
| `id` |The url of the resource. The top level collection holds its own url but every item object holds the url to the corresponding sub collection.|
| `type` |Type of the resource. Structural data has the type `Collection` documents have the type `Manifest`.|
|`label`|Label of the resource|
|`thumbnail`|Thumbnail image of the resource|
|`navDate`|Date of the resource. Used for sorting.|

### Structure

Below the root collection the annual collections are referenced. In an annual collection all monthly collections of that year are referenced. The monthly collections are the lowest collection level and reference the minutes manifests:

#### Minutes

| Property | Description |
|---|---|
|`id`|The url of the resource|
|`type`|The type of the resource. For minutes this is `Manifest`|
|`summary`|The title of the resource|
|`thumbnail`|Thumbnail image of the resource|
|`navDate`|Date of the resource. Used for sorting.|
|`metadata`|Object for metadata. Each element contains a localized `label` and `value`|
|`rendering`| Object for alternative representations of the given document. Each element contains a reference and a label. The following formats are provided: <br />PDF: Reference to a PDF on the „Amtsdruckschriften“ platform of the Swiss Federal Archives.<br />OCR: reference to an ocr text file<br />WebOZ: Reference to the detail page on the online access platform of the Swiss Federal Archives|
|`rendering/id`|Reference to an external file or exernal website|
|`rendering/label`|Label of that reference|
|`items`|Pages of the minutes document as `Canvas` objects|
|`items/id`|Reference to the IIIF image server info json|
|`items/items/body/id`|Reference to the page's full size image file|
|`items/items/body/type`|Resource type `Image`|
|`items/seeAlso/id`|Reference to the page's hocr file|

# Authors

- [Swiss Federal Archives](https://www.bar.admin.ch/)
- [Schweizerisches Sozialarchiv](https://www.sozialarchiv.ch/)
- [4eyes GmbH](https://www.4eyes.ch/)

# License

GNU Affero General Public License (AGPLv3), see [LICENSE](LICENSE)

# Contribute

This repository is a copy which is updated regularly - therefore contributions via pull requests are not possible. However, independent copies (forks) are possible under consideration of the The MIT license.

# Contact

- For general questions (and technical support), please contact the Swiss Federal Archives by e-mail at bundesarchiv@bar.admin.ch.
- Technical questions or problems concerning the source code can be posted here on GitHub via the "Issues" interface.
