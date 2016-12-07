# FizzBuzz Coding Sample

## Node.js   
```node
var FizzBuzz = () => {
    for (var i = 1; i <= 100; i++){
        var f = i % 3 == 0, b = i % 5 == 0;
        console.log(f ? (b ? "FizzBuzz" : "Fizz" ) : (b ? "Buzz" : i));
    }
}
FizzBuzz()

```

## Python  
```python
map(lambda i : ("Fizz" * ( i % 5 == 0) + "Buzz"*(i % 3 == 0) )or i, range(1, 101))
```
