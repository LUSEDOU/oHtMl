Simple HTML builder

Objective:

1. Separate the HTML code in files
2. Build into a single HTML file
3. Select the components

Solutions

1. Separate the HTML code in files and Select the components

1.1 Version 1
For this, the HTML code is separated into different files, each one with a given name, no matter the extension, the content or the location.
Just that, error of compilation will not be handled and the file are just concatenated.
```html
<!-- file: page_header.html -->
<h1>Header</h1>

<!-- file: page_footer.html -->
<h1>Footer</h1>

<!-- file: index.html -->
{{ ./page_header.html }}
<h1>Main</h1>
{{ ./page_footer.html }}
```

Notes
* If the file is not found, it will handled as html code.
* Just copy the content of the file, no matter the extension.
* The file path is relative to the file that is calling it.

1.2 Version 2
For this, the HTML code are wrapped into files and this files are converted into "widgets" or "components". And will be called as such.
```html
<!-- file: page_header.html -->
<h1>Header</h1>

<!-- file: page_footer.html -->
<h1>Footer</h1>

<!-- file: index.html -->
<component src="./page_header.html"/>
<h1>Main</h1>
<widget src="./page_footer.html"/>
```

Notes
* Components or widgets are the same thing.
* If the file is not found, it will handled as html code.
* The file path is relative to the file that is calling it.
* The file can be whatever extension, text, html, etc. It will be handled by the html builder itself.
* The file can be in any location, as long as the path is correct.

1.3 Version 2.5
An extension of the version 2, but with the possibility to pass parameters to the components.
```html
<!-- file: page_header.html -->
<h1>{{title}}</h1>

<!-- file: page_footer.html -->
<h1>Footer</h1>
<h2>{{ . }}</h2>

<!-- file: index.html -->
<component src="./page_header.html" title="Header"/>
<h1>Main</h1>
<widget src="./page_footer.html">
    <p>Footer</p>
</widget>
```

Notes
* The parameters are passed as attributes of the component or widget.
* If an attribute is not found, it will do nothing.
* If the component or widget is not found, it will handled as html code.
* The file path is relative to the file that is calling it.
* The build will crash if its recursive (obviously).

1.4 Version 3
A less verbose version of the version 2.5, with the possibility export the components.
```html
<!-- file: page_header.html -->
<h1>{{title}}</h1>

<!-- file: page_footer.html -->
<h1>Footer</h1>

<!-- file: barrel.html -->
<export src="./page_header.html" name="Header"/>
<export src="./page_footer.html" name="Footer"/>

<!-- file: index.html -->
<import src="./barrel.html"/>
<Header title="Header"/>
<h1>Main</h1>
<Footer>
    <p>Footer</p>
</Footer>
```

Notes
* The components are exported with a name.
* The components are imported with a name.
* The file path is relative to the file that is calling it.
* The build will crash if its recursive (obviously).
* It will crash if the component has same name as an HTML tag (like div, h1, etc).
* It will crash if the component has same name as another component, and will be handled everything as html code.
* The component can be called with or without attributes, it your fault if it has attributes and you don't pass them.
* If a component is not found, it will handled as html code.

2. Build into a single HTML file

2.1 Version 1

* The building its called by the command line, with the files to be built. With the default directory as `./build/`.
```bash
$ ohtml index.html page/page.html page/another_page.html -o ./public/
```

* If any error occurs, wont be handled or informed and will be handled as html code.
```html
<!-- file: index.html -->
{{ ./not_found_file.html }} -- Your fault
<h1>Main</h1>
<p1>Page found</p1>
```

2.2 Version 2
Can create a build watcher, that will build the files when they are changed.
```bash
$ ohtml -w index.html page/page.html page/another_page.html -o ./public/
$ Building...
$ File changed: page/page.html
$ Building...
```
Note
* It will not detect changes in the imported files, just the main file.

2.3 Version 3
Can create a server that will build the files when they are requested.
```bash
$ ohtml -s index.html page/page.html page/another_page.html -o ./public/
$ Server running at http://localhost:3000
```
Can create a server that will build the files when they are requested and watch for changes.
```bash
$ ohtml -sw index.html page/page.html page/another_page.html -o ./public/
$ Server running at http://localhost:3000
$ Building...
$ File changed: page/page.html
$ Building...
```

--------------------------------------------
Side notes (optional features not covered in this document)
* LSP (Language Server Protocol) for the editor.
```html
<!-- file: footer.html -->
<!-- @param title subtitle subtitle2 -->
<h1>{{title}}</h1>
<h2>{{subtitle}}</h2>
<h3>{{subtitle2}}</h3>
```

* Error messages.
    * File not found.
    * Component not found.
    * Component with same name as another component.
    * etc

