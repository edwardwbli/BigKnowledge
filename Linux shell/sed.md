
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


#Appedix

<div id="article_content" class="article_content">

<h2 style="padding:0px; margin:1.833em 0px 0.611em; color:rgb(169,0,0); font-size:1.286em; line-height:1.222em; letter-spacing:-1px; font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t0"></a>
Append Lines Using Sed Command</h2>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
Sed provides the command “a” which appends a line after every line with the address or pattern.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)">Syntax:

#sed 'ADDRESS a\
	Line which you want to append' filename

#sed '/PATTERN/ a\
	Line which you want to append' filename</pre>
<h3 style="padding:0px; margin:1.833em 0px 0.611em; font-weight:normal; font-size:1.286em; line-height:1.222em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t1"></a>
Sed Append Example 1. Add a line after the 3rd line of the file.</h3>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
Add the line “Cool gadgets and websites” after the 3rd line. sed “a” command inserts the line after match.</p>
<center style="padding:0px; margin:0px; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
<div style="padding:0px; margin:10px 0px 10px 2px"></div>
</center>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)">$ <span style="padding:0px; margin:0px">sed '3 a\
&gt; Cool gadgets and websites' thegeekstuff.txt</span>

Linux Sysadmin
Databases - Oracle, mySQL etc.
Security (Firewall, Network, Online Security etc)
<span style="padding:0px; margin:0px">Cool gadgets and websites</span>
Storage in Linux
Productivity (Too many technologies to explore, not much time available)
Windows- Sysadmin, reboot etc.</pre>
<h3 style="padding:0px; margin:1.833em 0px 0.611em; font-weight:normal; font-size:1.286em; line-height:1.222em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t2"></a>
Sed Append Example 2. Append a line after every line matching the pattern</h3>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
The below sed command will add the line “<a href="http://lib.csdn.net/base/linux" class="replace_word" title="Linux知识库" target="_blank" style="color:#df3434; font-weight:bold;">Linux</a> Scripting” after every line that matches the pattern “Sysadmin”.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)"><span style="padding:0px; margin:0px">$ sed '/Sysadmin/a \
&gt; Linux Scripting' thegeekstuff.txt</span>

Linux Sysadmin
<span style="padding:0px; margin:0px">Linux Scripting</span>
Databases - Oracle, mySQL etc.
Security (Firewall, Network, Online Security etc)
Storage in Linux
Productivity (Too many technologies to explore, not much time available)
Windows- Sysadmin, reboot etc.
<span style="padding:0px; margin:0px">Linux Scripting</span></pre>
<h3 style="padding:0px; margin:1.833em 0px 0.611em; font-weight:normal; font-size:1.286em; line-height:1.222em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t3"></a>
Sed Append Example 3. Append a line at the end of the file</h3>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
The following example, appends the line “Website Design” at the end of the file.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)"><span style="padding:0px; margin:0px">$ sed '$ a\
&gt; Website Design' thegeekstuff.txt</span>

Linux Sysadmin
Databases - Oracle, mySQL etc.
Security (Firewall, Network, Online Security etc)
Storage in Linux
Productivity (Too many technologies to explore, not much time available)
Windows- Sysadmin, reboot etc.
<span style="padding:0px; margin:0px">Website Design</span></pre>
<div id="insert_lines" style="padding:0px; margin:0px; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
</div>
<h2 style="padding:0px; margin:1.833em 0px 0.611em; color:rgb(169,0,0); font-size:1.286em; line-height:1.222em; letter-spacing:-1px; font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t4"></a>
Insert Lines Using Sed Command</h2>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
Sed command “i” is used to insert a line before every line with the range or pattern.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)">Syntax:

#sed 'ADDRESS i\
	Line which you want to insert' filename

#sed '/PATTERN/ i\
	Line which you want to insert' filename</pre>
<h3 style="padding:0px; margin:1.833em 0px 0.611em; font-weight:normal; font-size:1.286em; line-height:1.222em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t5"></a>
Sed Insert Example 1. Add a line before the 4th line of the line.</h3>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
Add a line “Cool gadgets and websites” before 4th line. “a” command inserts the line after match whereas “i” inserts before match.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)"><span style="padding:0px; margin:0px">$ sed '4 i\
&gt; Cool gadgets and websites' thegeekstuff.txt</span>

Linux Sysadmin
Databases - Oracle, mySQL etc.
Security (Firewall, Network, Online Security etc)
<span style="padding:0px; margin:0px">Cool gadgets and websites</span>
Storage in Linux
Productivity (Too many technologies to explore, not much time available)
Windows- Sysadmin, reboot etc.</pre>
<h3 style="padding:0px; margin:1.833em 0px 0.611em; font-weight:normal; font-size:1.286em; line-height:1.222em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t6"></a>
Sed Insert Example 2. Insert a line before every line with the pattern</h3>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
The below sed command will add a line “Linux Scripting” before every line that matches with the pattern called ‘Sysadmin”.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)"><span style="padding:0px; margin:0px">$ sed '/Sysadmin/i \
&gt; Linux Scripting' thegeekstuff.txt

Linux Scripting</span>
Linux Sysadmin
Databases - Oracle, mySQL etc.
Security (Firewall, Network, Online Security etc)
Storage in Linux
Productivity (Too many technologies to explore, not much time available)
<span style="padding:0px; margin:0px">Linux Scripting</span>
Windows- Sysadmin, reboot etc.</pre>
<h3 style="padding:0px; margin:1.833em 0px 0.611em; font-weight:normal; font-size:1.286em; line-height:1.222em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t7"></a>
Sed Insert Example 3. Insert a line before the last line of the file.</h3>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
Append a line “Website Design” before the last line of the file.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)"><span style="padding:0px; margin:0px">$ sed '$ i\
&gt; Website Design' thegeekstuff.txt</span>

Linux Sysadmin
Databases - Oracle, mySQL etc.
Security (Firewall, Network, Online Security etc)
Storage in Linux
Productivity (Too many technologies to explore, not much time available)
<span style="padding:0px; margin:0px">Website Design</span>
Windows- Sysadmin, reboot etc.</pre>
<div id="replace_lines" style="padding:0px; margin:0px; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
</div>
<h3 style="padding:0px; margin:1.833em 0px 0.611em; font-weight:normal; font-size:1.286em; line-height:1.222em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t8"></a>
Replace Lines Using Sed Command</h3>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
“c” command in sed used to replace every line matches with the pattern or ranges with the new given line.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)">Syntax:

#sed 'ADDRESS c\
	new line' filename

#sed '/PATTERN/ c\
	new line' filename</pre>
<h3 style="padding:0px; margin:1.833em 0px 0.611em; font-weight:normal; font-size:1.286em; line-height:1.222em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t9"></a>
Sed Replace Example 1. Replace a first line of the file</h3>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
The below command replaces the first line of the file with the “The Geek Stuff”.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)"><span style="padding:0px; margin:0px">$ sed '1 c\
&gt; The Geek Stuff' thegeekstuff.txt

The Geek Stuff</span>
Databases - Oracle, mySQL etc.
Security (Firewall, Network, Online Security etc)
Storage in Linux
Productivity (Too many technologies to explore, not much time available)
Windows- Sysadmin, reboot etc.</pre>
<h3 style="padding:0px; margin:1.833em 0px 0.611em; font-weight:normal; font-size:1.286em; line-height:1.222em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t10"></a>
Sed Replace Example 2. Replace a line which matches the pattern</h3>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
Replace everyline which has a pattern “Linux Sysadmin” to “Linux Sysadmin – Scripting”.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)"><span style="padding:0px; margin:0px">$ sed '/Linux Sysadmin/c \
&gt; Linux Sysadmin - Scripting' thegeekstuff.txt

Linux Sysadmin - Scripting</span>
Databases - Oracle, mySQL etc.
Security (Firewall, Network, Online Security etc)
Storage in Linux
Productivity (Too many technologies to explore, not much time available)
Windows- Sysadmin, reboot etc.</pre>
<h3 style="padding:0px; margin:1.833em 0px 0.611em; font-weight:normal; font-size:1.286em; line-height:1.222em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t11"></a>
Sed Replace Example 3. Replace the last line of the file</h3>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
Sed command given below replaces the last line of the file with “Last Line of the file”.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)"><span style="padding:0px; margin:0px">$ sed '$ c\
&gt; Last line of the file' thegeekstuff.txt</span>

Linux Sysadmin
Databases - Oracle, mySQL etc.
Security (Firewall, Network, Online Security etc)
Storage in Linux
Productivity (Too many technologies to explore, not much time available)
<span style="padding:0px; margin:0px">Last line of the file</span></pre>
<div id="count_lines" style="padding:0px; margin:0px; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
</div>
<h2 style="padding:0px; margin:1.833em 0px 0.611em; color:rgb(169,0,0); font-size:1.286em; line-height:1.222em; letter-spacing:-1px; font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t12"></a>
Print Line Numbers Using Sed Command</h2>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
“=” is a command in sed to print the current line number to the standard output.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)">Syntax:

#sed '=' filename</pre>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
The above send command syntax prints line number in the first line and the original line from the file in the next line .</p>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
sed ‘=’ command accepts only one address, so if you want to print line number for a range of lines, you must use the curly braces.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)">Syntax:

# sed -n '/PATTERN/,/PATTERN/ {
=
p
}' filename</pre>
<h3 style="padding:0px; margin:1.833em 0px 0.611em; font-weight:normal; font-size:1.286em; line-height:1.222em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t13"></a>
Sed Line Number Example 1. Find the line number which contains the pattern</h3>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
The below sed command prints the line number for which matches with the pattern “Databases”</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)"><span style="padding:0px; margin:0px">$ sed -n '/Databases/=' thegeekstuff.txt</span>

2</pre>
<h3 style="padding:0px; margin:1.833em 0px 0.611em; font-weight:normal; font-size:1.286em; line-height:1.222em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t14"></a>
Sed Line Number Example 2. Printing Range of line numbers</h3>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
Print the line numbers for the lines matches from the pattern “<a href="http://lib.csdn.net/base/oracle" class="replace_word" title="Oracle知识库" target="_blank" style="color:#df3434; font-weight:bold;">Oracle</a>” to “Productivity”.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)"><span style="padding:0px; margin:0px">$ sed -n '/Oracle/,/Productivity/{
&gt; =
&gt; p
&gt; }' thegeekstuff.txt</span>

2
Databases - Oracle, mySQL etc.
3
Security (Firewall, Network, Online Security etc)
4
Storage in Linux
5
Productivity (Too many technologies to explore, not much time available)</pre>
<h3 style="padding:0px; margin:1.833em 0px 0.611em; font-weight:normal; font-size:1.286em; line-height:1.222em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif"><a name="t15"></a>
Sed Line Number Example 3. Print the total number of lines in a file</h3>
<p style="padding-top:0px; padding-bottom:0px; margin-top:0px; margin-bottom:1.571em; color:rgb(17,17,17); font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; font-size:14px; line-height:21.993999481201172px">
Line number of the last line of the file will be the total lines in a file. Pattern $ specifies the last line of the file.</p>
<pre style="padding:0.667em 0.917em; margin-top:0px; margin-bottom:1.833em; border:1px solid rgb(221,221,221); overflow:auto; clear:both; font-family:Consolas,'Andale Mono',Monaco,Courier,'Courier New',Verdana,sans-serif; font-size:0.857em; line-height:1.5em; color:rgb(17,17,17); background:rgb(238,238,238)"><span style="padding:0px; margin:0px">$ sed -n '$=' thegeekstuff.txt</span>

6</pre>
   
</div>