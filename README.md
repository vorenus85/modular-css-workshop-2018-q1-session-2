# Create mixins

## 1. A mixins mappa 
- A default mappában hozzuk létre a hövetkező fájlt
```
_mixins.scss
```

- A tartalma a következő legyen:
```$xslt
@import "mixins/index";
```

- Hozzunk létre egy <b>mixins</b> mappát a default mappában

- A mixins mappában hozzuk létre a következő fájlt:

```
_index.scss
```

## 2. dinamic-width mixin

- Hozzuk létre a következő fájlt:
```
dinamic-width.scss
```

- tartalma a következő legyen:

```
@mixin dinamic-width($item-per-row){
    width: 100% / $item-per-row;
}
```

- importáljuk az <b>_index.scss</b>-ben
```
@import "dinamic-width";
```

- hívjuk meg a mixint a megfelelő helyeken, a megfelelő paraméterekkel

```
modules/news.scss
modules/product-item.scss
```

## 3. dinamic-cols mixin

- Hozzuk létre a következő fájlt:
```
dinamic-cols.scss
```

- tartalma a következő legyen:

```
@mixin dinamic-cols(){
    $class-slug: col !default;
    @for $i from 1 through 12{
        .#{$class-slug}-#{$i} {
            width: (100% / $i);
        }
    }
}
```

- importáljuk az <b>_index.scss</b>-ben
```
@import "dinamic-cols";
```

- hívjuk meg a mixint a megfelelő helyeken, a megfelelő paraméterekkel

```
utils/cols.scss
```

## 4. standard-flex mixin

- Hozzuk létre a következő fájlt:
```
standard-flex.scss
```

- tartalma a következő legyen:

```
@mixin standard-flex($display: flex, $flex-wrap: wrap, $align-items: center, $justify-content: flex-start) {
    display: $display;
    flex-wrap: $flex-wrap;
    align-items: $align-items;
    justify-content: $justify-content;
}
```

- importáljuk az <b>_index.scss</b>-ben
```
@import "standard-flex";
```

- hívjuk meg a mixint a megfelelő helyeken, a megfelelő paraméterekkel

```
modules/news.scss
modules/product-item.scss
utils/cols.scss
```

## 5. button-size mixin

- Hozzuk létre a következő fájlt:
```
buttons.scss
```

- tartalma a következő legyen:

```
@mixin button-size($padding-y, $padding-x, $font-size, $border-radius) {
    padding: $padding-y $padding-x;
    font-size: $font-size;
    border-radius: $border-radius;
}
```

- a variables.scss-ben deklaráljuk a következő változókat:
```
$btn-padding-y-sm: 3px;
$btn-padding-x-sm: 5px;
$btn-font-size-sm: 10px;
$btn-border-radius-sm: $global-border-radius;

$btn-padding-y-lg: 10px;
$btn-padding-x-lg: 15px;
$btn-font-size-lg: 18px;
$btn-border-radius-lg: $global-border-radius;
```

- importáljuk az <b>_index.scss</b>-ben
```
@import "buttons";
```

- hívjuk meg a mixint a megfelelő helyeken, a megfelelő paraméterekkel

```
components/button.scss
```

## 6. button-variant mixin

- a mixins/buttons.scss fájlba tegyük bele a következő mixint:

```
@mixin button-variant($background, $border, $active-background: darken($background, 7.5%), $active-border: darken($border, 10%)) {
    background-color: $background;
    border-color: $border;

    &:hover {
        background-color: $active-background;
        border-color: $active-border;
        color: $white;
    }
}
```

- a variables.scss-ben deklaráljuk a következő tömböt:
```
$theme-colors: (
        primary: $global-color,
        secondary: $global-hover-color
) !default;
```

- töröljük a következő váltözőkat a variables.scss-ben mivel nem lesz rájuk szükségünk:
```
/* btn-primary */
$btn-primary-background: $white;
$btn-primary-border-color: $global-color;
$btn-primary-color: #222;
$btn-primary-hover-background: $white;
$btn-primary-hover-border-color: $global-hover-color;
$btn-primary-hover-color: #444;

/* btn-secondary*/
$btn-secondary-background: $global-color;
$btn-secondary-border-color: $global-color;
$btn-secondary-color: $white;
$btn-secondary-hover-background: $global-hover-color;
$btn-secondary-hover-border-color: $global-hover-color;
$btn-secondary-hover-color: $white;
```

- hívjuk meg a mixint egy each ciklusban a megfelelő helyeken, a megfelelő paraméterekkel

```
components/button.scss
```

```
//
// Alternate buttons
//

@each $color, $value in $theme-colors {
    .btn-#{$color} {
        @include button-variant($value, $value);
    }
}
```