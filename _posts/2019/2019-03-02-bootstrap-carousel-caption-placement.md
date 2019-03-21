---
layout: post
title: Bootstrap 4 carousel caption placement
date: '2019-03-02 7:09:00 -05:00'
tags: bootstrap
---

The standard Bootstrap carousel component is great and for most scenarios the default styling and position of the caption and indicators is fine. However, there are times when you want the caption and indicators to be shown below the image instead of being overlayed on it.

In Bootstrap 3, this wasn't easy to do. There are a lot of examples out there on how to do this. For Bootstrap 4, things are noticeably easier. 

We're going to start with the [example](https://getbootstrap.com/docs/4.3/components/carousel/#with-captions) in the Bootstrap documentation.

{% include post/image.html image-file="2019-03-02-19-06-05-carousel-bootstrap.png" alt="Bootstrap carousel with caption and indicators" %}

To move the placement of the caption, we need a very simple CSS rule:

```css
.carousel-caption {
    position: relative;
    left: 0;
    top: 0;
}
```

Unfortunately, this gives us white text on a white background. We can fix this by adding one of the standard background color utility classes. For our example, we're going to add the `bg-dark` class. 

{% include post/image.html image-file="2019-03-02-19-41-24-carousel-bootstrap.png" alt="Bootstrap carousel with caption and indicators" %}

If we want to adjust the spacing around the indicators, we can add `mb-4` to the carousel caption and `my-4` to the carousel indicators.

{% include post/image.html image-file="2019-03-02-19-52-03-carousel-bootstrap.png" alt="Bootstrap carousel with caption and indicators" %}

That's it. We added a single CSS rule, added `bg-dark mb-4` utility classes to the carousel caption and added the `my-4` utiity class to the carousel indicators. Our updated HTML from the original Bootstrap example now looks like

```html
<div class="bd-example">
  <div id="carouselExampleCaptions" class="carousel slide" data-ride="carousel">
    <ol class="carousel-indicators my-4">
      <li data-target="#carouselExampleCaptions" data-slide-to="0" class="active"></li>
      <li data-target="#carouselExampleCaptions" data-slide-to="1"></li>
      <li data-target="#carouselExampleCaptions" data-slide-to="2"></li>
    </ol>
    <div class="carousel-inner">
      <div class="carousel-item active">
        <img src="..." class="d-block w-100" alt="...">
        <div class="carousel-caption d-none d-md-block bg-dark mb-4">
          <h5>First slide label</h5>
          <p>Nulla vitae elit libero, a pharetra augue mollis interdum.</p>
        </div>
      </div>
      <div class="carousel-item">
        <img src="..." class="d-block w-100" alt="...">
        <div class="carousel-caption d-none d-md-block bg-dark mb-4">
          <h5>Second slide label</h5>
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
        </div>
      </div>
      <div class="carousel-item">
        <img src="..." class="d-block w-100" alt="...">
        <div class="carousel-caption d-none d-md-block bg-dark mb-4">
          <h5>Third slide label</h5>
          <p>Praesent commodo cursus magna, vel scelerisque nisl consectetur.</p>
        </div>
      </div>
    </div>
    <a class="carousel-control-prev" href="#carouselExampleCaptions" role="button" data-slide="prev">
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="sr-only">Previous</span>
    </a>
    <a class="carousel-control-next" href="#carouselExampleCaptions" role="button" data-slide="next">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="sr-only">Next</span>
    </a>
  </div>
</div>
```

> Let's take another look at the caption. The example for the caption looks like
>
>```html
><div class="carousel-caption d-none d-md-block">
>    <h5>First slide label</h5>
>    <p>Nulla vitae elit libero, a pharetra augue mollis interdum.</p>
></div>
>```
>
> The `d-none d-md-block` classes hide the caption by default and then only dispay it on medium sized devices and up. If we want the caption to always be visible, replace those classes with `d-sm-block`. You might also want to add the following media query CSS to reduce the font size slightly.
>
> ```css
> @media only screen and (max-width: 576px) {
>     .carousel-caption {
>         h5 {
>             font-size: 1rem;
>         }
>     }
> }
>```
