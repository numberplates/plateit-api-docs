# Plate Files

To use Plateit, your application will need to generate the final print (and preview) files, which are then submitted to Plateit for processing. For convenience and maximum compatibility, we offer [our own number plate image generator](https://numberplates.github.io/plateit-generator-docs), which you can use to create the previews and print files. Alternatively, you can develop your own custom solution, providing it adheres the simple rules outlined on this page.

## Rules

### Format

The final image files need to be in [SVG](https://developer.mozilla.org/en-US/docs/Web/SVG) format.

### ViewBox

The width and height sections of the SVG's `viewBox` attribute need to match the width and height in mm of the number plate being purchased. For example, the viewBox attribute for a standard 520x111mm oblong would need to be:

```xml
<svg viewBox="0 0 520 111">
  <!-- remaining data -->
</svg>
```

Failure to adhere to the above viewBox rule will return a validation error.

### Fonts

Font file URLs should NOT be referenced in the file. All occurrences of text should be "flattened" into raw path coordinates. This is to ensure rendering consistency between devices and ensures longevity of the files (they will continue to render long after the dependencies have vanished).

For example, do this:

```xml
<svg viewBox="0 0 520 111">
  <path d="M10 20 H 50 V 30 H 10 L 10 20 Z" fill="#000" />
</svg>
```

Don't do this:

```xml
<svg viewBox="0 0 520 111">
  <text x="10" y="20" font-family="https://example.com/font.ttf" font-size="24">Text</text>
</svg>
```
### Embedded Images

As with fonts, please avoid referencing external image files. Embedded images are permitted but they must be self contained. All files should render *without* the need for an internet connection.

## Recommendations

### The "Do Not Print" Class

You can instruct Plateit to ignore elements in the final print SVG by giving those elements the `do-not-print` class. This is handy for elements that need to be there for preview images but are not required for printing, such as a yellow background for a standard rear number plate.

All [OrderPackagePlate](/objects/order-package-plate.md) objects require a `design_print` SVG. This also acts as the preview by default. You can optionally assign an entirely different `design_preview` SVG, but this may not be necessary if you can effectively utilise the `do-not-print` class.

For example, the rectangle in the following SVG string will be present when displaying preview files, but ignored when printing.

```xml
<svg viewBox="0 0 520 111">
  <rect width="520" height="111" rx="3" ry="3" fill="yellow" class="do-not-print"></rect>
</svg>
```

### Design Metadata

When creating or updating an [OrderPackagePlate](/objects/order-package-plate.md) object (or utilising the [Build Order](/helpers/build-order.md) helper endpoint), it is recommended to include not only the final SVG, but also a JSON representation of the design as a `design_object` property. This will allow you to bring the design back into your editor should you wish to make changes to it as a later date. For example:

```json
{
  "design_print": "<svg viewBox="0 0 520 111"><!-- remaining data --></svg>",
  "design_preview": "<svg viewBox="0 0 520 111"><!-- remaining data --></svg>",
  "design_object": {
    "document": {
      "width": 520,
      "height": 111,
    },
    "background": {
      "backgroundColour": "yellow",
      "isPreviewOnly": true
    },
    "reg": {
      "text": "NG25 XYZ",
      "textFontUrl": "../assets/fonts/CharlesWright-Car.ttf",
      "textHeight": 79,
      "textLineGap": 19,
      "textColour": "black"
    },
    "bottomLine": {
      "text": "ACME Number Plates, SW1A 2AA",
      "textFontUrl": "../assets/fonts/OpenSans-Regular.ttf",
      "textHeight": 4,
      "textColour": "black"
    },
    "bsau": {
      "text": "BSAU 145E",
      "textFontUrl": "../assets/fonts/OpenSans-Regular.ttf",
      "textHeight": 2,
      "textColour": "black"
    }
  }
}
```