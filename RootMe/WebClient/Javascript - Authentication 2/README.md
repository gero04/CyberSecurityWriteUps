# Root-Me: Javascript - Authentication 2

**Platform:** [Root-Me](https://www.root-me.org/)  
**Challenge:** [Web-Client: Javascript - Authentication 2](https://www.root-me.org/en/Challenges/Web-Client/Javascript-Authentication-2)  
**Difficulty:** Easy  
**Objective:** Find the hidden flag by bypassing client-side authentication.

## 1. General Information

This is a client-side web challenge. Upon loading, the page presents a login button that triggers a prompt asking for a username and password. Since the validation is handled on the client side via an external JavaScript file, we can inspect it to retrieve the credentials.

- **Target IP:** Not applicable (client-side challenge)
- **Tools used:** Web browser developer tools (F12)

## 2. Enumeration

Upon visiting the challenge page, we see a simple "login" button. Clicking it triggers two prompts asking for a username and a password — a clear sign that authentication is handled client-side via JavaScript.

**Step 1 — Inspect with DevTools (F12)**  
Opening the browser's developer tools and navigating to the **Debugger** tab (Firefox) or **Sources** tab (Chrome) reveals an external JavaScript file being loaded: `login.js`. Unlike the previous challenge, the logic is not inline in the HTML — it's in a separate file, which is a slightly more obfuscated approach.

**Step 2 — View Page Source (`Ctrl+U`)**  
Viewing the HTML source confirms that no credentials are embedded there. The only relevant line is:
```html
<script language="JavaScript" src="login.js"></script>
```

**Step 3 — Read `login.js`**  
Opening `login.js` in the Debugger reveals the full authentication logic:
```javascript
function connexion(){
    var username = prompt("Username :", "");
    var password = prompt("Password :", "");
    var TheLists = ["GOD:HIDDEN"];
    for (i = 0; i < TheLists.length; i++)
    {
        if (TheLists[i].indexOf(username) == 0)
        {
            var TheSplit = TheLists[i].split(":");
            var TheUsername = TheSplit[0];
            var ThePassword = TheSplit[1];
            if (username == TheUsername && password == ThePassword)
            {
                alert("Vous pouvez utiliser ce mot de passe pour valider ce challenge (en majuscules) / You can use this password to validate this challenge (uppercase)");
            }
        }
        else
        {
            alert("Nope, you're a naughty hacker.")
        }
    }
}
```

The credentials are hardcoded inside the `TheLists` array in `"USERNAME:PASSWORD"` format. Splitting on `:` gives us:
```
Username: GOD
Password: HIDDEN
```

## 3. Exploiting

With the credentials discovered, exploitation is straightforward:

1. Click the "login" button.
2. Enter `GOD` in the username prompt.
3. Enter `HIDDEN` in the password prompt.
4. An alert box appears confirming the password is correct.

The challenge instructs us to submit the password in uppercase — which it already is.

## 4. Privilege Escalation

Not applicable.

## 5. Flags

The flag is: `HIDDEN`

## 6. Conclusion

This challenge builds on the previous one, introducing a slightly more obfuscated approach: instead of embedding the credentials directly in the HTML, they are moved to an external `.js` file. However, this provides no real security improvement — external JavaScript files are just as publicly accessible as inline code.

A second interesting detail is the credential format: `"GOD:HIDDEN"` inside an array suggests the developer may have intended to support multiple users. This pattern (credentials stored as `user:pass` strings in client-side arrays) is still completely insecure regardless of how many entries it contains.

**What I learned:**
- Moving credentials to an external JS file does not add any security — it's security through obscurity at best.
- The Debugger tab in DevTools is essential for finding and reading external JavaScript files.
- Any data hardcoded on the client side is always recoverable by the user.

## Note

This writeup is for educational purposes only. Always practice ethical hacking and only test on platforms you have permission to use.