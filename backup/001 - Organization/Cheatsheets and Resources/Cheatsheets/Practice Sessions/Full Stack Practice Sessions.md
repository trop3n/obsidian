## CSS Declarations

```CSS
/*
CSS declaration format:
property-name: value;
*/

/* CSS declarations */
text-align: center;
color: purple;
width: 100px;
```

> In CSS, a *declaration* is the key-value pair of a CSS property and its value. CSS declarations are used to set style properties and construct rules to apply to individual or groups of elements. The property name and value are separated by a colon, and the entire declaration must be terminated by a semi-colon.

## Selector Chaining

CSS *selectors* define the set of elements to which a CSS rule set applies. For isntance, to select all `<p>` elements, the `p` selector can be used to create style rules.

## `!important` Rule

```CSS
#column-one {
  width: 200px !important;
}

.post-title {
  color:blue !important;
}
```

The CSS `!important` rule is used on declarations to override any other declarations for a property and ignore selector specificity. `!important` rules will ensure that a specific declaration always applies to the matched elements. However, generally it is good to avoid using `!important` as bad practice.

## Inline Styles

```CSS
<h2 style="text-align: center;">Centered text</h2>

<p style="color: blue; font-size: 18px;">Blue, 18-point text</p>
```

CSS styles can be directly added to HTML elements by using the `style` attribute in the element's opening tag. Each style declaration is ended with a semicolon. Styles added in this manner are known as *inline styles*. 

## Write CSS in Separate Files

```HTML
<head>
  <link href="style.css" type="text/css" rel="stylesheet">
</head>
```

CSS code can be written in its own files to keep it separate from the HTML code. The extension for CSS files is `.css`. These can be linked to an HTML file using a `<link>` tag in the `<head>` section.

## Selector Specificity

```CSS
h1#header {
  color:blue;
} /* implemented */

h1 {
  color: red;
} /* Not implemented */
```

**Specificity** is a ranking system that is used when there are multiple conflicting property values that point to the same element. When determining which rule to apply, the selector with the highest specificity wins out. The most specific selector type is the ID selector, followed by class selectors, followed by the type selectors. In this example, only `color: blue` will be implemented as it has an ID selector whereas `color: red` has a *type selector*.

## Setting Foreground Text Color in CSS

```CSS
p {
  color: #2a2aff ;
}

span {
  color : green ;
}
```

> Using the `color` property, foreground text color of an element can be set in CSS. The value can be a valid color name supported in CSS like `green` or `blue`. Also 3 digit or 6 digit color code like `#22f` or `#2n2aff` can be used to set the color.

## Opacity

```CSS
opacity: 0.5;
```

The `opacity` CSS property can be used to control the transparency of an element. The value of this property ranges from `0` (transparent) to `1` (opaque). 

## Purpose of CSS

CSS, or Cascading Style Sheets, is a language that is used in combination with HTML that customizes how HTML elements will appear. CSS can define styles and change the layout and design of a sheet.

## CSS Class Selectors

```CSS
.calender-cell {
  color: #fff;
}
```

## CSS Descendant Selector

```CSS
div p { }

section ol li { }
```

The CSS *descendant* selector combinator is used to match elements that are descended from another matched selector. They are denoted by a single space between each selector and the descended selector. They are denoted by a single space between each selector and the descended selector. All matching elements are selected regardless of the nesting level in the HTML.

## Text Align

```CSS
text-align: right;
```

The `text-align` CSS property can be used to set the text alignment of inline contents. This property can be set to these values: `left`, `right` or `center`.

## CSS ID Selectors

```CSS
#job-title {
  font-weight: bold;
}
```

The CSS ID selector *matches events based on the contents of their `id` attribute*. The valies of `id` attribute should be unique in the entire DOM. For selecting the element having `job-title` as the value of the `id` attribute, a `#` needs to be **prepended**.

## CSS Rule Sets

```CSS
h1 {
  color: blue;
  text-align: center;
}
```

A CSS rule set contains one or more selectors and one or more declarations. The selector(s), which in this example is `h1`, points to an HTML element. The declaration(s), which in this example are `color: blue` and `text-alight: center` style the element with a property and value. The rule set is the main building block of a CSS sheet. 

## Font Family

```CSS
h2 {
  font-family: Verdana;
}

#page-title {
  font-family: "Courier New";
}
```

The `font-family` CSS property is used to specify the typeface in a ruleset. Fonts must be available in the browser to display correctly, either on the computer or linked as a web font. If a font value is not available, browsers will display their default font. When using a multi-word font name, it is *best practice to wrap them in quotes*.

