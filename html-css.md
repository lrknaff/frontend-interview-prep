##HTML/CSS
####If you have two elements inside of an outer containing element, one with float: left; and other with float: right;, how can you ensure that the containing element exapands around the floated elements and does not collapse?
* on the containing element => `overflow: auto;`
* using a clearfix

  ```.clearfix:after { 
   content: "."; 
   visibility: hidden; 
   display: block; 
   height: 0; 
   clear: both;
}```

####What are Media Queries?
* A CSS3 Module that allows content rendering to adapt to conditions such as screen resolutions

####positives and negatives of using a CSS pre-processor?
#####positives:
* ablility to nest, define variables and mixins, use of mathematical operations, ability to join multiple files into one file

#####negatives:
* difficulty tracking file size, maintenance and updating, difficulties debugging

####What is a pseudo class? What are they used for?
* Pseudo classes are similar to classes, but no explicitly definted in the markup.
* Used for addition effects to selected HTML element.
  - i.e. link colors, hover actions, etc
* Syntax: selector:pseudo-class. (a:link, a:visited)

####Explain the 3 main ways to apply CSS styles to a Web page:
* Inline
  - use very sparingly. Done by inserting a 'style' attribut inside an HTML element.
* Embedded/Internal
  - `<style>` tag in head of HTML document
* Linked/External
  - CSS is in an external .css file and linked in HTML document with `<link>` tags

####What is grouping?
* Grouping allows you to apply the same style to multiple elements with a single declaration using a selector list, serparated by commas.
* Enhances memory usage and readability 


####What are pseudo-elements and how are they made?
* Made by using a double colon (::) followed by tht ename of the pseudo element
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
* Relative sizing allows fonts to be kept proportionate in their relationships to eachother === more flexibility.

####What are some of the new freatures of CSS3?
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

####What's the difference between inline, inline-block and block?
* **Block:** Has some whitespace above and below it and does not tolerate HTML elements next to it. `<div>, <h1>, <p>, <form>`
* **Inline:** Does not start on a new line and only takes up as much width as necessary. Respects left & right margins and padding but **not** top and bottom `<span>, <a>, <img>`
* **Inline-Block:** Placed as an inline element but behaves as a block element. Respect top and bottom, width and height.