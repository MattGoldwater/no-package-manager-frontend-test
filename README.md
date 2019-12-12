[I experimented with trying not to use a package manager on the back-end](https://github.com/MattGoldwater/no-package-manager-backend-test). That convinced me i should use a package manager on the back-end, but I still wasn't sure if it was worthwhile on the front-end.

That's because I remembered what it was like when I first started coding when I created front-end only projects with [jQuery](https://jquery.com/). Back then I used a script tag to [load jQuery through a cdn](https://code.jquery.com/). And I didn't need to wait for jQuery to install! 

You can do the same thing today with a modern framework such as React. Open the index.html file in the folder entitled quick-react-setup to see how that works. 

I now realize that back when I was creating those jQuery projects, 2016, not every library was available over a cdn. (now every npm package can be accessed through the [unpkg cdn]((https://unpkg.com/) As a result, if you made a front-end only project you probably had to install packages through GitHub. As I established, when [I experimented with not using a package manager on the back-end](https://github.com/MattGoldwater/no-package-manager-backend-test) that takes a long time. 

In 2016, if you were willing to use npm a little you could use it to install [bower](https://bower.io/#install-bower), a front-end package manager.

However, regardless of whether you used GitHub or the Bower package manager you used script tags to load your packages. For example, here's an example of adding jQuery to your site [from the Bower docs](https://bower.io/#use-packages)

```html
<script src="bower_components/jquery/dist/jquery.min.js"></script>
```

Running libraries and your application code through script tags on the front-end led users to accidentally use or reuse global variables. 

You can check out the index.html file in the variables-add-to-global-scope directory to see how variables were added to the global scope. While, my example is short, imagine having to deal with thousands of global variables from libraries you didn't write. That often led to bugs in your programs. 

This problem was actually solved by module bundlers, rather than package managers. Module bundlers let front-end developers use a module system such as [ES modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules) (aka JavaScript Modules) to avoid adding global variables. This is explained in more detail here (https://wesbos.com/javascript-modules/). 

JavaScript module bundlers run in node on the back-end. That's why you can use them with a package manager for node such as npm, yarn or pnpm to install packages. The module bundler then creates the application or library code that will actually run on the browser.

The workflow described in the Wes Bos blog post I linked to above is still common today, though [webpack](https://webpack.js.org/) has overtaken [browserify](http://browserify.org/) as the most popular module bundler.

While I doubt package managers and module bundlers will disappear, its possible they'll become less useful in the future. 

The current versions of all major browsers natively support ES modules. This solves the problem of having too many variables in the global scope without using a module bundler or package manager. For an example of ES modules in the browser, take a look at my index.html file in the folder es-modules-in-browser. 

Then again, a lot of issues would be fixed before we directly use ES modules in the browser.

First, I'd wait for more libraries to let users import a file, which uses ES modules. For example, you could add a script tag with the attribute type set to module to [this file](https://unpkg.com/browse/d3@5.12.0/index.js) to import D3 and use ES modules.

That would look like this `<script type="module" src="https://unpkg.com/browse/d3@5.12.0/index.js">`

However, you can't currently do this with many popular libraries such as react because it [only lets users import a file that uses common js modules](https://unpkg.com/browse/react@16.12.0/index.js). [The React team is open to working on it](https://github.com/facebook/react/issues/10021). 

Additionally, you currently can't use bare specifiers in the browser. This means you'd need to type out an actual file path instead of react in the code `import React from react` or whatever library you're importing. 

Lastly, the performance of loading ES modules in the browser without a module bundler would need to be improved. That's largely because you'd need to make too many requests to the server for files. It's possible HTTP/2 Server Push and a service worker could be used to solve this problem. To learn more about the efforts to use modules in the browser you can check out [this presentation on unpkg](https://www.youtube.com/watch?v=2rhkgB8Cohc).

Using ES modules in the browser wouldn't completely eliminate the uses of a package manager or module bundler. For example, a package manager would still be useful for checks for package version updates and security vulnerabilities of your front-end dependencies. Additionally, you may still want to use features of modern module bundlers such as [tree shaking](https://webpack.js.org/guides/tree-shaking/) or minimizing your code. In this case, the tool wouldn't need to let you use ES modules or necessarily bundle your files. That means build tool would be a more appropriate name than module bundler for such a tool.
