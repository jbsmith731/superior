# superior.scss
Superior is a small collection of scss mixins that allow for less code bloat and more flexibility! Highly influenced and inspired by [Susy](http://oddbird.net/susy/) and [Bootstrap](http://getbootstrap.com/).

### Default Variables
```sass
$cols   : 12 !default;
$gutter : 1rem !default;
```
Superior defaults to a 12 column grid system with 16px gutters. Gutters can be set to pixel, em, rem etc. although percentage gutters are not recommended due to issues when nesting.

## Column Wrapper (row)
All columns need to be wrapped with a `div` that uses the `cols()` mixin.

**Mixin:**
```sass
@mixin cols($flex: flex, $dir: row, $wrap: wrap, $justify: flex-start, $align-items: flex-start)
```
**Example:**
```sass
// scss
.my-div {
  @include cols()
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
```sass
@mixin flex-span($span, $cols: $cols, $order: null)
```
If `$order` is left null it will not be included in the compiled css.

**Example:**
```sass
// scss
.my-div {
  @include flex-span(3);
}

// compiled css
.my-div {
  flex: 0 1 25%
  padding: 0 0.5rem;
  box-sizing: border-box;
}


// scss
.my-div {
  @include flex-span(6, $order: 2);
}

// compiled css
.my-div {
  flex: 0 1 50%
  padding: 0 0.5rem;
  box-sizing: border-box;
  order: 2;
}
```

### Floated Columns
**Mixin:**
```sass
@mixin float-span($span, $cols: $cols, $float: left) 
```
**Example:**
```sass
// scss
.my-div {
  @include float-span(4);
}

// compiled css
.my-div {
  width: 25%;
  padding: 0 0.5rem;
  box-sizing: border-box;
}
```

## Utility Mixins
### Offset
**Mixin:**
```sass
@mixin offset($span, $direction: left, $cols: $cols)
```
**Example:**
```
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
```sass
@include clearfix;
```
