[I experimented with trying not to use a package manager on the back-end](https://github.com/MattGoldwater/no-package-manager-backend-test). That convinced me i should use a package manager on the back-end, but I still wasn't sure if it was worthwhile on the front-end.

That's because I remembered what it was like when I first started coding when I created [jQuery](https://jquery.com/) projects. Back then I used a script tag to load jQuery  through a cdn on the front-end. And I didn't need to wait for jQuery to install! 

You can do the same thing today with a modern framework such as React. Open the index.html file in the folder entitled quick-react-setup to see how that works. 

But, I realize now that at that time, 2016, not every library was available over a cdn. As a result, many front-end developers had to install packages through GitHub. As I established, when trying to not use a package manager on the back-end that's a pain. 

Furthermore, running libraries and your application code through script tags on the front-end led users to accidentally use or reuse global variables causing errors in their program. 

You can check out the index.html file in the variables-add-to-global-scope directory to see how variables were added to the global scope. While, my example is short, having to deal with thousands of global variables from libraries you didn't write could cause bugs in your program. 

To solve these problems developers turned to module bundlers, which let front-end developers use a module system to avoid adding global variables. This is explained in more detail here (https://wesbos.com/javascript-modules/). If you've already used ES modules and a module bundler in a project before you can stop reading that article at the header "Creating Your Own Modules." 

JavaScript module bundlers run in node on the back-end. That's why you can use a package manager for node to install packages. The module bundler will create the application or library code that will actually run on the browser.

The workflow described in the wes bos blog post I linked to above is still common today, though [webpack](https://webpack.js.org/) and [parcel](https://parceljs.org/) have emerged as the two most popular module bundlers.

While I'd still recommend using a package manager and module bundler today, I think this could change in the future. Firstly, now [unpkg](https://unpkg.com/) exists, which is a cdn for every package on the npm package registry. This means you can now put any package in a script tag and not take the time to install a package. 

Secondly, the current versions of all major browsers natively support ES modules, which prevents developers from having to worry about accidentally overwriting a global variable in their project. For an example, take a look at my index.html file in the folder es-modules-in-browser. 

Before switching to using ES modules in the browser I'd wait for more libraries to let users import a file, which uses ES modules. For example, you could add a script tag with the attribute type set to module to [this file](https://unpkg.com/browse/d3@5.12.0/index.js) to import D3 and use ES modules.

That would look like this `<script type="module" src="https://unpkg.com/browse/d3@5.12.0/index.js">`

However, you can't currently do this with many popular libraries such as react because it only lets users import a file that uses common js modules. Additionally, the performance of loading ES modules in the browser still needs to be improved. If you want to learn more about modules in the browser you can check out [this presentation on unpkg](https://www.youtube.com/watch?v=2rhkgB8Cohc).

Even if these problems were solved there still would be a use for a tool that checks for updates and security vulnerabilities of your front-end dependencies.
