# Entry 5
##### 4/8/24

## SASS
I had learned a lot about SASS from reading the [SASS documentations](https://sass-lang.com/documentation/). Things that I leanred this past few weeks that I thought are the most important are 
- the `@use` function
- the "placeholder selector" and the `@extend` function
- variables
- private members
- the `!default` flag
- the `@forward` function
- the `@mixin` and `@include` functions. 

## Compile SCSS to CSS
At first, I did not know how to compile SCSS to CSS. I went on slack to see if someone can help me. One of my classmates Kyle who also chose SASS as his tool had the same problem as me. He asked his question, and Austin was able to help him out. Austin told us that we could install SASS using `npm install -g sass`. Then, we can use the **`sass scss/style.scss css/style.css`** command to compile our SCSS codes to CSS codes. I was able to use this command to compile codes when I am tinkering with SASS. 

Kyle later on told me another way that can compile SCSS to CSS, which is "Live Sass: Watch Sass". It will automatically compile SCSS code into CSS code without me writing the command in the terminal. But I did not like it, so I never use it. 

## `@use` function
**The `@use` function** is used to **load up multiple SASS stylesheets and combine the codes together.** 

Stylesheets that load up by `@use` are call "modules". 

To load up a stylesheet, I will write `@use` follow by the name of the stylesheet before any rules. 

My original SCSS file is called "style.scss". I created two more SCSS file, one called "style2.scss" and one called "style3.scss". I wrote some SCSS codes in them. I load these two stylesheets into my original stylesheet by using `@use`.  
``` SCSS
@use 'style2';
@use 'style3';
```
I can use mixins from other modules by using `@include`.  
I will write it as `@include <namespace>.<mixin>()`, which it just means `@include name-of-the-scss-file.name-of-the-mixin`. 

``` SCSS
style2.scss
@mixin font{
    font:{
    family: sans-serif;
    size: 100px;
    }
}
```
``` SCSS
style.scss
@use 'style2';

h1 {
    @include style2.font;
    color: blue;
}
```
``` CSS
h1 {
font-family: sans-serif;
font-size: 100px;
color: blue;
}
```
I can give a shortcut to the name of the scss file if its name is too long. The shortcut can only be letters. Numbers or symbols will be undefined. 
``` SCSS
@use 'style2' as two;

h1 {
    @include two.font;
}
```

## The "placeholder selector" and the @extend function
The placeholder selector start with a `%` symbol, and **it will not be included in the CSS output**. The `@extend` function **allows one selector to inherit styles from another selector**.

``` SCSS
$primary-color: red;
$value:2px;

%border {
border: {
    width: $value;
    style: solid;
    color: $primary-color;
}
}

div {
@extend %border; 
}
```
``` CSS
div {
border-width: 2px;
border-style: solid;
border-color: red;
}
```

## Variables
The **variable** is the **name of the value**, and everytime you refer to that variable that means you want to use that value for your property. Variables start with a `$` symbol. It is written as `<variable>: <expression>`. It can be located anywhere of the page. There is global variable and local variable. 
  - If a variable changes value, the earlier property will have the old value and the later will have the new value. 
  - Global variable is declare at the top of the stylesheet. It can be accessed anywhere. 
  - Local variable is declare in blocks. It can be only accessed within the block it was declared. Selectors cannot use local variables that were declared in other selectors. 
  - Global and local variables can have the same name, but local variable will override global variable. 
  
  ``` SCSS
  p {
    $value: 10px;
    font-size: $value;
  }

  h1 {
    font-size: $value; 
  }
  ```

  ``` CSS
  p {
  font-size: 10px;
  }

  h1 {
    font-size: 2px;
  }
  ```
  - You can make a local variable became global variable by using `!global` statement. 
  ``` SCSS 
  p {
    $value: 10px !global;
    font-size: $value;
  }

  h1 {
    font-size: $value;
  }
  ``` 
  ``` CSS
  p {
    font-size: 10px;
  }

  h1 {
    font-size: 10px;
  }
  ```
  If the local variable and the global variable has the same name, the value for the global variable will be changed if you use the `!global` for the local variable.

## Private member
I can make some of **the members of my stylesheet to not be available outside of that stylesheet**. I can do that by **add a "-" or "_" to the begining of its name**. These members are **private members**. It will pop up error in my terminal if I load up a stylesheet and try to use the private members in that stylesheet. 

``` SCSS
style2.css
@mixin font{
    font:{
    family: sans-serif;
    size: 100px;
    }
} 

@mixin -border {
    border: {
    radius:2px;
    width: 10px;
    }
}
``` 
``` SCSS
style.scss
@use 'style2' as two;

h1 {
    @include two.font;
    color: blue;
    @include two.border;
}
```
```
Error: Undefined mixin.

6   │   @include two.border;
    │   ^^^^^^^^^^^^^^^^^^^
    ╵
```

## The `!default` flag
**Variables with the `!default flag` are configurable**. If the value of a variable is not defined, the vriable will keep its default value. If the variable is defined with a new value, the new will override the default value. Only global variables written at the top level of the stylesheet can be configured. 
``` SCSS
style2.scss
$family: sans-serif !default;
$size: 100px !default;

@mixin font{
    font:{
    family: $family;
    size: $size;
    }
}
```
``` SCSS
style.scss
@use 'style2' as two with (
    $size: 20px
);

h1 {
    @include two.font;
    color: blue;
}
```
``` CSS
h1 {
font-family: sans-serif;
font-size: 20px;
color: blue;
}
```
## `@forward` function
**`@foward`** loads a Sass stylesheet and makes its mixins, functions, and variable available when your stylesheet is loaded with the `@use` rule. 

**Add prefix** to the stylesheets when they are load with `@forward` can organize mixins that are from different stylesheets but have the same name.

``` SCSS
style2.scss
@mixin font{
font-family: sans-serif;
}
```
``` SCSS
style3.scss
@mixin font {
    font-family: monospace;
}
```
``` SCSS
style-library.scss
@forward "style2" as two-*;
@forward "style3" as three-*;
```
``` SCSS
style.scss
@use "sass-library" as sass;

p {
    @include sass.two-font;
}

h1{
    @include sass.three-font;
}
```
``` CSS
p {
    font-family: sans-serif;
}

h1 {
    font-family: monospace;
}
```
**Control whether a member of a module is visible** by writing `@forward "<url>" hide <members...> or @forward "<url>" show <members...>`. 

## The @mixin and @include functions.
**`@mixin` and `@include`** define styles that can be re-used throughout the stylesheet. 

**Mixins can make arguements where their behaviors were not specified at first but can be customized** by `@include` each time they are used. It will pop up error if you did not declare the values in `@include`. 
``` SCSS
@mixin font($size, $color) {
    font-size:$size;
    font-color:$color;
}

p {
    @include font(10px, red)
}
``` 
``` CSS
p {
font-size: 10px;
font-color: red;
}
```
**Mixins can have an arguement where default values** were set. If the values are not declared in `@include`, it will use the default values. The name of the variable that you want to change value for need to be specify if there are multiple variables.
``` SCSS
@mixin font($size:20px, $color:blue) {
font-size:$size;
font-color:$color;
}

p {
    @include font($color:red);
}
```
``` CSS
p {
font-size: 20px;
font-color: red;
} 
```
## Skills 
### How to read 
The main skill that I learned is "how to read" because I need to read through the SASS documentations to learn about the asspect of SASS and how to use them. I first read about what they do and look at the examples. If there is something wrong when I am tinkering, I would go back to the documentation to read it again to see if I miss something. 

For example, when I am working with the `!default` flag, I first make the variables `$family: sans-serif !default;` and `$size: 100px !default;` in the local scope. 
```
Error: This variable was not declared with !default in the @used module.

2 │   $size: 20px
  │  
```
When I go back to the SASS documentation, I noticed that they put the variable in the global scope, so I moved my variables out of the block.

### How to google
The second skill that I learned is how to google. Sometimes when I am confused with something, I couldn't find the solution in the SASS documentation, so I need to google it. 

For example, I faced a problem when I want to change values for my mixins. I want to change the value for the second variable but keep the default value for my first variable, but my terminal kept poping up error. 
``` SCSS
@mixin font($size:20px, $color:blue) {
font-size:$size;
font-color:$color;
}

p {
    @include font(red);
}
```  
```
Error: Missing argument $color.
    ╷
1   │ @mixin font($size:20px, $color) {
    │        ━━━━━━━━━━━━━━━━━━━━━━━━ declaration
... │
7   │   @include font(red);
    │   ^^^^^^^^^^^^^^^^^^ invocation
```
I searched online to see how to fix this problem and I found the solution on this [website](https://medium.com/@seth.poulin/simplifying-sass-mixins-with-default-values-163da334a51e). The author was able to show multiple ways that I can change the value for the second variable but keep the first one. 

[Previous](entry04.md) | [Next](entry06.md)

[Home](../README.md)