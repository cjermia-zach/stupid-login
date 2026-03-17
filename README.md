# CSCE 477 Homework 3: A Stupid Login Page
This is a simple HTML &amp; JavaScript document to demonstrate vulnerability in a simple login form. This is part of Texas A&amp;M's CSCE 477 course and shall not be used for malicious purposes.

In this example, instead of creating the JavaScript file separately, the HTML and JavaScript codes are combined. The body of the HTML itself is relatively simple, with a username field, a password field, and an access button, as seen in this snippet:

```
<body>
    <h1>Stupid Login</h1>
    <form onsubmit="return login()">
        <label>Email:</label><br>
        <input type="text" id="email" name="email"><br><br>
        <label>Password:</label><br>
        <input type="password" id="password" name="password"><br><br>
        <button type="submit">Access</button>
    </form>
</body>
```

The JavaScript portion is on the following lines of code:

```

<script>
        function login() {
            // Get the input values
            const email = document.getElementById("email").value;
            const password = document.getElementById("password").value;
            // I don't want to make it fully stupid and vulnerable
            // so at least fix the access control a bit
            // by input validation
            if (email === "" || password === "") {
                alert("ERROR: Empty field. Try again.");
                return false;
            }
            //verify that it has "@"
            if(!email.includes("@")) {
                alert("ERROR: Invalid email format. Try again.");
                return false;
            }
            //practice secure password requirements...at least
            if (password.length < 8) {
                alert("ERROR: Password is weak. Try again.");
                return false;
            } 
            //valid?
            alert("Login successful! Welcome, " + email + "!");
            return true;
        }
    </script>
```

The goal of this website is to make the website as stupid as possible when it comes to input handling, but also not make the same mistake as the OWASP Juice Shop example. In the OWASP Juice Shop example, the login page is easily exploitable by injecting the following script (SQL Injection):

```
' OR 1=1--
```

This website mitigates that by creating the simplest guards possible: input validation. The script checks whether your username is valid with the character "@", whether your password is 8 characters or longer, or whether both fields are empty, as seen in the following lines:

```
if (email === "" || password === "") {
                alert("ERROR: Empty field. Try again.");
                return false;
            }
            //verify that it has "@"
            if(!email.includes("@")) {
                alert("ERROR: Invalid email format. Try again.");
                return false;
            }
            //practice secure password requirements...at least
            if (password.length < 8) {
                alert("ERROR: Password is weak. Try again.");
                return false;
            } 
            //valid?
            alert("Login successful! Welcome, " + email + "!");
            return true;
```

That way, even though other vulnerabilities exist, simply entering OR 1 = 1 will not work anymore, as it fails the "@" test. Other aspects of this simple login page will remain stupid and deliberately vulnerable to showcase further vulnerabilities that can be exploited. 


