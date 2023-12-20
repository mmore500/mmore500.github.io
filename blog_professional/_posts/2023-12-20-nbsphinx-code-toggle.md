---
layout: post
title:  "Toggle Jupyter Code Cells in nbsphinx Documentation"
date:   2023-12-20
no_toc: true
---

Gallery and cookbook sections punch way above their weight in software documentation.
The best way to get started with something new is often with something that already works.

To keep content in sync and stay sane managing generated output files, some kind of tooling beyond manual updatesbecomes necessary.
A Jupyter notebook would be great for this --- and, indeed, there's a nice existing ecosystem to marry notebooks and Sphinx documentation.
Among other tools, `nbsphinx` will execute `.ipynb` files and inject the output into the documentation build.
ReadTheDocs has [a great primer on the subject](https://docs.readthedocs.io/en/stable/guides/jupyter.html).

## Problem

Although the code should certainly be available, I've found it's nice to have it collapsed away to make gallery content more skimmable.
Toggling seems like an ideal solution --- readers can pop open cells as they read along and click to expand snippets they're particularly interested.
The nbsphinx package only supports [entirely-hidden cells](https://nbsphinx.readthedocs.io/en/0.9.3/hidden-cells.html).

Although there appears to be something a cottage industry of one-off code snippets related to this problem in interactive Jupyter notebooks, I came up empty trawling Google and StackOverflow for Sphinx-specific solutions.
Eoin Travers in particular has a nice [blog post](http://eointravers.com/post/jupyter-toggle/) on toggle buttons in Jupyter notebooks by way of IPython JavaScript magic (i.e., `%%javascript`) for runtime injection of code into the notebook's DOM at runtime.
Most of the other solutions I found were variations on this theme.

For compatibility with the `nbsphinx` pipeline, where notebooks execute only at build time and not in viewer's DOMs, I thought to take another tack to injecting buttons: having Sphinx bundle JavaScript with the built html docs.
Sphinx has a straightforward hook for this.

After a little styling and animation fiddling, here's what it looks like in action.

![toggling notebook cell in sphinx docs](/resources/2023-12-20-nbsphinx-code-toggle.gif){:style="width: 80%;display:block; margin-left:auto; margin-right:auto;"}

To get things readable, I ended up adding `<hline>` breaks around code cells and hiding the cell numbers.

## Ctrl-C Ctrl-V

Anyway, here's the code you'll want.

add to `docs/conf.py`:
```python
# -- Options for HTML output -------------------------------------------------

# Add any paths that contain custom static files (such as style sheets) here,
# relative to this directory. They are copied after the builtin static files,
# so a file named "default.css" will overwrite the builtin "default.css".
html_static_path = ["_static"]

html_js_files = [
    "hide_code_cells.js",
]
```

`docs/_static/hide_code_cells.js`:
```javascript
document.addEventListener("DOMContentLoaded", () => {
    // Function to create and append a toggle button to a div
    const addToggleButton = (div) => {
        const button = document.createElement("button");
        button.textContent = "Show Code »";
        styleButton(button);
        initializeDivStyle(div);
        addClickEvent(button, div);
        insertButtonAboveDiv(div, button);
    };

    // Styling the toggle button
    const styleButton = (button) => {
        Object.assign(button.style, {
            backgroundColor: "#F5F5F5",
            color: "#333333",
            border: "1px solid #DDD",
            padding: "2px 5px",
            marginTop: "5px",
            cursor: "pointer",
            borderRadius: "3px",
            fontSize: "0.9em",
            width: "100%",
            maxWidth: "100px",
            transition: "max-width 0.5s ease, background-color 1s ease"
        });
    };

    // Initialize div style for hiding
    const initializeDivStyle = (div) => {
        Object.assign(div.style, {
            opacity: '0',
            maxHeight: '0px',
            overflow: 'hidden',
            transition: 'opacity 0.2s ease, max-height 0.6s ease'
        });
    };

    // Handle click event for the toggle button
    const addClickEvent = (button, div) => {
        button.onclick = () => {
            if (div.style.maxHeight === '0px') {
                Object.assign(div.style, {
                    opacity: '1',
                    maxHeight: '500px',
                });
                button.textContent = "»» Hide Code ««";
                button.style.maxWidth = "100%";
            } else {
                Object.assign(div.style, {
                    opacity: '0',
                    maxHeight: '0px'
                });
                button.textContent = "Show Code »";
                button.style.maxWidth = "100px";
            }
        };
    };

    // Insert the toggle button above the div
    const insertButtonAboveDiv = (div, button) => {
        const hr = document.createElement("hr");
        div.parentNode.insertBefore(hr, div);
        div.parentNode.insertBefore(button, div);
    };

    // Select and apply toggle functionality to code and output divs
    const codeDivs = document.querySelectorAll('.nbinput.docutils.container');
    codeDivs.forEach(addToggleButton);

    // Hide cell numbers (which don't play nice with button layout)
    const outputDivs = document.querySelectorAll('.prompt');
    outputDivs.forEach(div => div.style.display = 'none');
});
```
