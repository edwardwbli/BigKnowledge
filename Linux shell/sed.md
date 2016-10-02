
# Sed command sample 

1. tack on a nice header in a file( sample on MAC os) 

 sample 1
```bash  
  sed  '1 i\ 
  cool' test.csv
```
```
cool will be add in 1st line
```
 sample 2
```bash  
  sed  '1 i\ 
  cool
  ' test.csv
```
```
cool 
will be add before 1st line
```
2. override specific line, in below example , we override the second line in nginx.conf file.
```bash
sed -i '2s/.*/worker_processes 1;/' /etc/nginx/nginx.conf 	
```

3. search for line that matching pattern ,and return the line number. -n for return number only

 sample 1
```bash
sed -n '/jfkdf/=' test.csv
```
```
3
```
 sample 2
```bash
sed '/jfkdf/=' test.csv
```
```
cool cool cool cool pay
cool cool 
3
jfkdf
```
