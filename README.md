Infinite Loader
===============

Infinite scroll for Jekyll, Eleventy, and other static site blogs.

See it rollin':

* [Infinite SoundCloud Embeds](https://trebledj.github.io/music)
* ...other examples to come?

## Getting Started

1. Load jQuery. Infinite Loader uses jQuery, if you haven't installed it yet, you can use the quick 'n dirty method by pasting this in your `head.html` (or wherever your `<head>` element is):
    ```html
    <script src="https://code.jquery.com/jquery-3.6.3.min.js"></script>
    ```

2. Copy `/js/infinite-loader.js` to your site.

3. Add CSS for the spinner. You can choose to...

    * `spinner.css` contains a simple CSS spinner that works in most modern browsers. Open up `css/main.css`, and at the very end, paste everything from `spinner.css`. 
    * If you're using SASS, rename `spinner.css` to `_spinner.scss` and add an import in your main SCSS file.
        ```css
        @import "spinner";
        ```

    Infinite Loader will only try to lazy load posts if there's a spinner present.

4. Depending on whether you're using Jekyll, Eleventy, or some other static site generator, you'll want to copy files from `examples/*/`.

    * For Jekyll, copy `all-posts.json` to your project root.
    * For Eleventy, copy `posts.njk` and `all-posts.json.njk` to `content/`.

5. Build your site. You should be able to see the infinite loader in action at `localhost:XXXX/infinite-posts`. (Replace `XXXX` with your site port: 4000 for Jekyll, 8080 for Eleventy.)


## Configuration

### Parameters

* `data`: Path to your JSON data. This data should be a JSON **array**. You may fill this array with strings, objects, and whatnot, as you'll be the one handling this data in the end (see the `html` parameter).
* `items.num`: Initial number of items to load. Defaults to 10.
* `items.after`: Subsequent number of items to load. Subsequent loads are triggered when the user scrolls beyond a certain threshold. Defaults to `items.num`.
* `items.max`: Maximum number of items to load. Loading stops indefinitely after loading this many items. Unlimited by default.
* `append`: The HTML id or class to append your HTML to. Defaults to `.post-list` (i.e. `class="post-list"`).
* `html`: A string or converter function. If a string, it will be appended directly. If a function, it will be used to convert items to HTML. An example function is:
    ```js
    (item, index) => {
        return `<p>Post ${index+1}: <a href="${item.url}">${item.title}</a></p><br/>`;
    }
    ```
    * `item` is whatever object you used in your data file (see `data` parameter).
    * `index` is the index of the item your JSON data. Index 0 refers to the first item in the list.

### Example
```js
$(async function() {
    InfiniteLoader({
        data: "/path/to/data.json",
        items: {
            num: 10,
            after: 5,
            max: 30,
        },
        append: '#post-list',
        html: item => `<p>${item}</p><br/>`,
    });
});
```
