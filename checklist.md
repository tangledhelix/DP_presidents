# Guiguts PP Process Checklist

"Our Presidents and how we make them" by McClure, Alexander Kelly

## Process the Pages
Our first set of activities will combine all proofed and formatted pages, fixing any errors and inconsistencies.

### Initial Setup
* Choose a short, simple project name, e.g. `pascal` for “*The Provincial Letters of Blaise Pascal*”
* Run the [setup script](https://github.com/tangledhelix/dp_pp_utils) to fetch the project resources and create the [Github](https://github.com/tangledhelix?tab=repositories&q=DP_&type=&language=&sort=) project
```shell
cd ~/dp/util
. venv/bin/activate
./make_project.py
```
* [x] Read the [project comments](https://www.pgdp.net/c/project.php?id=projectID5f4c25334130b#project-comments)
* [x] Subscribe to the [forum topic](https://www.pgdp.net/phpBB3/viewtopic.php?t=71657) and read all posts
* [x] Open `presidents-utf8.txt` in Guiguts
* [x] `File → Project → Configure Page Labels`. Check for roman numerals and unnumbered pages. Go to end of book to check page numbers line up.

### Sequential Inspection of Text
* [x] `Preferences → Appearance → Enable Scanno Highlighting`
* [x] Open images in Pixea: `open -a Pixea pngs`

Check for:

* Proper spacing for chapters and paragraphs
  * Before chapter start: 4 blank lines
  * Between chapter head and subhead: 1 blank line
  * Between head (or subhead) and chapter body: 2 blank lines
  * Pages should **not** start with a blank line unless starting a new chapter, section, or paragraph.
* Proper markup of `<i>italic</i>` and `<b>bold</b>`.
  * Watch for punctuation wrongly contained in markup, such as `<i>(ibid.</i>` or `<b>Subtopic.</b>`.
* Proper markup of Greek and other transliterations
* Languages other than the main book language can be noted for later
  * In HTML they can be labeled with `<span lang="fr">..</span>`
  * If they're in italic print, that's handled later during italic handling
* Block material all marked in some fashion:
  * Poetry, misc. tabular in `/* */`
  * Block quotes in `/# #/`
  * Where blocks cross page boundary, remove the extra markers around page marker
  * Each overall block should have blank lines before & after
* Join words hyphenated across page boundary
* Figures properly in `[Illustration: caption]`
  * Check that caption text agrees with List of Illustrations (if any)
  * Consistent spelling, abbreviation, capitalization in captions
  * For captionless (`[Illustration: ]`), remove colon & whitespace
* Fix Footnotes, Illustrations still inside a paragraph
  * Move outside paragraph to next or prior page, as appropriate
  * Don't worry about duplicate footnote numbers/symbols for now
  * Sidenotes are handled later
* Make notes of things that will need attention in the HTML:
  * Author cross-references like "`(p. 150)`" and "`see page 222`" that should become links.
  * How the editor laid out special sections such as tables and sidebars.
* Check that `[Blank Page]` are actually blank pages! Can also remove them.
* Note any illustrations in a list in `README.md` for later handling

* [x] Move illustrations to `illustrations/` folder

### Basic Fixup
* [x] Use `Tools → Basic Fixup` with all options checked.
  * Use it judiciously. E.g., you may want to turn off "Fix up spaces around hyphens" and "Format ellipses correctly."
* [x] `Tools → Remove End-of-line Spaces`
* [x] Remove any remaining `[Blank Page]` lines

### Errata
* [x] If original book had errata, apply it and note in TN

### Fix Block Markups and Proofer Notes
* [x] Use the `Search` menu to step through all `/* */` blocks.
  * Regex: `^(/\*|\*/)`
  * Check for a blank line before and after markup
  * Make sure correct [Rewrap Markers](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_Manual/Tools_Menu#Rewrap_Markers) are used
  * Close-up where broken at page boundaries, if not already done
  * Apply specific [indent value](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_Manual/Tools_Menu#Table_Indent) if desired
  * Make sure poetry line numbers are at least two spaces to the right of the line.
* [x] Use the `Search` menu to step through all `/#..#/` blocks.
  * Regex: `^(/#|#/)`
  * Check for a blank line before and after markup
  * Make sure correct [Rewrap Markers](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_Manual/Tools_Menu#Rewrap_Markers) are used
  * Close-up where broken at page boundaries, if not already done
  * Check consistent indentation of block text
  * Apply specific [margin values](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_Manual/Tools_Menu#Block_Quote_Indent_and_Margins) if desired
* [x] `Search → Find Next Proofer Comment`. Resolve all proofer's notes.
* [x] `Search → Find Orphaned DP Markup`.
* [x] Search `(</i>)([!?;:])` & replace `$2$1` to find punct that should move inside quotes
* [x] Use `Tools → Check Orphaned Brackets` to check each type of bracket and markup.
  * Do not omit the lowly parenthesis, often mis-scanned as curly-brace.
* [x] Look for malformed thought-breaks (5 stars). Regex: `\*\s*\*\s*\*\s*\*\s*\*`

### Format Front Matter
* [x] Format the title page, preserving as much of the original material as possible. Protect in `/X...X/` (no rewrap, no indent) or `/F...F/` (the same, except that it will be centered in the html version).
* [x] Edit the TOC. Find each matching chapter head; make sure heads are 1:1 with TOC. Protect TOC with `/X...X/`. Note that your TOC will probably need to be indented to prevent rewrapping, particularly if you use multiple spaces to align page numbers.
* [x] If book has illustrations, edit or create *List of Illustrations* (**Note:** this is not a requirement). Make sure it is 1:1 with `[Illustration]` captions. Protect with `/X...X/`.

### Edit Transliterations
* [x] Use `Tools → Character Tools` to search for transliterations. Check the content of each transliteration. For Greek, there's a "Greek Transliteration Tool", but entering Unicode Greek is preferable.

### Remove Visible Page Breaks
* [x] Run `Tools → Fixup Page Separators` to remove visible page separators

### Apply Word-Frequency Checks
* [x] Open `Tools → Word Frequency`. Double click on a word to search for it.
* [x] Set the `Frq` switch; click `All Words`. List is now sorted by word frequency; scroll to the end and skim up the list of words that only appear 1 time looking for oddities and obvious misspellings.
* [x] Click `Character Cnts`.
  * Note characters that appear only once, check usage.
  * Check for equal counts of left & right parens and brackets.
* [x] Set the `Alph` switch; click `All Words`. Scroll to the word Footnote and write down count for later use. (If the count is large, click once on Footnote and click 1st Harm. The harmonic window shows you any of the common misspellings of "Footnote" that occur.)
* [x] Click `Emdashes`. This shows words with emdashes in them as well as similar words without emdashes (aka: suspects) marked with `****`. Check suspects against the text and page images. Preserve author's intent even when inconsistent. **Hint**: Enable the `Suspects` flag and click `Emdashes` again to see only suspects words.
* [x] Click `Hyphens`. Same as Emdashes above but for Hyphens.
* [x] Click `Alpha/num`. Scan list for `one/ell` and `oh/zero` errors.
* [x] Click `ALL CAPS`. Scan list looking for oddities.
* [x] Click `MiXeD CasE`. Scan list looking for letters such as o that sometimes OCR wrongly as uppercase. `Oh/zero` errors can show up here, too.
* [x] Click `Check Accents`. Scan list looking for mistakes, inconsistent usages.
* [x] Click `Check , Upper`. Scan list for comma-for-period errors.
* [x] Click `Check . Lower`. Scan list for period-for-comma errors.
* [x] Click `Ital/Bold/SC`. Scan list for incorrect or inconsistent use of italics, bold face, and small caps.
* [x] Click `Ligatures`. Scan list for [incorrect or inconsistent use](https://www.pgdp.net/wiki/Æ_and_œ_ligatures) of `ae` and `oe` ligatures.
```text
æ Æ    <Opt> '    /ai/ to rhyme with “eye”.
œ Œ    <Opt> q    /ɔɪ/ to rhyme with “oi” in “foil”
<shift> for capital letter
```
* [x] Look for missed ligature / diacritical transliterations. Regex: `\[[^*]`

### Apply Scanno Checks
* [x] Use `Tools → Stealth Scannos` with `Auto Advance`.
  * [x] Start scanno searching based on `en-commn.rc`. Work through the list.
  * [x] Apply scanno searching based on `misspelled.rc`. Work through the list.
  * [x] Apply scanno searching based on `regex.rc`. Work through the list.
* [x] `Tools → Run Jeebies`. Examine its report of possible `he/be` errors.

### Misc checks
* [x] Check for chapter/section spacing. Regex: `\n\n\n`
* [x] Check spaces around hyphens. Regex: `(\s+-|-\s+)`
* [x] Check spaces before punctuation. Regex: `\s+[.!?;:,]`
* [x] Check spaces around quotes. Regex: `(\s+['"][^\s]|[^\s]['"]\s+)`
* [x] Check spaces around brackets. Regex: `(\s+[({[\]})]|[({[\]})]\s+)`
* [x] Search regex `(Dr|M(me|lle|essrs|rs?)|St|Fr|Rev)\s` and add missing period if needed
* [x] Check `A.M.`, `P.M.` and similar for spacing to match book - regex: `[AP]\.\s*M\.`
  * Note these to do `&nbsp;` in HTML, to avoid line wrap mid-abbreviation
* [x] Does book use small-caps A.D. B.C.?
  * Search `[A-Z]\.\s*[A-Z]\.`, add `<sc>` and note for `&nbsp;` if needed
* [x] Check for multiple consecutive spaces which are not in a no-wrap block
* [x] Look at `<tb>` and look for improper uses
* [x] Check all ellipses. Regex: `\.\.\.`
* [x] Check for 3 dashes (not either 2 or 4). Regex: `[^-]---[^-]`
* [x] Look for spaces around em- or long-dash. Regex: `\s+--(--)?\s+`
* [x] Check adjacent letters and numbers. Regex: `([0-9][A-Za-z]|[A-Za-z][0-9])`
* [x] Superscripts (search `^` without regex). Can use `^` or `^{th}` form
  * Add TN to text version about this superscript notation

### Apply Bookloupe
* [x] If you have Bookloupe installed, use `Tools → Bookloupe`.
  * Forward slash
  * HTML tag
  * No CR
  * Non-ASCII character
  * Non-ISO-8859 character
* Otherwise, use pptext from the [Post-Processing Workbench](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/Post-Processing_Workbench).
* Work through the list, correcting as appropriate.

### Apply Spellcheck
* [x] Use `Tools → Spell Query`. Proceed through the document, correcting words or adding them to the project dictionary as appropriate.

### Fix Sidenotes
* [x] Read the [discussion](https://www.pgdp.net/wiki/PPTools/Guiguts/Fixup#Sidenotes). Step through sidenotes with: Search & Replace of `[S`, not regex, not whole word, ignore case. Click `Search` to find each Sidenote.
  * Compare to page image. Move note above paragraph if feasible.
  * Otherwise, position it above the sentence to which it applies, with blank lines to prevent rewrapping if you decide that is best.

### Fix Footnotes
* [x] Use `Tools → Footnote Fixup`. This will help you validate and move any footnotes.
  * `First Pass`
  * `Next / Prev FN` to navigate
  * Look for `*` and use `Join with Previous` to join them
  * THERE MUST BE NO ERRORS AT TOP OF WINDOW
* [x] Move footnotes between paragraphs
  * `Footnote Fixup`, `First Pass`
  * `All to Number`, `Reindex`
  * `First Pass`, `Move FNs to Para`
  * Save file, `Tools → Bookloupe` and check only `No punctuation at para end`
  * Run checks, find para and error, move footnotes as needed

### Fix Poetry Line Numbers
* [x] If the book has poetry that uses line numbers, read [this page](https://www.pgdp.net/wiki/PPTools/Guiguts/Fixup#Poetry_Line_Numbers) and align the line numbers consistently.

### Check balanced markup
Use the `Search` menu:

* [x] `Search → Find Orphaned Markup` (which searches for the regular expression `\<(\w+)>\n?[^<]+<(?!/\1>)`, that is any markup starting in `<..>` that doesn't end in an identical closing markup.
  * Note: this regular expression sees `<tb>` as unbalanced, and shows the text from the `<tb>` to the next markup as an error. (If you can devise a better regex please do!)
  * Possible alternate that explicitly lists all current markup `\<(i|b|sc|g||f|u)>\n?[^<]+<(?!/\1>)`
  * Because it includes a newline, the search may take several seconds to return the first result.
* [x] Correct the error and click search until no more are found.

### Consider page numbers and curly quotes
* [x] Curly quotes are [recommended](https://www.pgdp.net/phpBB3/viewtopic.php?f=3&t=73290) in both the text and HTML versions. Now is the time to put them in, before the split. Select `Txt → Convert to Curly Quotes`.
  * There are fixup menu items too
* [x] Search for remaining upright single quotation marks and replace them with either a ‘ or a ’.
* [x] Check for lingering straight quotes: `['"]`
* [x] `Txt → Curly Quote Corrections → Select Next @ Line` and handle each occurrence
* [x] Validate quotes pairings by searching for `[“”‘’]`

### Unicode dashes

* [x] Long dash: S/R `([^-])----([^-]|$)` → `$1——$2`
  * There exists a “long dash” Unicode character (TWO-EM DASH, U+2E3A). However, display support for it is not broad, so it’s better to use two consecutive EM DASH, which is widely supported.
* [x] Em dash: S/R `([^-])--([^-]|$)` → `$1—$2`
  * There exists another dash (HORIZONTAL BAR, U+2015) which one PM/PP prefers to EM DASH (using two bars for one EM DASH), based on appearance in text version. I opted not to use this in favor of using the EM DASH character in both text and HTML.
* [x] [En dash](https://www.pgdp.net/wiki/En-dash): S/R `([^-])-([^-]|$)` → `$1–$2`
  * Range of numbers `12–15`
  * Mathematical minus sign `15 – 12 = 3`
  * Negative numbers `–14º`
* Any dashes not covered above are simple hyphens.

### Last pre-split check
* [x] Look at the revisit list for anything to handle before text/html split
* [x] Check for unexpected `*` to make sure no stray proofer notes or split-word/fn markers were missed

### Save Edited Markup
* [x] Save any unsaved changes
* [x] Use `File → Save a Copy As` to make `presidents.html`
  * This will be the starting file for the HTML version. You can also use it  as fallback in case you mess up and need to start the following steps over.

## Prepare the Plain Text Version
We now proceed to create a Plain Text Version of the book.

* [x] Re-open `presidents-utf8.txt` (if not still open).

### Convert `<tb>`, Italic, Bold, and Smallcap
* [x] Use `Txt → Txt Conversion Palette`:
  * [x] Convert [inline formatting](https://www.pgdp.net/wiki/DP_Official_Documentation:Formatting/Formatting_Guidelines#Formatting_at_the_Character_Level:).
  * [x] Convert [thought breaks](https://www.pgdp.net/wiki/DP_Official_Documentation:Formatting/Formatting_Guidelines#Thought_Breaks_.28Extra_Spacing.2FDecoration_Between_Paragraphs.29).
  * [x] Convert [smallcaps](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/Guide_to_smallcaps).

### Fix ASCII Tables
* [x] Use `Search → Find Next /**/ Block` to step through all tabular material.
  * Compare to page image; reformat to best convey author intent.
  * For complex tables, use `Txt → ASCII Table Effects` to reformat.

### Rewrap and Clear Rewrap Markers
* [x] Save the file if any unsaved changes.
* [x] Use `Tools → Rewrap All`. Wait while rewrap completes.
* [x] Page through entire text, looking for improper indentation. If found, re-open, clicking NO when asked if you want to save the edits. Find and fix broken rewrap markups. Repeat this step.
* [x] Under `Tools → Footnote Fixup`, use the `Tidy Up Footnotes` button.
* [x] Use `Tools → Clean Up Rewrap Markers`.
* [x] Use `Tools → Remove End-of-line Spaces`.
* [x] Rerun Bookloupe or pptext. Resolve any new issues.
* [x] Save the document.

### Final checks
* [x] check if illustrations should be moved around within document.
* [x] Search for `<` and `>` to locate any tag markup not yet removed.

### Check revisit list
* [x] Check "things to revisit" list for anything lingering in the text version

### Add TN
* [x] Add transcriber's notes, example follows. Use 4+2 blank lines as in new chapter
* [x] Rewrap this section of text when finished.

```text
Transcriber’s Note


Some inconsistencies in spelling, hyphenation, and punctuation have been
retained.

This file uses _underscores_ to indicate italic text.
```

If bold is used, add also `and =equals= to indicate bold text`

If there were small-caps, `Small capitals changed to all capitals`

An example entry might look like this. Use the book's page numbers, not PNG number

```text
p. 123: changed “foo” to “fool” (the fool and his money)
```

### Final review
* [x] Skim over text file to find any obvious issues

### Validation
* [x] Run [PWBB](https://www.pgdp.net/ppwb/index.php) pptext check
* [x] Run text checks at [pptools](https://pptools.tangledhelix.com)

## Prepare the HTML Version
Finally, we create an HTML version of the book.

### Generate the HTML
* [x] Open `presidents.html` that was saved previously.
* [x] It is preferable for the source line-breaks to match the book; however HTML poetry markup won't work unless `/P..P/` sections have been rewrapped. If the book has much poetry, rewrap it all; else select and rewrap poetry sections individually.
  * Don't remove the rewrap markers. These are needed for generation of proper HTML.
* [x] Open `HTML → HTML Generator`.
  * Set optional switches as desired.
  * Use the `Autogenerate HTML` button.
* [x] Save the file and open it in a browser by using the `View in Browser` button.
* [x] Scroll through looking for systematic errors. (Title pages, tables, etc. will look terrible; no matter). If automatic conversion messed up, start this step over with a reset file.
* [x] Page through the book looking for text that was not handled well by automatic HTML generation, in particular:
  * [Title pages](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/DP_HTML_Best_Practices/Case_Studies/Title_Pages).
  * [Tables and Tables of Contents](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/DP_HTML_Best_Practices/Case_Studies/Tables). The `Auto Table` button can help format tables.
  * [Indexes](https://www.pgdp.net/wiki/Indexes), which are best formatted using unsigned lists, rather than the markup Guiguts generates for `/$..$/`.
* [x] Use `HTML → HTML Markup` to make improvements. Use regex replacements to make systematic changes.
  * Where you see a problem, make a correction in Guiguts, save the file, and click the "reload" button in the web browser.
* [x] Hyperlink page references in text, TOC, and index (discussed [here](https://www.pgdp.net/wiki/PPTools/Guiguts/HTML#Hyperlinking_Page_Numbers) and [here](https://www.pgdp.net/wiki/Indexes)).
* [x] Remove the [Generated TOC](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_Manual/HTML_Menu#Generated_TOC) if it is not needed.
* [x] If `A.M.` `P.M.` or similar abbreviations were used and have spaces, insert `&nbsp;` to avoid undesirable mid-abbreviation line wraps.
* [x] If superscripts were used, convert to `<sup>`
* [x] Semantic fixup for italics
  * Search `<i>((.|\n)+?)</i>`
  * Replace (emphasis) `<em>$1</em>`
  * Replace (citation) `<cite>$1</cite>`
  * Replace ([languages](http://www.w3schools.com/tags/ref_language_codes.asp)) `<i lang="fr">$1</i>`
  * Leave other cases as `<i>..</i>`
* [x] Add `abbr` tags if appropriate. ([Reference](https://www.pgdp.net/wiki/Accessibility_Recipes/Abbreviations))
* [x] If there is a cover image for e-readers supplied with the project, or you are creating one yourself, you can find information on what is needed in your HTML in the [Proofreaders' Guide to EPUB](https://www.pgdp.net/wiki/The_Proofreader%27s_Guide_to_EPUB#Cover_Page) or the [PP guide to cover pages](https://www.pgdp.net/wiki/PP_guide_to_cover_pages).

### Process Hi-resolution Images
If the project manager provided high-resolution scans of the images in the text, use an image processing program such as GIMP or Adobe Photoshop Elements to optimize them—see [Guide to Image Processing](https://www.pgdp.net/wiki/Guide_to_Image_Processing). You can do this before, during, or after HTML conversion.

Unless purely decorative, add an `alt` tag for each image unless it has a caption. For decoration, use `alt="" data-role="presentation"` (empty string to satisfy the validator).

Image [sizes](https://www.pgdp.net/phpBB3/viewtopic.php?f=3&t=70286):
* Inline: up to 256K, 5000x5000 pixels
* Linked: up to 1MB, 5000x5000 pixels. Should only need linked images for large or complex things, e.g. maps.
* Covers: see [cover documentation](https://www.pgdp.net/wiki/PP_guide_to_cover_pages). Recommend 1600x2560, aspect ratio ~1:1.6. Not over 5000x5000px. Minimum 650x1000. **No specific file size limit**, but use judgement and don't make it larger than necessary.

For each image:
* [x] Load image from the `illustrations/` folder (see the Initial Setup step).
* [x] Straighten it (almost all scanned images are off-perpendicular; some are trapezoidal owing to the page not being flat on the scan window). Perspective tool.
* [x] Crop it to remove all redundant white space and borders (provide margins and borders with CSS styling of the `<img>` markup).
* [x] Correct the contrast
* [x] Use the [dodge/burn layer technique](https://www.pgdp.net/wiki/Guide_to_Image_Processing#Linear_Light_in_The_GIMP) to clean up, at least for line drawings
* [x] Sharpen.
* [x] Correct any major scratches, freckles, dirt, etc.
* [x] Save in the subfolder images using appropriate type:
  * Line drawings in `.png` at 8 bits per pixel (not the default 24-bit RGB format).
  * Photographs as `.jpg` with an appropriate compression level such as (Photoshop) level 6.
* [x] Under `HTML → HTML Generator`, use the `Auto Illus Search` button. This will help add the images to the book.
* [x] Page through entire HTML book making sure that each image is being loaded correctly. Test each thumbnail if used.
* [x] If any images were modified substantially (including removing a library sticker or stamp), add a TN. Place the new image in the public domain in the TN. This is a PG requirement.
* [x] If fabricating your own cover, add the TN as noted in [Easy_Epub/Cover](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/Easy_Epub/Cover).

### Check "things to revisit"
* [x] Check revisit list for anything left for the HTML version

### Add TN
* [x] Add transcriber's notes, example follows.

```html
<div class="transnote">
<h2>Transcriber’s Note</h2>

<p>
Some inconsistencies in spelling, hyphenation, and punctuation have been
retained.
</p>
</div>
```

An example entry might look like this. Use the book's page numbers, not PNG number.

```html
<ul>
<li>
<a href="#Page_123">p. 123</a>: changed “foo” to “fool”
(<a href="#TN1">the fool and his money</a>)
</li>
</ul>
```

And accompany this with a target in the correction site, e.g. the below.
Use a `<span>` if another element isn't already present; otherwise use the
existing element and add the `id` attribute.

```html
They say that <span id="TN1">the fool and his money</span> are soon separated
```

* [x] Make sure the TN has no straight-quotes `'"` and instead uses curly quotes `“”‘’`

### Validate HTML and CSS
Perform these validation steps before submitting your book. Validation is also helpful while customizing the HTML and CSS above.

* [x] File should start with HTML opening
```html
<!DOCTYPE html>
<html lang="en">
```
* [x] Confirm that the `<title>` tag matches the format specified by the [Post-Processing FAQ](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/Post-Processing_FAQ#HTML_title).
  * `<title>Alice's Adventures in Wonderland | Project Gutenberg</title>`
  * Sentence case isn't required here (but it is on the upload form)
* [x] Use `HTML → HTML Tidy`. Fix any reported problems.
* [x] Use [W3C Markup Validation Service](http://validator.w3.org/#validate-by-upload). Fix any reported problems.
* [x] Remove unused CSS. `HTML → PPhtml` can help with this. Alternatively, check manually or use a tool such as the Firefox addons Firebug (with CSS Usage extension) or Dust-Me Selectors.
* [x] Use [W3C CSS Validation Service](http://jigsaw.w3.org/css-validator/#validate_by_upload). Fix any reported problems.
  * Validate as CSS 2.1
  * CSS3 is acceptable if current status is `REC` on [this page](https://www.w3.org/Style/CSS/current-work)
    * e.g. CSS3 drop-caps
    * or use of `display: flex;` for centering a div (poetry)
    * if uploading CSS3, leave a note for WWer about it.
* [x] Use `HTML → HTML Link Checker`. Fix any reported problems.
* [x] Use `HTML → PPVimage` to check for image-related errors. Fix any reported problems.
* [x] Run [PWBB](https://www.pgdp.net/ppwb/index.php) checks
  * [x] [pphtml](https://www.pgdp.net/ppwb/pphtml.php)
  * [x] [ppcomp](https://www.pgdp.net/ppwb/ppcomp.php) to compare text/html files
* TODO: add pptools here when it supports HTML5
  * CSS transform for pptools:
```css
/* projects with bold <b> markup */
b:before { content: "="; }
b:after { content: "="; }
```

### Review HTML
* [x] Review in multiple browsers
* [x] Pay particular attention to complex items like tables, poetry

## Ebook generation

### Notes on rendering
* Don't use `!important` in CSS, ADE has a parsing issue with it
* ADE doesn't render small-caps
* Kindle doesn't seem to honor `width` on divs? Set all of `min-width`, `width`, `max-width` to fix. Kindle may set `min-width` 100% and need an override?
  * Other advice: "Kindle ignores max-width. If you want your narrow text to be centered (column-centered with smooth margins), add `margin: auto;` to the "narrow" definition. Otherwise, it'll be left-positioned along the body's main left margin.
* Kindle on Mac renderes PNG transparent backgrounds as black
* Sometimes page breaks show in weird places due to ebookmaker's chunking
* Kindle doesn't always honor `page-break-*` CSS
* If no cover was included, the first illustration is used instead.
* E-readers are bad at wide tables and non-trivial tables
* Nook is particularly bad at table rendering
* Kindle sometimes can show SVG, sometimes not??
* Apple Books isn't reliably able to show PNGs in table cells??
* Renaming epub3 to end in `.kepub.epub` improves rendering a lot
* Also a utility `kepubify` (link below) that converts; it's unclear what this conversion does that's any better than just renaming the file. Changing the filename is enough to invoke a different / better rendering engine on Kobo devices.

### Build and upload Ebooks
* [x] `make zip`
* [x] Upload to [ebookmaker](https://ebookmaker.pglaf.org/) to generate Ebook files
* [x] `make ebooksget cache={cache_number}` to download ebook files
* [x] Convert epub3 with [kepubify](https://pgaskin.net/kepubify/try/)
* [x] Upload epub3 with [Send to Kindle](https://www.amazon.com/gp/sendtokindle)
* [x] Add epub3 to Apple Books
* [x] Add epub, epub3, renamed-kepub, converted-kepub to Dropbox for Kobo

### Ebook review
<details>
<summary>
Don't necessarily have to do *all* of these, but these are what I have.
</summary>

* [x] Review Ebook ToC in at least one e-reader, for structure & content
  * Can try using `title=` attr if a header title has footnote marker etc.
* [x] Mac
  * [x] Adobe Digital Editions (epub3)
  * [x] Apple Books
  * [x] Kindle Previewer (epub3)
  * [x] Calibre (epub3)
* [x] Phone
  * [x] Apple Books (iPhone)
  * [x] Kindle (iPhone)
* [x] Tablet
  * [x] Kindle (Android)
  * [x] Google Play Books - Android (Dropbox)
  * [x] Moon+ Reader - Android (Dropbox)
  * [x] Apple Books - iPad mini
* [x] E-ink
  * [x] Kobo Libra Colour (renamed-kepub)
  * [x] Kobo Libra Colour (converted-kepub)
  * [x] Kindle Paperwhite

</details>

## Smooth Reading

### Submit to SR pool

Submit for a decent length of time, up to the maximum. Check what's in `ebooks/` folder, it'll all be uploaded.

* [x] Make sure git is clean, committed, pushed
* [x] `make sr`
* [x] Go to [project page](https://www.pgdp.net/c/project.php?id=projectID5f4c25334130b), select SR time period, upload `presidents-sr.zip`
* [x] Subscribe to “user uploads a SR report” item
* [x] Update my Trello project board with due date, set card to SR status
* [x] If time permits, smooth read it myself as well

### Process SR feedback
* [ ] After SR is finished, processed SR feedback into project.
* [ ] Add **anonymized** files to git, e.g. `presidents-smoothread01.txt`
* [ ] Thank your smooth readers with a PM!
* [ ] If there were changes from the SR round, re-do final checks from above (validators etc)

## Upload the Finished Project

[Guide to DU and Posting to PG](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/Guide_to_Direct_Uploading_%28DU%29_and_Posting_to_PG)

* [ ] Run through [ebookmaker](https://ebookmaker.pglaf.org/), check output.txt
  * No errors!
  * Warnings are OK
  * Copy link to the output.txt file (will persist about 3 days)
* [ ] `make zip`
* [ ] Go to the [PGLAF upload site](https://upload.pglaf.org/)
* [ ] Enter copyright clearance (get from DP [project page](https://www.pgdp.net/c/project.php?id=projectID5f4c25334130b))
* [ ] Choose zip file to upload
* [ ] Add `dp-post@pgdp.net` as a Cc on Posted announcement
* [ ] Carefully check submission details against title page from book
  * If anything won't fit in the form add it to the Notes field
  * If you make any changes mention them in Notes field
  * Use sentence case for title. Proper nouns such as names should be capitalized.
    * The story of the little red hen
    * What the wind did
    * The writing of fiction
    * Travels in Africa, Egypt, and Syria from the year 1792 to 1798
    * The Squire's young folk : A Christmas story
* [ ] Credits line
  * Paste in from DP [project page](https://www.pgdp.net/c/project.php?id=projectID5f4c25334130b)
  * Add myself to credits line
  * DO NOT alter any other names, DO NOT turn a DP username into real name!
  * Assume `Produced by` will be added as a prefix to whatever you enter
  * Should be only ASCII, no Unicode
  * Example: `Joe Schmo, Jane Doe, and the Online Distributed Proofreading Team at https://www.pgdp.net (This file was produced from images generously made available by The Internet Archive/American Libraries.)`
* [ ] Anything else important, add to Notes field
  * Any CSS3 should be noted, e.g. drop-cap or other stuff.
  * If project contains Hebrew, let WWer know that
* [ ] Preview the submission
  * **After preview you have to select the upload file again!**
  * [ ] If the preview looks good and indicates no problem, then submit
* If you notice an error post-upload, contact pgww at lists.pglaf.org ASAP
* If you notice an error in your own recently posted project, contact pgww at lists.pglaf.org ASAP
* For projects over a month old, use the [errata process](https://www.gutenberg.org/help/errata.html)
* If not posted within a week, contact WWers pgww at lists.pglaf.org

## Project wrap-up
* [ ] When posted, then update PG URL in README.md, and [personal website list](https://tangledhelix.com/about)

### Device / cloud cleanup
* [ ] Remove from Dropbox
* [ ] Remove from Kindle and Kindle library
* [ ] Remove from Apple Books
* [ ] Remove from Kobo device

## Related Pages
* [Beginner PP advice](https://www.pgdp.net/wiki/Beginner_PP_advice)
* [Post-Processing FAQ](https://www.pgdp.net/c/faq/post_proof.php)
* [Post-Processing Advice](https://www.pgdp.net/wiki/Post-Processing_Advice)
* [Guiguts Tutorial](https://www.pgdp.net/wiki/Guiguts_Tutorial)
* [Guiguts Manual](https://www.pgdp.net/wiki/PPTools/Guiguts)
* [Getting your PP Project Ready for PPV](https://www.pgdp.net/wiki/Getting_your_PP_Project_Ready_for_PPV)
* [Poetry Case Study](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/DP_HTML_Best_Practices/Case_Studies/Poetry)
