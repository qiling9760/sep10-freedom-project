# Tool Learning Log

Tool: SASS

---

3/3/24
- I need to find a way to make SCSS compile to CSS.
  - I went on slack and saw Kyle asked the same question as me. Austin answered his question and reply with steps of how to do it, so I copied the codes he put to my IDE and it worked.
    -  The code I used was **`sass scss/style.scss css/style.css`**
    - I learned that whenever I wrote `scss` codes, I need to use this code in my terminal to make it compile to my `css` file.

- I made a variable for `border-width` and I put `$border: border-width: 2px;` but it does not work. It only work if I only put the `$border: 2px;`. And I would use my variable like
``` CSS
p {
    border-width: $border;
}
```
- I learned that I can only put `variable: value` and cannot put `variable: property: value`.

3/11/24:
- My classmate Kyle told me a trick that could compile SCSS to CSS without writing a command
  - I will need to click on the function key and the f1 key to make the search bar to pop up. Then I find the "Live Sass: Watch Sass" and it will automatically compile SCSS code into CSS code without me writing the command in the terminal. To stop compiling, I will click on the "Live Sass: Stop Watching."

- When writing SCSS codes in two different SCSS file, I can use **`@use`** to make **the codes in one SCSS file to be into another SCSS file**.
  - I created two more SCSS file, one called "style2.scss" and one called "style3.scss". I wrote some SCSS codes in them. I can just write `@use` in my style.scss file and the codes in my other two SCSS file will be imported to my style.scss file.
  ``` SCSS
  @use 'style2';
  @use 'style3';
  ```
  - The benefit of `@use` is that the SCSS codes in my other SCSS file won't take up space in my style.scss file.

3/17/24:
- I learned how to **combine variables with operations**.
  - I can use `+`, `-`, `*`, `/` to change the value of a property.
  - I made a variable called `$value:2px;` and use it in my `border-wdith` propety.
  ``` SCSS
  .happy {
    border: {
    style: solid;
    width: $value + 10;
  }
  }
  ```
  The output CSS are
  ``` CSS
  .happy {
  border-style: solid;
  border-width: 12px;
  }
  ```
  - The addition sign add 10px to the original 2px.

- I learned to use **`&`**. This symbol means **parent selector**.
  - I can use `&` to add suffixes. For example, I have two classes, one is `emotion` and the other one is `emotion-sad`. I can use `&` when I want to write SCSS for these two classes without writing their full name out.
  ``` SCSS
  .emotion {
  border: {
    style: solid;
    width: $value + 10;
  }

  &-sad {
    border:{
      style: dot;
      radius: $value;
    }
  }
  }
  ```
  The output CSS are
  ``` CSS
  .emotion {
  border-style: solid;
  border-width: 12px;
  }

  .emotion-sad {
  border-style: dot;
  border-radius: 2px;
  }
  ```
  - If I have a group of `div` that are in the same section of the page, I can organize them with classes that have the same prefix and different suffixes. When I want to style these `div`, I don't need to write the prefix over and over again.

3/24/24:
- I learned how to use the **placeholder selector** and the **`@extend` function**. 
  - The placeholder selector start with a `%` symbol, and it will not be included in the CSS output. The `@extend` function allows one selector to inherit styles from another selector. 
  - I made a placeholder selector called `%border` and use `@extend` to let my `div` selector to inherit its styles. 
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

  - The placeholder selector is very helpful when I want to give multiple selectors the same style properties. 

- The **variable** is the **name of the value**, and everytime you refer to that variable that means you want to use that value for your property. Variables start with a `$` symbol. It is written as `<variable>: <expression>`. It can be located anywhere of the page. There is global variable and local variable. 
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

4/1/24 
- I learned more about **`@use`**. 
  - Stylesheets that load up by `@use` are call "modules". 
  - I can use mixins from other modules by using `@include`. 
    -  **`@include <namespace>.<mixin>()`** `@include name-of-the-scss-file.name-of-the-mixin`
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

  - I can give a shortcut to the name of the scss file if its name is too long. 
    ``` SCSS
    @use 'style2' as two;

    h1 {
      @include two.font;
    }
    ```
    - I tried to use `2` for the shortcut of `style2.scss` but it does not work. I tried to use symbols like `%` and it also does not work. I figured out that I can only use letters for shortcut names. 


  - **Private member**. I can make some of the members of my stylesheet to not be available outside of that stylesheet. I can do that by **add a "-" or "_" to the begining of its name**. 
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
    - My terminal will pop up error if I try to use `@mixin border` in my `style.scss`. 
    ```
    Error: Undefined mixin.

    6 │   @include two.border;
      │   ^^^^^^^^^^^^^^^^^^^
      ╵
    ```
  - I can define variables with the `!default flag` to make them configurable. This means if I do not define the value for the variable, it will keep the default value. But if I define it with a new value, the new value will override the default value. 
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
    - At first, I make the variables `$family: sans-serif !default;` and `$size: 100px !default;` in the local scope. But when I try to compile my SCSS to CSS, my terminal says error. 
      ``` SCSS
      style2.scss
      @mixin font{
        $family: sans-serif !default;
        $size: 100px !default;
        font:{
        family: $family;
        size: $size;
        }
      }
      ```
      ```
      Error: This variable was not declared with !default in the @used module.

      2 │   $size: 20px
        │   ^^^^^^^^^^^
      ```
    - I did not know why that happened but when I go back to the SASS documentation, I noticed that the put the variable in the global scope, so I moved my variables out of the block. I learned only global variables written at the top level of the stylesheet can be configured. 

4/8/24
- **`@foward`** loads a Sass stylesheet and makes its mixins, functions, and variable available when your stylesheet is loaded with the `@use` rule. 
  - **Add prefix** to the stylesheets when they are load with `@forward` allows me to organize mixins that are from different stylesheets but have the same name. 
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
      - Both mixins from `style2.scss` and `style3.scss` are named `font`. Adding prefixes to the modules allows the computer to know which `font` mixin that I am refering to. 

  - **Control whether a member of a module is visible** by writing `@forward "<url>" hide <members...> or @forward "<url>" show <members...>`
      ``` SCSS
      style2.scss
      $size: 20px;
      ```
      ``` SCSS
      style3.scss
      $size: 10px;
      ```
      ``` SCSS
      sass-library.scss
      @forward "style2";
      @forward "style3" hide $size;
      ```
      ``` SCSS
      style.scss
      @use "sass-library" as sass;

      p {
        font-size: sass.$size;
      }
      ```
      ``` CSS
      p {
      font-size: 20px;
      }
      ```
      - Although both variable are named `size`, the computer knows that I am refering to `$size:20px;` because I have hidden `$size:10px;`. 
      - If I did not hide one of the variable, it will pop up error. 
        ```
        Error: Two forwarded modules both define a variable named $size.
        ```
- **`@mixin` and `@include`** define styles that can be re-used throughout your stylesheet
  - **Mixins can make arguements where their behaviors were not specified at first but can be customized** by `@include` each time they are used.
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
    - It will pop up error if you did not declare the values in `@include`
    ```
    Error: Missing argument $size.
    1   │ @mixin font($size, $color) {
        │        ━━━━━━━━━━━━━━━━━━━ declaration
    ... │
    7   │   @include font
        │   ^^^^^^^^^^^^^ invocation
    ```
  - **Mixins can have an arguement where default values** were set. If the values are not declared in `@include`, it will use the default values. 
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
    - If I want to keep the first default value and change the second one, I need to specify the name of the variable that I want to change. If not, the program will view the value that I put is for the first variable. 
    - At first, I wrote the following code but it pops up error. 
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
<!--
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->
