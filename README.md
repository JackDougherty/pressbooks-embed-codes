# pressbooks-embed-codes
notes on embed codes for OnTheLine book project in Pressbooks

## About Pressbooks hosted and self-hosted platforms

PressBooks is an open-source platform that packages WordPress-style content into various book formats, including an online web edition and downloadable pdf/epub/mobi (kindle) editions. The http://PressBooks.com freemium service hosts your books for you, and provides this useful guide: http://guide.pressbooks.com/.

If you have access to a WordPress server and the necessary skills, create a self-hosted Pressbooks site for greater flexibility than the freemium service above. See detailed installation instructions for https://wordpress.org/plugins/pressbooks/. To create open-access publicly downloadable books, also install the Pressbooks Textbook plugin/theme, created by Brad Payne, https://wordpress.org/plugins/pressbooks-textbook/.

# Embed codes

These PressBooks embed codes were designed for my http://OnTheLine.trincoll.edu book project, which blends text with interactive maps, documents, videos on a self-hosted PressBooks site, with PressBooks Textbook plugin/theme. These methods work well with PB web editions, and in most cases work on standard PB downloadable formats: epub/mobi/pdf via Prince. (But use at your own risk.)

## Internal links to the book

To create an internal link (from one PressBook page to another page in the same book) in the hosted PressBooks.com service, where each book is created as a **subdomain**, follow their guide: http://guide.pressbooks.com/chapter/adding-hyperlinks-internal-and-external/

But on my self-hosted PressBooks sites, each book is created as a **subdirectory**, where the title appears after the primary URL, like this: http://ontheline.trincoll.edu/book/

Create internal links using the Text editor tab (not the Visual editor) to insert an href tag in these formats:

```
<a href="/book/front-matter/introduction/"> jump to introduction</a>

<a href="/book/part/part-2/"> jump to part 2</a>

<a href="/book/chapter/title/"> jump to chapter</a>
```

## Part introductions display chapter contents, web-only

If your book is divided into parts, then readers of the web edition normally will encounter a blank page at the beginning of each part. While this blank page is fine for print/ebook editions, readers of web editions expect to see content, and this method efficiently delivers it to them.

1) install the List Category Posts plugin for WordPress https://wordpress.org/plugins/list-category-posts/

2) For each part of the book, insert a version of this code in the text editor, which displays only in the web version. The post_parent must be individually set to the post number of each specific part, shown in its url.

3) This code displays chapter links in order of their "published" date, so edit the dates accordingly (August 1, August 2, August 3...) in each part

```
<div class="web-only">
Chapters include:
[catlist post_type="chapter" post_parent=46 orderby=date order=asc numberposts=-1]
</div>
```

## Insert static image and link

Use this method to insert a conventional static image and link. Use only a caption (with no title about user actions), and use a non-shaded textbox border (to distinguish from shaded for more interactive versions)

#### Generic static image and caption in non-shaded textbox

```
<div id="INSERT NAME" class="textbox">
INSERT STATIC IMAGE LINK FROM PB
Insert HTML LINK with TEXT that will appear in all editions, so that readers of pdf/epub/mobi editions can click to go to the dynamic web version. INSERT SOURCE CREDIT, with optional [footnote]Note.[/footnote]
</div>
```

#### Sample static image and caption in non-shaded textbox

```
<div id="1937HOLCInhabitantsC10" class="textbox">
<a href="http://ontheline.trincoll.edu/book/wp-content/uploads/sites/3/2016/01/1937HOLCInhabitantsC10.png"><img src="http://ontheline.trincoll.edu/book/wp-content/uploads/sites/3/2016/01/1937HOLCInhabitantsC10.png" alt="" width="731" height="103" class="alignnone size-full wp-image-49" /></a>
This section of the <a href=https://github.com/JackDougherty/otl-redlining/blob/master/sources/holc-hartford-1937-appraisal.pdf>HOLC area descriptions form</a> required the appraiser to report the social composition of the neighborhood as a factor to measure mortgage risk. Source: Hartford area C-10, 1937, from the National Archives. [footnote]Home Owners’ Loan Corporation, “Residential Security Map and Area Descriptions, Hartford-West Hartford-East Hartford, Connecticut,” 1937, Record Group 195: Records of the Federal Home Loan Bank Board, Box 64, City Survey Files, National Archives II, College Park, Maryland, http://digitalrepository.trincoll.edu/cssp_archives/14/.[/footnote]
</div>
```

## Embed dynamic iframe and static image, with title and caption, in shaded textbox

Use this method to embed a dynamic iframe (for interactive maps, documents, videos, etc.) in the web edition, and a parallel static image (such as a screenshot of the interactive content, plus a web link to it) in the pdf/epub/mobi editions.

As a result, all editions of the book display some version of this visual content. The web edition is preferable because it embeds live interactive content directly into the web page. Also, the Web edition displays a title above the image, which cues readers to interact with the object. But the downloadable pdf/epub/mobi editions also display static images, with clickable links to the online version. All versions appear in a shaded textbox to draw the eye of the reader more than the non-shaded, non-interactive static images.

1) In a self-hosted PressBooks site, install iframe plugin: https://wordpress.org/plugins/iframe/
2) Upload a static image of the dynamic content (usually a screenshot of an interactive map or chart) to the PressBooks/WordPress media library.
3) Insert the static image into the PressBooks page, as normal.
4) In the Text editor tab (not the Visual editor), paste this **generic** code above and below the STATIC image code from the prior step, and modify the code and text to fit your needs.

#### Generic interactive and static embed

```
<div id="INSERT NAME" class="textbox shaded">
<div class="web-only">
<h2>Explore/Watch/Listen to the Map/Source/Video/Audio: Title for readers of web edition </h2>
[iframe src=“https://INSERT-YOUR-URL” width=“100%” height="500”]
</div>
<div class="not-web">
STATIC IMAGE CODE HERE
</div>
Insert HTML LINK with TEXT that will appear in all editions, so that readers of pdf/epub/mobi editions can click to go to the dynamic web version. INSERT SOURCE CREDIT, with optional [footnote]Note.[/footnote]
</div>
```

#### Example embedded interactive map iframe and static image

```
<div id="homevalue" class="textbox shaded">
<div class="web-only">
<h2>Explore the Map: Home Value Index in Hartford County, CT, 1910-2010</h2>
[iframe src="https://jackdougherty.github.io/otl-home-value/index.html" width="100%" height=550]
</div>
<div class="not-web">
<a href="https://ontheline.trincoll.edu/book/wp-content/uploads/sites/3/2016/05/1910-2010-home-value.jpg" rel="attachment wp-att-167"><img src="https://ontheline.trincoll.edu/book/wp-content/uploads/sites/3/2016/05/1910-2010-home-value.jpg" alt="1910-2010-home-value" width="910" height="490" class="alignnone size-full wp-image-167" /></a>
</div>
Follow the money in <a href="https://jackdougherty.github.io/otl-home-value/index-frame.html">this interactive map</a> as the most valuable single-family homes (in dark green) shifted from the capital city to selected suburbs over time. Click the tabs or use arrow keys to advance years. Hover over towns for details. Home values have been indexed (where county average = 1.0) to adjust for rising prices over time. Missing values appear in gray. View <a href="https://github.com/jackdougherty/otl-home-value">source data</a> for 1910-1980 from Connecticut Tax Commissioner, author's calculation of average dwelling value from equalized assessments; 1990 from Capital Region Council of Governments, median single-family home sales price; 2000-10 from State of Connecticut, Office of Policy and Management, average single-family home sales price (2000-2010). Learn more in Backstory: Calculating Wealth and Poverty in Past and Present, **to come** in this volume.[footnote]“Home Value Index in Hartford County, CT, 1910-2010,” 2016, https://jackdougherty.github.io/otl-home-value/index-frame.html.[/footnote]
</div>
```

#### Example of embedded Google Book iframe and static image

```
<div id="scribners" class="textbox shaded">
<div class="web-only">
<h2>Explore the Source: Hartford, "The Richest City in the United States," 1876</h2>
[iframe src="https://jackdougherty.github.io/otl-google-books-api/scribners-monthly-1876.html" width="100%" height=615]
</div>
<div class="not-web"><a href="https://ontheline.trincoll.edu/book/wp-content/uploads/sites/3/2016/01/1876ScribnersCover.png "><img src="https://ontheline.trincoll.edu/book/wp-content/uploads/sites/3/2016/01/1876ScribnersCover.png" alt="1876ScribnersCover" class="alignnone size-full wp-image-100" height="538" width="600" /></a></div>
<a href="https://books.google.com/books?id=2q_PAAAAMAAJ&amp;pg=PA1#v=onepage&amp;q&amp;f=false"> <em>Scribner's Monthly in 1876</em></a> declared Hartford as the richest city in the United States, relative to its population. Digitized by Google Books.[footnote]Charles H. Clark, “The Charter Oak City,” <em>Scribner’s Monthly</em> 13, no. 1 (November 1876): 1–21, https://books.google.com/books?id=2q_PAAAAMAAJ&amp;pg=PA1#v=onepage&amp;q&amp;f=false.[/footnote]
</div>
```

#### Example of Vimeo embed code and static image

```
<div id="2011-how-we-found-restrictive-covenants" class="textbox shaded">
<div class="web-only">
<h2>Watch the Video: How We Found Restrictive Covenants</h2>
[iframe src="https://player.vimeo.com/video/220562166" width="100%" height=400 frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen]
</div>
<div class="not-web"><a href="https://ontheline.trincoll.edu/book/wp-content/uploads/sites/3/2017/06/2011-how-we-found-restrictive-covenants.png"><img src="https://ontheline.trincoll.edu/book/wp-content/uploads/sites/3/2017/06/2011-how-we-found-restrictive-covenants.png" alt="2011-how-we-found-restrictive-covenants" width="856" height="478" class="alignnone size-full wp-image-373" /></a></div>
Watch the <a href="https://vimeo.com/220562166">video</a> to learn how we found restrictive covenants.[footnote]Katie Campbell and Jack Dougherty, "How We Found Restrictive Covenants," 2017, https://vimeo.com/220562166.[/footnote]
</div>
```


#### Generic version of scrollable PDF and static screenshot

- Install plugin https://wordpress.org/plugins/vanilla-pdf-embed/
- See sample HTML below. Insert pdf title to appear in graceful fallback for non-web versions
- Default width="100%" or adjust to pixels "500px"

```
<div id="INSERT NAME" class="textbox shaded">
<div class="web-only">
<h2>Explore the Source: Race and Class in the FHA Underwriting Manual, 1936 </h2>
[pdf title="INSERT TITLE OF PDF"]
INSERT LINK TO UPLOADED PDF IN MEDIA FOLDER[/pdf]
</div>
<div class="not-web">
STATIC IMAGE LINK
</div>
Insert HTML LINK with TEXT that will appear in all editions, so that readers of pdf/epub/mobi editions can click to go to the dynamic web version. INSERT SOURCE CREDIT, with optional [footnote]Note.[/footnote]
</div>
```

#### Example of scrollable PDF and static screenshot

```
<div id="1936FHA-Underwriting" class="textbox shaded">
<div class="web-only">
<h2>Explore the Source: Race and Class in the FHA Underwriting Manual, 1936 </h2>
[pdf title="Rating of Location, Underwriting Manual, Federal Housing Administration, 1936"]http://ontheline.trincoll.edu/book/wp-content/uploads/sites/3/2017/08/1936FHA-Underwriting-excerpts.pdf[/pdf]
</div>
<div class="not-web">
<a href="http://ontheline.trincoll.edu/book/wp-content/uploads/sites/3/2016/01/1936FHA-Underwriting-screenshot.png"><img src="http://ontheline.trincoll.edu/book/wp-content/uploads/sites/3/2016/01/1936FHA-Underwriting-screenshot.png" alt="" width="715" height="233" class="alignnone size-full wp-image-51" /></a>
</div>
The <a href='https://babel.hathitrust.org/cgi/pt?id=mdp.39015018409246;view=1up;seq=195'>1936 FHA Underwriting Manual</a> reduced a mortgage application location score where neighborhoods or schools might face changes in race or social class. Digitized by Google and HathiTrust.[footnote]Federal Housing Administration, <em>Underwriting Manual: Underwriting Analysis Under Title II, Section 203 of the National Housing Act.</em> (Washington, D.C.: US Government Printing Office, 1936), part II, sections 226-289, https://babel.hathitrust.org/cgi/pt?id=mdp.39015018409246;view=1up;seq=195.[/footnote]
</div>
```   


#### Embed brief line of non-executed code

To embed a brief line of code in PressBooks, without it being executed or processed by the browser, follow guidelines in this WordPress Codex: https://codex.wordpress.org/Writing_Code_in_Your_Posts

In the Text editor, wrap the HTML character entities for your line of code inside a div class = textbox and code tags, in this format:

```
<div class="textbox"><code> &lt; a href="/book/chapter/internal-link-test"&gt; text of link &lt;/a&gt;</code></div>
```

which will display in Web/Epub/Mobi/PDF via Prince editions as a line of code inside a box, similar to this:

```
<a href="/book/chapter/internal-link-test"> text of link </a>
```

#### Embed longer non-executed code via Gist

To embed several lines of non-executed code inside PressBooks, the best and simplest solution is to embed it as a GitHub Gist. This looks good in the Web edition, with automatic fall-back links in the Epub/Mobi editions, but does NOT display in the PDF edition -- see more below).

- Install the oEmbed WordPress plugin in a self-hosted PressBooks site: https://wordpress.org/plugins/oembed-gist/
- Create a free GitHub Gist account to store lines of sample code: https://gist.github.com
- To display several lines of Gist code in PressBooks, copy and paste the Gist permanlink directly into PressBooks, like this:

```
https://gist.github.com/JackDougherty/b4ccef475f78a6250c98
```

To display a specific file within a Gist, follow steps above, then right-click to copy the permalink of the file, and paste it directly into PressBooks, where it will appear with a "#file" prefix and underscore (in place of the period), like this:

```
https://gist.github.com/JackDougherty/8e14be951eac396801a8#file-sample-multi-file-subfile-html
```

Since these Gist oEmbeds do not display properly in PressBooks PDF editions, wrap these URLs inside a not-PDF div tag, and add an explanatory note inside a pdf-only div tag, like this:

```
<div class="not-pdf">
https://gist.github.com/JackDougherty/b4ccef475f78a6250c98
</div>
<div class = "pdf-only">
<a href="https://gist.github.com/JackDougherty/b4ccef475f78a6250c98">View code on GitHub Gist</a>
</div>
```

**TO DO**: Fix the cause of the validation error generated by the oEmbed Gist code above:
ERROR: /var/www/pressbookstest/wp-content/uploads/sites/22/exports/book-1441138153.epub/OEBPS/chapter-001-internal-link-test.html(14,82): element "script" missing required attribute "type"


## Using Zotero and Zotpress with Pressbooks

Zotero (http://zotero.org) is a free bibliographic manager tool from the Center for History and New Media, which also allows users to store data online. Zotpress (https://wordpress.org/plugins/zotpress/) is a free WordPress plugin by Katie Seaborn, which pulls selected bibliographic entries from your online Zotero library to display on self-hosted WordPress.org sites. Together, Zotero and Zotpress allow authors to display a continually updated bibliography, with hyperlinks, for scholarly web editions. For example, see the Bibliography for On The Line book at:
https://ontheline.trincoll.edu/book/part/bibliography/

Since Zotero + Zotpress records are dynamically generated when readers open a web page, there may be a momentary delay. Furthermore, Zotpress bibliographies will appear ONLY in the web edition, and will NOT appear in the exported books (pdf/mobi/kindle).

To elegantly display a Zotpress bibliography on a Pressbooks site with the Pressbooks Textbook plugin and Opentextbooks theme, make this modification:

1) Install the WP Add Custom CSS plugin (https://wordpress.org/plugins/wp-add-custom-css/).Since Pressbooks Textbook is a child-theme of the PB Luther theme, it does not allow users to create another child-of-a-child theme, so this is a workaround to insert custom CSS.

2) In the Dashboard, insert this code in the Add Custom CSS menu:

```
/* to make ZotPress bib display in Pressbooks Textbook without large empty space */
.zp-Zotpress p {
  display: none;
}
```

3) After you follow the Zotpress installation directions and connect to your Zotero library, insert a bibliography shortcode in Pressbooks text editor, like this:

```
[zotpress collection="M7AGPJ4D" sortby="author"]
```



#### OLD notes on former CSS modifications (before mid-2016)

```
/* change link color from black to blue; change back for PDF printing */
a {
    color: #12c;
}

/* transform upper-case to normal font */
h1, h2, h3, h4 {
    text-transform: none;
}

/* modify book home page */
.book-author {
    font-size: 1.2em;
}
.book-info-container h1 {
    font-weight: 500;
}

/* modify chapter pages */
h1.book-title {
    font-size: 1em;
}
h2.chapter_author {
    font-size: 1em;
    text-align: left;
    text-transform: none;
    font-style: italic
}

/* make invisible pressbooks-logo (multisite name) in top-left corner of each chapter page */
.pressbooks-logo a {
    color: #333
}

/* center div when needed, such as "Learn more..." footer */
.centered {
  text-align: center
}
```

#### OLD notes about analytics tracking in PB Textbook (before mid-2016)

```
// for Google Analytics (classic), change to:
// $tracking = "_gaq.push(['_trackEvent','exportFiles','Downloads','{$file_class}']);";
// for Google Analytics (universal), change to:
$tracking = "ga('send','event','exportFiles','Downloads','{$file_class}');";
// Piwik Analytics event tracking _paq.push('trackEvent', category, action, name)
// $tracking = "_paq.push(['trackEvent','exportFiles','Downloads','{$file_class}']);";
```
Additional steps required:
- Set up Google Analytics account and property.
- Sync Google Analytics with WordPress plugin such as Google Analyticator
- Pressbooks dashboard > Utilities > Google analyticator settings
	* Outbound link tracking = enabled (default)
	* Event tracking = enabled (default)
	* Download extensions to track = pdf,epub,mobi (no spaces)
- See results in Google Analytics > Behavior > Events > Event Label (to see number of downloads by epub, mobi, pdf)
