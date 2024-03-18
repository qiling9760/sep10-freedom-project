# Tool Learning Log

Tool: SASS

---

3/3/24
- I need to find a way to make SCSS compile to CSS.
  - I went on slack and saw Kyle asked the same question as me. Austin answered his question and reply with steps of how to do it, so I copied the codes he put to my IDE and it worked.
    -  The code I used was `sass scss/style.scss css/style.css`
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

- When writing SCSS codes in two different SCSS file, I can use `@use` to make the codes in one SCSS file to be into another SCSS file.
  - I created two more SCSS file, one called "style2.scss" and one called "style3.scss". I wrote some SCSS codes in them. I can just write `@use` in my style.scss file and the codes in my other two SCSS file will be imported to my style.scss file.
  ``` SCSS
  @use 'style2';
  @use 'style3';
  ```
  - The benefit of `@use` is that the SCSS codes in my other SCSS file won't take up space in my style.scss file.

3/17/24:
- I learned how to combine variables with operations.
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

- I learned to use `&`. This symbol means parent selector.
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

<!--
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->
