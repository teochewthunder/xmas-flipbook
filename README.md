# Xmas Flipbook (in progress)
This is a HTML/CSS/jQuery script that simulates a Christmas-themed flipbook.

## HTML
For this to work, we need two divs as placeholders for "pages" on the left side and right side. Each side has:
- a div with id `left_back`
- a div with id `left_middle`
- a div with id `left_front`
- these three divs are layered on top of each other, with `left_back` at the rear, followed by `left_middle` superimposed on top of it, and `left_front` on top of them both. Repeat the same for the right side, with the appropriate ids.

We also have two buttons at the bottom to "flip" left and right.

## CSS
- `cover` styles divs that are supposed to look like covers.
- `page` styles divs that are supposed to look like pages. They are slightly smaller than "covers" and some floating is required to fold it all together.
- FOr this to look like an open book, "pages" and "covers" need to have their gradient backgrounds reversed.
- `rotatable` is used to specify things like the rotation and origin. For the left side divs, the point of origin is the right edge, and for the right side divs, the point of origin is the left edge. 

## jQuery
