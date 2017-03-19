# This sample to tell how to block browser refresh 

```HTML
<!DOCTYPE HTML>
<html><head>
<title> New Document </title>
<meta http-equiv="content-type" content="text/html; charset=UTF-8" />
</head>
<script language="javascript">
    //function not supported by firefox.
    function RunOnBeforeUnload() {window.onbeforeunload = function(){ return '将丢失未保存的数据!'; } }
</script>
<body onload="RunOnBeforeUnload()">
刷新,关闭,后退,F5 测试
</body>
</html>

```
