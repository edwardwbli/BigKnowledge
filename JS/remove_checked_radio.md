# double click to remove checked  


## Sample:
### Html segment
```html
<input id="control" type="radio" value="control" name="ok"/>control
<input id="newrun" type="radio" value="newrun" name="ok"/>new
```

### Js Segment
```js
var I = function (str) {
	return document.getElementById(str);
}
var control = I("control");
var newrun = I("newrun");
 
control.addEventListener("dblclick", function(e){
	e.target.checked = false;
})

 
newrun.addEventListener("dblclick", function(e){
	e.target.checked = false;
})
```
