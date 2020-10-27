```js
var current_text = gs.getProperty('glide.product.description');
var iso = current_text.split('(');
var new_text = iso[0].trim() + ' (Last cloned: ' + new GlideDate() + ' ' + new GlideDateTime().getLocalTime().getByFormat('hh:mm:ss a') + ')';
gs.setProperty('glide.product.description', new_text);
//Hi Rob
```
