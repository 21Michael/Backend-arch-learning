# API architectural styles (server - client):

![link](https://content.altexsoft.com/media/2020/05/word-image-52.png)

![link](https://www.altexsoft.com/media/2020/05/word-image-53.png)

## API Data Formats:
  - **XML (Extensible Markup Language);**

**Xml (eXtensible Markup Language)** is a mark up language. XML is designed to store and transport data. 
Whereas HTML tells a browser application how a document should look, XML describes what’s in the document. 
In other words, XML is concerned with how information is organized, not how it is displayed.

**XML is just information wrapped in tags:**
```xml
<note>
  <to>Tove</to>
  <from>Jani</from>
  <heading>Reminder</heading>
  <body>Don't forget me this weekend!</body>
</note>
```
**XML documents form a tree structure that starts at "the root" and branches to "the leaves" (XML DOM):**

![link](https://www.w3schools.com/xml/nodetree.gif)

All major browsers have a built-in XML parser to access and manipulate XML. The XML DOM (Document Object
Model) defines the properties and methods for accessing and editing XML. However, before an XML document 
can be accessed, it must be loaded into an XML DOM object. All modern browsers have a built-in XML parser
that can convert text into an XML DOM object.

**The XML DOM** defines a standard way for accessing and manipulating XML documents. 
It presents an XML document as a tree-structure.
  
  - **Plain Text;**
  - **HTML;**
  - **JSON (JavaScript Object Notation);**  
    
**JSON (Javascript Object Notation)** is a text-based, human-readable data interchange format used for 
representing simple data structures and objects in Web browser-based code. The JSON format is syntactically
identical to the code for creating JavaScript objects. Because of this similarity, a JavaScript program can
easily convert JSON data into native JavaScript objects. JSON data is written as name/value pairs, just
like JavaScript object properties.

**JavaScript has a built in function for converting JSON strings into JavaScript objects:**

```js
  JSON.parse()
```

**JavaScript also has a built in function for converting an object into a JSON string:**
```js
  JSON.stringify()
```
**Valid Data Types:**
  - a string
  - a number
  - an object (JSON object)
  - an array
  - a boolean
  - null

**XML vs JSON:**  
XML is much more difficult to parse than JSON. JSON is parsed into a ready-to-use JavaScript object.
Using XML

**1) Fetch an XML document**
  - Use the XML DOM to loop through the document
  - Extract values and store in variables 
    
**2) Using JSON:**
  - Fetch a JSON string
  - JSON.Parse the JSON string

![link](https://drive.google.com/uc?id=1jBYIersCgFsN9IYyS8bWpy1EgxD8PTxw)
