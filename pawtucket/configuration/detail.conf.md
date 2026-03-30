---
title: detail.conf
sidebar_position: 3
---

# detail.conf
## Overview
The detail.conf configuration file defines all available detail views for a theme. Details are, as their name implies, detailed metadata displays for a specific item — a *subject*. At a minimum, a detail will be bound to a table. A detail may be designed to display data for one of the following tables: objects, entities, occurrences, places, or collections.

You may define any number of details. Each will have a unique code that is used in Pawtucket URLs to reference the detail.

## Top-level settings

The primary top-level setting is *detailTypes*, a dictionary that contains definitions for each detail. Other top-level settings control download of media.

| Setting | Description | Allowed values | Required? | Default | Synonyms |
|---|---|---|---|---|---|
| detailTypes | Dictionary of all detail pages available in this theme. Dictionary keys are short, unique codes for each available detail. Values are dictionaries of options for the detail, the format of which is defined below. | Dictionary | yes | none | |
| allowObjectRepresentationDownload | Controls whether download of representations on object detail pages are allowed, and to whom they are available. | anyone, logged_in, logged_in_privileged, never | no | never | allow_ca_objects_representation_download |
| restrictObjectRepresentationDownloadToObjectTypes | Controls which types of object records allow downloads when the policy set in allowObjectRepresentationDownload enables downloads. | A list of object types. Ex. [books, maps, images] | no | none - all types allow downloads | allow_ca_objects_representation_download_types |

## Settings for *detailTypes*

Keys in the *detailTypes* dictionary are used as unique detail codes. Values control detail display and functionality.

| Setting | Description | Allowed values | Required? | Default | Synonyms |
|---|---|---|---|---|---|
| displayName | Name of detail for display to end users. | Text | Yes | None | |
| table | Kind of record this detail displays. | Ex. ca_objects, ca_entities, ca_collections, etc. | Yes | None | |
| restrictToTypes | List of types to limit use of this detail to. Use type codes defined for the specified table. | Any valid type code for the detail's table. Ex. [books, maps, postcards] | No | [] (no type restriction) | |
| options | A dictionary of options for the detail. Available options are described in detail below. | Dictionary | Yes | None | |

## Settings for *detailTypes* options

Many display settings for a detail are set in the *options* dictionary.

| Setting | Description | Allowed values | Required? | Default | Synonyms |
|---|---|---|---|---|---|
| nextLink | HTML to use for "next search result" link | HTML text | No | Next | |
| previousLink | HTML to use for "previous search result" link | HTML text | No | Previous | |
| resultsLink | HTML to use for "back to search results" link | HTML text | No | Back | |
| enableComments | Controls whether the user comment form is enabled for this detail. | 0 or 1 | No | 0 | |
| enableShare | Controls whether the sharing form is enabled for this detail. | 0 or 1 | No | 0 | |
| shareLabel | Text to use for sharing link on detail. | HTML text | No | Share | |
| enablePDF | Controls whether PDF export is enabled for this detail. | 0 or 1 | No | 0 | |
| disableExport | Disable all exports in detail. | 0 or 1 | No | 0 | |
| pdfExportTitle | Display template used to format download file name for export. The template is evaluated relative to the detail's subject. If not set download file is named "export" plus a file extension appropriate to the export format. | HTML text | No | export | |
| representationViewerPrimaryOnly | Only show primary representation in detail's media viewer. | 0 or 1 | No | 0 | |
| representationViewerDontShowPlaceholder | Controls whether a placeholder is shown when no representations are available for the detail's subject. | 0 or 1; leave set to 0 to display placeholders. | No | 0 | |
| representationViewerCaptionTemplate | Display template used to format caption in representation viewer control bar. The template will be evaluated relative to the object representation record. | Display template text. Ex. `^ca_object_representations.preferred_labels.name` | No | none | |
| displayAnnotations | Controls display of time-based annotations. | viewer (in viewer), div (in external div with class #detailAnnotations), none (no display) | No | none | |
| displayAnnotationTemplate | Display template used to format each annotation in the annotation list. The template will be evaluated relative to the annotation, allowing you to output content from the annotation as well as its related object representation and/or object. | Display template text. Ex. `^ca_representation_annotations.preferred_labels.name` | No | none | |
| mapAttribute | A georeference metadata element code to plot on the detail's map. If not set, the element does not have values set for the detail's subject, or the element is invalid, no map will be displayed. | Ex. `ca_objects.georeference` or `ca_objects.location.georef` | No | none | map_attribute |
| mapAttributes | A list of georeference metadata element codes to plot on the detail's map. If not set, or none of the listed elements have values or are valid, no map will be displayed. | Ex. `[ca_objects.georeference, ca_objects.old_location]` | No | none | map_attributes |
| mapWidth | Width of map in pixels or percent of available width. | Ex. 285, 285px, 100% | No | 285px | map_width |
| mapHeight | Height of map in pixels or percent of available width. | Ex. 285, 285px, 100% | No | 200px | map_height |
| mapZoomLevel | Zoom level to set for map on page load. | A value between 0 and 18 | No | 12 | zoom_level |
| mapContentTemplate | Display template used to format label displayed when a map marker is clicked. The template is evaluated relative to the detail's subject. If not set map markers will not respond to clicks. | Display template text. Ex. `^ca_objects.idno` | No | none | |

## Detail URLs

Unique codes are used in URLs to select a detail for display. The URL format is:

```
https://<your-hostname>/Detail/<code>/<identifier>
```

where `<code>` is the detail's code and `<identifier>` is the numeric row id or alphanumeric record identifier to display.