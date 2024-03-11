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




<!--
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->
