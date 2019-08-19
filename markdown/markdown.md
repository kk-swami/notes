# This is a cheatsheet documenting markdown commands


What is markdown ?

Here's (https://en.wikipedia.org/wiki/Markdown) the wiki page.

In brief , markdown was originally designed as a simpler way to write web pages (the markdown syntax is much easier than html syntax)
Note that markdown is a markup language, like html, and is concerned with the content, not  how the text is presented (that's the job of the styling/CSS) 
(For more on separation of content and style, read (https://en.wikipedia.org/wiki/Separation_of_content_and_presentation) )

 

# Headers

To make a phrase as a header use "#" between 1 and 6 times, 1 being the largest and 6 the smallest

For illustration,

# The quick brown fox jumped over the lazy dog

## The quick brown fox jumped over the lazy dog

### The quick brown fox jumped over the lazy dog

#### The quick brown fox jumped over the lazy dog

###### The quick brown fox jumped over the lazy dog





# Emphasizing phrases (bold, italics)


To emphasize a phrase , use asterisks or _ on either side of phrase. The number of asteriks or _ give different behaviour
1) One asterisk/_ : italics
    
    The *quick brown fox* jumped over the lazy dog (One asterisk before and after quick brown fox)
     
2) Two asterisks/_ : bold
    
    The **quick brown fox** jumped over the lazy dog (Two asterisks before and after quick brown fox)
    
3) Three asterisks/_ : italicized + bold
    
    The ***quick brown fox*** jumped over the lazy dog (Three asterisks before and after quick brown fox)
    
4) More asterisks/_ : Superfluous : bold or italicized + bold depending on number of asterisks (even - bold, odd - italicized + bold))


5) Two ~ before and after phrase : strike out phrase

    The ~~quick brown fox~~ jumped over the lazy dog (Two tildes before and after quick brown fox)
    
6) Underlining a word does not exist in vanilla markdown (it can be handled while styling, or using html inside markdown)


# Paragraph/Line seperator

Just use enter ! Entern  twice to go next paragraph, enter once, and make sure you have two empty spaces at end of line to move to next line in same paragraph

This is the first paragraph.  
I used one enter to go to next line in the same paragraph, and made sure I had two empty spaces after the previous line. 


I used two enters to move to the next paragraph. So I am in paragraph 2. 
Using one enter to go to next line in paragraph 2 did not work as I did not have two empty spaces after the previous line



# Centering text with markdown


Similar to underlining, native markdown does not handle centering. We can handle it during styling, or using some HTML code inside markdown

<p style="text-align: center;">Centered text</p>



# Adding hyperlinks to markdown

The format used to hyperlink a phrase  is "[phrase](hyperlink address)". The hyperlink address can be a web site address or an absolute or relative path locally

[This phrase links to google](https://www.google.com)



# Adding images to markdown

The format used is  "![alt text](hyperlink to image "Optional title")" The hyperlink address can be a web site address or an absolute or relative path locally

What is alt text ?  It is a text displayed in case image is not completely loaded on the website

Image from local link - 

![alt text](pexels_ex.png "Image Credit: eberhard grossgasteiger/Pexels")  
<p style="text-align: center;">Image Credit: eberhard grossgasteiger/Pexels</p>


Image from web link - 


![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")



# Bullets and numbered bullets


Numbered bullets - just use numbers

1. This is the first point  
2. This is the second point
3. This is the third point


Non-numbered bullets - use * or - or +

* Using * : this is the first bullet
    - Using - : this is the first subbullet inside the first bullet
        + Using + : This is the first sub-subbullet :) inside the first bullet
        

#  Embedding Code

For embedding code, use three back ticks ` before and after embedded code

starting python code

```
import numpy as np
a = np.array([1,2,3])
print(a)
```

Of course this does not execute code. Jupyter is one solution to combine markdown with executable code.    
[pweave](http://mpastell.com/pweave/) might do this, have not tried it



# Line seperators

Use Three or more hyphens or asterisks or underscores

---


# Writing math equations

Markdown supports writing math equations using a latex syntax  
This can be rendered while visualizing by libraries such as [MathJax](https://github.com/mathjax/MathJax) or [KaTeX](https://github.com/KaTeX/KaTeX)

For example, Integral $\int_{a}^{b} x^2 dx = \frac{b^3}{3} - \frac{a^3}{3}$


# References

[A good reference](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#lines)
    