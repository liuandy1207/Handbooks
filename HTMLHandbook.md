# <img src = https://www.w3.org/html/logo/downloads/HTML5_Logo_512.png width=40px> HTML5 Handbook

## Table of Contents
> ### [Basics](#basics) <br>
>> [Commenting](#commenting) <br>
>> [Setup](#setup) <br>
>> [Elements and Attributes](#elements-and-attributes) <br>
>>> [Empty Elements](#empty-elements) <br>
>>
>> [Headings and Paragraphs](#headings-and-paragraphs) <br>
>> [Links](#links) <br>
>> [Images](#images) <br> 




<br><br><br><br><br><br>
<hr> 

## Basics
- HTML stands for Hyper Text Markup Language.
- HTML describes the structure of a webpage.
- 

### Commenting
```html
<!-- COMMENT -->
```

### Setup
- `<!DOCTYPE html>` must appear only once at the top of the HTML document, before any HTML elements. 
```html
<!DOCTYPE html>
<html>
  ...
</html>
````

### Elements and Attributes
- HTML consists of elements define by a start tag, content, and an end tag.
- An **attribute** is a piece of additional information about an element.
- Attributes typically come as `NAME="VALUE"` pairs.
- Attributes are specified in the start tag. 

#### Empty Elements
- An **empty element** is an element with no content.
```html
<!-- Line Break -->
<br>
```

### Headings and Paragraphs
- Heading 1 is the most important and heading 6 is the least important.
```html
<h1> HEADING 1 </h1>
<h2> HEADING 2 </h2>
<h3> HEADING 3 </h3>
<h4> HEADING 4 </h4>
<h5> HEADING 5 </h5>
<h6> HEADING 6 </h6>

<p> PARAGRAPH </p>
```


### Links
```html
<a href="LINK_TO_SOMETHING"> LINK_TEXT </a>
```

### Images
```html
<img src="LINK_TO_IMAGE" alt="ALT_TEXT">

<!-- Specify the dimensions of an image? -->
<img src="LINK_TO_IMAGE" alt="ALT_TEXT" width="WIDTH">
<img src="LINK_TO_IMAGE" alt="ALT_TEXT" height="HEIGHT">
```










