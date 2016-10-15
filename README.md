# Human Readable Kulturarvsdata for Wikidata

Userscript for Wikidata to make all Kulturarvsdata URIs(`P1260`) link to their human readable source.

## Usage

Paste the following into your `commons.js` file:

```
mw.loader.using(['jquery.ui.dialog'], function() {
  $(window).on('load', function() {
    // common functions
    String.prototype.insertAt=function(index, string) {
      return this.substr(0, index) + string + this.substr(index);
    }

    if (window.mw.config.values.wbEntity) {
      // replace external kulturarvsdata.se(P1260) RDF links with human readable ones
      if (JSON.parse(window.mw.config.values.wbEntity).claims.P1260) {
        var link = $('a[href*="kulturarvsdata.se"]');
        if (link.attr('href').indexOf('/html/') == -1) {
          var re = new RegExp('\/.[^/]+(|\/)$');

          insertIndex = re.exec(link.attr('href'))['index'];
          newUrl = link.attr('href').insertAt(insertIndex, '/html')
          link.attr('href', newUrl);
        }
      }
    }
  });
});
```
