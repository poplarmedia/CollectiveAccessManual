# detail.conf

The detail.conf configuration file defines all available detail views
for a theme. Details are, as their name implies, detailed metadata
displays for a specific item -- a *subject*. At a minimum, a detail will
be bound to a table. A detail may be designed to display data for one of
the following tables: objects, entities, occurrences, places, or
collections.

You may define any number of details. Each will have a unique code that
is used in Pawtucket URLs to reference the detail.

## Top-level settings

The primary top-level setting is *detailTypes*, a dictionary that
contains definitions for each detail. Other top-level settings control
download of media.

+---------------------------------------------------+-----------------------------------+-----------------------+-----------+-----------+------------------------------------------------+
| Setting                                           | Description                       | Allowed values        | Required? | Default   | Synonyms                                       |
+===================================================+===================================+=======================+===========+===========+================================================+
| detailTypes                                       | Dictionary of all detail pages    | Dictionary            | yes       | none      |                                                |
|                                                   | available in this theme.          |                       |           |           |                                                |
|                                                   | Dictionary keys are short, unique |                       |           |           |                                                |
|                                                   | codes for each available detail.  |                       |           |           |                                                |
|                                                   | Values are dictionaries of        |                       |           |           |                                                |
|                                                   | options for the detail, the       |                       |           |           |                                                |
|                                                   | format of which is defined below. |                       |           |           |                                                |
+---------------------------------------------------+-----------------------------------+-----------------------+-----------+-----------+------------------------------------------------+
| allowObjectRepresentationDownload                 | Controls whether download of      | anyone, logged_in,    | no        | never     | allow_ca_objects_representation_download       |
|                                                   | representations on object detail  | logged_in_privileged, |           |           |                                                |
|                                                   | pages are allowed, and to whom    | never                 |           |           |                                                |
|                                                   | they are available.               |                       |           |           |                                                |
+---------------------------------------------------+-----------------------------------+-----------------------+-----------+-----------+------------------------------------------------+
| restrictObjectRepresentationDownloadToObjectTypes | Controls which types of object    | A list of object      | no        | none -    | allow_ca_objects_representation_download_types |
|                                                   | records allow downloads when the  | types.                |           | all types |                                                |
|                                                   | policy set in                     |                       |           | allow     |                                                |
|                                                   | allowObjectRepresentationDownload | Ex. \[books, maps,    |           | downloads |                                                |
|                                                   | enables downloads.                | images\]              |           |           |                                                |
+---------------------------------------------------+-----------------------------------+-----------------------+-----------+-----------+------------------------------------------------+

## Settings for *detailTypes*

Keys in the *detailTypes* dictionary are used as unique detail codes.
Values control detail display and functionality.

  ------------------------------------------------------------------------------------------------------
  Setting           Description              Allowed values        Required?   Default        Synonyms
  ----------------- ------------------------ --------------------- ----------- -------------- ----------
  displayName       Name of detail for       Text                  Yes         None           
                    display to end users.                                                     

  table             Kind of record this      Ex. ca_objects,       Yes         None           
                    detail displays.         ca_entities,                                     
                                             ca_collections, Etc.                             

  restrictToTypes   List of types to limit   Any valid type code   No          \[\] (no type  
                    use of this detail to.   for the detail\'s                 restriction)   
                    Use type codes defined   table. Ex. \[books,                              
                    for the specified table. maps, postcards\]                                

  options           A dictionary of options  Dictionary            Yes         None           
                    for the detail.                                                           
                    Available options are                                                     
                    described in detail                                                       
                    below.                                                                    
  ------------------------------------------------------------------------------------------------------

## Settings for *detailTypes* options

Many display settings for a detail are set in the *options* dictionary.

+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| Setting                                 | Description            | Allowed values                                            | Required? | Default  | Synonyms       |
+=========================================+========================+===========================================================+===========+==========+================+
| nextLink                                | HTML to use for \"next | HTML text                                                 | No        | Next     |                |
|                                         | search result\" link   |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| previousLink                            | HTML to use for        | HTML text                                                 | No        | Previous |                |
|                                         | \"previous search      |                                                           |           |          |                |
|                                         | result\" link          |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| resultsLink                             | HTML to use for \"back | HTML text                                                 | No        | Back     |                |
|                                         | to search results\"    |                                                           |           |          |                |
|                                         | link                   |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| enableComments                          | Controls whether the   | 0 or 1                                                    | No        | 0        |                |
|                                         | user comment form is   |                                                           |           |          |                |
|                                         | enabled for this       |                                                           |           |          |                |
|                                         | detail.                |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| enableShare                             | Controls whether the   | 0 or 1                                                    | No        | 0        |                |
|                                         | sharing form is        |                                                           |           |          |                |
|                                         | enabled for this       |                                                           |           |          |                |
|                                         | detail.                |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| shareLabel                              | Text to use for        | HTML text                                                 | No        | Share    |                |
|                                         | sharing link on        |                                                           |           |          |                |
|                                         | detail.                |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| enablePDF                               | Controls whether PDF   | 0 or 1                                                    | No        | 0        |                |
|                                         | export is enabled for  |                                                           |           |          |                |
|                                         | this detail.           |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| disableExport                           | Disable all exports in | 0 or 1                                                    | No        | 0        |                |
|                                         | detaii.                |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| pdfExportTitle                          | Display template used  | HTML text                                                 | No        | export   |                |
|                                         | to format download     |                                                           |           |          |                |
|                                         | file name for export . |                                                           |           |          |                |
|                                         | The template is        |                                                           |           |          |                |
|                                         | evaluated relative to  |                                                           |           |          |                |
|                                         | the detail\'s subject. |                                                           |           |          |                |
|                                         | If not set download    |                                                           |           |          |                |
|                                         | file is named          |                                                           |           |          |                |
|                                         | \"export\" plus a file |                                                           |           |          |                |
|                                         | extension appropriate  |                                                           |           |          |                |
|                                         | to the export format.  |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| representationViewerPrimaryOnly         | Only show primary      | 0 or 1                                                    |           | 0        |                |
|                                         | representation in      |                                                           |           |          |                |
|                                         | detail\'s media viewer |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| representationViewerDontShowPlaceholder | Controls whether a     | 0 or 1; leave set to 0 to display placeholders.           | No        | 0        |                |
|                                         | placeholder is shown   |                                                           |           |          |                |
|                                         | when no                |                                                           |           |          |                |
|                                         | representations are    |                                                           |           |          |                |
|                                         | available for the      |                                                           |           |          |                |
|                                         | detail\'s subject.     |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| representationViewerCaptionTemplate     | Display template used  | Display template text. Ex.                                | No        | none     |                |
|                                         | to format caption in   | \^ca_object_representations.preferred_labels.name         |           |          |                |
|                                         | representation viewer  |                                                           |           |          |                |
|                                         | control bar. The       |                                                           |           |          |                |
|                                         | template will be       |                                                           |           |          |                |
|                                         | evaluated relative to  |                                                           |           |          |                |
|                                         | the object             |                                                           |           |          |                |
|                                         | representation record. |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| displayAnnotations                      | Controls display of    | viewer (in viewer), div (in external div with class       | No        | none     |                |
|                                         | time-based             | #detailAnnotations), none (no display)                    |           |          |                |
|                                         | annotations.           |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| displayAnnotationTemplate               | Display template used  | Display template text. Ex.                                | No        | none     |                |
|                                         | to format each         | \^ca_representation_annotations.preferred_labels.name     |           |          |                |
|                                         | annotation in the list | (\^ca_representation_annotations.duration%asTimecode=hms) |           |          |                |
|                                         | annotation list. The   |                                                           |           |          |                |
|                                         | template will be       |                                                           |           |          |                |
|                                         | evaluated relative to  |                                                           |           |          |                |
|                                         | the annotation,        |                                                           |           |          |                |
|                                         | allowing you to output |                                                           |           |          |                |
|                                         | content from the       |                                                           |           |          |                |
|                                         | annotation as well as  |                                                           |           |          |                |
|                                         | its related object     |                                                           |           |          |                |
|                                         | representation and/or  |                                                           |           |          |                |
|                                         | object.                |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| mapAttribute                            | A georeference         | ca_objects.georeference (stand alone georeference element | No        | none     | map_attribute  |
|                                         | metadata element code  | attached to an object) ca_objects.location.georef         |           |          |                |
|                                         | to plot on the         | (georeference element in a container element named        |           |          |                |
|                                         | detail\'s map. If not  | \"location\" attached to an object)                       |           |          |                |
|                                         | set, the element does  |                                                           |           |          |                |
|                                         | not have values set    |                                                           |           |          |                |
|                                         | for the detail\'s      |                                                           |           |          |                |
|                                         | subject, or the        |                                                           |           |          |                |
|                                         | element is invalid no  |                                                           |           |          |                |
|                                         | map will be displayed. |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| mapAttributes                           | A list of georeference | \[ca_objects.georeference, ca_objects.old_location\]      | No        | none     | map_attributes |
|                                         | metadata element codes |                                                           |           |          |                |
|                                         | to plot on the         |                                                           |           |          |                |
|                                         | detail\'s map. If not  |                                                           |           |          |                |
|                                         | set, none of the       |                                                           |           |          |                |
|                                         | listed elements have   |                                                           |           |          |                |
|                                         | values set for the     |                                                           |           |          |                |
|                                         | detail\'s subject, or  |                                                           |           |          |                |
|                                         | none of the listed     |                                                           |           |          |                |
|                                         | elements are valid no  |                                                           |           |          |                |
|                                         | map will be displayed. |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| mapWidth                                | Width of map in pixels | 285                                                       | No        | 285px    | map_width      |
|                                         | or percent of          |                                                           |           |          |                |
|                                         | available width.       | 285px                                                     |           |          |                |
|                                         |                        |                                                           |           |          |                |
|                                         |                        | 100%                                                      |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| mapHeight                               | Height of map in       | 285                                                       | No        | 200px    | map_height     |
|                                         | pixels or percent of   |                                                           |           |          |                |
|                                         | available width.       | 285px                                                     |           |          |                |
|                                         |                        |                                                           |           |          |                |
|                                         |                        | 100%                                                      |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| mapZoomLevel                            | Zoom level to set for  | A value between 0 and 18                                  | No        | 12       | zoom_level     |
|                                         | map on page load.      |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+
| mapContentTemplate                      | Display template used  | Display template text. Ex. \^ca_objects.idno              | No        | none     |                |
|                                         | to format label        |                                                           |           |          |                |
|                                         | displayed when a map   | If not set map markers will not respond to clicks.        |           |          |                |
|                                         | marker is clicked. The |                                                           |           |          |                |
|                                         | template is evaluated  |                                                           |           |          |                |
|                                         | relative to the        |                                                           |           |          |                |
|                                         | details subject.       |                                                           |           |          |                |
+-----------------------------------------+------------------------+-----------------------------------------------------------+-----------+----------+----------------+

## Detail URLs

Unique codes are used in URLs to select a detail for display. The URL
format is:

https://\<your-hostname\>/Detail/\<code\>/\<identifier\> where \<code\>
is the detail\'s code and \<identifier\> is the numeric row id or
alphanumeric record identifier to display.
