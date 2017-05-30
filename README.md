# CS4All.io Round Two: Hugo Site Boogaloo

To localhost the site, [install Hugo](https://gohugo.io/overview/installing/), download this repository, navigate to it in Terminal, and run 
```
hugo server
```
Terminal will display instructions on how to view the site in your browser. To view full site with draft pages, which are currently under construction or otherwise not displayed on the site, run
```
hugo server --buildDrafts
```

## Updating the Site
The content for this site is written in Markdown, which makes it easy to update. GitHub provides an excellent [guide](https://guides.github.com/features/mastering-markdown/) to using Markdown, and though Hugo doesn't use the same GitHub flavored verison of Markdown as GitHub itself does, it does replicate certain features (and relevant syntax) of that variant such as [task lists](https://gohugo.io/content/markdown-extras/) and tables. A useful tutorial for formatting text in Markdown can also be found [here](http://www.markdowntutorial.com).

If you need to do something more advanced than what Markdown syntax offers, you can insert lines of raw HTML into the Markdown document (some basic uses of which are described below) or you can use a Hugo [shortcode](https://gohugo.io/extras/shortcodes/). 

*Instructions for pushing updates to the live site are included below.*

### Editing Existing Pages
Navigate to the target page's Markdown (`.md`) file in the `content/` folder, and open in a plain text editor. Now, you can edit it like a normal Markdown document and save it when you're done. If you're localhosting, the changes should be updated live, so you can see what you've done. For the most part, the [file path to the content](https://gohugo.io/content/organization/) within the `content` folder is identical to the structure of the page's URL, such that
```
http://www.cs4all.io/about/staff
```
is found at
```
content/about/staff.md
```
There are, however, the notable exceptions of list pages, which are found at the [_index.md](https://gohugo.io/content/using-index-md/) page of their corresponding directory. For example,
```
http://www.cs4all.io/about
```
is found at
```
content/about/_index.md
```
and the homepage `http://www.cs4all.io` is found at `content/_index.md`.

### Adding New Pages
You can generate a new Markdown document that includes the proper [header](https://gohugo.io/content/front-matter/) automatically by typing
```
hugo new section/page.md
```
or, for further nested pages,
```
hugo new section/path/to/page.md
```
while you are in the `site` directory. You can also just make a new Markdown document and write the header manually.

*If you want to work on a page but don't want it to show up on the site until you're done, make sure `draft = true` is included in the header. Use the intructions above for localhosting the site with and without drafts.*

If you want to add the page in a new section or folder and are unfamiliar with Hugo, you should first consult the [source organization](https://gohugo.io/overview/source-directory/) and [content organization](https://gohugo.io/content/organization/) pages in the Hugo documentation. For your section to show up in the site's main navbar, you need to include `menu = "main"` in the header of the `_index.md` file in the section's directory.

### Embedding Content
To embed an **image**, put the image in the `static` directory so that you can link to it from anywhere within the site as `/img-file.png`. Then, you can include it in any page by inserting the relevant HTML or the following [shortcode](https://gohugo.io/extras/shortcodes/):
```
{{< figure src="/media/spf13.jpg" >}}
```
as a line in the page's Markdown file. You can add a title or caption as well:
```
{{< figure src="/media/spf13.jpg" title="Steve Francia" >}}
```

Embedding **YouTube** content works similarly. You can click "Share" above the video description and then click "Embed" on the video's YouTube page and simply copy and paste the HTML it generates for you into your Markdown document as its own line like so
```
<iframe width="560" height="315" src="https://www.youtube.com/embed/auDh3S4jiDc" frameborder="0" allowfullscreen></iframe>
```
Alternatively, Hugo provides a shortcode for working with YouTube videos that requires only the video ID, which can be found in the URL. Below are the two usual formations for a YouTube URL:
```
https://www.youtube.com/watch?v=auDh3S4jiDc&feature=youtu.be
https://youtu.be/auDh3S4jiDc
```
The ID for the video, then, is the `auDh3S4jiDc` after the `v=` in the long URL and the final `/` in the shortened URL. You can embed the video on your page, then, by inserting
```
{{< youtube auDh3S4jiDc >}}
```
or you can insert it with autoplay turned on by instead inserting
```
{{< youtube id="auDh3S4jiDc" autoplay="true" >}}
```
There is an identical shortcode for **Vimeo** videos. That shortcode, as well as shortcodes for embedding content from other popular services like **Instagram** and **GitHub** can be found [here](https://gohugo.io/extras/shortcodes/).

To embed a **Google Form**, click the "Send" button at the top of the form editor page, and then next to "Send via," click on the embed icon `<>`, and copy the HTML that appears. Then, all you have to do is paste the HTML as its own line into the Markdown document for your chosen page like was done above for YouTube videos.

### Shortcodes
In addition to using Hugo's own shortcodes, you can [create your own shortcodes](https://gohugo.io/extras/shortcodes/#creating-your-own-shortcodes). This site, for example, has two custom shortcodes to format the bios on the [staff page](http://www.cs4all.io/about/staff). A full, paragraph length bio is produced by
```
{{< big-bio src="/headshot.png" name="John Smith" desc=" is an accomplished..." >}}
```
A smaller bio with only a name and position is produced by
```
{{< bio src="/headshot.png" name="John Smith" desc="Example Specialist" >}}
```

The HTML for these shortcodes can be found in `layouts/shortcodes/`. If you make a shortocde for the site, please update this README with details so other people can make use of it later.

## Hugo
This site is rendered in [Hugo](https://gohugo.io), a static site generator; the creators of Hugo provide an official [guide](https://gohugo.io/overview/quickstart/) to using the site rendering engine, though I've covered some details that are more relevant to this specific site or that I found particularly irritating to information about below.

Some relevant pages from the Hugo guide include:

* [Source organization](https://gohugo.io/overview/source-directory/) and [Content organization](https://gohugo.io/content/organization/)

	* [Here is](https://gohugo.io/overview/source-directory/#content-for-home-page-and-other-list-pages) a page with details more specific to content for the home page and for other list pages, which are orgnized slightly differently.

* [Summaries](https://gohugo.io/content/summaries/) -- Hugo can generate summaries for pages (which are not so much summaries as they are the first solid paragraph's worth of text) and the guide includes sample HTML code for including these summaries in a disambiguation/taxonomy/list page. The template our site uses utilizes this feature by default, but removing the relevant HTML code from the files in `themes/zen-mod/layouts/` will turn that off.

* [Ordering content](https://gohugo.io/content/ordering/) -- Weights are not currently assigned to content, so it's ordered either alphabetically or by date depending on the page. If you want to change that, this page is a good resource.

* [Site configuration](https://gohugo.io/overview/configuration/) and [page configuration](https://gohugo.io/content/front-matter/), which is relevant to adding pages to menus.

* Speaking of [menus](https://gohugo.io/extras/menus/), there's a page on those.

	* The HTML in our modified theme includes the code in the [rendering nested menus](https://gohugo.io/extras/menus/#rendering-nested-menus) section, though we don't currently use any nested menus.

* [Aliases](https://gohugo.io/extras/aliases/) allow you to redirect specified URLs to the page of your choice.

* Some other features we don't currently utilize but may want to in the future:

	* [Analytics](https://gohugo.io/extras/analytics/)
	* [Data-driven content](https://gohugo.io/extras/datadrivencontent/)
	* [Pagination](https://gohugo.io/extras/pagination/) -- Our blog and news pages may be short now, but this will be useful should that change.
	* [Table of Contents](https://gohugo.io/extras/toc/)
	* [Multilingual mode](https://gohugo.io/content/multilingual/)

## Theme
The site uses a modified version of the [Zen](https://themes.gohugo.io/hugo-theme-zen/) theme for Hugo, which is itself a port of the Drupal zen base theme. Our version differs primarily in its handling of menus and some of the Zen stock content has been replaced with CS4All stock content. If you're just updating the content of the site, you won't have to deal with the theme at all, but if you you want to edit the site theme, it may be useful to know that the contents of
```
/layouts/index.html
/layouts/partials/menu.html
/layouts/partials/menu_include.html
/layouts/partials/menu_recursive.html
/layouts/partials/sidebar.html
/layouts/partials/home-sidebar.html
/layouts/_default/baseof.html
/layouts/_default/single.html
/static/
```
depart from the original theme, but the other contents of the `/themes/zen-mod/` folder should be identical to those of the original [Zen repository](https://github.com/frjo/hugo-theme-zen).

## Pushing Changes to Live Site
Once you're satisfied with the changes you've made on your machine, you should, of course, push to this repository so everyone has the current code, but that won't update the live site, which is actually kept in the seperate repository `cs4allcps.github.io` (which I've added as a subrepository in the `/public` folder for ease of use).

To push changes to the live site, you want to use Hugo to render the new site from your machine and then push it to `cs4allcps.github.io`. To do so, starting in the `site` directory, run
```
hugo
cd public
git add .
git commit -m "Updating site (you can obviously make this message whatever you want)"
git push
```




