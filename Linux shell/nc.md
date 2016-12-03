# Use nc to connect to a UNIX domain socket server:  

```bash
  nc -U /tmp/echo.sock
```

with a node.js net server listening on /tmp/echo.sock
```node.js
  server.listen('/tmp/echo.sock', () => {
    console.log('server bound');
  });
```
