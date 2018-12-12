# SASS / SCSS

We learn about how Sass makes it easier to write clean and reusable CSS code. The preprocessor, Sass, has the right tools to make that happen like:

1.  _Variables_: for reusable values such as colors, font sizes, spacing etc.
2.  _Nesting_: to nest selectors inside of one another, allowing us to write less code.
3.  _Operators_: for mathematical operations right inside of CSS.
4.  _Partials and imports_: to write CSS in different files and importing them all into one single file.
5.  _Mixins_: to write reusable pieces of CSS code.
6.  _Functions_: similar to mixins, with the difference that they produce and return a value that can be used.
7.  _Extends_: to make different selectors inherit declarations that are common to all of them.
8.  _Control directives_: for writing complex code using conditionals and loops (Not covered in this course).

Check out [this codepen](https://codepen.io/Anikion/pen/KreYyo?editors=1100#0), this is how I got acquainted with Mixins, Extends and Functions in Sass.

Here are a few code snippets:

### Mixin {

```SASS
  @mixin style-link-text($col) {
    text-decoration: none;
    text-transform: uppercase;
    color: $col;
  }
```

```SASS
  .navigation {
    list-style: none;
    float: left;

    li {
      display: inline-block;
      margin-left: 30px;

      &:first-child {
        margin: 0;
      }

      a:link {
        @include style-link-text($color-text-dark);
      }
    }
  }

  .buttons {
    float: right;
  }

  .btn-main:link,
  .btn-hot:link {
    padding: 10px;
    display: inline-block;
    text-align: center;
    border-radius: 100px;
    width: $width-button;
    @include style-link-text($color-text-light);
  }
```

### }

### Function {

```SASS
  @function divide($a, $b) {
    @return $a / $b;
  }

  nav {
    margin: divide(60, 2) * 1px;
    background-color: $color-primary;

    @include clearfix;
  }
```

### }

### Extend {

Before using Extend

```SASS
  .btn-main:link,
  .btn-hot:link {
    padding: 10px;
    display: inline-block;
    text-align: center;
    border-radius: 100px;
    width: $width-button;
    @include style-link-text($color-text-light);
  }

  .btn-main {
    &:link {
      background-color: $color-secondary;
    }

    &:hover {
      background-color: darken($color-secondary, 15%);
    }
  }

  .btn-hot {
    &:link {
      background-color: $color-tertiary;
    }

    &:hover {
      background-color: lighten($color-secondary, 10%);
    }
  }
```

After using Extend

```SASS
  %btn-placeholder {
    padding: 10px;
    display: inline-block;
    text-align: center;
    border-radius: 100px;
    width: $width-button;
    @include style-link-text($color-text-light);
  }


  .btn-main {
    &:link {
      @extend %btn-placeholder;
      background-color: $color-secondary;
    }

    &:hover {
      background-color: darken($color-secondary, 15%);
    }
  }

  .btn-hot {
    &:link {
      @extend %btn-placeholder;
      background-color: $color-tertiary;
    }

    &:hover {
      background-color: lighten($color-secondary, 10%);
    }
  }
```

### }

###Full SASS {

```SASS
  * {
  margin: 0;
  padding: 0;
}

$color-primary: #f9ed69; // Yellow color
$color-secondary: #f08a5d; // orange
$color-tertiary: #b83b5e; // pink
$color-text-dark: gray;
$color-text-light: #eee;

$width-button: 150px;

@mixin clearfix {
  &::after {
    content: "";
    clear: both;
    display: table;
  }
}

@mixin style-link-text($col) {
  text-decoration: none;
  text-transform: uppercase;
  color: $col;
}

@function divide($a, $b) {
  @return $a / $b;
}

nav {
  margin: divide(60, 2) * 1px;
  background-color: $color-primary;

  @include clearfix;
}

.navigation {
  list-style: none;
  float: left;

  li {
    display: inline-block;
    margin-left: 30px;

    &:first-child {
      margin: 0;
    }

    a:link {
      @include style-link-text($color-text-dark);
    }
  }
}

.buttons {
  float: right;
}

%btn-placeholder {
  padding: 10px;
  display: inline-block;
  text-align: center;
  border-radius: 100px;
  width: $width-button;
  @include style-link-text($color-text-light);
}


.btn-main {
  &:link {
    @extend %btn-placeholder;
    background-color: $color-secondary;
  }

  &:hover {
    background-color: darken($color-secondary, 15%);
  }
}

.btn-hot {
  &:link {
    @extend %btn-placeholder;
    background-color: $color-tertiary;
  }

  &:hover {
    background-color: lighten($color-secondary, 10%);
  }
}
```

###}

### Compiled CSS {

```CSS
* {
  margin: 0;
  padding: 0;
}

nav {
  margin: 30px;
  background-color: #f9ed69;
}
nav::after {
  content: "";
  clear: both;
  display: table;
}

.navigation {
  list-style: none;
  float: left;
}
.navigation li {
  display: inline-block;
  margin-left: 30px;
}
.navigation li:first-child {
  margin: 0;
}
.navigation li a:link {
  text-decoration: none;
  text-transform: uppercase;
  color: gray;
}

.buttons {
  float: right;
}

.btn-main:link, .btn-hot:link {
  padding: 10px;
  display: inline-block;
  text-align: center;
  border-radius: 100px;
  width: 150px;
  text-decoration: none;
  text-transform: uppercase;
  color: #eee;
}

.btn-main:link {
  background-color: #f08a5d;
}
.btn-main:hover {
  background-color: #ea5717;
}

.btn-hot:link {
  background-color: #b83b5e;
}
.btn-hot:hover {
  background-color: #f4ac8c;
}
```

###}


# REVIEW: Basic Responsive Design Principles

1. Fluid Grids and Layouts - 
  To allow content to easily adapt to the currant fiewport width used to browse the website. Uses % rather than px for all layout-related lengths.

2. Flexible/Responsive Images - 
  Images behave differently than text content, and so we need to ensure that they also adapt nicely to the current viewport.

3. Media Queries -
  To change styles on certain viewport widths (breakpoints), allowing us to create different versions of our website for different widths.


# Building a custom grid with Floats!
It'll be interesting to see how this pure CSS grid will differ to my tic tac toe grid (made with css and jQuery).