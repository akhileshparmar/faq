# What is HTML?

**HTML (Hypertext Markup Language)** is the standard markup language used to create and design web pages. It structures the content of a webpage by defining elements such as headings, paragraphs, links, images, and other multimedia. HTML is fundamental to web development and provides the basic framework for web content.

### Key Concepts of HTML

- **Tags**: HTML uses tags to define elements. Tags are enclosed in angle brackets (e.g., `<tagname>`). Tags usually come in pairs: an opening tag and a closing tag (e.g., `<p>` and `</p>`).
- **Attributes**: Tags can have attributes that provide additional information about an element. Attributes are included within the opening tag (e.g., `<a href="https://www.example.com">`).
- **Nesting**: HTML elements can be nested inside one another to create complex structures.

### Common HTML Tags

Here is a list of some commonly used HTML tags and their purposes:

| **Tag**          | **Description**                                                         | **Example**                                        |
| ---------------- | ----------------------------------------------------------------------- | -------------------------------------------------- |
| `<html>`         | The root element of an HTML document.                                   | `<html> ... </html>`                               |
| `<head>`         | Contains meta-information about the document.                           | `<head> ... </head>`                               |
| `<title>`        | Sets the title of the document (displayed in the browser's title bar).  | `<title>My Web Page</title>`                       |
| `<body>`         | Contains the content of the document.                                   | `<body> ... </body>`                               |
| `<h1>` to `<h6>` | Define headings, with `<h1>` being the largest and `<h6>` the smallest. | `<h1>Main Heading</h1>`                            |
| `<p>`            | Defines a paragraph.                                                    | `<p>This is a paragraph.</p>`                      |
| `<a>`            | Defines a hyperlink.                                                    | `<a href="https://www.example.com">Click here</a>` |
| `<img>`          | Embeds an image.                                                        | `<img src="image.jpg" alt="Description">`          |
| `<ul>`           | Defines an unordered (bulleted) list.                                   | `<ul><li>Item 1</li><li>Item 2</li></ul>`          |
| `<ol>`           | Defines an ordered (numbered) list.                                     | `<ol><li>First</li><li>Second</li></ol>`           |
| `<li>`           | Defines a list item.                                                    | `<li>List item</li>`                               |
| `<table>`        | Defines a table.                                                        | `<table> ... </table>`                             |
| `<tr>`           | Defines a table row.                                                    | `<tr> ... </tr>`                                   |
| `<td>`           | Defines a table cell.                                                   | `<td>Cell content</td>`                            |
| `<th>`           | Defines a table header cell.                                            | `<th>Header</th>`                                  |
| `<form>`         | Defines an HTML form for user input.                                    | `<form> ... </form>`                               |
| `<input>`        | Defines an input control.                                               | `<input type="text" name="username">`              |
| `<button>`       | Defines a clickable button.                                             | `<button>Click me</button>`                        |
| `<div>`          | Defines a division or section.                                          | `<div> ... </div>`                                 |
| `<span>`         | Defines a span of inline content.                                       | `<span>Inline text</span>`                         |

### HTML Document Structure

An HTML document typically follows this structure:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document Title</title>
  </head>
  <body>
    <h1>Heading</h1>
    <p>This is a paragraph.</p>
    <a href="https://www.example.com">Example Link</a>
    <img src="image.jpg" alt="Description" />
  </body>
</html>
```

- **`<!DOCTYPE html>`**: Declares the document type and version of HTML.
- **`<html>`**: The root element of the document.
- **`<head>`**: Contains meta-information and links to external resources (e.g., CSS).
- **`<body>`**: Contains the content of the document.

### Conclusion

HTML is the backbone of web pages, defining the structure and layout of content. Understanding HTML tags and their attributes is essential for web development, enabling you to create well-structured and accessible web pages.
