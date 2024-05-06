---
---

## Prerequisite
- Basic format of the bibtex file.
- Basic knowledge of HTML, and preferably some knowledge of JavaScript.

## Introduction
If you want to list your publications in HTML just like the one on my [personal website](/pub), but is tired of manually designing HTML elements for each entry, then you can use the `bibtex_js.js` to parse your bibtex file and automatically generate the HTML elements for you. This blog will guide you on how to use `bibtex_js.js` to incorporate your bibtex file in HTML.

## Installation
1. Download [`bibtex_js.js`](https://github.com/pcooksey/bibtex-js/blob/master/src/bibtex_js.js).
1. (Optional if you want better display format.) Download [`jquery.min.js`](https://ajax.aspnetcdn.com/ajax/jquery/jquery-3.7.1.min.js) and [`bootstrap.min.js`](https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.min.js).

## Basic Usage
First, include the `bibtex_js.js` in your HTML file. You may need to modify `src` attribute to the correct path.
```html
<script src="/src/bibtex_js.js" type="text/javascript" charset="utf-8"></script>
```

Second, specify your bibtex file. There are two ways to do this:
1. Use the `bibtex` tag. Change the `src` attribute to the correct path.
```html
<bibtex src="pub.bib"></bibtex>
```
2. Create a `textarea` element with `id="bibtex_input"`. Then, paste your bibtex entries inside the `textarea`.
```html
<textarea id="bibtex_input" style="display:none;">
@inproceedings{example_entry,
  title={{Title of the Paper}},
  author={Author1 and Author2},
  year={2024}
}
</textarea>
```

Finally, create a `div` element with an `id` attribute being `bibtex_display`.
```html
<div id="bibtex_display"></div>
```

## Customization
The steps above generates the list of publications in the default format, but it is not so beautiful. You can customize the display format by providing `bibtex_template` inside the `bibtex_display` element. It specifies the format of displaying the entries. For example, the following is what I did.
```html
<div id="bibtex_display">
    <div class="bibtex_template" style="display: none;">
        <ul>
            <li>
                <span class="if title">
                    <span class="title" style="font-weight: bold;"></span>
                </span>
                <div class="if author">
                    <span class="author" style="font-size: 14px;"></span>
                </div>
                <div>
                    <span class="if journal"><em><span class="journal"></span></em>,</span>
                    <span class="if publisher"><em><span class="publisher"></span></em>,</span>
                    <span class="if booktitle">In <em><span class="booktitle"></span></em>,</span>
                    <span class="if address"><span class="address"></span>,</span>
                    <span class="if month"><span class="month"></span>,</span>
                    <span class="if year"><span class="year"></span>.</span>
                    <span class="if note"><span class="note"></span></span>
                </div>
                <div>
                    <a class="bibtexVar" href="pdf/+BIBTEXKEY+.pdf" extra="BIBTEXKEY">
                        [pdf]
                    </a>
                    <span class="if code">
                        <a class="code" extra="code">
                            [code]
                        </a>
                    </span>
                    <a class="bibtexVar" role="button" data-bs-toggle="collapse" href="#bib+BIBTEXKEY+"
                        aria-expanded="false" aria-controls="bib+BIBTEXKEY+" extra="BIBTEXKEY" bibtexjs-css-escape>
                        [bib]
                    </a>
                </div>
                <div class="bibtexVar collapse" id="bib+BIBTEXKEY+" extra="BIBTEXKEY">
                    <div class="well">
                        <pre><span class="bibtexraw noread"></span></pre>
                    </div>
                </div>
            </li>
        </ul>
    </div>
</div>
```

You can just paste and copy the above template (see [Attentions to using the `bibtex_template`](#template) for how to use it), or if you need more customization, go on to read the following explanations.

For each entry in the bibtex file, `bibtex_js.js` will store several key-value pairs. Three default keys are `BIBTEXKEY`, `BIBTEXTYPE`, and `BIBTEXRAW`. The `BIBTEXKEY` is the key of the entry (being `example_entry` in the example above). In addition to these three, all fields in the bibtex entry will be stored, like `title`, `author`, etc. To desplay a specific key, just create a `span` element or `a` element with the class being the key name like:
```html
<span class="title"></span>
<a class="code"></a>
```
The former will be automatically filled with the content of the `title` field. The latter is declares a hyperlink, whose `href` attribute will be automatically set to the value of `code` field. (See [About the `code` Field](#code) for more information.)

Somethimes, you are not sure whether a field exists in the entry. You can use the `if` class to check the existence of the field. For example:
```html
<span class="if journal"><span class="journal"></span></span>
```
The outer `span` element will be removed if the `journal` field does not exist in the entry.

For more advanced usages, you may need to set some attributes of an element according to the value of some key. In this case, include `bibtexVar` in `class` attribute and set `extra` attribute to the name of the key. For example:
```html
<a class="bibtexVar" href="pdf/+BIBTEXKEY+.pdf" extra="BIBTEXKEY">
    [pdf]
</a>
```
`bibtext_js.js` will replace `+BIBTEXKEY+` with the value of `BIBTEXKEY`. Then if you store the pdf file in the `pdf` with the same name as the `BIBTEXKEY`, the hyperlink will be automatically set to the correct path. Furthermore, if you need to translate escape characters in the value, set `bibtexjs-css-escape` attribute in the element.

## Footnote

### Attentions to using the `bibtex_template`
<a id="template"></a>
Include the followings in the head of your HTML file to use this `bibtex_template`. Change the `src` attribute to the correct path.
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css">
<script type="text/javascript" src="/src/jquery.min.js"></script>
<script type="text/javascript" src="/src/bootstrap.min.js"></script>
```

### About the `code` Field
<a id="code"></a>
`code` is not a standand field in bibtex file, but is still read by `bibtex_js.js`. I use this field in my template to provide a link to the source code. In this way, inserting a hyperlink in HTML is simplified to just adding a `code` field in the bibtex entry. A problem is that the `code` field will be displayed in the raw bibtex text. To avoid this, you can use the following js function to remove the `code` field from the raw bibtex text when rendering.
```html
removeExtraFields = function(){
    $('.bibtexraw').each(function(index, bib){
        innerHTML = bib.innerHTML;
        innerHTML = innerHTML.replace(/\n\s*code\s*=.*\n/g, "\n")
        bib.innerHTML = innerHTML;
    })
}
```

## Reference
- [bibtex_js repository](https://github.com/pcooksey/bibtex-js)
- [How to display references on html using bibtex format](http://gewhere.github.io/bibtex-js)
