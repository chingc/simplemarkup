# pxml

Programmatic XML is a simple tool that helps you write XML programmatically.


## Features

- Easy to use
- Single module
- No dependencies


## Usage

Actually, there's one dependency and it's Python 3.x.  Install Python and simply import the module.

``` python
>>> from pxml import PXML
>>> pxml = PXML()
>>> with pxml.itag("greeting"):
...     pxml.insert("Hello, World!")
...     
>>> print(pxml)
<greeting>Hello, World!</greeting>
```


## Reference


#### Constructor

`PXML(width)` : Creates a pxml object.
- width: (Optional) The number of spaces used for indentation.  Default: 4


#### Methods

`attributes(attr)` : Return the attribute list as a string.
- attr: A list of 2-tuple strings.

``` python
>>> pxml.attributes([("id", "skinner"), ("class", "principal")])
' id="skinner" class="principal"'
```

`etag(name, attr)` : Add empty tag content.
- name: Name of the tag.
- attr: (Optional) A list of 2-tuple strings.

``` python
>>> pxml.etag("img", [("src", "/channel_6/homer_file_photo.png"), ("width", "640"), ("height", "480")])
>>> print(pxml)
<img src="/channel_6/homer_file_photo.png" width="640" height="480" />
```

`indent(repeat)` : Add indentation.
- repeat: (Optional) The number of times to indent.  Default: 1

``` python
>>> print(pxml.indent().insert("Bart!"))  # assuming the current indentation depth is 1
    Bart!
```

`insert(string)` : Add a string.

``` python
>>> print(pxml.insert("Lisa"))
Lisa
```

`newline(repeat)` : Add a newline.
- repeat: (Optional) The number of newlines to add.  Default: 1

``` python
>>> print(pxml.insert('10 print "D\'oh!"').newline().insert("20 GOTO 10"))
10 print "D'oh!"
20 GOTO 10
```


#### Context Managers

`tag(name, attr)` : Add tag content.
- name: Name of the tag.
- attr: (Optional) A list of 2-tuple strings.

``` python
>>> with pxml.tag("div", [("class", "big")]):
...     pxml.indent().insert("pxml!").newline()
...
>>> print(pxml)
<div class="big">
    Embiggened!
</div>
```

`itag(name, attr)` : Add inline tag content.
- name: Name of the tag.
- attr: (Optional) A list of 2-tuple strings.

``` python
>>> with pxml.itag("beer"):
...     pxml.insert("Duff!")
...
>>> print(pxml)
<beer>Duff!</beer>
```


#### Instance Variables

`spaces` : The number of spaces used for indentation.

`depth` : The current indentation depth.

`raw` : The array of elements that will be outputted.


## Extra Example

``` python
>>> pxml = PXML()
>>> family = ["homer", "marge", "bart", "lisa", "maggie"]
>>> with pxml.tag("ul"):
...     for member in family:
...         pxml.indent()
...         with pxml.itag("li"):
...             pxml.insert(member)
...         pxml.newline()
...
>>> print(pxml)
<ul>
    <li>homer</li>
    <li>marge</li>
    <li>bart</li>
    <li>lisa</li>
    <li>maggie</li>
</ul>
```


## License

Simplified BSD license.

See the included `LICENSE` for details.
