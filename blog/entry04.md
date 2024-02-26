# Entry 4
##### 2/25/23

## Tool that I chose 
The tool that I chose was **SASS**. SASS was not my first choice and my first choice was Aframe. I have tried out Aframe but I thought it was too complicated to me to use it. SASS was my second option. It was very similar to CSS, which was what I am familiar with, and the source that my teacher gave me was easy to understand. I decided to stick with SASS when I have tried it out on JS Bin.  

## How I tinkered with it 
I tinkered with SASS by copied the code on [W3 Schools](https://www.w3schools.com/sass/sass_variables.php) to [Sass: Playground](https://sass-lang.com/playground/) and change around with the code. 

I learned that in SASS, you can write properties that has the same prefix as nested properties. I remembered there are properties that have the same prefix such as the border properties. So I wrote 
``` SCSS
border: {
 width: 2px;
 style: solid;
 color: red; 
}
```
I also nest them into a `p` selector so when it compiled into CSS, my paragraph would have all of the properties that I wrote. 

I learned that a `@mixin` directive allow you to create CSS code that can reuse through out the website and a `@include` directive allow you to use the mixin. I can use the mixin with nested properties. In this way, my paragraph and header both have the same border properties but I don't have to write the codes two times. 

I learned that the `@extend` directive allow you to share the CSS properties of one selector to other selectors. I combined `@extend` with `@mixin` and nested properties to give my paragraph and header similar properties but let my paragraph to have more properties than my header. 






[Previous](entry03.md) | [Next](entry05.md)

[Home](../README.md)