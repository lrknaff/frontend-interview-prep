##HTML/CSS
####If you have two elements inside of an outer containing element, one with float: left; and other with float: right;, how can you ensure that the containing element expands around the floated elements and does not collapse?
* on the containing element => `overflow: auto;`
* using a clearfix

  ```
  .clearfix:after {
   content: ".";
   visibility: hidden;
   display: block;
   height: 0;
   clear: both;
}
```

####What are Media Queries?
* A CSS3 Module that allows content rendering to adapt to conditions such as screen resolutions.
* Used in *Adaptive Page Layouts*
 	- An adaptive layout uses CSS media queries to detect the width of the browser and make layout adjustments accordingly. Unlike liquid layouts, adaptive layouts use fixed units like pixels to define widths. They behave like a series of static layouts defined by specific media queries.
* *Responsive Page Layouts* are best
	- A true responsive page layout combines the best parts of a liquid layout and an adaptive layout to create the best experience for your users as they move between devices and screen sizes. By using both relative units and media queries, a responsive site allows us to transition through screen sizes seamlessly and effortlessly.

####What are the positives and negatives of using a CSS pre-processor?
#####positives:
* ability to nest, define variables and mixins, use of mathematical operations, ability to join multiple files into one file

#####negatives:
* difficulty tracking file size, maintenance and updating, difficulties debugging

####What is a pseudo class? What are they used for?
* Pseudo classes are similar to classes, but no explicitly defined in the markup.
* Used for addition effects to selected HTML element.
  - i.e. link colors, hover actions, etc
* Syntax: selector:pseudo-class. (a:link, a:visited)

####Explain the 3 main ways to apply CSS styles to a Web page:
* Inline
  - use very sparingly. Done by inserting a 'style' attribute inside an HTML element.
* Embedded/Internal
  - `<style>` tag in head of HTML document
* Linked/External
  - CSS is in an external .css file and linked in HTML document with `<link>` tags

####What is grouping?
* Grouping allows you to apply the same style to multiple elements with a single declaration using a selector list, separated by commas.
* Enhances memory usage and readability


####What are pseudo-elements and how are they made?
* Made by using a double colon (::) followed by the name of the pseudo element
* Used to add special effects to some selectors.
  - Can only be applied to block level elements
* Examples (::first_line, ::first_letter, ::before, ::after)

####What is the difference between inline and block elements?
* **Block** elements take up the full width available with a line break before and after it. `<h1>, <p>, <li>, and <div>`
* **Inline** elements one take up as much width as necessary, cannot accept width and height values and do not force line breaks. `<a>, <span>`

####What is the z-index? How is it used?
* The z-index specifies the stacking order of positioned elements.
* Lowest z-index will be on the bottom and highest on the top
* It can take the following values:
 - **Auto**: Sets stack order equal to it's parents
 - **Number**: Orders the stack order
 - **Initial**: Sets to default value of 0
 - **Inherit**: Inherits from its parent element


####Why shouldn't I use fixed sized fonts?
* They often show up incorrectly on the user end which will prohibit responsiveness
* Relative sizing allows fonts to be kept proportionate in their relationships to each other === more flexibility.

####What are some of the new features of CSS3?
* Box Model
* Web fonts
* Rounded corners
* Border Images
* Box Shadows, Text Shadows
* Transform property
* Multi-column layout

####Why and how are shorthand properties used?
* Used to improve page load times/reduce file size
* Accomplished by listing the property values on a single line
`body {
    background: #00ff00 url("smiley.gif") no-repeat fixed center;
}`

####What's the difference between inline, inline-block and block?
* **Block:** Has some whitespace above and below it and does not tolerate HTML elements next to it. `<div>, <h1>, <p>, <form>`
* **Inline:** Does not start on a new line and only takes up as much width as necessary. Respects left & right margins and padding but **not** top and bottom `<span>, <a>, <img>`
* **Inline-Block:** Placed as an inline element but behaves as a block element. Respect top and bottom, width and height.

####What are `data` attributes good for?
* [Attribute Selectors](https://css-tricks.com/almanac/selectors/a/attribute/)
* [Using Data Attributes](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes)
* data-* attributes allow us to store extra information on standard, semantic HTML elements.
* You can use *any* of an element's attributes as selectors
* Syntax:

	```
	<article
  id="electriccars"
  data-columns="3"
  data-index-number="12314"
  data-parent="cars">
...
</article>
```
* Can use *attribute selectors* in CSS to change styles

	```
	article[data-columns='3'] {
	  width: 400px;
	}
	```
* There are 7 different types of attribute selectors:

	```
		[data-value] {
	  /* Attribute exists */
	}

	[data-value="foo"] {
	  /* Attribute has this exact value */
	}

	[data-value*="foo"] {
	  /* Attribute value contains this value somewhere in it */
	}

	[data-value~="foo"] {
	  /* Attribute has this value in a space-separated list somewhere */
	}

	[data-value^="foo"] {
	  /* Attribute value starts with this */
	}

	[data-value=|"foo"] {
	  /* Attribute value has this in a dash-separated list somewhere */
	}

	[data-value$="foo"] {
	  /* Attribute value ends with this */
	}
	```

####What is ARIA? How does it aide in accessibility?
* Accessibility in Web development means enabling as many people as possible to use Web sites, even when those people’s abilities are limited in some way.
* **ARIA**: Accessible Rich Internet Application
  - **Semantic HTML**: Use elements such as `<nav>, <button>, <header>, <aside>` that help clarify what part of html page someone is focused on.
  - **Alt Tags**: Use on images. Be verbose. `<img src="mountain.jpg" alt="The cascade mountains at sunset in January" />`
  - **ARIA Roles**: Define the purpose of an element. Each element can only have one ARIA role at a time

####What is the box model?
* Each element is a rectangular box. CSS leverages “the box model” to control layout and design. An HTML element is comprised of its content and the margins, borders, padding surrounding it. Boxes are “stacked” in the order they appear in your HTML. You can stack them horizontally, vertically, and in the z-plane
![Box Model](http://frontend.turing.io/assets/images/box-model.jpg)

####What's the difference between a relative, fixed, absolute and statically positioned element?
* [CSS](http://frontend.turing.io/lessons/module-1/css-1.html)
* **Relative**: A relatively positioned element preserves its space. The adjacent elements aren’t repositioned to occupy the reserved space for this element. However, the offsets of this element don’t occupy space. They’re completely ignored from the other elements, and hence that may causes elements to overlap each other.
* **Absolute**: An absolutely positioned element is completely removed from the normal flow. The adjacent sibling elements occupy its space.
* **Fixed**: A fixed positioned element (subcategory of the absolute positioning) is positioned relative to the viewport. It will stick in place despite any scrolling or resizing of the viewport
* **Static**: HTML elements are positioned static by default. Static positioned elements are not affected by the top, bottom, left, and right properties.

####What are the different ways to visually hide content (and make it available only for screen readers)?
* `text-indent: -1000px` This will allow the content to be visible off screen and thus accessible to screen readers.
* `clip: rect(1px, 1px, 1px, 1px)` Clips content that will not fit in a 1px area
* `position:absolute;
left:-10000px; overflow:hidden;` : Absolutely position element off screen
