# NTAG Sheet Designer

A fully static HTML/CSS/JavaScript tool for designing printable NFC card artwork sheets.

NTAG Sheet Designer lets you populate a Letter-size sheet with song or playlist cards intended for use with NTAG215 NFC cards. Each card can contain artwork, a title, a subtitle, and independently configurable font sizes.

The application runs entirely in the browser and requires no backend or server.

## Features

* Static HTML, CSS, and JavaScript application
* Letter-size 8.5 × 11 inch sheet
* 9 vertical cards per sheet
* 3 columns × 3 rows
* Each printed card is approximately 1.93 × 3.15 inches
* Intended for NTAG215 card artwork
* Song or playlist title
* Artist or description subtitle
* Independent title font size
* Independent subtitle font size
* Artwork from a direct image URL
* Artwork from a local image file
* Local artwork is stored as a browser data URL
* Duplicate cards
* Blank individual cards
* Clear the entire sheet
* Print directly from the browser
* Print layout optimized for Letter paper
* No backend or external application required

## Getting Started

No installation or build system is required.

Save the HTML source as:

```text
index.html
```

Then open it in a modern web browser.

For example:

```bash
firefox index.html
```

or open `index.html` directly from your file manager.

Because the application is completely static, it can also be hosted from any static web server.

## Using the Card Editor

The editor is organized into three sections.

### 1. Select Card

Use the Card Position selector to choose which card you want to edit.

Cards are identified by their position on the sheet:

```text
Card 1 · Row 1, Column 1
Card 2 · Row 1, Column 2
Card 3 · Row 1, Column 3
...
Card 9 · Row 3, Column 3
```

Selecting a card loads that card's current information into the editor.

### 2. Card Information

Each card supports two text fields.

#### Song or playlist name

The primary title displayed at the bottom of the card.

Example:

```text
Disney Favorites
```

#### Artist or description

The secondary text displayed underneath the title.

Example:

```text
Disney
```

### Font Size

Title and subtitle font sizes can be configured independently.

The current defaults are:

```text
Title:    22 px
Subtitle: 16 px
```

The available ranges are:

```text
Title:    8–48 px
Subtitle: 8–36 px
```

Font sizes are stored separately for each card. Changing the title size on one card does not change the title size on other cards.

Press **Apply to card** to save the changes.

### 3. Artwork

Artwork can be supplied in two ways.

#### Image URL

Paste a direct URL to an image:

```text
https://example.com/image.jpg
```

The image is rendered using an HTML `<img>` element rather than a CSS background image. This improves compatibility with browser printing.

#### Local Image

Select an image from the computer using the file picker.

Local artwork is converted into a browser data URL and stored in the current page. The image is not uploaded to a server.

## Applying Changes

After editing a card, press:

```text
Apply to card
```

The current editor values are saved to the selected card and the sheet is re-rendered.

The card stores:

```javascript
{
  title: "",
  subtitle: "",
  titleSize: 22,
  subtitleSize: 16,
  url: "",
  image: ""
}
```

## Duplicating Cards

Press **Duplicate** to copy the currently selected card.

The duplicate includes:

* Title
* Subtitle
* Title font size
* Subtitle font size
* Artwork URL
* Uploaded artwork

This is useful when creating several similar cards.

## Clearing Cards

There are two ways to remove card content.

### Blank

The **Blank** button on an individual card clears that card.

Its settings are reset to:

```text
Title font:    22 px
Subtitle font: 16 px
```

### Clear Sheet

The **Clear sheet** button resets all cards on the sheet.

All artwork and text are removed and all font sizes return to their defaults.

## Sheet Layout

The application currently renders a Letter-size sheet:

```text
8.5 × 11 inches
```

The sheet contains 9 cards arranged as:

```text
┌─────────┬─────────┬─────────┐
│ Card 1  │ Card 2  │ Card 3  │
├─────────┼─────────┼─────────┤
│ Card 4  │ Card 5  │ Card 6  │
├─────────┼─────────┼─────────┤
│ Card 7  │ Card 8  │ Card 9  │
└─────────┴─────────┴─────────┘
```

The printed card dimensions are approximately:

```text
1.93 × 3.15 inches
```

The cards are slightly smaller than the physical 2.13 × 3.35 inch NTAG215 card dimensions. This provides additional room for sticker paper and cutting around the cards.

## Printing

Press **Print sheet** to open the browser's print dialog.

The application waits for artwork images to finish loading before calling `window.print()`.

For accurate physical dimensions, use:

```text
Paper:       Letter
Orientation: Portrait
Scale:       100%
Sizing:      Actual Size
Margins:     None / 0
```

Disable browser options that automatically scale the page to fit the printable area.

The application uses:

```css
@page {
  size: Letter portrait;
  margin: 0;
}
```

and explicitly sets the printable page to:

```text
8.5 × 11 inches
```

Color printing should have **Background graphics** enabled if your browser/printer configuration requires it.

## Artwork Printing

Artwork is inserted into the page as an actual image:

```html
<img class="card-art">
```

This is intentional.

Using an `<img>` element is generally more reliable for printing than using:

```css
background-image: url(...);
```

The application also waits for the images to load before opening the print dialog.

## Browser Storage and Privacy

The application does not have a backend.

Images selected from the local computer are converted into data URLs and retained in the page's JavaScript state.

They are not uploaded by the application.

Refreshing or closing the page will clear the current in-memory sheet unless the application is extended with persistent browser storage in the future.

## Technology

The application uses only standard browser technologies:

```text
HTML5
CSS3
JavaScript
```

There are no required dependencies, frameworks, package managers, or build tools.

The application can be run from a single file:

```text
index.html
```

## Project Structure

The minimal project can consist of:

```text
ntag-sheet-designer/
└── index.html
```

The HTML file contains:

* Page structure
* Application styling
* Card layout
* Print styling
* Card data
* Rendering logic
* Editor logic
* Artwork handling
* Printing logic

## Browser Compatibility

The application is intended for modern desktop browsers with support for:

* HTML5
* CSS Grid
* CSS custom properties
* FileReader API
* DOM APIs
* Browser printing

Recommended browsers include current versions of:

* Firefox
* Chrome
* Chromium
* Microsoft Edge
* Safari

For the most accurate physical printing, verify the printer's scaling and margin settings before printing a full sheet.

## Current Limitations

The current implementation intentionally remains a simple static designer.

It does not currently provide:

* Persistent project saving
* Export/import of card layouts
* Multiple sheet management
* Automatic text fitting
* Automatic artwork cropping controls
* NFC tag writing
* Spotify integration
* Backend storage
* User accounts

The application is focused specifically on creating and printing the physical artwork sheet.

## License

No license is currently specified.

If this project is published or redistributed, add an appropriate license file such as:

```text
LICENSE
```

and update this section accordingly.
