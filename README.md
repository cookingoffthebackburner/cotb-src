# Cooking Off The Backburner

Website source code, with theme by Bootstrapious and Kishan B, (very) slight modifications by Rob Amezquita, and content by Annie Nguyen and Rob Amezquita, et al. 

## Source code layout

Source is organized as a default hugo themed website - [see the docs](https://gohugo.io/about/) for more information. 

Briefly:

* `content` - the _About_ and _Contact_ single pages, as well as the _Blog_ folder which contains all the blog posts. 
* `static` - files that can be referenced by posts, such as images; for any image reference in a post, link it in the form `/img/[blog-date-and-title]/[image-name.[JPG|PNG]]`
* `public` - do not touch this folder, as this is compiled every time via the hugo/blogdown engine, anything changed here will be overwritten; contains the website's current build
* `themes` - this is where all the code for the website theme's structure lives in "offthebackburner"

Within `themes/offthebackburner`, is the website's skeleton. Again, more info can be found on the hugo docs, but briefly the most important are:

* `layouts` - the skeletons to construct the various different types of pages
* `static` - the javascript and css that makes the website interactive and gives it its styling; the `css` folder is where site can be configured for colors, fonts, etc.


## Building the website

I use `R` to build the website using the `[blogdown](https://github.com/rstudio/blogdown)` package. The easiest way to install `R` is by first installing [`Homebrew`](https://brew.sh/) through the Terminal app, then running in a Terminal the following line (note that lines that start with a `#` are comments, and not actually run by the programs):

```{sh}
brew install R-devel
```

Once `R` is installed, in the Terminal, type `R` and press enter to start the `R` interpreter, and then run:

```{r}
install.packages('devtools') # if successful, then run:
devtools::install_github('rstudio/blogdown')
```

Once those are done installing, blogdown can the be used to build/serve the site. First, change the active directory to where the website source code is kept:

```{r}
setwd('/path/to/website') 
# tip: you can drag and drop via Finder the 
# website folder to the terminal and automagically
# get the path
```

Once that is all successfully installed and your current directory is set to the blog folder location, you can then run the following line to build/serve the website:

```{r}
blogdown::serve_site() 
```

This will render the website and serve it. Any changes that are made to the files prompt `R` to automatically re-build the website and refresh it as well, allowing for semi-interactive work on the site.


### Alternative: using Hugo

Alternatively, the website can be built using Hugo directly potentially but I have not tested this..


## Posts

(New) Posts are placed into the `content/blog` folder. Each post is formatted as a markdown file. For a quick primer, visit [the markdown guide](https://www.markdownguide.org/cheat-sheet) or view the example posts within the folder. 

### YAML Header

Various information is stored in the header portion delimited by `+++`. The options are:

* `showonlyimage` - set this to `true` to show only an image with no description on the website, or `false` if a description below the image is desired
* `draft` - whether to publish the post; useful for having in progress drafts that are not published to the main website
* `image` - the path to the hero image; images should live in the `static/img` folder, and are referenced as `img/[folder; ideally portfolio]/[folder for post with its title]/[image-file]`
* `date` - date should be formatted as `YYYY-MM-DD`; time can be appended as `T` followed by `HH-MM-SS` and the time zone modifier additionally appended as `+HH:MM`
* `title` - the title!
* `weight` - the "order" of the post relative to other posts; just keep this at 1, and posts will auto sort based on most recent date of publication

### Lead

The lead can be one or two short sentences that are posted below the image on the front page (assuming `showonlyimage = false` in the YAML header). The lead is ended by typing:

```{html}
<!--more-->
```

After the above line, any content will only appear upon following the link.

### Post content

A post can have text, pictures, links, etc. Simply follow the markdown guide, make sure image reference links are correct, and type away!


## Pushing the website live

To push the website live, the `/public` folder will need to be pushed to the repo `github.com/cookingoffthebackburner.github.io`. Simply change directories to `/public`, add changes within the folder, and then push. The `/public` directory will (should probably!) be left untracked by in the `cotb-src` repo to reduce redudundancy.
