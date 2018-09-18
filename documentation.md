# Documentation

## Installation

### Git submodule (recommended)

To seamlessly update the theme to the latest version, 
add it as a Git submodule to your repository.

```bash
git submodule add https://gitlab.com/dspechnikov/dimension-hugo themes/dimension
git submodule init
git submodule update
```

To get updates in the future:

```bash
git submodule update --remote themes/dimension
```

### Git clone

If you need a one-time installation, you can just clone the repository:

```bash
git clone https://gitlab.com/dspechnikov/dimension-hugo themes/dimension
```

## Usage

### Configuration

The theme can be configured via `config.toml` file. See demo site [configuration][demo site configuration] for examples.

#### Google Analytics

To use [Google Analytics](https://analytics.google.com/), add your tracking ID via `googleAnalytics` option in `config.toml`.

#### Supported site parameters

- `author` (default: `""`) - Site author used in meta author tag.
- `description` (default: `""`) - Site description used in meta description tag.
- `copyrightText` (default: `""`) - The text after copyright sign and years in the footer.
- `copyrightPublishYear` (default: `""`) - The year when site was published for the first time. See [this section](#automatic-copyright-year) for details.
- `disableLogo` (default: `false`) - Set to true to remove logo image and all borders above the title.
- `logoImage` (default: `""`) - Image to use as a logo. If set, `logoIcon` is ignored.
- `logoIcon` (default: `gem`) - Font awesome icon name to use as a logo.
- `titleFontSize` (default: `2.25rem`) - Font size of the title in the main page.
- `subtitleFontSize` (default: `0.8rem`) - Font size of the subtitle in the main page.
- `baseFontSize` (default: `1.0rem`) - Base font size used in article text.
- `overlayOpacityPercentage` (default: `50`) - Overlay opacity level. You may want to increase it to improve title and subtitle readability.
- `disableImageOverlay` (default: `false`) - Set to true to remove overlay from article images.
- `modalWidth` (default: `40rem`) - Width of modal window with article content.
- `customCSS` (default: `""`) - Custom CSS file name.

### Custom images

#### Background

The theme has dummy background image by default. To replace it with yours, copy it to `static/images/bg.jpg` file.

#### Logo

You can use custom logo image (a square one, preferably) instead of Font Awesome icon. To do this:
1. Place the image to `static/images/` directory.
1. Write image file name in `logoImage` option, i.e. `logo.jpg`.

### Pages content

#### Main page

1. Create `content/_index.md` file.
1. Change page title text with `title` front matter variable.
1. Change page subtitle text with page content.

See demo site [index page](./exampleSite/content/_index.md) for examples.

#### Regular pages

1. Create a new markdown file in `content` directory.
1. Set `title` front matter variable to set page title.
1. Write page content using markdown syntax and theme [shortcodes](#shortcodes).

##### Page ordering in the navigation menu

By default, the pages are sorted by title in the navigation menu. To change the ordering, set `weight` front matter variable. The page with the highest `weight` will appear first.

##### Exclude page from navigation menu

The page may be made visible only by direct link. Set `showInMenu` front matter variable to `false` to achieve that.

### Shortcodes

#### Form

An HTML form with support for [Formspree](https://formspree.io) custom attributes. 

##### Basic usage
```
{{< form action="actionURL" >}}
    {{< formField type="text" id="name" width="half" >}}
    {{< formField type="email" id="email" >}}
    {{< formField type="textarea" id="message">}}
{{< /form >}}
```

##### Supported options
- `action` - **required**. The URL which the form would be sent to.
- `submitButtonText` (default: `"Send Message"`) - The text on submit button.
- `resetButtonText` (default: `""`) - Use it to add form reset button.

The following options are specific for form using [Formspree](https://formspree.io):
- `formspreeRedirectURL` (default: `""`) - URL to redirect to after the form is sent.
- `formspreeSubject` (default: `""`) - Custom Email subject.
- `formspreeHoneypot` (default: `""`) - Set to `yes` to include a "Honeypot" field in your form.

#### Form field

A form field to use within [Form](#form) shortcode.

##### Basic usage
`{{< formField type="text" id="name" >}}`

##### Supported options
- `type` - **required**. The field type. 
If set to `textarea` the field will be rendered as text area instead of regular input.
- `id` - **required**. Used to distinguish the field from others. 
Also, it's used as a default label text and field name.
- `width` (default: `""`) - The field width. By default the field takes a full row. Possible values: 
    - `half` 
    - `third`
    - `quarter`
- `label` (default: `""`) - The field label text. If not set, uses `id` field value.
- `name` (default: `""`) - The field name. If not set, uses `id` field value.
- `rows` (default: `"5"`) - Applies only for field with `textarea` type. 
Sets the height of the field in rows.

#### Icons

A set of [Font Awesome](https://fontawesome.com/) icons.

##### Basic usage
```
{{< icons >}}
    {{< icon name="gitlab" link="#" title="GitLab" >}}
    {{< icon name="envelope-o" link="mailto:me@example.com" title="Email" >}}
{{< /icons >}}
```

##### Supported options
- `name` - **required**. The Font Awesome icon name.
- `link` - **required**. The URL for this icon.
- `title` - **required**. The label for this icon.

#### Image

An image inside the article.

##### Basic usage
```
{{< image position="right" src="images/img.jpg" >}}
```

##### Supported options
- `src` - **required**. The image file path.
- `position` (default: `"main"`) - Defines how image is placed to the rest of content.
By default it takes full article width. Possible values:
    - `left`
    - `right`
    - `fit`
    - `main`
- `alt` (default: `""`) - The alt image attribute.
- `title` (default: `""`) - The title image attribute.

### Custom styles

Basic style customization can be done via [configuration options](#configuration). 
If you need to change something else, you can do it in your own CSS file. To add it:

1. Create `assets/css/yourCustomCSSName.css` file.
1. Add `customCSS = "yourCustomCSSName.css"` to params section of `config.toml` file.  

### Translations

To translate site content to multiple languages:

1. Add languages configuration (see demo site [configuration][demo site configuration] for example).
1. Add `<page-name>.<language-code>.md` file for each page you want to translate. 
   I.e, `_index.fr.md` for French translation of the main page.
   
After that, "switch language" links will be shown in the site footer.

Content without translations will be displayed in default language.

### Automatic copyright year

Copyright message should include at least the year when the site was published 
for the first time. You can specify it in `copyrightPublishYear` option. Then 
copyright years will be updated with each passing year to look like this: `<copyrightPublishYear>-<currentYear>`.   

### Sitemap

Hugo default permalink format does not work with this theme. 
To get correct links in the sitemap, add the following section to the `config.toml`:
```
[permalinks]
    "" = "/#:filename"
``` 

[demo site configuration]: ./exampleSite/config.toml
