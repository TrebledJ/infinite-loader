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

3. Add CSS for the spinner. Infinite Loader will only try to lazy load posts if there's a spinner present. You can choose to...

    * `spinner.css` contains a simple CSS spinner that works in most modern browsers. Open up `css/main.css`, and at the very end, paste everything from `spinner.css`. 
    * If you're using SASS, rename `spinner.css` to `_spinner.scss` and add an import in your main SCSS file.
        ```css
        @import "spinner";
        ```

4. Follow examples from `examples/*/`, depending on which static site generator you're using.

    * For Jekyll, copy `all-posts.json` to your project root.
    * For Eleventy, copy `posts.njk` and `all-posts.json.njk` to `content/`.

5. Build your site. You should be able to see the infinite loader in action at `localhost:XXXX/infinite-posts`. (Replace `XXXX` with your site port: 4000 for Jekyll, 8080 for Eleventy.)


## Configuration

### Parameters

* `data`: Path to your JSON data. This data should be a JSON **array**. Array elements can be *any* JSON data, which can be passed to a custom data-to-HTML conversion function (see the `html` parameter).
* `items.num`: Initial number of items to load. Defaults to 10.
* `items.after`: Subsequent number of items to load. Subsequent loads are triggered when the user scrolls beyond a certain threshold. Defaults to `items.num`.
* `items.max`: Maximum number of items to load. Loading stops indefinitely after loading this many items. Unlimited by default.
* `append`: The id/class element to append your HTML to. Defaults to `.post-list` (i.e. `class="post-list"`).
* `html`: A string or converter function. If `typeof html ===`
    * `"string"`: then `html` be appended directly to the target element.
    * `"function"`: then `html` will be used to convert your JSON data to HTML. An example function is:
    ```js
    (item, index) => {
        return `<p>Post ${index+1}: <a href="${item.url}">${item.title}</a></p><br/>`;
    }
    ```
    A couple parameters are passed to the function:
    * `item` is the data from your JSON data file (see the `data` parameter).
    * `index` is the index of the item. Index 0 refers to the first item in your JSON array.

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
