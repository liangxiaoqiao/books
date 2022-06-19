### Python安装OCR

```
安装的anaconda 使用环境：Python3.6
```

##### Windows安装

1. 安装pillow

   ```
   anaconda安装： conda install pillow
   或者
   python安装：pip install pillow
   ```



2. 安装pytesseract

   ```
   anaconda安装： 打开anaconda prompt， 输入 pip install pytesseract
   或者
   python安装： pip isntall pytesseract
   ```

3. 安装tesseract-ocr [下载链接](https://github.com/tesseract-ocr/tesseract/wiki)

4. 下载汉语训练文件（默认识别英文）  [下载链接](https://github.com/tesseract-ocr/tesseract/wiki/Data-Files#data-files-for-version-400-november-29-2016)

```python
import pytesseract
from PIL import Image

# windows下识别中文
img = Image.open(path)
gray = img.convert('L')
filename = os.path.split(path)[1]
# 临时文件
gray.save('C:\\Test\\python\\1-gray' + filename)
# 转化
bw = gray.point(lambda x: 0 if x < 1 else 255, '1')
# 临时文件
bw.save('C:\\Test\\python\\1-threshold' + filename)
# ocr安装目录
tessdata_dir_config = '--tessdata-dir "C:\\Program Files (x86)\\Tesseract-OCR\\tessdata"'
pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files (x86)\Tesseract-OCR\tesseract'
# lang="chi_sim"选择识别中文，默认识别英文
word = pytesseract.image_to_string(img, config=tessdata_dir_config, lang="chi_sim")
```

