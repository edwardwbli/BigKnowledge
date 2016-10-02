
# Sed command sample 

1. tack on a nice header in a file
```bash  
  sed -i 1i "potato_id,potato_type,description" potatoes.csv
```
2. override specific line, in below example , we override the second line in nginx.conf file.
```bash
sed -i '2s/.*/worker_processes 1;/' /etc/nginx/nginx.conf 	
```