# Entry 4
##### 2/25/23

## Tool that I chose 
The tool that I chose was **SASS**. SASS was not my first choice and my first choice was Aframe. I have tried out Aframe but I thought it was too complicated for me to use it. SASS was my second option. It was very similar to CSS, which was what I am familiar with, and the source that my teacher gave me was easy to understand. I decided to stick with SASS when I have tried it out on [SASS: Playground](https://sass-lang.com/playground/).  

## How I tinkered with it 
I tinkered with SASS by copy the code on [W3 Schools](https://www.w3schools.com/sass/default.php) to [Sass: Playground](https://sass-lang.com/playground/) and change around with the code. 

I learned that in SASS, you can write properties that has the same prefix as nested properties. I remembered there are properties that have the same prefix such as the border properties. So I wrote 
``` SCSS
border: {
 width: 2px;
 style: solid;
 color: red; 
}
```
I also nest them into a `p` selector so when it compiled into CSS, my paragraph would have all of the border properties that I wrote. 
<img width="1087" alt="Screenshot 2024-02-26 at 1 16 41 AM" src="https://github.com/qiling9760/sep10-freedom-project/assets/146866841/670049aa-c3a0-45d6-9454-0a7160553b8c">

I learned that a `@mixin` directive allow you to create CSS code that can reuse through out the website and a `@include` directive allow you to use the mixin. I can use the mixin with nested properties. In this way, my paragraph and header both have the same border properties but I don't have to write the codes two times. 
<img width="1043" alt="Screenshot 2024-02-26 at 1 26 31 AM" src="https://github.com/qiling9760/sep10-freedom-project/assets/146866841/57679943-62e4-46a4-9eb7-7f4406d445d8">

I learned that the `@extend` directive allow you to share the CSS properties of one selector to other selectors. I combined `@extend` with `@mixin` and nested properties to give my paragraph and header similar properties but let my paragraph to have more properties than my header. 
<img width="988" alt="Screenshot 2024-02-26 at 1 39 31 AM" src="https://github.com/qiling9760/sep10-freedom-project/assets/146866841/84b959c7-63d4-4cf6-9e81-cf60b7933200">

## Skills
### Debugging
A skill that I learned is debugging. When I tried to write the border properties as nested properties in the playground, it did not show up the way I expected. It pop up as 
``` CSS
p border {
  width: 2px;
  style: solid;
  color: red;
}
```
When I look back to W3 Schools and compare my code to the example, I found my mistake. It was that I forgot about the colon after `border`. I mixed my bug after I get it. 

### Logical reasoning
Another skill I learned would be logical reasoning. In W3 Schools, I learned how I can nest properties if they have the same prefix. The examples that W3 Schools provide are  
``` SCSS
font: {
  family: Helvetica, sans-serif;
  size: 18px;
  weight: bold;
}
```
It could nest `font-family`, `font-size`, and `font-weight` together because they have the same prefix _font_. And the properties I know that have the same prefix are `border width`, `border-style`, and `border-color`. They all have the same prefix _border_. So, I tried to nest them together and it worked. 

[Previous](entry03.md) | [Next](entry05.md)

[Home](../README.md)
