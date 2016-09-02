# Contributor guidelines

These guidelines provide the general process for maintaining source code that builds the 
Rackspace Cloud Files developer documentation. 

- [Project description](#project-description)
- [Updating and adding content](#updating-and-adding-content)
- [General style guidelines](#general-style-guidelines)
- [Submitting your content](#submitting-changes)
- [Previewing changes](#previewing-changes)

##Project description
<!-- Provide as little or as much information about architecture as needed to help 
contributors figure out which file to update.-->

This project is developed and built by using the 
[Python Sphinx documentation generator](http://sphinx-doc.org/). Content is 
written in [reStructuredText](http://sphinx-doc.org/rest.html), which is the markup syntax and 
parser component of [Python Docutils](http://docutils.sourceforge.net/index.html).

Source files for the Sphinx documentation project are in the ``api-docs`` directory. 
Following are the key files that define project and content architecture: 


Content | File
--- | ---
|Index page for the main content structure| [index.rst](https://github.com/rackerlabs/docs-cloud-files/blob/master/api-docs/index.rst)
|Getting started|[getting-started folder](https://github.com/rackerlabs/docs-cloud-files/blob/master/api-docs/getting-started)
|General API information|[general-api-info folder](https://github.com/rackerlabs/docs-cloud-files/blob/master/api-docs/general-api-info)
|Use cases index|[use-cases folder](https://github.com/rackerlabs/docs-cloud-files/blob/master/api-docs/use-cases)
|Storage API reference| [storage-api-reference folder](https://github.com/rackerlabs/docs-cloud-files/blob/master/api-docs/storage-api-reference)
|Storage API operations methods including code samples|[storage-api-reference/methods folder](https://github.com/rackerlabs/docs-cloud-files/tree/master/api-docs/storage-api-reference/methods)
|CDN API reference| [cdn-api-reference folder](https://github.com/rackerlabs/docs-cloud-files/blob/master/api-docs/cdn-api-reference)
|CDN API operations methods including code samples|[cdn-api-reference/methods folder](https://github.com/rackerlabs/docs-cloud-files/tree/master/api-docs/cdn-api-reference/methods) 
|Release notes folder|[release-notes](https://github.com/rackerlabs/docs-cloud-files/tree/master/api-docs/release-notes)
|Sphinx documentation configuration file| [conf.py](https://github.com/rackerlabs/docs-cloud-files/blob/master/api-docs/conf.py) (Typically, this file does not require changes.)
|Linux and OS X build script|``Makefile``|
|Windows build script|``make.bat``|



## Updating and adding content

Contributions are submitted, reviewed, and accepted by using GitHub pull requests, following the [GitHub workflow](GITHUBING.md) for this repository. 

To update existing source files or add new ones, follow the [GitHub workflow](GITHUBING.md) for this repository.

* Update source files by using the GitHub editor or any plain text editor.
* Format source files with 
  [reStructuredText syntax](http://www.sphinx-doc.org/en/stable/rest.html).  
* For quick syntax checking, try the 
[Online reStructuredText editor](http://rst.ninjs.org/). 

## General style guidelines

When you add or update content, use the following general style guidelines, which are 
described in detail in [Style guidelines for technical content](http://rackerlabs.github.io/docs-rackspace/style-guide/index.html):

- Use [sentence-style capitalization](http://rackerlabs.github.io/docs-rackspace/style-guide/a-l-style-guidelines.html#titles-and-headings) for titles and headings
- Use consistent [text formatting](http://rackerlabs.github.io/docs-rackspace/style-guide/m-z-style-guidelines.html#text-formatting)
- Write clear and consistent [code examples](http://rackerlabs.github.io/docs-rackspace/style-guide/a-l-style-guidelines.html#code-examples)
- Use [active voice](http://rackerlabs.github.io/docs-rackspace/style-guide/basic-writing-guidelines.html#use-active-voice)
- Use [present tense](http://rackerlabs.github.io/docs-rackspace/style-guide/basic-writing-guidelines.html#use-present-tense)
- Write to the user by using [second person and imperative mood](http://rackerlabs.github.io/docs-rackspace/style-guide/basic-writing-guidelines.html#write-to-the-user-by-using-second-person-and-imperative-mood)
- Write clear and consistent [step text](http://rackerlabs.github.io/docs-rackspace/style-guide/m-z-style-guidelines.html#tasks-and-procedures)
- Clarify [pronouns](http://rackerlabs.github.io/docs-rackspace/style-guide/basic-writing-guidelines.html#clarify-pronouns) such as *it*, *this*, *there*, and *that*
- Clarify [gerunds and participles](http://rackerlabs.github.io/docs-rackspace/style-guide/basic-writing-guidelines.html#clarify-gerunds-and-participles)
- Use [consistent terminology](http://rackerlabs.github.io/docs-rackspace/style-guide/basic-writing-guidelines.html#use-consistent-terminology)

<!-- Adding build from source guidelines until we can provide a link to automated gh-pages 
output, or to the staging URL that Ash is working on. 
--> 

# Submitting changes

When you've completed your changes, submit a pull request. Someone on the Information Development team will review your PR.
- Minor updates and corrections get a quick review to ensure that content is error-free and doesn't introduce other issues.
- More complex changes or additions require both technical and editorial review. 

Depending on the review feedback, you might be asked to make additional changes. 

After content has been reviewed and approved, the updates can be merged to the master branch. The merge triggers the build and 
deploy process. Typically, new content is available on developer.rackspace.com within a minute or two after it is merged. Larger 
updates might take a bit longer.

## Previewing changes

When you submit a pull request, the Strider build process creates a preview of your changes in a staging environment. 
After the build process completes, the following message displays in the pull request comments with a link to the content: ``Your content preview is now ready.``

You can also build the project locally using the [Sphinx documentation generator](http://sphinx-doc.org/). For details, see 
[Building from source](https://github.com/rackerlabs/docs-rackspace/blob/master/doc/tools/build-from-source.rst).

