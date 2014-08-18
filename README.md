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

Given the following books.xml file (source: http://msdn.microsoft.com/en-us/library/ms762271(v=vs.85).aspx):

```
<?xml version="1.0"?>
<catalog>
   <book id="bk101">
      <author>Gambardella, Matthew</author>
      <title>XML Developer's Guide</title>
      <genre>Computer</genre>
      <price>44.95</price>
      <publish_date>2000-10-01</publish_date>
      <description>An in-depth look at creating applications 
      with XML.</description>
   </book>
   <book id="bk102">
      <author>Ralls, Kim</author>
      <title>Midnight Rain</title>
      <genre>Fantasy</genre>
      <price>5.95</price>
      <publish_date>2000-12-16</publish_date>
      <description>A former architect battles corporate zombies, 
      an evil sorceress, and her own childhood to become queen 
      of the world.</description>
   </book>
   <book id="bk103">
      <author>Corets, Eva</author>
      <title>Maeve Ascendant</title>
      <genre>Fantasy</genre>
      <price>5.95</price>
      <publish_date>2000-11-17</publish_date>
      <description>After the collapse of a nanotechnology 
      society in England, the young survivors lay the 
      foundation for a new society.</description>
   </book>
   <!-- and so on -->
</catalog>
```

Include the module in your node.js file, read the book.xml file and pass the text to the parser's load function:

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
// Outputs:
//
// XML Developer's Guide; Gambardella, Matthew; Computer
// Midnight Rain; Ralls, Kim; Fantasy
// Maeve Ascendant; Corets, Eva; Fantasy
// Oberon's Legacy; Corets, Eva; Fantasy
// The Sundered Grail; Corets, Eva; Fantasy
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

