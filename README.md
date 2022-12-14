# Xmas Flipbook
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
- For this to look like an open book, "pages" and "covers" need to have their gradient backgrounds reversed.
- `rotatable` is used to specify things like the rotation and origin. For the left side divs, the point of origin is the right edge, and for the right side divs, the point of origin is the left edge. 

## jQuery
The `book` object contains
- `currentView`: an integer (min 0) that tracks which element of `views` is currently active.
- `views`: an array of objects. Each object contains
    - `left` and `right`. Either or both can be present depending on what the current view requires.
        - `class`: The CSS style used for the visual of that view ("page" or "cover")
        - `pagenumber`: An integer. Present only if there is a page number.
        - `content`: text string for the HTML content.
- `flip`: a method which accepts one argument, `dir`.
    - `dir` is either 1 for forward or -1 for backward. 
    - checks if `dir` plus `currentView` is valid, and exits early if not.
    - if forward flip...
        - disable buttons
        - rotate `right_front` but at 1 second transition.
        - after 1 second (less a few milliseconds), call `renderView()`.
        - rotate `left_front` immediately.
        - after a very short time (a few milliseconds?), un-rotate `left_front` but at 1 second transition.
        - after 1 second, re-enable buttons.
    - if backward flip, do as for forward flip but reversed. 
- `renderView`: a method which generates the pages based on the value of `currentView`. 
    - If `currentView` is 2 or 2 less than the length of `views`, that means the cover must be rendered as a background. `left_back` and `right_back` are rendered using the HTML content from the first and last elements of `views`.
    - If `currentView` is 1 or 1 less than the length of `views`, that means the intermediary pages must be rendered. `left_middle` and `right_middle` are rendered using the HTML content from the previous or next (from `currentView`) elements of 'views`.
    - In any case, `left_front` and `right_front` must be rendered.
    - Rendering is done using `renderPage()`.
- `renderPage`: a method which populates a placeholder with HTML content, accepts a string which is the id of the placeholder (`id`) and an object which contains HTML content (`obj`).
    - create a div.
    - if placeholder is `left_front` or `right_front`, add CSS class "rotatable" and either "page" or "cover". If not, just add CSS class "page" or "cover" (depending of the `class` property of `obj`).
    - if `obj` contains `pagenumber`, insert a div with class of "pagenumber" and insert the value of `pagenumber`.
    - insert a div with the `content` property from `obj`.
    - insert the entire thing into the placeholder identified by `id`.
    
