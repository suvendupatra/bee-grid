---
layout: docs
title: Customize
description: You can use Sass variables and mixins to create custom, and responsive layouts
redirect_from:
  - /docs/
  - /docs/{{site.current_version}}/
  - /docs/{{site.current_version}}/introduction/
  - /docs/introduction/
---

# Sass variables

Sass variables defines grid gap, the number of columns and the layouts while media query determine its behavior. Beegrid framework use these to generate all the grid classes.

{% highlight scss %}
$grid-columns-number: 12 !default;
$grid-item-padding:   1rem !default;

// Grid breakpoints
//
// Define the maximum dimensions at which your layout will change,
// adapting to different screen sizes, for use in media queries.
$grid-breakpoints: (
  xs: 0px,
  sm: 480px,
  md: 960px,
  lg: 1280px,
  xl: 1440px
) !default;

// Grid widths
$grid-widths: (
  sm: 640px,
  md: 1024px,
  lg: 1280px,
  xl: 1440px
) !default;

// Define the grid gap dimensions at which your layout will change,
// adapting to different screen sizes
$grid-breakpoints-gap: (
  xl: 28px,
  lg: 24px,
  md: 20px,
  sm: 16px,
  xs: 12px
) !default;

// Layouts default values
$header-height:   minmax(56px, auto) !default;
$footer-height:   minmax(max-content, 50px) !default;
$nav-width:       250px !default;
$aside-width:     200px !default;
{% endhighlight %}

The number of grid columns can be modified via Sass variables. `$grid-columns` is used to generate the number of columns while `$grid-breakpoints-gap` determines the space that occurr between columns. You can modify these variables in order to define a new behavior of your grids.

# Mixins

{{ site.title }} use series of mixins, in conjunction with the variables explained above, that help us to generate the CSS for each grid specification.

{% highlight scss %}
// Generate default grid system with given columns and gap
@mixin make-grid($columns-number: $grid-columns-number, $gap: map-get($grid-breakpoints-gap, "sm"));

// span between columns of our grid system
@include col-start-end($col-start, $col-end);

// span between rows of our grid system
@include row-start-end($row-start, $row-end);

// Defines a grid layout by referencing the names of the grid areas
@mixin make-layout($rows-template, $columns-template, $template-areas);
{% endhighlight %}

## Examples

If you want to define a new CSS Grid with custom gap you can use the `make-grid($columns, $gap)` mixin, where `$columns` is the number of columns of your grid and `$gap` is the space, in pixel, that occurs between each one of them.

{% highlight scss %}
.fantastic-grid {
  @include make-grid(24, 20px);
}
{% endhighlight %}

In {{ site.title }} you can build a custom layout using `make-layout` mixin. If you don't have familiarity with CSS Grid layout take a [look here](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout).

{% highlight scss %}
$template-areas:
  "head head head"
  "nav main aside"
  "foot foot foot" !default;
$rows-template: 56px 1fr 40px !default;
$columns-template: 200px 1fr 150px !default;

.custom-layout {
  @include make-layout($rows-template, $columns-template, $template-areas);
}
{% endhighlight %}

<div class="docs-example">
  <div class="layout-7" style="max-height: 400px;">
    <header>This is header</header>
    <nav>This is navigation</nav>
    <main>This is Main content</main>
    <aside>This is aside</aside>
    <footer>This is Footer</footer>
  </div>
</div>

{% highlight html %}
<div class="custom-layout">
  <header>This is header</header>
  <nav>This is navigation</nav>
  <main>This is Main content</main>
  <aside>This is aside</aside>
  <footer>This is Footer</footer>
</div>
{% endhighlight %}
