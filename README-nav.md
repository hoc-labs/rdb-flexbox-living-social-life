# Living the Social Life Web Site

In this project we're going to build a site that has three pages. We can see how to share structure and styles across pages.

In most sites, these common elements, often called components, would be programatically generated. But our current understanding of web development is limited to building static pages, so we'll have to build each one individually.

Included in the project is the full HTML for the about-me.html and the recent-posts.html pages. The index.html, or home page, is the main page that we will be working on. 

We'll just need to hook up the navigation links and a few minor styling items on the other two pages.

So let's get started...

## Web Specifications
For this project, we're going to introduce another way that web developers often get design specifications. In this case, the specifications will be in Adobe XD.

[Here is the link to the spec.](https://xd.adobe.com/spec/75d448ea-569a-4b7e-721b-9bbd3b2b97b9-03e5/grid/)

Here are the three layouts for the desktop version. It's a little hard to see the detail here, so refer to the Adobe spec when needed.

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-living-social-img1.png)


## Site Navigation

Site navigation is usually built by taking advantage of the nesting structure of lists: specifically unordered lists and using flexbox to position the list elements.

Additionally, the semantic element `<nav>` usually wraps the list to assist in alerting assistive technologies in locating the site navigation section.

Here's what it looks like:

```markup
<nav>
  <ul>
    <li><a href="home.html">home</a></li>
    <li><a href="about-me.html">about me</a></li>
    <li><a href="recent-posts.html">recent posts</a></li>
  </ul>
</nav>
```

### Navigation Specs

**Note** 
* 1rem = 16px, which is the default font-size for the entire page.
* the fonts in the spec have already been included in the HTML file.

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img2.png)


### Navigation Layout
We're going to be creating a responsive nav bar. We'll start with the one on top, then make the one it the middle, which is the full desktop version. Last, we'll make the one on the bottom, which is the mobile version.

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img1.png)

### Visualizing Element Layout

Here is the big-picture outline of the grouping of the elements in the nav bar.

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img3.png)

**header**: the outer container. this will be the header of the larger page eventually. The semantic element, `<header>` should be used.

**site-title**: this contains both the title and the subtitle. they need to be grouped together in a div, such as `<div class="site-title">`, so that they move as a group.

**nav**: the `<nav>` element containing the site navigation.
  

### Start with the HTML markup
Create the HTML markup for this navigation.
When you are done, the page should look like this:

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img10.png)

See the solution in the navigation-solution folder if you need help.

### CSS Compound Selectors

This is a good place where we can use compound selectors, since the structure is very predictable and unlikely to change. It allows us to avoid having to put CSS classes on each of the descendent elements within the `<nav>`container.

```css
 nav ul {
     
 }
 
 nav li {
     
 }
 
 nav a {
     
 }
 
 nav a:hover,
 nav a:focus {
     
 }
 ```
If you are going to use compound selectors, keep them really simple. You don't need to include the full path to the target element, such as:
```css
nav ul li a {

}
```

### Styling the list to make it a navigation bar

The following tasks need to be completed to turn the unordered list into a navigation bar.
* Remove the dots.
* Change the `<li>` items to be horizontal/inline.
* Space the nav elements

Try doing these tasks on your own, and then if you run into trouble follow the step-by-step instructions below.


#### Steps to convert the unordered list into a navigation bar.
I've temporily added some borders so we can see what needs to be changed.

```css
nav ul {
  border: 1px solid magenta
}

nav li {
  border: 2px dotted orange;
}

nav a {
  border: 3px solid green;
}
```
![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img11.png)

* pink box is the `<ul>`
* orange box is the `<li>`
* green box is the `<a>`

We can see the the `<ul>` and the `<li>` elements are block elements, whereas the `<a>` elements are inline. This means that, even though the text of the links are really short, the `<li>` is stretching the full width.

Notice the big empty space on the left. That's because of the way the `<ul>` element is set up to give room for the dots for each `<li>` element.  

#### Remove the dots.

* the following style will remove the dots.

```css
nav ul {
  list-style: none;
}
```

The page should now look like this:

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img12.png)

#### Change the `<li>` items to be horizontal/inline.

How can we do this? We can use flex on the `<ul>` element.
```css
nav ul {
  list-style:none;
  display:flex;
}
```

With that change, the page should look like this:
![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img13.png)

#### Space the nav elements
We can use justify-content to do this. Let's start with trying space-between.
```css
nav ul {
  list-style:none;
  display:flex;
  justify-content: space-between;
}
```
![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img14.png)

The `<ul>` element has a default padding that is causing that extra padding you see on the left. So, we need to remove that padding to allow the justify-content to spread correctly to both edges.

```css
nav ul {
  list-style:none;
  display:flex;
  justify-content: space-between;
  padding:0;
}
```
![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img15.png)

There is a problem with using space-between for the justify-content. As the screen width increases, they are getting too spread out. 

A better choice is to use center. But then we need to add some space between the elements.

```css
nav ul {
  list-style:none;
  display:flex;
  justify-content: center;
  padding:0;
}

nav ul li {
  margin: 0 16px;
}
```

Now, the page should look like this:

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img16.png)


### General Styling

The following tasks need to be completed to turn style the navigation bar.
* center the header element content.
* remove the margin on the body element.
* set up the typography for `<h1>` and `<p class="subtitle>` and `<a>` nav links.
  * font-family, font-size, font-weight, text color
* style the header
  * background color
  * padding
  * remove some of the space between the title and the subtitle (use the inspector to help)
* style the nav link elements
  * remove the underline
  * set the hover,focus color
  * transform the link text to be capitalized
  * add an underline to the home link to indicate that it is the current page.


Try doing these tasks on your own, and then if you run into trouble, look at the detailed instructions for particular steps below or in the navigation-solution folder for the full source code.

#### Center the header
Unlike the `<li>` items, which are not block elements when they are within the flex container, the header elements are block elements, and therefore we can use `text-align:center` to center that content.

```css
header {
  text-align:center;
}
```

Now, the page should look like this:

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img17.png)

#### Remove the body margin
As a general rule, it is a good idea to remove the margin on the body element.

You can see the issue if you temporarily set the background-color on the header element to a darker color:

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img6.png)

To remove it, set the margin on the body element to 0.

```css
body {
  margin:0;
}
```

#### Remove some of the space between the title and the sub title. 

This one is a little tricky. Look in the inspector to see what is going on when you try to adjust the margins.

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img7.png)

It's because of the collapsing margins. The margins of the element above and below are still contributing to the space. So you wil need to set the margin-bottom:0 on the `<h1>` element above.

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img9.png)

#### Add underline to nav item
This is a common practice to underline the active link (the page you are on). The following technique can be used to do this:
* create a style, named `current-page`, that will indicate that a link is the active link.
* add that style to the home link.
* on the `current-page` style, create a border and some padding on the bottom to create the underline.

```css
.current-page {
  border-bottom: 1px solid #707070;
}
```

**Note:** In general, it's a good idea to add some padding around the `<a>` elements, especially for mobile devices, so that there is some space around the text that will be in cluded in the area that interacts with the link.

```css
nav a {
  text-decoration: none;
  color: #707070;
  font-weight: 700;
  text-transform: capitalize;
  padding: 4px 0;
}
```

With those changes, that wraps up the general styling for the navigation. And here is what it looks like:

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img18.png)

### Styling the Navigation - Layout 2

We're now going to move on to working on the second model, which will be used for the full desktop view.

This is a common layout, where you have some content, or a logo, on the left, and the navigation on the right.

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img19.png)

#### Layout
Here's the basic layout/structure for the elements for this view.

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img20.png)

The first step is that we need a container element to prevent the content from stretching all the way across the screen. 

This is the same container class that we have used multiple times before, that just sets the width, and margin, and max-width to get the content to be centered.

* add the container element around the content within the `<header>` element and style it as we have in the past with:
  * width
  * margin
  * max-width


### Using Flex to distribute the header elements.

We have a container class, but we want this class to remain generic so that it can be re-used for the rest of the page when we add that.  

So we need to add a new class that will allow us to set the header elements to flex to arrange the child elements.

* create a modifier style, named `container-flex`, or something similar, and add it to the same element that has the container class.
* use justify content to spread the two child elements across the top.

The page should look like this when you are done.

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img21.png)

### Fixing the margins for this layout

I've added a border to demonstrate an issue we need to fix. We added a margin to add space around each of the nav items when they were centered. Now that they are pushed to the right, that margin is causing a problem. So, we need to modfiy the margin style a bit. 

**Note:** We'll need to fix it for both layouts when we handle the responsive layout.

before: 
```css
nav li {
  margin: 0 16px;
}
```

after: 
```css
nav li {
  margin-left: 32px;
}
```

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img22.png)

### Left-aligning content
* For this layout, we want the content on the left, to be left-aligned. 
* We also want the subtitle to be uppercase.

It should now look like this:

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img23.png)


### Making it Responsive

Now we're going to add media queries to make the navigation responsive.

We'll use a breakpoint of 675px.

See if you can create the media query to get the screen to look like the following:

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img9.png)

Remember, you need to re-adjust the margin when the nav items are centered and center the header content.

### Mobile Layout

Finally, 
* we want to change the nav elements to stack and centered when on mobile
* we also want to add a little more space between the nav elements in the stacked version.

It should look like this:

![](https://raw.githubusercontent.com/hoc-labs/images/main/rdb-flexbox-nav-img24.png)

