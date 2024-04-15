# Entry 5
##### 4/8/24

## SASS
I had learned a lot about SASS from reading the [SASS documentations](https://sass-lang.com/documentation/). Things that I leanred this past few weeks that I thought are the most important are 
- the `@use` function
- the "placeholder selector" and the `@extend` function
- variables
- "private members"
- the `!default flag`
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
I can give a shortcut to the name of the scss file if its name is too long. 
``` SCSS
@use 'style2' as two;

h1 {
    @include two.font;
}
```
 - I tried to use `2` for the shortcut of `style2.scss` but it does not work. I tried to use symbols like `%` and it also does not work. I figured out that I can only use letters for shortcut names. 

## The "placeholder selector" and the @extend function
The placeholder selector start with a `%` symbol, and **it will not be included in the CSS output**. The `@extend` function **allows one selector to inherit styles from another selector**.

I tinker with it by made a placeholder selector called `%border` and use `@extend` to let my `div` selector to inherit its properties.

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
The output CSS are 

``` CSS
div {
border-width: 2px;
border-style: solid;
border-color: red;
}
```
Here it can see that when the SCSS is compile to CSS, only the `div` is being compiled. The placeholder selector allow me to give multiple selectors the same properties. 

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





[Previous](entry04.md) | [Next](entry06.md)

[Home](../README.md)