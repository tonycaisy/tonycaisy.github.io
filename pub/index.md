<h1>Publications</h1>
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
                    {% for field in site.pub.bibtex_extra_fields %}
                        <span class="if {{ field }}">
                            <a class="{{ field }}" extra="{{ field }}">
                                [{{ field }}]
                            </a>
                        </span>
                    {% endfor %}
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

<script src="/src/bibtex_js.js" type="text/javascript" charset="utf-8"></script>
<bibtex src="pub.bib"></bibtex>
<script>
$('bibtexraw.').each(function(index, bib){
    innerHTML = bib.innerHTML;
    {% for field in site.pub.bibtex_extra_fields %}
        innerHTML = innerHTML.replace(/^\s*{{ field }}\s* =.*$/g, ' ');
    {% endfor %}
    bib.innerHTML = innerHTML;
})
</script>