# Home Page

Now, we're going to focus on the home page of the site. 

## Examining the Layout

### Container to control width/centering
The first thing to notice is that the main content should be contained within the same container that the header is using to control the width and center the content.

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-living-social-img2.png)

### Two main columns

The next thing to notice is that there are two main columns of content.

This indicates that we should set up a main structure area on the left, and a sidebar structure on the right.

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-living-social-img3.png)

Then, inside those areas, there are more components. The color-coding indicates related items. 
* **light-yellow**: unique part of the content. the layout is unique. it stands out.
* **blue**: three items that repeat themselves in structure. just the content is changing.
* **orange**: another set of repeating items.

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-living-social-img4.png)

## Creating the main layout HTML markup

Since we haven't done a larger site like this yet, let's walk through the starting markup together. We're just going to create the HTML elements/classes without the content (text/images). This will allow us to more easily see the overall structure.

After we're done, and ready to start styling, we can replace our version with a completed version that contains all of the content.

### Top-level Sections

First, we'll just create the large sections:
* **div.container**: the main container to control the width/centering.
  * **main**: semantic element to indicate main content. 
  * **aside**: semantic element to indicate supplemental, or secondary content.
* **footer**: basic footer, the content will just be center-aligned.

Using these semantic elements is really important for assistive technologies.

```html
 <!-- header section goes here -->

<div class="container">
    <main></main>
    <aside></aside>
</div>

<footer>
    <p></p>
    <p></p>
</footer>       
```

That is all that is needed for the main content. We have the two columns that we can orient using flex.

### Main Article Section
Within the `<main>` section, we are going to have a series of `<article>` elements. Again, we're using semantic elements whenever possible.

```css
   <main>
    <article class="article-featured"></article>
    <article class="article-recent"></article>
    <article class="article-recent"></article>
    <article class="article-recent"></article>
   </main>
```

If you look at the articles, the first one is the featured article and the layout is a little bit different than the other three.

To handle this, we'll give the first `<article>` a unique class, `article-featured` and the others will all share a class `article-recent`.

### Article Structure
#### Components within each article
* Image
* Info (date/comments)
* Title
* Paragraph
* Link to continue reading

#### Featured article structure

```html
<article class="article-featured">
    <img src="" alt="" class="article-image">
    <p class="article-info"></p>
    <h2 class="article-title"></h2>
     <p class="article-body"></p>
    <a href="#" class="article-read-more"></a>
</article>
```

#### Recent Article Structure

```html
  <article class="article-recent">
    <div class="article-recent-main">
        <h2 class="article-title"></h2>
        <p class="article-body"></p>
        <a href="#" class="article-read-more"></a>
    </div>
    <div class="article-recent-secondary">
        <img src="" alt="" class="article-image">
        <p class="article-info"></p>
    </div>
</article>
```

#### Differences
The main difference between the two types of articles is that the recent articles have two sections that need to be positioned horizontally. This means that each section needs to be wrapped in its own div so that it can be positioned with flexbox.

#### Naming Conventions
Notice the naming conventions. The class names on the `<article>` elements all start with `article-`. That's not a requirement, but a convention many web developers use to build a nice pattern to be able to track where styles are located within the document.

In addition, there are classes on each element. This is often a pattern web developers follow so that they can plan ahead for the eventuality that they will need to style the element. 

If you work in phases, first creating the markup, and then the CSS, then it makes sense to add styles to all of the classes that are likely to need styles from the start.

### `<aside>` Structure

The `<aside>` element structure is pretty straight foward. We've got the upper section, followed by the lower section, with three repeating structures.

Becaues the upper and lower sections share some common styling, we'll create a single style `sidebar-widget` for the container for both of these.

Then, we can create the elements within the widgets, trying to re-use styles where they are similar. For example:
* the `<h2>` element in both will be similar, and is given a shared style `widget-title`.
* the `<img>` elements share the style `widget-image`.
* and the repeating section for each post share a repeating set of styles.

```html
<aside>              
  <div class="sidebar-widget">
    <img src="#" alt="" class="widget-image">
      <h2 class="widget-title"></h2>
      <p class="widget-body"></p>
  </div>
  
  <div class="sidebar-widget">
      <h2 class="widget-title"></h2>
      <div class="widget-recent-post">
          <img src="" alt="" class="widget-image">
          <h3 class="widget-recent-post-title"></div>
      </div>
      <div class="widget-recent-post">
          <img src="" alt="" class="widget-image">
          <h3 class="widget-recent-post-title"></div>
      </div>
      <div class="widget-recent-post">
          <img src="" alt="" class="widget-image">
          <h3 class="widget-recent-post-title"></div>
      </div>
  </div>
</aside>
```

## Styling

### Start with completed markup
Now, that we've walked through creating the markup for this layout, we need to add the real content. 
 
Look in the full-desktop-markup.html and copy the content and replace the content in index.html with it so that you have all of the text/images supplied as a starting point for adding the styling.

### Specs

Remember that you have access to a more detailed Adobe XD spec for this project [here](https://xd.adobe.com/spec/75d448ea-569a-4b7e-721b-9bbd3b2b97b9-03e5/grid/).

Here is a shortened spec to use as well.

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-living-social-img5.png)


### Typography

There are usually a lot of shared, or inherited styles that we want to setup for the entire page.

Let's start with the article-title. It shares the font, font-weight and text color with the `<h1>, <h2>, and <h3>` elements on the page. So we should start by re-factoring the common styles.

The .article-title is an `<h2>` elements, so we should use the more common element to target the style.

Also, we can setup the default font-size on the `<body>` element so that it is inherited for the entire document.

```css

body {
  font-size: 18px;
  font-weight: 300;
}

h1, 
h2,
h3 {
    font-family: 'Lora', serif;
    font-weight: 400;
    color: #143774;
}

.article-title {
      font-size: 24px;
}

```

Next, we can focus on the typography for the article link to read more and the article info.

```css
.article-read-more,
.article-info
{
    font-size: 12px;
}

.article-read-more {
    color: #1792d2; 
    text-decoration:none;
    font-weight:700;
}

.article-read-more:hover,
.article-read-more:focus {
    color: #143774;
    text-decoration: underline;
}

a {
    color: #1792d2;
}

a:hover,
a:focus {
    color: #143774;
}

strong {
    font-weight: 700;
}

```

#### Adding a font-weight to Google Font

You can add an additional font to a Google Font that you have already linked to in your HTML document. Just add the new font to the existing URL where it specifies the fonts.

In the markup below, there are currently two sizes, 400, 700. You could add an additional one to the list.

```html
    <head>
        <link href="https://fonts.googleapis.com/css?family=Lora|Ubuntu:400,700&display=swap" rel="stylesheet">
        <link rel="stylesheet" href="css/styles.css">
    </head>
  ```

### Big Picture Layout

We need to break down the larger container into two columns.  We don't want to add the flex to the container class because its being used in the header as well. We want it to remain generic for the purpose of setting the width/centering the content across the sections.

Looking at the `container-flex` container class in the header, it is already serving the purpose of controlling the layout of its child elements with flex. We can use it in both places.

Now, the main content area and the aside are horizontal.


```html
<header>
  <div class="container container-flex">            
  </div> 
</header>
        
<div class="container container-flex">
    <main role="main">
    </main>
    <aside class="aside">
    </aside>
</div>
```

### Images

Images are a bit quirky and the following css is almost a standard for every project.

```css
img {
    max-width: 100%;
    display: block;
}
```

We've seen the max-width used for images before. It's needed to make the images fill the width of its parent container, instead of its native width.

The `display:block` is needed because sometimes there is a little space on the bottom of an image that is due to it being an inline element (not going to go into the reason why now, just that this fixes it).

### Column Widths

We'll leave 2% to add some space between the columns.

```css
main {
    width: 68%;
}

aside {
    width: 30%;
}
```

### Switching to Mobile-First

Typically it is easier to start with a mobile-first approach. We didn't for this site, but we're going to switch to a mobile-first design now.

This is our current @media query for controlling the flex layout.

```css
.container-flex {
    display: flex;
    justify-content: space-between;
}

header {
    background: #f8f8f8;
    padding: 32px 0;
}

@media (max-width: 675px) {
    .container-flex {
        flex-direction: column;
    }
    
    header {
        text-align: center;
    }
}
```

We're going to switch to making it mobile first by moving the current @media queries into the default case and then adding the styles necessary to support the desktop version.

Remember, we need to change the max-width to min-width.

```css
.container-flex {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

header {
    background: #f8f8f8;
    padding: 32px 0;
    text-align: center;
}

@media (min-width: 675px) {
    .container-flex {
        flex-direction: row;
    }
    header {
        text-align:left;
    }
    main {
        width: 68%;
    }

    aside {
        width: 30%;
    }
}

```

### Feature Article Styling

We need to do some cleanup for the spacing.

Start with the space between the date and the comments in the info element.

```css
.article-info {
    margin: 32px 0;
}
```
Next, the line after the article

```css
.article-featured {
    border-bottom: #707070 1px solid;
    padding-bottom: 16px;
    margin-bottom:48px;
}
```

### Ordering the flex elements

The page currently  looks like the one on the left, but we want it to look like the one on the right.

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-living-social-img7.png)

To change the order of the flex children, we do it on the child elements by adding the order property. They will be positioned from lowest to highest value in the direction of the main axis.

With the change below, the secondary content will be displayed first.

```css
.article-recent {
    display: flex;
    flex-direction: column;
    margin-bottom: 32px;
}

.article-recent-main {
    order: 2;
}

.article-recent-secondary {
    order: 1;
}

```

Also, add the margin-top:0  to get rid of the space above on the headings.


```css 
h1, 
h2,
h3 {
    margin-top: 0;
}
```
Also, add a margin-bottom on the `<header>` element.
```css
header {
    background: #f8f8f8;
    padding: 36px 0;
    text-align: center;
    margin-bottom:36px;
}
```

### Making Articles Responsive

When the screen width enlarges, we want the articles to display with two columns and style them a bit.

```css
@media (min-width: 675px) {
    .article-recent {
        flex-direction: row;
        justify-content: space-between;
    }
    
    .article-recent-main {
        width: 68%;
    }
    
    .article-recent-secondary {
        width: 30%;
    }
    
    .article-featured {
        display: flex;
        flex-direction: column;
    }
}
```

#### Image Cropping with object-fit property
Another issues is that when the screen gets small the images are getting really small. There is a relatively new feature in CSS we can use to address this.

It's the object-fit property. It works similarly to background-image, in how you can size and position an image, but it can be applied to an img element, instead of a background.

Currently the image just re-sizes in proportion to thr parent container.

But if we use the object-fit:cover, in combination with a hard-coded width, it will crop the image instead of stretching it.

Using object-position:left will keep the left-size of the image, instead of the center, which will help in the case of the third image, that has most of the content on the left-side of the image.

```css
    .article-image {
        width: 100%;
        height: 400px;
        object-fit: cover;
        object-position: left;
    }
```

#### `<aside>` widget title styling

```css
.widget-title,
.widget-recent-post-title {
    font-size: 16px;
}

.widget-title {
    font-family: 'Ubuntu', sans-serif;
    font-weight: 700;
}

```

#### Lines separating widgets

```css
.widget-recent-post {
    display: flex;
    flex-direction: column;
    border-bottom: 1px solid #707070;
    margin-bottom: 16px;
}
```
#### Removing the last line using a pseudo-class selector

```css
.widget-recent-post:last-child {
    border: 0;
    margin: 0;
}
```

### The Footer
```css
footer {
    background:#143774;
    color: white;
    text-align:center;
    padding: 48px 0;
}
```

### Recent Posts Page

This page is very similar to the Home page. It just doesn't have the featured article at the top.

The one thing we do need to do is update the links at the top of the page in both the home and recent-posts pages.


### About Me Page

#### Adjusting the Image Size
We can use the same technique we used for the article images to make the image fit the size of the page better.
```css
.image-full {
    max-height: 300px;
    width: 100%;
    object-fit: cover;
    margin-bottom: 24px;
}
```

### h3 headers have override colors 

```css
h3 {
    color: #1792d2;
}

.widget-recent-post-title {
    color: #143774;
}

```