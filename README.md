XMLParser.js
============

A simple javascript XML parser I made to process some xml files, such as:

* Basic xml files (configuration files, etc.)
* GPX files with GPS data

It has not been thoroughly tested so don't expect to be able to parse too complex xml files. Also, there is a lot of room for improvement (performance and memory wise).

# Usage

## As a node.js module

Add the following line at the end of the XMLParse.js file to export the XML parser:

```
module.exports = new XMLParser();
```

Include the module in your node.js files:

```
var fs = require('fs');
var parser = require('XMLParser');

fs.readFile('/home/user/downloads/books.xml', 'utf8', function (err, data) {

    if (err) {
        return console.log(err);
    }

    var dom = parser.load(data);

    dom.getElementsByTagName("book").forEach(function(book) {

        var line = "",
            title = book.getElementsByTagName("title"),
            author = book.getElementsByTagName("author"),
            genre = book.getElementsByTagName("genre");

        line += title[0].innerText + "; " + author[0].innerText + "; " + genre[0].innerText;
        console.log(line);

    });

});
```

## As a standalone library

Include the file in your html page:

```
<script type="text/javascript" src="XMLParser.js"></script>
```

Then use it in your javascript section:

```
var parser = new XMLParser();

var xmlString = "<book><title>A Game Of Thrones</title><author>George R. R. Martin</author></book>";

var dom = parser.load(xmlString);

dom.getElementsByTagName("book").forEach(function(book) {

    console.log(book.getElementsByTagName("title")[0].innerText);
    // Outputs: Game Of Thrones

    console.log(book.getElementsByTagName("author")[0].innerText);
    // Outputs: George R. R. Martin

});
```

Note: consider using a minified version.

# Wishlist

* Tests
* Events
* Fallbacks
* Better performance

# License

None. Feel free to use it, wherever you want, as long as I am not liable for whatever harm your decision may cause :)

# Q&A

Q: Why don't you create a nodejs npm module?
A: There are plenty (and much better) XML parsers for nodejs.

Q: Why don't you use one that is already made and tested?
A: Needed to fill some spare time, wanted one of my own, ... whatever.

