
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