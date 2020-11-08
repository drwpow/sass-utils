# 🍣 sass-utils

Grab-and-go Sass utility classes for any occasion.

## Intro

#### Utilities? In 2020?

**Why use utilities? Isn’t global CSS bad?** Of course not! CSS’ major strength is that it can be global.

Even following modern [component-based practices][css] and [layout-isolated components][layout], there are still times when you find yourself writing the same CSS over and over and over. Even with a consistent design methodology, you’ll find some aberrant styles break the mold and don’t neatly fit in with the reusable parts of each component.

Just as even the most organized, well-designed homes need junk drawers, so do the best-designed, organized web apps need utility classes. Below are a list of utilities I use in every project. It not only reduces duplicate styling; it also improves clarity in the project and keeps components tidier, and more concerned with their own responsibilities.

## Utilities

Copy and paste these into any `.scss` file in your app.

💁 **Be sure to load these last in your app!** Otherwise you’ll find they won’t work if other styles take priority.

### 🎨 Color

Color will be specific to your app, but here are some patterns that help color management:

#### Code

<!-- prettier-ignore -->
```scss
// ----------
//  (C)olor
// ----------

$c-gray-l4: #e5e5e5; // lighter 4
$c-gray-l3: #ccc;    // lighter 3
$c-gray-l2: #b2b2b2; // lighter 2
$c-gray-l1: #999;    // lighter 1
$c-gray: #808080;    // base
$c-gray-d1: #666;    // darker 1
$c-gray-d2: #4d4d4d; // darker 2
$c-gray-d3: #333;    // darker 3
$c-gray-d4: #1a1a1a; // darker 4

// text color
.tc-gray    { color: $c-gray; }
.tc-gray-l1 { color: $c-gray-l1; }
.tc-gray-d1 { color: $c-gray-d1; }
// etc.

// background color
.bc-gray    { background-color: $c-gray; }
.bc-gray-l1 { background-color: $c-gray-l1; }
.bc-gray-d1 { background-color: $c-gray-d1; }
// etc.
```

_Note: this example uses Sass variables but can just as easily work with CSS variables_

As you can see, this works with any color, but we use a generic gray as an example. We outline our palette from the center, allowing it to go **lighter** (`l`) or **darker** (`d`) by some arbitrary number (here we go up to `4` in either direction, but you can use more or fewer if needed). We use as many colors as we need to, to capture the entire palette range for that color.

See how easy this is to use?

<!-- prettier-ignore -->
```scss
.button       { background-color: $c-blue; }
.button:hover { background-color: $c-blue-l2; } // “Ah! I can easily see this gets lighter on :hover”
```

This is predictable and easy-to-remember. And it doesn’t limit us to only 3 values in either direction, as so many other systems do: `.gray-light`, `.gray-lighter`, `.gray-lightest`, etc. While using plain English like this is easier-to-memorize, in practice we demand many more colors to work with so the “`-light`/`-lighter`/`-lightest`” system usually falls flat very quickly.

While this isn’t as “copy and paste” as the rest, it’s a good, simple system that will get you pretty far. In this system a common word like `blue` can house several related colors and not just one. For example, it’s easy to remember `.blue-l4` for a very light blue instead of having to decide between `.light-cornflower` and `.periwinkle` (but hey if silly color names are your jam don’t let me rain on your parade).

### 📐 Margin & Padding

Modify `margin-*` and `padding-*` on individual elements based on an `8px` grid. These are generated by Sass because there are too many combinations.

#### Code

<!-- prettier-ignore -->
```scss
// ----------
//  (M)argin
// ----------
@for $i from 0 to 16 {
  .ma-#{$i} { margin: #{$i * 0.5}rem; }
  .my-#{$i} { margin-top: #{$i * 0.5}rem; margin-bottom: #{$i * 0.5}rem; }
  .mx-#{$i} { margin-right: #{$i * 0.5}rem; margin-left: #{$i * 0.5}rem; }
  .mt-#{$i} { margin-top: #{$i * 0.5}rem; }
  .mr-#{$i} { margin-right: #{$i * 0.5}rem; }
  .mb-#{$i} { margin-bottom: #{$i * 0.5}rem; }
  .ml-#{$i} { margin-left: #{$i * 0.5}rem; }
}
.ma-auto { margin: auto }
.my-auto { margin-top: auto; margin-bottom: auto; }
.mx-auto { margin-left: auto; margin-right: auto; }
.mt-auto { margin-top: auto; }
.mr-auto { margin-right: auto; }
.mb-auto { margin-bottom: auto; }
.ml-auto { margin-left: auto; }

// ----------
//  (P)adding
// ----------
@for $i from 0 to 16 {
  .pa#{$i} { padding: #{$i * 0.5}rem; }
  .py#{$i} { padding-top: #{$i * 0.5}rem; padding-bottom: #{$i * 0.5}rem; }
  .px#{$i} { padding-right: #{$i * 0.5}rem; padding-left: #{$i * 0.5}rem; }
  .pt#{$i} { padding-top: #{$i * 0.5}rem; }
  .pr#{$i} { padding-right: #{$i * 0.5}rem; }
  .pb#{$i} { padding-bottom: #{$i * 0.5}rem; }
  .pl#{$i} { padding-left: #{$i * 0.5}rem; }
}
```

#### Examples

- `.mt-1`/`.mr-1`/`.mb-1`/`.ml-1`: increase `margin-top`/`-right`/`-bottom`/`-left` by 1 unit (`8px`)
- `.mx-2`: increase `margin-left` and `margin-right` by 2 units (`16px`)
- `.my-2`: increase `margin-top` and `margin-bottom` by 2 units (`16px`)
- `.ma-3`: set all margins to 3 units (`margin: 24px`)
- `.mx-auto`: set `margin-left` and `margin-right` to `auto`

_Replace `m` with `p` for padding_

Note that classes are ordered from less specific to more specific, so `class="ma-2 ml-0"` would set all margins to 2 units (`16px`) except for the left margin, which would be `0`.

### 🅰️ Font & Text

Modify font and type characteristics easily.

#### Code

<!-- prettier-ignore -->
```scss
// ----------
//  (F)ont
// ----------
.fw-100 { font-weight: 100; }
.fw-200 { font-weight: 200; }
.fw-300 { font-weight: 300; }
.fw-400 { font-weight: 400; }
.fw-500 { font-weight: 500; }
.fw-600 { font-weight: 600; }
.fw-700 { font-weight: 700; }
.fw-800 { font-weight: 800; }
.fw-900 { font-weight: 900; }

.fs-n   { font-style: normal; }
.fs-i   { font-style: italic; }

// ----------
//  (T)ext
// ----------
.ta-c   { text-align: center; }
.ta-r   { text-align: right; }
.ta-l   { text-align: left; }
.ta-j   { text-align: justify; }
.td-n   { text-decoration: none; }
.td-u   { text-decoration: underline; }
.tt-n   { text-transform: none; }
.tt-u   { text-transform: uppercase; }
```

#### Examples

- `.ta-l`/`.ta-c`/`.ta-r`/`.ta-j`: Align text to `left`/`center`/`right`/`justify` respectively
- `.td-n`/`.td-u`: Set `text-decoration` to `none` or `underline`
- `.tt-n`/`.tt-u`: Set `text-transform` to `none` or `uppercase`
- `.fw-700`: Set `font-weight` to `700` (bold)\*

💁 \* For `font-weight`, use `400` instead of `normal` and `700` instead of `bold`. Many typefaces (including variable fonts) support more than 2 weights, and using the `100`–`900` numbers lets you take advantage of the full range more easily.

## More thoughts on usage

#### Why no responsive utilities?

Those should be components’ responsibilities! Whenever you try and apply global rulesets for responsiveness across things that have separate responsibilities, you’re going to have a bad time! Utilities should only be used if they apply to all screen sizes.

_“But what if I have multiple components that do related things at the same breakpoints?”_ Then they probably shouldn’t be separate components 😉.

#### Why no `!important`?

**Utilities should always be loaded last**, but they should never take `!important` or require any higher specificity than one class name. If some of your components rely on nested styles or higher specificity, then you are already past the help of a global utility. By nesting styles, you’ve introduced contextual scoping that means that component is trying to override everything cascading to it, and it operates on a more specific level by default than a global utility. Try and avoid nesting classes if possible! It will make your components more reusable.

[css]: http://www.didoo.net/2017/10/let-there-be-peace-on-css/
[layout]: https://visly.app/blogposts/layout-isolated-components
