# OCR - Optical Character Recognition

## Python recipe

### Dependency : tesseract + PyOCR + Wand + PIL

### [Reference](https://kknews.cc/tech/6pjmzm.html)

### Code sample 

```python
from wand.image import Image
from PIL import Image as PI
import pyocr
import pyocr.builders
import codecs
import io

tool = pyocr.get_available_tools()[0]
lang = tool.get_available_languages()[0]

req_image = []
final_text = []

image_pdf = Image(filename="./YA_TBYD.pdf", resolution=300)
image_jpeg = image_pdf.convert('jpeg')

for img in image_jpeg.sequence:
    img_page = Image(image=img)
    req_image.append(img_page.make_blob('jpeg'))

for img in req_image:
    txt = tool.image_to_string(PI.open(io.BytesIO(img)),lang=lang,builder=pyocr.builders.TextBuilder())
    final_text.append(txt)

text_file = codecs.open("output.txt","w","utf-8")
text_file.write(final_text[0])
```

## Javascript recipe

### Dependency : [ocrad.js or GOCR.js](http://antimatter15.com/ocrad.js/demo.html)

### Code Sample: 

```js
var string = OCRAD(image); /*TODO what is that image object?*/
alert(string);
```



