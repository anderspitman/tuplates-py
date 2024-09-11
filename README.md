# Introduction

Tale as old as time. I started developing a new static site. At first it was
just a single page. But
of course eventually I needed to add more ages and a header section with links to
them, and I needed that header section on every page. And of course HTML doesn't
havea way to
[include another HTML file](https://css-tricks.com/the-simplest-ways-to-handle-html-includes/),
because the popularity of JavaScript frameworks has slowed progress in
other web APIs.

tuplates is a simple way to template your static sites, without creating a
dependency on your templating tool. Rather than replacing your template tags,
it works by replacing lines between your template tags. This means that both
your template and code live together in your files. When you need to make a 
change, you update the fragment and re-run tuplates, and it replaces the old
code. This way you can check your actual code into source control, rather than
your templates.

The name comes from "update templates".


# Installation

Just copy tuplates.py into your repo. Or rewrite it from scratch in your
language of choice. It's very simple.

# Usage

Create a directory containing your fragments as files. You can
name them whatever you want.

```
project_directory/
  index.html
  index.js
  templates/
    header.html
    footer.html
    data.txt
```

Insert tuplate tags as comments in your code:

```html
<!-- index.html -->
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>tuplates</title>

  </head>

  <body>
    <!-- tuplate_start(templates/header.html) -->
    <!-- tuplate_end() -->

    <main>
      <h1>My Awesome Content</h1>
    </main>

    <!-- tuplate_start(templates/footer.html) -->
    <!-- tuplate_end() -->
  </body>

</html>
```

```javascript
// index.js
console.log("Hi there");

// tuplate_start(data.js)
// tuplate_end()

console.log(data);
```

Run the `tuplates.py` script in the directory above the `templates` directory.
It will walk the directory and replace the lines between the tags with the
tuplates.

After running once, the source files look like this:

```html
<!-- index.html -->
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>tuplates</title>
  </head>

  <body>
    <!-- tuplate_start(templates/header.html) -->
    <!-- tuplates/header.html -->
    <div class='header'>
      <h1>My Awesome Header</h1>
    </div>
    <!-- tuplate_end() -->

    <main>
      <h1>My Awesome Content</h1>
    </main>

    <!-- tuplate_start(templates/footer.html) -->
    <!-- tuplates/footer.html -->
    <div class='footer'>
      <h1>Awesome Footer</h1>
    </div>
    <!-- tuplate_end() -->
  </body>

</html>
```

```javascript
// index.js
console.log("Hi there");

// tuplate_start(template/data.js)
// tuplates/data.js
const data = {
  a: 1,
  b: 2,
  c: 3,
};
// tuplate_end()

console.log(data);
```

If you re-run it again, the result is the same, even though there's already
code between the tuplate tags. It simply replaces whatever is in there (if
there is anything). Just make sure your tuplate commands are on a line by
themselves.
