# Glyder

Glyder is a flexible markdown-based style guide generator with support for code previews.

Once installed, the `glyder` command can be used to transform any directory of Markdown files into a website.


## Installation

Glyder can be installed with plain ol' NPM:

    npm install -g glyder

If you'd like to install it local to a project, use the `--save-dev` flag:

    npm install --save-dev glyder

Please note that if you install glyder local to a project you will need to use the `npx` command with the glyder binary. For example:

    npx glyder --help


## Configuration

Configuration is stored in a `glyder.json` file stored in the root of your Glyder project.

Here are the options, with default values shown:


    {
      "input": "src",                        // Directory where markdown and other source files are stored
      
      "output": "build",                     // Directory where build files are generated (HTML, etc.) 

      "tmp": ".tmp",                         // Directory for temp files generated by glyder command

      "logo": "/glyder-logo.svg",            // Relative URL for the logo of your project

      "edit": null,                          // Edit URL template. Use this format for GitHub:
                                             // "http://github.com/username/repository/edit/master/%filename%"

      "copyright": "© %Y Your Company Here"  // Copyright for your project filtered through strftime

      "sections": [                          // Sections for the navigation 
        { "name": "Guidelines", "key": "guidelines" },
        { "name": "Components", "key": "components" }
      ],

      "packages": [                          // Package sets for code previews
        {
          name: 'oxygen',
          styles: [ 'http://oxygencss.com/styles/site.css' ],
          scripts: [ 'http://oxygencss.com/styles/site.js' ]
        }
      ]
    }


## Composing articles

Articles are created by putting markdown files in your source directory. By default this is `src` in the root of your project, but it can be configured in the Glyder configuration file (`glyder.json`). All markdown files must use the ".md" file extension.

Glyder articles must include front matter. By default the title key is the only required frontmater option:

    ---
    title: My article
    ---

    Markdown contents here

Frontmater options include:

| Key            | Description |
| :------------  | :---------- |
| **title**      | The title of the article. This appears as an H1 at the top of the page. |
| **section**    | The section in the side navigation where this article should appear. Sections are reference by key and can be declared in your Glyder config. |
| **index**      | Used to order the navigation within a section in the sidebar. Lower values are sorted first. And then by the title of the article. By default articles have a index value of 100. |
| **noHeading**  | Do not output the title. Instead rely on the author to include it in the Markdown portion of the article. |
| **redirectTo** | Redirect to a specific URL. Implemented with an HTML meta refresh tag. |


## Development server

To bring up a lightweight developement server to preview your project, use the `serve` command:

    glyder serve

This will launch a preview server here:

  <http://localhost:9000>

You must use the glyder command from the root directory of the project.


## Building HTML

To generate a site in the build directory (specified in the config), use the `build` command:

    glyder build 


## Made with Gulp

Glyder is really a frontend for a bunch of [Gulp][gulp] tasks that combine to make a flexible style guide generator. If you are familiar with Gulp, you should find it fairly easy to contribute.


## Acknowledgements

Originally based on code from [John Long's styleguide repo][styleguide] with improvements by [Michael Lee][mlee].

[styleguide]: https://github.com/jlong/styleguide
[mlee]: https://github.com/michaellee
[gulp]: http://gulpjs.com/
