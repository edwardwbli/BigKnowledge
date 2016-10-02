#Hexdump sample

1. print hex 
```bash
hexdump text.txt
```
```
0000000 6a 66 6b 64 66 0a 0a                           
0000007
```
2. print charater
```bash
hexdump -c text.txt
```
```
0000000   j   f   k   d   f  \n  \n                                    
0000007
```