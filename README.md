# Newpaper Hugo Subtheme
### newspaper-hugo-subtheme

First credit goes to Silke V at codepen.io name "silkine" [http://www.silkevoigts.de/].
Original source code can be found here: https://codepen.io/silkine/pen/jldif

![](./static/img/newspaper-hugo-subtheme.png)

I had a coworker who had a non-profit business blog that wanted to offer a newsletter to her clients.
So I got interested in finding an HTML format that gave an old traditional newspaper style
and Silke offered a solution that provided a strong simple css base. Currently (2017) I find
the hugo cms system to be the easiest most portable static web building application freely available.
The challenge was to create a full newsletter style theme as a subtheme within an existing theme
structure. So I mocked up a ported version of Silke's newspaper css into a hugo "section".

This project is a drop in offering to any existing hugo themed structure which will produce
a newsletter format in an "article(s)" hugo section. A user only needs to change the title, city,
and state varbiable that are stored as front matter in the ./content/articles/_index.md file.
Hugo uses this file natively to discover section (in this case "articles") specific data. All
posts to the newsletter subtheme should be created in this ./content/articles/ directory as markdown
files. Running hugo new articles/mynewarticle.md will create a new file with the default front matter
pulled from ./archtypes/articles.md.

This project then becomes a drop in addition to any hugo theme to add a newspaper type subtheme section.

<!--more-->

It might be useful to examine the directoy file structure for this project:

<pre>
============================================================
+-----archtypes
|     +-----articles.md # this file is used by hugo when you create a new article - provides front matter
+-----content
|     +-----articles # this is where all user created article markdown postings reside
|     |     +-----_index.md # this file is used by hugo to read front matter and populate general variable - similar to a config file
|     |     +-----newspaper-hugo-subtheme.md # this file - an article posting
+-----layouts
|     +-----articles # layout template specific to single page articles
|     |     +-----single.html # hugo uses this template to produce and single page for a posted article
|     +-----partials # tmeplates used for building all newsletter-hugo-subtheme pages - thanks and credit to codepen.io name "silkine"
|     |     +-----np-cols-ftr.html
|     |     +-----np-cols-hdr.html
|     |     +-----np-ftr.html
|     |     +-----np-hdr.html
|     |     +-----np-morebox.html
|     |     +-----np-nav.html
|     |     +-----np-weather.html
|     +-----section # hugo uses this directory to find "section" specific "list" templates
|     |     +-----articles.html # hugo uses this (optional - not included here) template to combine postings into a newletter front page
+-----static
|     +-----css # needed newspaper styles - (can be shared with other themes of course)
|     |     +-----np-gen.css # newspaper general styles
|     |     +-----np-nav.css # styles needed for menu navigation
|     +-----js # directory for local javascript code - (can be shared with other themes of course)
|     |     +-----np-nav.js # navigation menu javascript
|     |     +-----np-weather.js # weatherbox javascript - credit and thanks to simpleweatherjs.com
|     +-----img # directory for all images used in article (can be shared with other themes of course)
|     |     +-----np.jpg # used as the background for newpaper-hugo-subtheme
|     |     +-----royal101.jpg # a sample only
============================================================
</pre>

I have used the hugo "casper" theme (https://github.com/vjeantet/hugo-theme-casper.git) as my standard for some time now so the 
menu format is in this project is similar to (but not as good as) the casper theme navigation menu. Note also that the menu
system used here is the standard hugo menu.main method for generating menu entries. These entries come from either
your config.toml file and/or markdown files that have this included in the front matter

Your base build directory will have a config.toml file and if entries such as these below exist they will be included in the
newspaper subtheme menu.

```
# config.toml
# ... examples only
[[menu.main]]
  name = "About"
  weight = 130
  identifier = "about"
  url = "//page/about"

[[menu.main]]
  name = "Contact"
  weight = 140
  identifier = "contact"
  url = "//page/contact"

[[menu.main]]
  name = "Links"
  weight = 150
  identifier = "links"
  url = "//page/links"
# ...
```

As a default this next line is included in the ./content/articles/_index.md which is normally used by hugo 
when building out the ./layouts/articles/list.html page but this subtheme also grabs the front matter
values for the ./layouts/articles/single.html builds as well using the .GetPage method. The next line is included
in the ./content/articles/_index.md to add the Title "Newspaper" to the "main" menu.

```
# This line exists in ./content/articles/_index.md to populate 
# the main menu with the Title value also declared in this file
menu = "main"
```

Also the template file for the footer (./layouts/partial/np-ftr.html) will use additional entries in the base 
config.toml file to populate the copyright footer.

```
# config.toml
# ... example only
Title= "Your Company"
Copyright = "Copyright &copy; yourdomain.com"  
# ...
```

All the section pages will include the Title (Newspaper) from ./content/articles/_index.md becuase 
it also includes the above menu = "main" line.

### Installation:

* build out a standard hugo site with any theme you prefer.
* from the base hugo working directory for that site extract these project files or
  add these files by git clone ie:
```
cd /tmp/
git clone https://github.com/geoffmcnamara/newspaper-hugo-subtheme
cd newspaper-hugo-subtheme
rsync -av --exclude=".*" --exclude="README.md" ./ /your/hugo/website-base/  # this will exclude the .git directory and the README.md
cd /your/hugo/website-base/
```
* edit the ./content/articles/_index.md file to change the general variables used in this subtheme
* build your hugo files with:
```
hugo serve -v
```
* use your browser and go to localhost:1313/articles/

### Notes:

* Several google fonts are called in ./layouts/partial/np-hdr.html - this requires internet access
* Several javascripts  are called in ./layouts/partial/np-ftr.html or ./layouts/partial/np-weather.html - this requires internet access
* Different headline styles and subheadline styles can be used for each listed article 
  - examples of these can be seen in the example posts
  - these are set in front matter variables for each post - see this article front matter with hl = 3 and subhl = 2
  - there are six headline styles and 6 subheadline styles - see ./static/css/np-gen.css for more info on these styles.
  - the image variable in the article front matter is used on single article pages and the style is less than ideal.


Lots of improvements can be made to this and I encourage you to make and changes you want. Only request is that you retain the credits
contained within. Please let me know of any suggestions or improvements.

geoff.mcnamara@gmail.com
<script src="https://gist.github.com/geoffmcnamara/bc0fe7d23e3a63c0da6544ee995b5d2e.js"></script>
