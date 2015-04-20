# Style Guide

[Our style guide](http://styleguide.fusion.net/) is an auto-updated tool based on KSS that organizes the available objects and styles within the Fusion theme repository.

## How to update the style guide content
The style guide is maintained by commenting on the Fusion Theme’s SASS files. Style guide comments should be placed above the corresponding code, wherever possible.

Here's an example:

    /*doc
    ---
    title: Blockquote
    name: blockquote
    category: Typography
    ---

    ```html_example
    <div class="article-content">
        <blockquote>
        <p>Blockquote style for within article content.</p>
        </blockquote>
    </div>
    ```
    */

- `title` is the descriptive title of the content “block” with a page.
- `name` is the anchor name of the content “block” within a page. (note: this name should be a single word. For example, “photo caption” should become “photocaption”.)
- `category` is the page that the block belongs to.

There are two content block templates.

- `html_example` will create a single example block
- `html_example_table` will create multiple examples in a table format.