# Plate Files

The final number plate print (and preview) files sent to Plateit need to adhere to a few rules.

## Rules

### Format

The final image files need to be in [SVG](https://developer.mozilla.org/en-US/docs/Web/SVG) format.

### Viewport

The width and height sections of the SVG's `viewport` attribute need to match the width and height in mm of the number plate being purchased. For example, the viewport attribute for a standard 520x111mm oblong would need to be:

```xml
<svg viewBox="0 0 520 111">
  <!-- remaining data -->
</svg>
```

Failure to adhere to the above viewport rule will return a validation error.

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

By default, any [plate](/objects/order-package-plate.md) belonging to a [package](/objects/order-package.md) requires a `design_print` SVG string. This will also act as the preview by default. You can optionally pass an entirely different `design_preview` SVG string, but this may not be necessary if you can effectively utilise the `do-not-print` class.

For example, the rectangle in the following SVG string will be present when displaying preview files, but ignored when printing.

```xml
<svg viewBox="0 0 520 111">
  <rect width="520" height="111" rx="3" ry="3" fill="yellow" class="do-not-print"></rect>
</svg>
```