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
<!DOCTYPE html>
<html>
<head>
  <title>Simple Calculator</title>
</head>
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
<!DOCTYPE html>
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
<!DOCTYPE html>
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
<!DOCTYPE html>
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

# 6. Image Map Using HTML

## Question

Create a web page with the following using HTML:

i. To embed an image map in a web page.  
ii. To fix the hotspots.  
iii. Show all the related information when the hotspots are clicked.

## Program

### File: `imagemap.html`

```html
<!DOCTYPE html>
<html>
<head>
    <title>Image Map</title>
</head>
<body>
    <h2>Computer Parts Image Map</h2>

    <img src="computer.jpg" usemap="#parts" width="400">

    <map name="parts">
        <area shape="rect" coords="20,20,180,150"
              href="#" onclick="show('Monitor: Displays output'); return false;">

        <area shape="rect" coords="200,20,350,150"
              href="#" onclick="show('CPU: Processes data'); return false;">

        <area shape="rect" coords="50,170,250,250"
              href="#" onclick="show('Keyboard: Enters text'); return false;">
    </map>

    <h3 id="info">Click a computer part</h3>

    <script>
        function show(text) {
            document.getElementById("info").innerHTML = text;
        }
    </script>
</body>
</html>
```

## Sample Output

- Clicking the monitor hotspot displays: `Monitor: Displays output`
- Clicking the CPU hotspot displays: `CPU: Processes data`
- Clicking the keyboard hotspot displays: `Keyboard: Enters text`

## Execution Steps

1. Save the code as `imagemap.html`.
2. Keep an image named `computer.jpg` in the same folder.
3. Open the HTML file in a browser.
4. Click the different hotspots to view their information.

## Result

Thus, an image map was created with fixed clickable hotspots, and the related information is displayed when each hotspot is clicked.

# 7. Home Page with Three Links

## Question

Write an HTML code to create a Home page having three links: About Us, Our Services and Contact Us. Create separate web pages for the three links.

## Program

### File 1: `index.html`

```html
<!DOCTYPE html>
<html>
<body>
    <h1>Home Page</h1>

    <a href="about.html">About Us</a><br><br>
    <a href="services.html">Our Services</a><br><br>
    <a href="contact.html">Contact Us</a>
</body>
</html>
```

### File 2: `about.html`

```html
<!DOCTYPE html>
<html>
<body>
    <h2>About Us</h2>
    <p>We are a company providing quality services.</p>
    <a href="index.html">Home</a>
</body>
</html>
```

### File 3: `services.html`

```html
<!DOCTYPE html>
<html>
<body>
    <h2>Our Services</h2>
    <p>We provide web development and software services.</p>
    <a href="index.html">Home</a>
</body>
</html>
```

### File 4: `contact.html`

```html
<!DOCTYPE html>
<html>
<body>
    <h2>Contact Us</h2>
    <p>Email: info@example.com</p>
    <p>Phone: 9876543210</p>
    <a href="index.html">Home</a>
</body>
</html>
```

## Sample Output

The home page displays three links:

- About Us
- Our Services
- Contact Us

Clicking each link opens its respective page. The Home link returns to the main page.

## Execution Steps

1. Save all four HTML files in the same folder.
2. Open `index.html` in a browser.
3. Click each link to navigate between pages.

## Result

Thus, a home page with three links and three separate web pages was created successfully using HTML hyperlinks.

# Java Servlet Practical – Employee Login

**Level:** Absolute Beginner  
**Software:** Windows Notepad, JDK, Apache Tomcat  
**Aim:** To write a servlet that reads parameters from an employee login page.

## 1. Understand the Program

We will create an employee login form. When the employee enters an ID and password and clicks Login, the servlet reads the submitted values and displays the employee ID.

- `employee.html` — displays the login form.
- `LoginServlet.java` — receives the form parameters.
- `web.xml` — maps the URL to the servlet.
- Apache Tomcat — runs the servlet.

**Important:** Notepad is used to write code. You need Apache Tomcat and the Java Servlet API to execute the servlet.

## 2. Create the Folder Structure

Create a folder named `EmployeeLogin` on your Desktop.

For a traditional Tomcat web application, create this structure:

```text
EmployeeLogin/
└── WEB-INF/
    ├── web.xml
    ├── classes/
    │   └── LoginServlet.class
    └── lib/
```

Also create:

```text
EmployeeLogin/
└── employee.html
```

The `LoginServlet.java` source file can be kept in a separate working folder. After compiling it, copy the generated `LoginServlet.class` into `WEB-INF/classes/`.

## 3. Create employee.html

### Steps

1. Open Notepad.
2. Copy the code below.
3. Click **File → Save As**.
4. Select the `EmployeeLogin` folder.
5. Enter `employee.html` as the filename.
6. Select **All Files** under Save as type.
7. Click Save.

### Code

```html
<html>
<body>
    <h2>Employee Login</h2>

    <form action="LoginServlet" method="post">
        Employee ID:
        <input type="text" name="id"><br><br>

        Password:
        <input type="password" name="pass"><br><br>

        <input type="submit" value="Login">
    </form>
</body>
</html>
```

### Explanation

- `action="LoginServlet"` sends the form to the servlet.
- `method="post"` submits the form using HTTP POST.
- `name="id"` identifies the employee ID parameter.
- `name="pass"` identifies the password parameter.

## 4. Create LoginServlet.java

### Steps

1. Open a new Notepad window.
2. Paste the following code.
3. Click **File → Save As**.
4. Save the file as `LoginServlet.java`.
5. Select **All Files** as the file type.

### Code for Tomcat 9

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class LoginServlet extends HttpServlet {

    public void doPost(HttpServletRequest request,
                       HttpServletResponse response)
                       throws IOException {

        response.setContentType("text/html");
        PrintWriter out = response.getWriter();

        String id = request.getParameter("id");
        String pass = request.getParameter("pass");

        out.println("<html><body>");
        out.println("<h2>Employee Login Details</h2>");
        out.println("Employee ID: " + id + "<br>");
        out.println("Password received successfully");
        out.println("</body></html>");
    }
}
```

## 5. Create web.xml

### Steps

1. Open Notepad.
2. Paste the following code.
3. Save the file as `web.xml`.
4. Place it inside `EmployeeLogin/WEB-INF/`.

### Code

```xml
<?xml version="1.0" encoding="UTF-8"?>

<web-app>
    <servlet>
        <servlet-name>LoginServlet</servlet-name>
        <servlet-class>LoginServlet</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>LoginServlet</servlet-name>
        <url-pattern>/LoginServlet</url-pattern>
    </servlet-mapping>
</web-app>
```

### Explanation

- `servlet-name` identifies the servlet in the configuration.
- `servlet-class` specifies its Java class.
- `url-pattern` specifies the URL used to access the servlet.

## 6. Compile and Deploy the Servlet

You cannot run the servlet by double-clicking `employee.html`. The Java source must be compiled against the matching Servlet API and deployed to Tomcat.

### Step A: Check Java

Open Command Prompt and enter:

```text
java -version
javac -version
```

If these commands are not recognized, the JDK may be missing or not configured in PATH. Ask your lab instructor before changing shared computer settings.

### Step B: Check Tomcat

Find the Tomcat installation folder. For example, it might be:

```text
C:\apache-tomcat-9
```

The actual folder may be different in your lab.

### Step C: Compile the servlet

For a Tomcat 9 installation, open Command Prompt and change to the folder containing `LoginServlet.java`. Run the following command, replacing the example paths with your actual paths:

```text
javac -cp "C:\apache-tomcat-9\lib\servlet-api.jar" LoginServlet.java
```

If compilation succeeds, a file named `LoginServlet.class` is generated.

Copy that file into:

```text
EmployeeLogin\WEB-INF\classes\
```

Create the `classes` folder if it does not exist.

### Step D: Deploy to Tomcat

Copy the complete `EmployeeLogin` web application folder into Tomcat's `webapps` directory.

For example:

```text
C:\apache-tomcat-9\webapps\EmployeeLogin\
```

Confirm that `employee.html`, `WEB-INF/web.xml`, and `WEB-INF/classes/LoginServlet.class` are in their correct locations.

Start Tomcat using the lab's configured method. On a standard installation, its startup script is located in the `bin` directory.

## 7. Execute the Program

Open a browser and enter:

```text
http://localhost:8080/EmployeeLogin/employee.html
```

Enter these sample values:

- Employee ID: `E101`
- Password: `abc123`

Click **Login**.

## 8. Expected Output

```text
Employee Login Details

Employee ID: E101
Password received successfully
```

The password is read by the servlet but is not displayed.

## 9. Common Errors

| Error | What to check |
|---|---|
| 404 Not Found | Application folder, URL and servlet mapping |
| `javax.servlet` package missing | Servlet API classpath and Tomcat version |
| `ClassNotFoundException` | Class name and `WEB-INF/classes` location |
| Tomcat does not start | Server configuration and port conflicts |
| HTML opens but Login fails | Ensure the application is deployed and Tomcat is running |

## 10. Important Practical Viva Questions

**1. What is a servlet?**  
A Java server-side component that handles client requests and generates responses.

**2. What is Apache Tomcat?**  
A web server and servlet container that runs Java web applications.

**3. What does `getParameter()` do?**  
It retrieves a submitted request parameter by name.

**4. What is `doPost()`?**  
It handles HTTP POST requests.

**5. What is `web.xml`?**  
A deployment descriptor used to configure a web application, including servlet mappings.

**6. What is the difference between HTML and a servlet?**  
HTML defines the page displayed in a browser; a servlet processes requests on the server.

## Result

Thus, an employee login page was created, and a Java servlet was configured to read the submitted employee ID and password parameters.

# 9. JavaScript Form Validation

## (i) JavaScript Program to Validate the User Login Page

### Aim
To write a JavaScript program to validate the username and password fields in a login form.

### Folder Structure

```text
LoginValidation/
└── login.html
```

### Program: `login.html`

```html
<!DOCTYPE html>
<html>
<body>
    <h2>User Login</h2>

    <form onsubmit="return validate()">
        Username:
        <input type="text" id="user"><br><br>

        Password:
        <input type="password" id="pass"><br><br>

        <input type="submit" value="Login">
    </form>

    <script>
        function validate() {
            let u = document.getElementById("user").value;
            let p = document.getElementById("pass").value;

            if (u == "" || p == "") {
                alert("Please fill all fields");
                return false;
            }

            alert("Login form validated successfully");
            return false;
        }
    </script>
</body>
</html>
```

### Steps to Execute

1. Open Notepad.
2. Type or paste the program.
3. Click **File → Save As**.
4. Enter `login.html` as the file name.
5. Select **All Files** as Save as type.
6. Save the file inside the `LoginValidation` folder.
7. Double-click `login.html` to open it in a browser.
8. Leave the fields empty and click Login to test validation.
9. Enter both fields and click Login again.

### Expected Output

- If the fields are empty: `Please fill all fields`
- If both fields are filled: `Login form validated successfully`

### Result
Thus, the JavaScript program to validate the user login page was written and executed successfully.

---

## (ii) JavaScript Program to Validate the Registration Form

### Aim
To write a JavaScript program to validate the name, email, password, and gender fields in a registration form.

### Folder Structure

```text
RegistrationValidation/
└── register.html
```

### Program: `register.html`

```html
<!DOCTYPE html>
<html>
<body>
    <h2>Registration Form</h2>

    <form onsubmit="return validate()">
        Name:
        <input type="text" id="name"><br><br>

        Email:
        <input type="text" id="email"><br><br>

        Password:
        <input type="password" id="pass"><br><br>

        Gender:
        <input type="radio" name="gender" value="Male"> Male
        <input type="radio" name="gender" value="Female"> Female
        <br><br>

        <input type="submit" value="Register">
    </form>

    <script>
        function validate() {
            let n = document.getElementById("name").value;
            let e = document.getElementById("email").value;
            let p = document.getElementById("pass").value;
            let g = document.querySelector(
                'input[name="gender"]:checked'
            );

            if (n == "" || e == "" || p == "") {
                alert("Please fill all fields");
                return false;
            }

            if (!e.includes("@") || !e.includes(".")) {
                alert("Enter a valid email");
                return false;
            }

            if (p.length < 6) {
                alert("Password must contain at least 6 characters");
                return false;
            }

            if (g == null) {
                alert("Please select gender");
                return false;
            }

            alert("Registration successful");
            return false;
        }
    </script>
</body>
</html>
```

### Steps to Execute

1. Open Notepad.
2. Type or paste the program.
3. Click **File → Save As**.
4. Enter `register.html` as the file name.
5. Select **All Files** as Save as type.
6. Save the file inside the `RegistrationValidation` folder.
7. Double-click `register.html` to open it in a browser.
8. Test the form with empty fields, an invalid email, a short password, and no gender selection.
9. Enter valid sample details and click Register.

### Expected Output

- Empty fields: `Please fill all fields`
- Invalid email: `Enter a valid email`
- Password shorter than 6 characters: `Password must contain at least 6 characters`
- Gender not selected: `Please select gender`
- All checks passed: `Registration successful`

### Result
Thus, the JavaScript program to validate the registration form was written and executed successfully.

---

## Important Viva Questions

**1. What is JavaScript?**  
JavaScript is a scripting language used to make web pages interactive.

**2. What is form validation?**  
Form validation checks user input before the form is accepted.

**3. What does `getElementById()` do?**  
It selects an HTML element using its ID.

**4. What does `alert()` do?**  
It displays a message box in the browser.

**5. What does `return false` do?**  
It prevents the form from being submitted.

**6. What does `length` return?**  
It returns the number of characters in a string.

**7. What is `onsubmit`?**  
It is an event that occurs when a form is submitted.

**Note:** These are beginner-level client-side validation programs. They do not authenticate a real user or save registration data to a database.

# 10. DHTML and CSS Heading Programs

## (i) DHTML Program to Give Different Colors for Different Heading Tags

### Aim
To write a DHTML program to apply different colors to the heading tags `<h1>` to `<h6>` using JavaScript.

### Folder Structure

```text
HeadingColors/
└── headings.html
```

### Program: `headings.html`

```html
<html>
<head>
    <title>Heading Colors</title>
</head>
<body>
    <h1 id="h1">Heading 1</h1>
    <h2 id="h2">Heading 2</h2>
    <h3 id="h3">Heading 3</h3>
    <h4 id="h4">Heading 4</h4>
    <h5 id="h5">Heading 5</h5>
    <h6 id="h6">Heading 6</h6>

    <script>
        document.getElementById("h1").style.color = "red";
        document.getElementById("h2").style.color = "blue";
        document.getElementById("h3").style.color = "green";
        document.getElementById("h4").style.color = "orange";
        document.getElementById("h5").style.color = "purple";
        document.getElementById("h6").style.color = "brown";
    </script>
</body>
</html>
```

### Steps to Execute

1. Open Notepad.
2. Type or paste the program.
3. Click **File → Save As**.
4. Enter `headings.html` as the file name.
5. Select **All Files** as Save as type.
6. Save it inside the `HeadingColors` folder.
7. Double-click `headings.html` to open it in a browser.

### Expected Output

Six headings appear in different colors:

- Heading 1 — Red
- Heading 2 — Blue
- Heading 3 — Green
- Heading 4 — Orange
- Heading 5 — Purple
- Heading 6 — Brown

### Result
Thus, different colors were applied to the heading tags using JavaScript in a DHTML program.

---

## (ii) Using CSS to Implement the Behavior of `<h1>` to `<h6>` Tags

### Aim
To use CSS to set different font sizes for the heading tags `<h1>` to `<h6>`.

### Folder Structure

```text
CSSHeadings/
└── headings.html
```

### Program: `headings.html`

```html
<html>
<head>
    <title>CSS Heading Styles</title>

    <style>
        h1 {
            font-size: 32px;
        }

        h2 {
            font-size: 24px;
        }

        h3 {
            font-size: 19px;
        }

        h4 {
            font-size: 16px;
        }

        h5 {
            font-size: 13px;
        }

        h6 {
            font-size: 11px;
        }
    </style>
</head>
<body>
    <h1>Heading 1</h1>
    <h2>Heading 2</h2>
    <h3>Heading 3</h3>
    <h4>Heading 4</h4>
    <h5>Heading 5</h5>
    <h6>Heading 6</h6>
</body>
</html>
```

### Steps to Execute

1. Open Notepad.
2. Type or paste the program.
3. Click **File → Save As**.
4. Enter `headings.html` as the file name.
5. Select **All Files** as Save as type.
6. Save it inside the `CSSHeadings` folder.
7. Double-click `headings.html` to open it in a browser.

### Expected Output

The browser displays six headings in decreasing font sizes.

| Heading tag | Font size |
|---|---:|
| `<h1>` | 32px |
| `<h2>` | 24px |
| `<h3>` | 19px |
| `<h4>` | 16px |
| `<h5>` | 13px |
| `<h6>` | 11px |

These sizes approximate traditional browser defaults; actual default sizes may vary.

### Result
Thus, CSS was used to control the font sizes of heading tags from `<h1>` to `<h6>`.

---

## Important Viva Questions

**1. What is DHTML?**  
DHTML stands for Dynamic HTML. It combines HTML, CSS, and JavaScript to make web pages dynamic.

**2. What is CSS?**  
CSS stands for Cascading Style Sheets. It controls the appearance of HTML elements.

**3. What is JavaScript used for in the first program?**  
JavaScript changes the color of each heading dynamically.

**4. What is the purpose of `getElementById()`?**  
It selects an HTML element using its ID.

**5. What does `font-size` do?**  
It specifies the size of the text.

**6. What is the difference between DHTML and CSS?**  
DHTML combines technologies to make pages dynamic, while CSS is used to style HTML elements.

# 11. HTML Lists

## Aim
To write an HTML program to illustrate the usage of ordered lists, unordered lists, and definition lists.

## Folder Structure

```text
HTMLLists/
└── lists.html
```

## Program: `lists.html`

```html
<html>
<head>
    <title>HTML Lists</title>
</head>
<body>
    <h2>Ordered List</h2>
    <ol>
        <li>HTML</li>
        <li>CSS</li>
        <li>JavaScript</li>
    </ol>

    <h2>Unordered List</h2>
    <ul>
        <li>Apple</li>
        <li>Mango</li>
        <li>Orange</li>
    </ul>

    <h2>Definition List</h2>
    <dl>
        <dt>HTML</dt>
        <dd>Used to create web pages.</dd>

        <dt>CSS</dt>
        <dd>Used to style web pages.</dd>

        <dt>JavaScript</dt>
        <dd>Used to make web pages interactive.</dd>
    </dl>
</body>
</html>
```

## Steps to Execute

1. Create a folder named `HTMLLists`.
2. Open Notepad.
3. Copy and paste the program.
4. Click **File → Save As**.
5. Enter `lists.html` as the file name.
6. Select **All Files** as Save as type.
7. Save the file inside the `HTMLLists` folder.
8. Double-click `lists.html` to open it in a web browser.

## Expected Output

### Ordered List
1. HTML
2. CSS
3. JavaScript

### Unordered List
- Apple
- Mango
- Orange

## Result

Thus, an HTML program illustrating ordered, unordered, and definition lists was written and executed successfully.

# 12. JavaScript Program to Calculate Squares and Cubes

## Aim
To write a JavaScript program to calculate the squares and cubes of numbers from 0 to 10 and display the results in an HTML table.

## Folder Structure

```text
SquaresCubes/
└── index.html
```

## Program: `index.html`

```html
<html>
<head>
    <title>Squares and Cubes</title>
</head>
<body>
    <h2>Squares and Cubes of Numbers</h2>

    <table border="1" cellpadding="8">
        <tr>
            <th>Number</th>
            <th>Square</th>
            <th>Cube</th>
        </tr>

        <script>
            for (let i = 0; i <= 10; i++) {
                document.write("<tr>");
                document.write("<td>" + i + "</td>");
                document.write("<td>" + (i * i) + "</td>");
                document.write("<td>" + (i * i * i) + "</td>");
                document.write("</tr>");
            }
        </script>
    </table>
</body>
</html>
```

## Steps to Execute

1. Create a folder named `SquaresCubes`.
2. Open Notepad.
3. Copy and paste the program.
4. Click **File → Save As**.
5. Enter `index.html` as the file name.
6. Select **All Files** as Save as type.
7. Save the file inside the `SquaresCubes` folder.
8. Double-click `index.html` to open it in a web browser.

## Expected Output

| Number | Square | Cube |
|---:|---:|---:|
| 0 | 0 | 0 |
| 1 | 1 | 1 |
| 2 | 4 | 8 |
| 3 | 9 | 27 |
| 4 | 16 | 64 |
| 5 | 25 | 125 |
| 6 | 36 | 216 |
| 7 | 49 | 343 |
| 8 | 64 | 512 |
| 9 | 81 | 729 |
| 10 | 100 | 1000 |

## Simple Explanation

- `for (let i = 0; i <= 10; i++)` repeats the loop from 0 to 10.
- `i * i` calculates the square.
- `i * i * i` calculates the cube.
- `document.write()` writes HTML content into the page.
- `<tr>` creates a table row.
- `<th>` creates a heading cell.
- `<td>` creates a data cell.

### Example

For the number 3:

- Square = 3 × 3 = 9
- Cube = 3 × 3 × 3 = 27

## Result

Thus, the squares and cubes of numbers from 0 to 10 were calculated and displayed in an HTML table using JavaScript.

# 13. Client-Side Validation of Web Form Controls Using DHTML

## Aim

To write a client-side script using DHTML to validate web form controls such as name, email, and password.

## Folder Structure

```text
FormValidation/
└── index.html
```

## Program

```html
<!DOCTYPE html>
<html>
<head>
    <title>Form Validation</title>

    <script>
        function validateForm() {
            let name = document.getElementById("name").value;
            let email = document.getElementById("email").value;
            let password = document.getElementById("password").value;

            if (name.trim() == "") {
                alert("Please enter your name");
                return false;
            }

            if (email == "" || !email.includes("@")) {
                alert("Please enter a valid email");
                return false;
            }

            if (password.length < 6) {
                alert("Password must contain at least 6 characters");
                return false;
            }

            alert("Form submitted successfully!");
            return true;
        }
    </script>
</head>

<body>
    <h2>Registration Form</h2>

    <form onsubmit="return validateForm()">
        Name:
        <input type="text" id="name">
        <br><br>

        Email:
        <input type="text" id="email">
        <br><br>

        Password:
        <input type="password" id="password">
        <br><br>

        <input type="submit" value="Register">
        <input type="reset" value="Clear">
    </form>
</body>
</html>
```

## Procedure

1. Create a folder named `FormValidation`.
2. Open Notepad and type the above program.
3. Select **File → Save As**.
4. Save the file as `index.html`.
5. Set **Save as type** to `All Files`.
6. Open `index.html` in a web browser.
7. Enter the details and click **Register** to test the validation.

## Expected Output

The browser displays a registration form containing:

- Name
- Email
- Password
- Register button
- Clear button

When invalid data is entered, an appropriate alert message is displayed. When valid data is entered, the message **"Form submitted successfully!"** is displayed.

## Explanation

- `getElementById()` selects an HTML element using its ID.
- `.value` retrieves the value entered by the user.
- `if` checks whether the entered data satisfies the conditions.
- `alert()` displays a message in the browser.
- `return false` prevents form submission when validation fails.
- `onsubmit` calls the validation function when the form is submitted.
- `password.length < 6` checks whether the password contains at least six characters.

## Result

Thus, the client-side script for validating web form controls using DHTML was implemented successfully.

# 14. XML Document for Customer Details

## Aim

To create an XML document to store customer details such as customer ID, name, address, phone number, and email.

## Folder Structure

```text
CustomerDetails/
└── customer.xml
```

## Program — `customer.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>

<customers>
    <customer>
        <customer_id>101</customer_id>
        <name>Arun Kumar</name>
        <address>Chennai, Tamil Nadu</address>
        <phone>9876543210</phone>
        <email>arun@gmail.com</email>
    </customer>

    <customer>
        <customer_id>102</customer_id>
        <name>Priya</name>
        <address>Coimbatore, Tamil Nadu</address>
        <phone>9876501234</phone>
        <email>priya@gmail.com</email>
    </customer>
</customers>
```

## Procedure

1. Create a folder named `CustomerDetails`.
2. Open Notepad and type the XML program.
3. Select **File → Save As**.
4. Enter `customer.xml` as the file name.
5. Select **All Files** under Save as type.
6. Choose **UTF-8** encoding and save the file.
7. Open `customer.xml` in a web browser to view the document.

## Expected Output

The XML document displays two customer records containing:

- Customer ID
- Name
- Address
- Phone number
- Email address

## Explanation

- `<?xml version="1.0" encoding="UTF-8"?>` declares the XML version and encoding.
- `<customers>` is the root element.
- `<customer>` represents an individual customer.
- `<customer_id>`, `<name>`, `<address>`, `<phone>`, and `<email>` store customer information.
- Each opening tag must have a matching closing tag.

## Result

Thus, an XML document for storing customer details was created successfully.


# 14. Sort Numbers in Descending Order Using HTML and JavaScript

## Aim

To write an HTML page using JavaScript to accept integers from the user and display them in descending order.

## Folder Structure

```text
DescendingSort/
└── index.html
```

## Program — `index.html`

```html
<html>
<head>
    <title>Descending Order</title>
</head>
<body>
    <h2>Sort Numbers in Descending Order</h2>

    Enter numbers:
    <input type="text" id="num" placeholder="5,2,9,1,7">

    <button onclick="sort()">Sort</button>

    <p id="result"></p>

    <script>
        function sort() {
            let a = document.getElementById("num").value.split(",").map(Number);

            for (let i = 0; i < a.length; i++) {
                for (let j = i + 1; j < a.length; j++) {
                    if (a[i] < a[j]) {
                        let temp = a[i];
                        a[i] = a[j];
                        a[j] = temp;
                    }
                }
            }

            document.getElementById("result").innerHTML =
                "Descending Order: " + a;
        }
    </script>
</body>
</html>
```

## Procedure

1. Create a folder named `DescendingSort`.
2. Open Notepad and type the program.
3. Select **File → Save As**.
4. Save the program as `index.html`.
5. Choose **All Files** under Save as type.
6. Open `index.html` in a web browser.
7. Enter numbers separated by commas and click **Sort**.

## Sample Input

```text
5,2,9,1,7
```

## Output

```text
Descending Order: 9,7,5,2,1
```

## Explanation

- `getElementById()` gets an HTML element using its ID.
- `.value` reads the numbers entered in the text box.
- `split(",")` separates the numbers using commas.
- `map(Number)` converts the input strings into numbers.
- Two `for` loops compare the numbers.
- `if (a[i] < a[j])` checks whether the later number is larger.
- `temp` temporarily stores a number while swapping.
- `innerHTML` displays the sorted result.

## Result

Thus, an HTML page using JavaScript to accept integers from the user and display them in descending order was implemented successfully.







