# Root-Me: Javascript - Authentication

**Platform:** [Root-Me](https://www.root-me.org/)  
**Challenge:** [Web-Client: Javascript - Authentication](https://www.root-me.org/en/Challenges/Web-Client/Javascript-Source)  
**Difficulty:** Easy  
**Objective:** Find the hidden flag by bypassing client-side authentication.

## 1. General Information

This is a client-side web challenge. Upon loading, the page presents an alert asking for a password. The hint suggests that we need to find a valid credential to authenticate. Since the validation is handled on the client side, we can inspect the code to retrieve them.
- **Target IP:** Not applicable (client-side challenge)
- **Tools used:** Web browser developer tools (F12)

## 2. Enumeration

Upon visiting the challenge page, a password prompt appears immediately — a clear sign that authentication is handled client-side via JavaScript.

**Step 1 — Inspect with DevTools (F12)**  
Opening the browser's developer tools and navigating to the **Sources** tab reveals the JavaScript files loaded by the page. This is often the first place to look for client-side logic.

**Step 2 — View Page Source (`Ctrl+U`)**  
Viewing the full HTML source confirms that the authentication logic is embedded directly in the page inside a `<script>` tag. A quick `Ctrl+F` search for keywords like `pass` or `password` leads us straight to the relevant code:

```
<html>
    <head>
	<script type="text/javascript">
	/* <![CDATA[ */
	    function login(){
		pass=prompt("Entrez le mot de passe / Enter password");
		if ( pass == "123456azerty" ) {
		    alert("Mot de passe accepté, vous pouvez valider le challenge avec ce mot de passe.\nYou can validate the challenge using this password.");  }
		else {
		    alert("Mauvais mot de passe / wrong password !");
		}
	    }
	/* ]]> */
	</script>
    </head>
   <body onload="login();"><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>

    </body>
</html>
```
On this fragment of code, we find the credentials, as they are hardcoded in plain text:
```
Password: 123456azerty
```
## 3. Exploiting

With the credentials discovered, exploitation is straightforward:
1. Enter `123456azerty` in the password field.
2. Click the "Accept" button.
3. An alert box appears with a success message, confirming that the password is correct and can be used to validate the challenge.
The flag is the password itself, as it is the secret required to complete the challenge.
## 4. Privilege escalation

Not applicable

## 5. Flags

The flag is: `123456azerty`

## 6. Conclusion

This simple challenge highlights a fundamental security principle: never trust client-side validation. Any logic or credentials embedded in client-side code (HTML, JavaScript, etc.) are fully visible to anyone using the browser. An attacker can easily inspect the source and extract sensitive information.
**What I learned:**
- Authentication logic must always be implemented on the server side.
- Client-side checks are only for user experience, never for security.
- Developer tools are essential for inspecting and understanding web applications.

## Note

This writeup is for educational purposes only. Always practice ethical hacking and only test on platforms you have permission to use.