---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---


<div id="placeholder"></div>

<div id="reading-list">
{% for entry in site.literature %}
<div data-category="{{ entry.categories | join: ", " }}" data-keywords="{{ entry.keywords | join: ", " }}" data-authors="{{ entry.authors | join: ", " }}">
{% include list-entry.html title=entry.title authors=entry.authors release=entry.release link=entry.link comment=entry.comment %}
</div>
{% endfor %}
</div>

<script>
$(function() {
    $.filtrify("reading-list", "placeholder", {
      close: true,
      callback: function(query, match, mismatch) {
          let keywordLists = document.querySelectorAll("ul.ft-tags")

          for(let j=0; j<keywordLists.length; j++) {
            // Get keywords list
            let keywords = keywordLists[j].querySelectorAll("li[data-count]")

            // iterate through keywords
            for(let i=0; i<keywords.length; i++) {
              let keyword = keywords[i]

              // Unhide keyword first
              keyword.setAttribute("style", "display: block")

              // Hide empty keyword from list
              if(keyword.getAttribute("data-count") == 0) {
                keyword.setAttribute("style", "display: none")
              }
            }
          }
      }
    });
});
</script>