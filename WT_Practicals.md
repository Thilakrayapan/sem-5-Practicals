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


# 2. Simple Calculator Web Application

## Question

Write a simple calculator web application that takes two numbers and an operator (+, -, *, /, %) from an HTML page. It should return the result page with the operation performed on the operands.

## Program

### File 1: `calculator.html`

```html
<html>
<body>
    <h2>Simple Calculator</h2>

    Number 1: <input id="a"><br><br>
    Number 2: <input id="b"><br><br>

    <button onclick="op='+'; show()">+</button>
    <button onclick="op='-'; show()">-</button>
    <button onclick="op='*'; show()">*</button>
    <button onclick="op='/'; show()">/</button>
    <button onclick="op='%'; show()">%</button>

    <h3 id="display"></h3>

    <button onclick="calculate()">Calculate</button>

    <script>
        let op = '+';

        function show() {
            document.getElementById("display").innerHTML =
                a.value + " " + op + " " + b.value;
        }

        function calculate() {
            let x = Number(a.value);
            let y = Number(b.value);
            let r;

            if (op == '+') r = x + y;
            else if (op == '-') r = x - y;
            else if (op == '*') r = x * y;
            else if (op == '/') r = x / y;
            else r = x % y;

            location.href = "result.html?answer=" + r;
        }
    </script>
</body>
</html>
```

### File 2: `result.html`

```html
<html>
<body>
    <h2>Result Page</h2>

    <script>
        let r = location.search.split("=")[1];
        document.write("Result: " + r);
    </script>

    <br><br>
    <a href="calculator.html">Back</a>
</body>
</html>
```

## Sample Output

Enter the numbers `10` and `3`.

Click the `+` button.

```text
10 + 3
```

Click **Calculate**.

Result page:

```text
Result Page

Result: 13

Back
```

## Execution Steps

1. Save both HTML files in the same folder.
2. Open `calculator.html` in a browser.
3. Enter two numbers.
4. Click an operator button to display the operation.
5. Click Calculate to open the result page.

## Result

Thus, a simple calculator was implemented using HTML and JavaScript with operator buttons and a separate result page.

# 3. College Information Using Various Style Sheets

## Question

Create a web page that displays college information using various style sheets.

## Program

### File 1: `college.html`

```html
<html>
<head>
    <title>College Information</title>

    <!-- Internal Style Sheet -->
    <style>
        h2 {
            color: blue;
            text-align: center;
        }
    </style>

    <!-- External Style Sheet -->
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <!-- Inline Style Sheet -->
    <h1 style="color: red; text-align: center;">
        ABC Engineering College
    </h1>

    <h2>College Information</h2>

    <p>Address: Chennai, Tamil Nadu</p>
    <p>Courses: CSE, ECE, EEE, IT</p>
    <p>Facilities: Library, Laboratory, Hostel</p>
    <p>Established Year: 2005</p>
    <p>Departments: CSE, ECE, EEE, IT, Mechanical</p>
</body>
</html>
```

### File 2: `style.css`

```css
body {
    background-color: lightyellow;
    font-family: Arial;
}

p {
    color: green;
    font-size: 18px;
}
```

## Output

- College name appears in red.
- College information heading appears in blue.
- College details appear in green.
- Background appears light yellow.

## Result

Thus, a college information web page was created successfully using inline, internal, and external style sheets.

# 4. Person Information Using XML and XSL

## Question

Write an XML for person information in XML and access the data using XSL.

## Program

### File 1: `person.xml`

```xml
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="person.xsl"?>

<persons>
    <person>
        <name>Arun</name>
        <age>20</age>
        <city>Chennai</city>
    </person>
    <person>
        <name>Priya</name>
        <age>21</age>
        <city>Trichy</city>
    </person>
</persons>
```

### File 2: `person.xsl`

```xml
<?xml version="1.0"?>

<xsl:stylesheet version="1.0"
xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

<xsl:template match="/">
<html>
<body>
    <h2>Person Information</h2>

    <table border="1">
        <tr>
            <th>Name</th>
            <th>Age</th>
            <th>City</th>
        </tr>

        <xsl:for-each select="persons/person">
            <tr>
                <td><xsl:value-of select="name"/></td>
                <td><xsl:value-of select="age"/></td>
                <td><xsl:value-of select="city"/></td>
            </tr>
        </xsl:for-each>
    </table>
</body>
</html>
</xsl:template>

</xsl:stylesheet>
```

## Sample Output

| Name | Age | City |
|---|---:|---|
| Arun | 20 | Chennai |
| Priya | 21 | Trichy |

## Execution Steps

1. Save both files in the same folder.
2. Open `person.xml` in a browser that supports XSLT.

## Result

Thus, person information was stored in XML and accessed and displayed in tabular form using XSL.

# 5. Static Registration Form

## Question

Write an HTML program to develop a static registration form.

## Program

### File: `registration.html`

```html
<html>
<head>
    <title>Registration Form</title>
</head>
<body>
    <h2>Registration Form</h2>

    <form>
        Name: <input type="text"><br><br>

        Email: <input type="email"><br><br>

        Password: <input type="password"><br><br>

        Gender:
        <input type="radio" name="gender"> Male
        <input type="radio" name="gender"> Female
        <br><br>

        Course:
        <select>
            <option>CSE</option>
            <option>ECE</option>
            <option>IT</option>
            <option>EEE</option>
        </select>
        <br><br>

        Address: <textarea></textarea><br><br>

        <input type="submit" value="Register">
        <input type="reset" value="Clear">
    </form>
</body>
</html>
```

## Sample Output

The registration form displays the following fields:

- Name
- Email
- Password
- Gender (Male/Female)
- Course selection
- Address
- Register and Clear buttons

## Result

Thus, a static registration form was created successfully using HTML form elements.


