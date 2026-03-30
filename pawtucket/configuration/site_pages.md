---
title: Site Pages
sidebar_position: 8
---

# Site Pages
## Overview

The site page feature provides users with an easy way to add blog-like functionality to their Pawtucket site through the use of static page templates, which are edited in Providence, and which generate stand-alone pages on their front end. These pages are fully customizable and also allow for media upload through Providence to give users without a background in HTML/CSS the ability to create new pages for their site. This allows for easier editing of About, Contact and other pages that may require occasional updates but which are not part of an organization's digital collections.

## General Steps
There are several components that provide the design and configuration for these pages: the page template(s) (a `.tmpl` file), your theme's `template.conf` file in Pawtucket, and the Site Page editor in Providence.

1. Create one or more `.tmpl` files. These provide the HTML markup for each type of site page and contain `{{{[field]}}}` placeholders for user-supplied values. These pages can use Bootstrap CSS classes to structure the layout. Several examples are included in the default Pawtucket theme.
2. Add and modify a `template.conf` file to the Pawtucket theme. This file provides title and format instructions for how the user-supplied `{{{[field]}}}` values can be edited, including WYSIWYG editor options. An example `template.conf` file is also included in the default Pawtucket theme.
3. Run the `scan-site-page-templates` utility in your Pawtucket's support directory.
4. Create site page(s) in Providence using the site page editor.

:::note
A site page editor must be defined in your configuration file for this to be enabled.
:::

## Template (.tmpl) Files

These files provide the HTML layout of a site page and include the triple-curly bracketed field placeholders that designate where user-editable text will be included. A simple example:

```html
<h1>{{{title}}}</h1>
<h3>{{{subtitle}}}</h3>

<div class="bodytext">
   {{{bodytext}}}
</div>
```

## template.conf

This file controls how the user-editable fields defined in your templates (e.g. `{{{title}}}`) can be edited. The full list of options is:

| Option | Description | Values | Example |
|---|---|---|---|
| label | Main label for this field in Providence | Plain text | Page title |
| description | A brief description of the purpose of this field | Plain text | The top-level title for this page |
| width | The width of the editor in Providence, in pixels | Width in pixels | 600px |
| height | The height of the editor in Providence | Set to "1" for a single row editor, otherwise set in pixels | 1 or 250px |
| usewysiwygeditor | Enable or disable a WYSIWYG editor for this field. Enabling allows for embedding images. | 1 or 0 | 1 |

A simple `template.conf` file will look like:

```
fields = {
  title = {
    label = Page title,
    description = Title of page,
    width = 600px,
    height = 1
  },
  bodytext = {
    label = Page text,
    description = Main text for page,
    usewysiwygeditor = 1,
    width = 600px,
    height = 300px
  }
}
```

## scan-site-page-templates caUtils Script

Before these pages can be created or edited, you must run a caUtils script on the command line for Providence to detect new or changed templates in Pawtucket. From the support directory of your Pawtucket install, run:

```bash
php -f bin/caUtils scan-site-page-templates
```

## Providence Editor

:::note
If you are implementing Site Pages on an older version of Providence, you may not have created a User Interface for editing Site Pages. You must create this interface before you can create or edit these pages.
:::

Once you have created the templates and conf file, you can create and edit these pages through **Manage > Pawtucket > Site Pages**. To be made available, each page must be assigned a unique URL in the "URL Path" field. This path must start with a forward slash (e.g. `/About/hours`).

Images uploaded through the Site Page media bundle are available to embed in any field with WYSIWYG editing enabled. They can be selected by clicking the image icon in the editor's toolbar.

## Special Placeholders

In your `.tmpl` files there are several special placeholders that perform specific functions:

| Placeholder | Description | Output |
|---|---|---|
| `{{{page_view_count}}}` | Displays the number of times this site page has been displayed | "42" |