# Images

> Documentation and examples for opting images (via `<b-img>` component) into
responsive behavior (so they never become larger than their parent elements),
optionally adding lightweight styles to them — all via props. Support for
rounded images, thumbnail styling, alignment, and even the ability to create
blank images with  an optional solid background color.

## Responsive images
Images in Bootstrap-Vue can be made responsive with the `fluid` prop (which
sets `max-width: 100%; height: auto;` via CSS classes) so that it scales
with the parent element - up to the maximum native width of the image.

```html
<div>
  <b-img src="https://lorempixel.com/1024/400/" fluid alt="Responsive image" />
</div>

<!-- b-img-responsive-1.vue -->
```

To make a fluid image that will grow to fill the width of it's container, use
the `fluid-grow` prop. Note this may cause bluring on small bitmap images.

```html
<div>
  <h5>Small image with <code>fluid</code>:</h5>
  <b-img src="https://lorempixel.com/300/150/" fluid alt="Fluid image" />
  <h5 class="my-3">Small image with <code>fluid-grow</code>:</h5>
  <b-img src="https://lorempixel.com/300/150/" fluid-grow alt="Fluid-Grow image" />
</div>

<!-- b-img-responsive-2.vue -->
```

Use the `block` prop to force the image to display as a block element rather than the
browser default of inline-block element.

**Note:** _In Internet Explorer 10, SVG images with `fluid` are disproportionately sized.
To fix this, add the style `width: 100% \9;` where necessary. This fix improperly sizes
other image formats, so Bootstrap V4 doesn’t apply it automatically._

## Image thumbnails
You can use prop `thumbnail` to give an image a rounded light border appearance.

```html
<b-container fluid class="p-4 bg-dark">
  <b-row>
    <b-col>
      <b-img thumbnail fluid src="https://lorempixel.com/250/250/technics/4/" alt="Thumbnail" />
    </b-col>
    <b-col>
      <b-img thumbnail fluid src="https://lorempixel.com/250/250/technics/8/" alt="Thumbnail" />
    </b-col>
    <b-col>
      <b-img thumbnail fluid src="https://lorempixel.com/250/250/technics/4/" alt="Thumbnail" />
    </b-col>
  </b-row>
</b-container>

<!-- b-img-thumbnail.vue -->
```

## Rounded corners
You can control which corners are rounded by setting the rounded prop to one
of the following values:
- `true` (or prop present with no value): round all corners
- `false` (or prop not present): no explit rounding or corners (default)
- `'top'`: round the top corners
- `'right'`: round the right corners
- `'bottom'`: round the bottom corners
- `'left'`: round the left corners
- `'circle'`: make a circle (if square image) or oval (if not square) border
- `'0'`: explicity turn off rounding of corners

```html
<div>
  <b-img rounded blank width="75" height="75" blank-color="#777" alt="img" class="m-1" />
  <b-img rounded="top" blank width="75" height="75" blank-color="#777" alt="img" class="m-1" />
  <b-img rounded="right" blank width="75" height="75" blank-color="#777" alt="img" class="m-1" />
  <b-img rounded="bottom" blank width="75" height="75" blank-color="#777" alt="img" class="m-1" />
  <b-img rounded="left" blank width="75" height="75" blank-color="#777" alt="img" class="m-1" />
  <b-img rounded="circle" blank width="75" height="75" blank-color="#777" alt="img" class="m-1" />
  <b-img rounded="0" blank width="75" height="75" blank-color="#777" alt="img" class="m-1" />
</div>

<!-- b-img-rounded.vue -->
```

## Aligning images
Align images with the boolean props `left` (floats left) `right`(floats right),
and `center` (auto left+right margins). You can also center images by placing them
in a container that has the class `text-center`.

**Left an Right aligned (float):**
```html
<div class="clearfix">
  <b-img left src="https://lorempixel.com/125/125/technics/8/" alt="left image" />
  <b-img right src="https://lorempixel.com/125/125/technics/8/" alt="right image" />
</div>

<!-- b-img-left-right.vue -->
```

**Center aligned (block):**
```html
<div>
  <b-img center src="https://lorempixel.com/125/125/technics/8/" alt="center image" />
</div>

<!-- b-img-center.vue -->
```

Note: `left` takes precedence over `right` which takes precedence over `center`.


## Blank (or solid color) Images
`<b-img>` provides built-in support for generating blank images (transparent by
default) of any width and height, by setting the `blank` prop, and specifying 
`width` and `height` values (in pixels). You can apply any of the other
`<b-img>` props to change the style/behavior of the generted image.

Use the `blank-color` prop to set the blank image color. The `blank-color`prop
can accept any CSS color value:
- Named colors — i.e. `orange` or `blue`
- Hex colors — i.e. `#FF9E2C`
- RGB and RGBa colors — i.e. `rgb(255, 158, 44)` and `rgba(255, 158, 44, .5)`
- HSL and HSLa colors — i.e. `hsl(32, 100%, 59%)` and `hsla(32, 100%, 59%, .5)`

The default `blank-color` is `transparent`.

```html
<div>
  <b-img blank width="75" height="75" alt="transparent" class="m-1" />
  <b-img blank width="75" height="75" blank-color="#777" alt="hex shorthand color" class="m-1" />
  <b-img blank width="75" height="75" blank-color="red" alt="named color" class="m-1" />
  <b-img blank width="75" height="75" blank-color="black" alt="named color" class="m-1" />
  <b-img blank width="75" height="75" blank-color="#338833" alt="hex color" class="m-1" />
  <b-img blank width="75" height="75" blank-color="rgba(128,255,255,0.5)" alt="RGBa color" class="m-1" />
  <b-img blank width="75" height="75" blank-color="#88f" alt="hex shorthand color" class="m-1" />
</div>

<!-- b-img-blank.vue -->
```

**Notes:**
- In blank image mode, if only one of width or height is set, the image will be have both width and height set to the same value.
- In blank image mode, if width and height are not set, both width and height will internally be set to 1.
- The `blank` prop takes precedence over the `src` prop.  If you set both and later set `blank` to `false` the image specified in `src` will then be displayed.
- Blank images are rendered using SVG image data URLs.
- The `width` and `height` props will also apply the `width` and `height` attributes to the rendered `<img>` tag, even if `blank` is not set.


## Lazy Loaded images
> Use our complementary `<b-img-lazy>` image component (based on `<b-img>`) to lazy
load images as they are scrolled into view (or within `offset` pixels of the viewport).

### Usage
Set the `src` prop to the URL of the image you want loadied lazily, and either specify a
placeholder image URL via the prop `blank-src`, or have a blank placeholder image generated
for you by leaving `blank-src` as `null`.

Specify the width and height of the placeholder via the `blank-width` and `blank-height`
props.  If these props are not set, then they will fall back to the `width` and `height`
props (which are applied to the image specified via `src`).

Control the generated blank image color by setting the prop `blank-color`.

Placeholder images (either explicity provided, or dynamicaly generated) should have the same
width and height values, or at least the same aspect ratio, as the `src` image.

Feel free to use the `fluid`, `fluid-grow`, `thumbnail`, and `rounded` props of `<b-img>`.

The `offset` prop specifies the number of pixels that an image needs to be near to
the viewport to trigger it to be shown. The default value is `360`.

The `throttle` prop controls how long (in ms) after a scroll (or resize or
orientationchange) event happens before checking if the image is has come within
view (or within `offset` of view).  The default is `100` (ms).

Once an image has come into view and is shown, the scroll event listeners are
removed.

**Example usage:**
```html
<div>
  <b-img-lazy src="https://lorempixel.com/600/400/cats/1/" center fluid-grow width="600" height="400" blank-color="#bbb" alt="img" class="my-5" />
  <b-img-lazy src="https://lorempixel.com/600/400/cats/3/" center fluid-grow width="600" height="400" blank-color="#bbb" alt="img" class="my-5" />
  <b-img-lazy src="https://lorempixel.com/600/400/cats/4/" center fluid-grow width="600" height="400" blank-color="#bbb" alt="img" class="my-5" />
  <b-img-lazy src="https://lorempixel.com/600/400/cats/5/" center fluid-grow width="600" height="400" blank-color="#bbb" alt="img" class="my-5" />
  <b-img-lazy src="https://lorempixel.com/600/400/cats/6/" center fluid-grow width="600" height="400" blank-color="#bbb" alt="img" class="my-5" />
  <b-img-lazy src="https://lorempixel.com/600/400/cats/7/" center fluid-grow width="600" height="400" blank-color="#bbb" alt="img" class="my-5" />
  <b-img-lazy src="https://lorempixel.com/600/400/cats/8/" center fluid-grow width="600" height="400" blank-color="#bbb" alt="img" class="my-5" />
  <b-img-lazy src="https://lorempixel.com/600/400/cats/9/" center fluid-grow width="600" height="400" blank-color="#bbb" alt="img" class="my-5" />
  <b-img-lazy src="https://lorempixel.com/600/400/cats/10/" center fluid-grow width="600" height="400" blank-color="#bbb" alt="img" class="my-5" />
</div>

<!-- b-img-lazy.vue -->
```

## Component Reference
