---
title: Extensions
nav_order: 40
has_children: true
---

# Extensions

Lamarkdown provides access to [Python-Markdown extension system](https://python-markdown.github.io/extensions/), to extend the markdown language. (The core language, though clean and simple, is too limited for many purposes.)

In Lamarkdown, you can determine which extensions you want to use in several ways:

* Accept the defaults (which are in place if you don't have a build file);

* Write a build file that calls `doc()` or another such function representing a predefined bundle of settings which happens to include an extension.

* Write a [build file](./BuildFiles) that calls `extension()` or `extensions()`. Normally you would provide one or more extension names, as strings. You can also pass in an Extension _object_, which may be easiest if you choose to create your own extension(s).

{: .note}
An _extension_ changes the markdown dialect, whereas other constructs provided by Larmarkdown (like `doc()` and build files) make decisions about _which_ extensions to use, as well as the styling/scripting of the output document.


## What Extensions are Available?

* Python-Markdown provides [various standard extensions](https://python-markdown.github.io/extensions/). Some, [attr_list](https://python-markdown.github.io/extensions/attr_list/) in particular, may be important for styling, scripting and accessibility purposes.

* Lamarkdown provides some of its own extensions:

    * [`lamarkdown.ext.eval`](eval.md) lets you insert placeholders using the syntax `` $`...` ``, to be replaced by corresponding values defined in the build file. If `allow_code` is enabled, this also lets you insert full Python expressions, which will be evaluated and replaced by their result.
    * [`lamarkdown.ext.heading_numbers`](heading_numbers.md) adds a decimal numbering scheme to document headings.
    * [`lamarkdown.ext.latex`](latex.md) lets you insert Latex code, to be compiled, converted to SVG, to be embedded in the output HTML.
    * [`lamarkdown.ext.markers`](markers.md) lets you assign styling to lists.
    * [`lamarkdown.ext.sections`](sections.md) lets you divide a document into `<section>` elements using `---` dividers, which may be used to create slideshows with [RevealJS](https://revealjs.com/)), for instance.

* [PyMdown Extensions](https://facelessuser.github.io/pymdown-extensions/) provides a range of other specialist extensions. Lamarkdown has a dependency on PyMdown Extensions, so you should be able to use these without too much trouble.

* The Python-Markdown documentation also lists a [range of other third-party extensions](https://github.com/Python-Markdown/markdown/wiki/Third-Party-Extensions). You will need to manually install these, though.

* You can create your own extensions, conforming to the [Python-Markdown extensions API](https://python-markdown.github.io/extensions/api/).


## Extension Configuration

Each extension can have configuration options. In Lamarkdown, these can be set by calling `extension()`, and passing it a keyword argument for each option you want to configure. You can call `extension()` multiple times for a given extension in order to accumulate or overwrite various options. It also returns a dictionary of config options, letting you query their current values and modify them asynchronously.

The `extension()` function is also described in the [Build API](../build_files.md#build-api).

Note that [Python Markdown](https://python-markdown.github.io/reference/) uses a parameter called "`extension_configs`" to specify configuration options to extensions, and Lamarkdown ultimately uses this mechanism, but does not _directly_ expose it to build files.
