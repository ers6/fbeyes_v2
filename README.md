# About this READ_ME 

- **About F. B. Eyes** offers a brief project history
- **Customized Collection Builder Elements** documents scripts and pages that have been customized from the CollectionBuilder github package
- **Updating F. B. Eyes** documents the workflow for adding a new person/institution to the digital archive. 
# About F. B. Eyes
 The F.B. Eyes Digital Archive is a digital collection of essays and FBI files about surveilled Black authors and institutions amassed by Professor William Maxwell for his 2015 monograph,  *F. B. Eyes: How J. Edgar Hoover’s Ghostreaders Framed African American Literature*. Professor Maxwell built the first version of this project using Omeka Classic. In 2024, University Library staff migrated the collection to a static site generated using Collection Builder. Collection Builder is a set of static webpage templates and workflows for librarians to build digital collections and exhibits using the static site generator, Jekyll. *F. B. Eyes* is built on top of CollectionBuilder's compound object template and incorporates a few custom elements including: 
 - a customized metadata schema
 - archive_reader.html: a template for an internet archive reader object
 - fbeyes-compound-item-modal-gallery.html 
 - customized homepage elements:
	 - list-people.html 
	 - book-cover.html
For more information on how to use CollectionBuilder, visit their [documentation](https://collectionbuilder.github.io/cb-docs/). 

# Customized CollectionBuilder Elements
## Metadata Schema
The `fbeyes-cb-metadata.csv` file is the metadata file for this repository from which the CollectionBuilder scripts generate all of the object pages. It is based on the compound object CollectionBuilder [template](https://collectionbuilder.github.io/cb-docs/docs/metadata/compound-objects/).
Each record in the collection is composed of 2 rows of the csv file. The first row is the parent object row. Each parent object is a Black author or literary institution. The row following each parent object, the child object, is the FBI file for that person or institution. 

### Fields
- objectid: a unique identifier. Every row has a unique identifier. 
- parentid: the objectid associated with a child object's parent object. Only children objects have a parentid. 
- identifier: the Internet Archive unique identifier for an object. Only children objects have an entry in the identifier field because parent objects do not have IA files (FBI files) sorted with them.
- title: the title of the object. For parent objects, enter the name of the person or institution. For children objects, enter the title of their FBI file. For example, for Richard Wright, enter "Richard Wright" as the title of the parent object and "Wright, Richard" as the child object.
- last_name: The last name of the person or name of the institution. Only parent objects have last names. Note that this is how the list of people/institutions included in the archive (list_people.html) is alphabetized. The last_name field is otherwise invisible. For example, if you want *The Black Scholar* to follow *Black Arts Repertory Theater/School* enter "Black Scholar" in the last_name field. 
- creator: dc:creator. the creator of the object. Only enter for children objects. This will always be the Federal Bureau of Investigations
- date: the range of dates during which the FBI surveilled the person or institution given in the YYYY-YYYY format. Only enter for children objects.
- description: description of the person or file. For parent objects, this is the essay describing the person or institution written by Professor Maxwell. For children objects, this reads "FBI documents describe [enter name]"
- publisher: dc:publisher. The entity responsible for making the resource (in this case the FBI file) available to the public. Only enter for children objects. Will always be "FBI."
- type: dc:type. Enter text for children objects. Leave blank for parent objects.
- format: dc:format. Enter application/pdf for children objects. Leave blank for parent objects.
- language: Language of the resource. Enter "eng" for children objects. Leave blank for parent objects.
- rights: dc:rights. Enter "Public Domain" for children objects because all FOIA requested documents are made available under the public domain. Leave blank for parent objects.
- rightsstatement: Apply a public domain creative commons license statement for children objects. Leave blank for parent objects.
- display_template: How CollectionBuilder should render the information entered in this row of the csv file. For parent objects, enter compound_object. For children objects, enter archive_reader.
- object_location: The location of any media associated with the object. For parent objects, enter the file name with the full directory path of the image of the person or institution. For children objects, enter the permalink to the Internet Archive object. 
- image_small: Location of a smaller image derived from the larger image made in the website build process. The path of this image for parent objects will always be `/objects/small/[objectid]_sm.jpg`. For children objects, use this path to create a small icon of an FBI file `/assets/img/fbi_file_icon.png`
- image_thumb: Location of thumbnail images derived from the larger image associated with an object made during the website build process. For the parent object, this path will always be `/objects/thumbs/[objectid]_th.jpg`. For children objects, use this path to create a small icon of an FBI file `/assets/img/fbi_file_icon.png`
- image_alt_text: alt text for an image. Use only for parent object images because children object images are only shown as icons.
- start_date: first date of entry in the FBI file on the person or institution given in the YYYY format. Enter for children objects, and leave blank for parent objects.
- end_date: last date of entry in the FBI file on the person or institution given in the YYYY format. Enter for children objects, and leave blank for parent objects.
### Example: 
See an example of Richard Wright's parent object and child object rows. Note that Wright's FBI file is a child object, and Wright the person serves as the parent object.

| objectid   | parentid   | identifier              | title           | last_name | creator | date      | description                      | publisher | type | format          | language | rights        | rightsstatement                                                                                          | display_template | object_location                                                                                            | image_small                      | image_thumb                       | image_alt_text | start_date | end_date |
| ---------- | ---------- | ----------------------- | --------------- | --------- | ------- | --------- | -------------------------------- | --------- | ---- | --------------- | -------- | ------------- | -------------------------------------------------------------------------------------------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------- | -------------------------------- | --------------------------------- | -------------- | ---------- | -------- |
| fbeyes_000 |            |                         | Richard Wright  | Wright    |         |           | Essay about Wright goes here     |           |      |                 |          |               |                                                                                                          | compound_object  | /objects/fbeyes_000.jpeg                                                                                   | /objects/small/fbeyes_000_sm.jpg | /objects/thumbs/fbeyes_000_th.jpg | enter alt text |            |          |
| fbeyes_001 | fbeyes_000 | fbeyeswrightrichard8116 | Wright, Richard |           | FBI     | 1942-1963 | FBI documents surveilling Wright | FBI       | Text | application/pdf | eng      | Public Domain | [https://creativecommons.org/publicdomain/mark/1.0/](https://creativecommons.org/publicdomain/mark/1.0/) | archive_reader   | [https://archive.org/details/fbeyeswrightrichard8116](https://archive.org/details/fbeyeswrightrichard8116) | /assets/img/fbi_file_icon.png    | /assets/img/fbi_file_icon.png     |                | 1942       | 1963     |


## Archive Reader
CollectionBuilder comes with a number of display_templates for different types of media, but it does not currently have a way to embed an object from Internet Archive. The archive_reader.html is a display template for embedding books from Internet Archive into a collection builder project. 

The archive_reader.html display template isolates the Internet Archive id for an object using the `object_location` field. Next, it places that identifier inside an Internet Archive book reader iframe. If this is not working, make sure that you have entered the `object_location` correctly in your metadata file. 

## Home Page Elements

The homepage of FBEyes has a 2 custom elements not built in with CollectionBuilder: a vertical navigation bar listing all the people/institutions included in the archive (list-people.html) and an image of the book's cover (book-cover.html). Other built in elements have been customized. 

### Custom Built Elements
#### list-people.html 
The list of people's/institution's names on the right side of the homepage is generated from the list-people.html file. 
This file contains a javascript function that iterates over all of the parent objects in the metadata file and sorts them based on the `last_name` field. For each parent object, the script creates a button using the `title` metadata field as the text and the `objectid` field to create the link to the item page. 
#### book-cover.html
This html file creates the book cover on the front page of the website and links out the World Cat page for the monograph. 
### Customized Elements
In addition to building the above two elements, I've customized the theme for the website (see `_custom_css.scss`) and added all of the parent objects to the carousel function (`carousel.html`). Text for some items has also been changed from document-centered language, i.e. "view record", to person-centered language, "View" because this is a collection structured around people, not documents/files.  

# Updating the archive

New files to the F. B. Eyes Digital archive must be added in 2 major steps: first upload the files to internet archive and then add them to the website.
## Internet Archive Workflow
When you have a new FBI file on a person or institution, contact the University Libraries to ask them to add it to the [F.B. Eyes collection](https://archive.org/details/FBEyes) in Internet Archive. You will need to supply them with the following: 
- the FBI file(s) on the person(s) saved as a .pdf document. 
- a [record creation csv file](https://github.com/ers6/fbeyes_v2/blob/d16248be2abdeac9d60a99387e51d5aac6570f80/ia_workflow/record-creation-template.csv) 
- a [metadata csv file](https://github.com/ers6/fbeyes_v2/blob/d16248be2abdeac9d60a99387e51d5aac6570f80/ia_workflow/IA-metadata-sheet-template.csv) 
If the library is unable to add the files to IA for you, you will need to create your own Internet Archive account and download the Internet Archive [python library](https://archive.org/developers/internetarchive/). Then, follow the [bulk upload instructions](https://github.com/ers6/fbeyes_v2/blob/ba5d8fefcacdaa395f7bf02817a40e0557ac4ecb/ia_workflow/bulk_upload_workflow.md) from the IA workflow directory in this repository. 

## Adding new content to the website
1. Follow the [installation instructions](https://collectionbuilder.github.io/cb-docs/docs/software/) to download and configure the software your need to run Collection Builder CSV. 
2. Next, download/clone the F. B. Eyes Digital Archive repository to your desktop. 
3. Locate the `fbeyes-cb-metadata.csv` file in the `/data/` directory of the repository. Open the file in your preferred text editor, and add 2 new rows for each new entry to the archive. Refer to the Metadata Schema section of this documentation for guidance on using the fields appropriately. Save the file.
4. Select an image to represent the person(s) or institution(s) you're adding to the archive. Save that image in the `/objects/` directory of the repository, and ensure that its title is identical to the corresponding parent object's `objectid` in the metadata csv file. 
5. Run the [build process](https://collectionbuilder.github.io/cb-docs/docs/deploy/build/) outlined in the CollectionBuilder docs to rebuild and redeploy the website.
