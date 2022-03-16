# Simpler Color

Create your own complete color system fast and easy!

Color is at the heart of every UI design system. A cohesive **color system** enables your application to:

- **consistently** express brand identity and style
- **effectively** communicate intent and meaning

Simpler Color makes it super easy to implement your own color system, no matter what platform, framework, or UI library you are using. It comes as a JavaScript/TypeScript library that works on both browser and Node.

## Easy as 1-2-3!

**Step 1:** Install simpler-color

```
npm install simpler-color
```

**Step 2:** Define your color palettes and their corresponding base colors

```js
const baseColors = {
  primary: '#336669',
  secondary: '#57614E',
  neutral: '#5E5F5A',
}
```

**Step 3:** Create your color scheme(s) by mapping UI roles to specific colors from your palettes

```js
import { colorScheme } from 'simpler-color'

const uiColors = colorScheme(baseColors, colors => ({
  primaryButton: colors.primary(40),
  primaryButtonText: colors.primary(95),
  surface: colors.neutral(98),
  text: colors.neutral(10),
}))

// You can now access your various UI colors as `uiColors.primaryButton` and so on.
```

If some of those terms sound alien to you, read on...

> **BUT FIRST, if you like this library, the concept, and its simplicity, please give it a star ⭐️ on the [GitHub repo](https://github.com/arnelenero/simpler-color) to let me know.** 😀

## Key Concepts

We're not gonna discuss Color Theory here, but let's talk a bit about what a proper color system comprises.

### Color Palette

Creating your color system begins with building your _color palettes_. Each palette consists of a group of related colors, generated from one _base color_.

You decide what sort of relationship should be between colors in the palette. The most common type is the _tonal palette_ (also called _monochromatic_), which is made up of various "tones" of the same general hue. For example, various shades of blue is a tonal palette.

<img src="./docs/assets/palette.png" alt="shades of blue with varying lightness" width="800"/>

Each color in a palette is accessed by a unique _color key_, which is a string or number that indicates its relationship with the base color. The color values are determined by a _color mapping function_, which returns a specific color value for a given color key.

By default, simpler-color generates tonal palettes, with specific tones generated by passing a numeric key between 0 and 100, which represents % lightness (0 = black, 100 = white). Any value in between generates a specific shade of the base color.

You can, of course, define your own color mapping function to override the default.

### Color Set

The _color set_ is simply the collective term for all the color palettes you've built.

Typically a color set would have a _primary_ palette. This represents the main "brand" color of your app. This is the most prominent hue across your UI.

Common additional palettes can be any of (but not limited to) these:

- _secondary_: less prominent, usually more muted
- _accent_: usually complementary (opposite) to primary, to provide contrast
- _neutral_: typically shades of gray or similar neutral tones

To ensure consistency of your color set, simpler-color enforces that you use the same set of color keys (and thus the same color mapping function) across all your palettes.

### Color Scheme

A color system consists of one or several _color schemes_. These days, it's quite common to implement both Light and Dark color schemes.

To create a color scheme, you first identify the various _UI roles_ in your design system. Each role indicates a specific use or purpose of color as it applies to specific elements of the UI.

Some common examples of UI role:

- primary button
- primary button text
- surface/background color
- text color

The final step is to map each UI role to a specific color value from one of the palettes in your color set. Each such mapping gives us one color scheme. By using a consistent set of color roles, simpler-color helps ensure that your UI can easily and safely switch between color schemes.

## Recipes

### Defining a custom color mapping function

```js
function awesomeColor(baseColor, key) {
  const colorValue = /** insert logic here **/
  return colorValue
}

const uiColors = colorScheme(
  baseColors,
  colors => ({
    primaryButton: colors.primary(40),
    /** rest of the UI role mapping here **/
  }),
  {
    colorMapping: awesomeColor
  }
)
```
