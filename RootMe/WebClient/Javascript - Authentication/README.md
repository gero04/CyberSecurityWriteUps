# Root-Me: Javascript - Authentication

**Platform:** [Root-Me](https://www.root-me.org/)  
**Challenge:** [Web-Client: Javascript - Authentication](https://www.root-me.org/en/Challenges/Web-Client/Javascript-authentication)  
**Difficulty:** Easy  
**Objective:** Find the hidden flag by bypassing client-side authentication.
## 1. General Information

This is a client-side web challenge. The page presents a simple login form with two fields (Username and Password) and a "login" button. The hint suggests that we need to find valid credentials to authenticate. Since the validation is handled on the client side, we can inspect the code to retrieve them.
- **Target IP:** Not applicable (client-side challenge)
- **Tools used:** Web browser developer tools (F12)
## 2. Enumeration

First, we view the page source (right-click → "View Page Source" or `Ctrl+U`). The HTML reveals that an external JavaScript file is included:

```
html> 
<head> 
<script type="text/javascript" src="[login.js](view-source:http://challenge01.root-me.org/web-client/ch9/login.js)">
</script> 
</head> 
	<body>
	<link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='[/template/s.css](view-source:http://challenge01.root-me.org/template/s.css)' media='all' />
	<iframe id='iframe' src='[https://www.root-me.org/?page=externe_header](view-source:https://www.root-me.org/?page=externe_header)'>
	</iframe> 
		<fieldset style="margin-top: 10px; padding: 10px;" width="60%"> 
		<legend>
			<b>Login</b>
		</legend>
		<br/> 
		<form name="login" method="POST" action="[](view-source:http://challenge01.root-me.org/web-client/ch9/)">
			Username : 
			<input name="pseudo" /> <br/> 
			Password : 
			<input type="password" name="password" />
			</br></br> 
			<input onclick="Login()" type="button" value="login" name="button" /> 
		</form> 
		</fieldset> 
	</body> 
</html>
```
The form has no `action` attribute, and the button triggers a JavaScript function `Login()` when clicked. This indicates that authentication is entirely client-side.

Opening the browser's Developer Tools (F12) and navigating to the **Sources** (or **Debugger**) tab, we find the `login.js` file. Its content is:
```
login.js

/* <![CDATA[ */

function Login(){
	var pseudo=document.login.pseudo.value;
	var username=pseudo.toLowerCase();
	var password=document.login.password.value;
	password=password.toLowerCase();
	if (pseudo=="4dm1n" && password=="sh.org") {
	    alert("Password accepté, vous pouvez valider le challenge avec ce mot de passe.\nYou can validate the challenge using this password.");
	} else { 
	    alert("Mauvais mot de passe / wrong password"); 
	}
}
/* ]]> */ 
```
On this fragment of code, we finally find the credentials, as they are hardcoded in plain text:
```
Username: 4dm1n
Password: sh.org
```
# 3. Exploiting

With the credentials discovered, exploitation is straightforward:
1. Enter `4dm1n` in the username field and `sh.org` in the password field.
2. Click the "login" button.
3. An alert box appears with a success message, confirming that the password is correct and can be used to validate the challenge.
The flag is the password itself, as it is the secret required to complete the challenge.
# 4. Privilege escalation

Not applicable
# Flags

The flag is: `sh.org`
# 5. Conclusion

This simple challenge highlights a fundamental security principle: never trust client-side validation. Any logic or credentials embedded in client-side code (HTML, JavaScript, etc.) are fully visible to anyone using the browser. An attacker can easily inspect the source and extract sensitive information.
**What I learned:**
- Authentication logic must always be implemented on the server side.
- Client-side checks are only for user experience, never for security.
- Developer tools are essential for inspecting and understanding web applications.
# Note

This writeup is for educational purposes only. Always practice ethical hacking and only test on platforms you have permission to use.