# 1. Demonstration of Hyperlinks

## Question

Write an HTML program for demonstrating Hyperlinks.

i. Navigation from one page to another.  
ii. Navigation within the page.

## Program

**File 1: `index.html`**

```html
<!DOCTYPE html>
<html>
<head>
    <title>Hyperlinks</title>
</head>
<body>

    <h1 id="top">Hyperlinks Demo</h1>

    <h2>1. Navigation from One Page to Another</h2>
    <a href="page2.html">Go to Page 2</a>

    <h2>2. Navigation Within the Page</h2>
    <a href="#bottom">Go to Bottom</a>

    <br><br><br><br><br><br>

    <h2 id="bottom">Bottom of the Page</h2>
    <p>You have reached the bottom!</p>

    <a href="#top">Go to Top</a>

</body>
</html>
```

**File 2: `page2.html`**

```html
<!DOCTYPE html>
<html>
<head>
    <title>Page 2</title>
</head>
<body>

    <h1>Welcome to Page 2</h1>
    <a href="index.html">Go Back to Home</a>

</body>
</html>
```

## Output

1. Clicking **Go to Page 2** opens the second HTML page.
2. Clicking **Go to Bottom** moves to the bottom of the same page.
3. Clicking **Go to Top** moves back to the top of the page.

## Result

Thus, hyperlinks for navigation between two pages and within the same page were successfully demonstrated.
