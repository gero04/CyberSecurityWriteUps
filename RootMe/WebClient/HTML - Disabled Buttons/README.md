# Root-Me: Disabled Buttons

- **Site:** [Root-Me](https://www.root-me.org/en/Challenges/Web-Client/)
- **Category:** Web Client
- **Difficulty:** Easy
- **Objective:** Find the hidden flag by enabling and using a disabled form.
## 1. General Information

This is a client-side web challenge where the page presents a simple HTML form with two disabled input fields: a text field and a submit button. The hint suggests that the form is disabled and cannot be used, implying that we need to find a way to enable it.
- **Target IP:** Not applicable (client-side challenge)
- **Tools used:** Web browser developer tools (F12)
## 2. Enumeration

Upon viewing the page source (right click -> "Inspect" or `CTRL + U`) we will find the following HTML

```
<html>
	<head>
		<title>Under construction</title>
		<link rel="stylesheet" property="stylesheet" type="text/css" href="style.css" media="all">
	</head>
	<body>
		<link rel="stylesheet" property="stylesheet" id="s" type="text/css" href="/template/s.css" media="all">
		<iframe id="iframe" src="https://www.root-me.org/?page=externe_header"></iframe>
		<h1>Website temporarily closed.</h1>
		<hr>
		<form action="" method="post" name="authform">
			<div>
				<input disabled="" type="text" name="auth-login" value="">
				<input disabled="" type="submit" value="Member access" name="authbutton">
			</div>
		</form>
	</body>
</html>
```
The key observation is the `disabled=""` attribute on both `<input>` elements, as this attribute prevents user interaction with the form fields. Since this is client-side HTML, it can be modified directly in the browser.
# 3. Exploiting

The exploitation is really straightforward:
1. **Open Developer Tools:** Right-click on the page and select "Inspect" (or press F12).
2. **Locate the form elements:** Find the two `<input>` tags with the `disabled=""` attribute.
3. **Remove the attribute:** Double-click on `disabled=""` and delete it. Do this for both inputs.
4. **Interact with the form:** The text field and the "Member access" button are now enabled.
5. **Submit the form:** Enter any value (e.g., "test") in the text field and click the button.
Upon submission, the page reveals the flag.
**Alternative method:** You could also modify the attributes via the "Elements" tab or even use the browser console to enable them with JavaScript (e.g., `document.querySelector('input[name="authbutton"]').disabled = false`).
# 4. Privilege escalation

Not applicable
# 5. Flags

the flag is: `HTMLCantStopYou`
# 6. Conclusion

This simple challenge highlights an important security principle: **never trust client-side validation or restrictions**. HTML attributes like `disabled`, `hidden`, or `readonly` are only enforced by the browser and can be easily bypassed by an attacker. Any security-critical logic must be implemented on the server side.
Additionally, this exercise reinforces the habit of inspecting page source and using developer tools to understand and manipulate the client-side environment—a fundamental skill for web security testing.
**What I learned:**
- How the `disabled` attribute works in HTML forms.
- The importance of server-side validation.
- A quick technique to bypass client-side restrictions for testing purposes.
# Note
This writeup is for educational purposes only. Always practice ethical hacking and only test on platforms you have permission to use.