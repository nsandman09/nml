#NML
NML is a simple preprocessor for HTML that makes it easier to write. In this document, you will learn how to write and read it. You can also read "parse.py" if you want to learn how it is parsed.

###Sample NML Page
NML is just an HTML preprocessor. This means that it is "compiled" into plain HTML.

Here is an example.

```
$head
	title 'Hello World'
%
$body
	$div (id: content)
		h1 'Hello World'	
	%
%
```

This looks simple, and it is. It will compile into this (without the whitespace):

```
<!DOCTYPE html>
<html>
	<head>
		<title>Hello World</title>
	</head>
	<body>
		<div id="content">
			<h1>Hello World</h1>
		</div>
	</body>
</html>
```

It's quite simple, and it boils down to this:

1. Tags that start with the "$" token will be closed at the corresponding "%" token.
2. Currently being implemented: The "&" token signifies a macro (Which you can also think of as a variable)
3. Tags that start with the "@" token are closed on the same line with their value (If there is one) in between.

The example above is the *preferred* syntax for NML, but it is not the only way. The parser does not discriminate between single `'` and double `"` quotes.

Finally, because the NML parser is token-based, whitespace does *not* matter. Again, indenting is preferred (as well as new tags on new lines), but not necessary. This is part of NML's flexibilities.

###Changes
NML does change a few things in HTML. The only ones so far are including stylesheets and javascript. Here is how you do this in NML. And of course, some of these tags must be closed.

| | HTML | NML |
| ------------- | :--------------------------------------------: | :-----:
| **Inline JS** | `<script type="text/javascript">...</script>` | `$js...%`
| **Include JS** | `<script type="text/javascript" src="..."></script>` | `js ...`
| **Inline CSS** | `<style type="text/css">...</style>` | `$css...%`
| **Include CSS** | `<link rel="stylesheet" type="text/css" href="..." />` | `css ...`

###Parser Usage
Using the parser is simple. The syntax is literally just:

```
./parser.py [infile]
```

So how do you write to a file? Simple. Just direct the program's stdout to your path:
```
./parser.py [infile] > [outfile]
```
