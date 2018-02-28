# superior.scss 3.0
Superior is a small collection of scss mixins that allow for less code bloat and more flexibility! Highly influenced and inspired by [Susy](http://oddbird.net/susy/) and [Bootstrap](http://getbootstrap.com/).

*Superior does not include browser prefixes. Superior was created under the assumption most developers use autoprefixers for the most control of browser support.*

[Demo](https://codepen.io/jbsmith731/pen/xYmgyW)

### Default Variables
```scss
$cols   : 12 !default;
$gutter : 1rem !default;
```
Superior defaults to a 12 column grid system with 16px gutters. Gutters can be set to pixel, em, rem etc. although percentage gutters are not recommended due to issues when nesting.

## Column Wrapper (row)
All columns need to be wrapped with a `div` that uses the `cols()` mixin. It is **NOT** recommended to use `cols()` directly on your `.container` element. 

**Mixin:**
```scss
@mixin cols($flex: flex, $dir: row, $wrap: wrap, $justify: flex-start, $align-items: flex-start)
```
**Example:**
```scss
// scss
.my-div {
  @include cols();
}

// compiled css
.my-div {
  margin: 0 -0.5rem;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: flex-start;
}
```
Don't want to use flexbox? Set `$flex: false` to use floated columns.

## Columns
The total number of columns is defaulted to the `$cols` variable but can be changed to any number.

### Flexbox columns
**Mixin:**
```scss
@mixin makeFlex($span, $cols: $cols, $order: null)
```
If `$order` is left null it will not be included in the compiled css.

**Example:**
```scss
// scss
.my-div {
  @include makeFlex(3);
}

// compiled css
.my-div {
  flex: 0 1 25%;
  max-width: 25%;
  padding: 0 0.5rem;
  box-sizing: border-box;
}


// scss
.my-div {
  @include makeFlex(6, $order: 2);
}

// compiled css
.my-div {
  flex: 0 1 50%;
  max-width: 50%;
  padding: 0 0.5rem;
  box-sizing: border-box;
  order: 2;
}
```

### Update flexbox columns
To add new flex dimensions on an element that already has `makeFlex` use `updateFlex`.

**Mixin:**
```scss
@mixin updateFlex($span, $cols: $cols)
```

**Example:**
```scss
// scss
.my-div {
  @include makeFlex(3);
  
  @media(...) {
    @include updateFlex(12);
  }
}

// compiled css
.my-div {
  flex: 0 1 25%;
  max-width: 25%;
  padding: 0 0.5rem;
  box-sizing: border-box;
}

@media(...) {
  .my-div {
    flex: 0 1 100%
    max-width: 100%;
  }
}
```

### Floated Columns
**Mixin:**
```scss
@mixin makeFloat($span, $cols: $cols, $float: left) 
```
**Example:**
```scss
// scss
.my-div {
  @include makeFloat(4);
}

// compiled css
.my-div {
  width: 25%;
  padding: 0 0.5rem;
  box-sizing: border-box;
  float: left;
}
```

## Functions
### Span
```scss
span($span, $cols: $cols)
```

**Example:**
```scss
// scss
.my-div {
  width: span(4);
}

.my-other-div {
  flex: 0 1 span(3, 6);
}


// compiled css
.my-div {
  width: 25%;
}

.my-other-div {
  flex: 0 1 50%;
}
```


## Utility Mixins
### Offset
**Mixin:**
```scss
@mixin offset($span, $direction: left, $cols: $cols)
```
**Example:**
```scss
// scss
.my-div {
  @include offset(4);
}

// compiled css
.my-div {
  margin-left: 25%;
}
```

### Clearfix
The clearfix mixin is already included in the `cols()` mixin if `$flex: false`

**Mixin:**
```scss
@include clearfix;
```
