---
title: HTML cheat sheet
type: page
description: HTML cheat sheet to copy and paste
topic: web dev
---

## Element Content

### HTML Boilerplate Structure
HTML is organized into a family tree structure. HTML elements can have parents, grandparents, siblings, children, grandchildren, etc.
```{html}
<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <meta http-equiv="X-UA-Compatible" content="IE=edge">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>Document</title>
</head>
<body>
   
</body>
</html>
```

### Attribute Name and Values
HTML attributes consist of a name and a value using the following syntax: name="value" and can be added to the opening tag of an HTML element to configure or change the behavior of the element.
```{html}
<elementName name="value"></elementName>
```

### Line Break Element
The `<br>` line break element will create a line break in text and is especially useful where a division of text is required, like in a postal address. The line break element requires only an opening tag and must not have a closing tag.
```{html}
A line break haiku.<br>
Poems are a great use case.<br>
Oh joy! A line break.
```

### Image Element
HTML image `<img>` elements embed images in documents. The src attribute contains the image URL and is mandatory. `<img>` is an empty element meaning it should not have a closing tag.
```{html}
<img src="image.png">
```

### Heading Elements
HTML can use six different levels of heading elements. The heading elements are ordered from the highest level `<h1>` to the lowest level `<h6>`.
```{html}
<h1>Breaking News</h1>
<h2>This is the 1st subheading</h2>
<h3>This is the 2nd subheading</h3>
...
<h6>This is the 5th subheading</h6>
```

### Paragraph Element
The `<p>` paragraph element contains and displays a block of text.
```{html}
<p>This is a block of text! Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
```

### List Item Element
The `<li>` list item element create list items inside:
- Ordered lists <ol>
- Unordered lists <ul>
```{html}
<ol>
  <li>Head east on Prince St</li>
  <li>Turn left on Elizabeth</li>
</ol>

<ul>
  <li>Cookies</li>
  <li>Milk</li>
</ul>
```

### Emphasis Element
The `<em>` element emphasizes text and browsers will usually italicize the emphasized text by default.
```{html}
<p>This <em>word</em> will be emphasized in italics.</p>
```

### Ordered List Element
The `<ol>` ordered list element creates a list of items in sequential order. Each list item appears numbered by default.
```{html}
<ol>
  <li>Preheat oven to 325 F 👩‍🍳</li>
  <li>Drop cookie dough 🍪</li>
  <li>Bake for 15 min ⏰</li>
</ol>
```

### Div Element
The `<div>` element is used as a container (box-like) that divides an HTML document into sections and is short for “division. `<div>` elements can contain flow content such as headings, paragraphs, links, images, etc.

```{html}
<div>
  <h1>A section of grouped elements</h1>
  <p>Here’s some text for the section</p>
</div>
<div>
  <h1>Second section of grouped elements</h1>
  <p>Here’s some text</p>
</div>
```