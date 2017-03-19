# Cross Domain Request

## Hack 1
Use iframe as a target of form target to submit a post request to avoid redirecting to the action URL, 
and manipulate the loaded response in iframe, by add load event listener to iframe node.   

Note: Should disable we security
* Chrome: start chrome with --disable-web-security

Sample: 

```html
<!DOCTYPE html>
<HTML>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<HEAD>
        <TITLE>MQ TOOLS FOR WMB</TITLE>
</HEAD>
<STYLE>
<!--
body,td,a,p{font-family:arial,sans-serif}
body,td,a,p{font-size:14px}
b{color:#555555}
//-->
</STYLE>
<BODY>

        <FORM NAME="dummy_mqget">
                <B>MQM:</B>
                <BR/>
                <INPUT TYPE="TEXT" NAME="mqm" VALUE="UA0L001WMB" SIZE="80"/>
                <BR/>
                <B>MQ:</B>
                <BR/>
                <INPUT TYPE="TEXT" NAME="mq" VALUE="TLNXDTX.HKDTX.HKDTX.HKHSBC.DUMMY.001" SIZE="80"/>
                <BR/>
                <B>Character Set Encoding (Conversion by Java):</B>
                <BR/>
        </FORM>

        <FORM NAME="mqget" METHOD="POST"  target="gettarget" ACTION="http://ua0l001wmb-mqm.hk.hsbc:7804/mqget">
                <INPUT TYPE="HIDDEN" NAME="DATA" VALUE="" />
        </FORM>
        </TD>
        </TR>
        </TABLE>

		<iframe id="gettarget" name="gettarget" style="display:none;"></iframe>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
<SCRIPT LANGUAGE="javascript">
<!--

function goMqGet() {
        var mqm = document.dummy_mqget.mqm.value;
        var mq = document.dummy_mqget.mq.value;
        var conversion = document.dummy_mqget.conversion.options[document.dummy_mqget.conversion.selectedIndex].value;
        var mode = document.dummy_mqget.mode.options[document.dummy_mqget.mode.selectedIndex].value;
        var data = mqm + '\n' + mq + '\n' + conversion + '\n' + mode;
        document.mqget.DATA.value = data;
		document.mqget.addEventListener('submit', function () {
			document.domain = 'http://ua0l001wmb-mqm.hk.hsbc:7804';
			window.addData = function (data) {
			var dataCode = data.code;
			var dataMsg = data.message;
			if (dataCode === 0) {
				console.log('submit success!');
			} else {
				console.log('submit failed!');
			}
		}
		});
        document.mqget.submit();
}

var fileInput = document.getElementById('reqfile');
fileInput.addEventListener('change', function () {
	var file = fileInput.files[0];
	var reader = new FileReader();
	// Closure to capture the file information.
    reader.onload = (function(theFile) {
        return function(e) {
			var data = e.target.result;
			document.dummy_mqput.message.value = data;
        };
      })(file);
	reader.readAsText(file);
})

var ifr = document.getElementById('gettarget');
ifr.addEventListener('load',function() {
	console.log(ifr.contentWindow);
	console.log(ifr.contentWindow.document.getElementsByTagName('textarea'));

})

//-->
</SCRIPT>
</BODY>
</HTML> 
```
