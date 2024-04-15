# Entry 5
##### 4/8/24

## Tool that I chose - SASS
I learned about the `@use` function, how to combine variables with operations, the "parent selector", the "placeholder selector" and the `@extend` function, variables, "private members", the `!default flag`, the `@forward` function, and the `@mixin` and `@include` functions. 

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

## Combine variables with operations





[Previous](entry04.md) | [Next](entry06.md)

[Home](../README.md)