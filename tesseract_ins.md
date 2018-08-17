###### tesseract download
https://github.com/UB-Mannheim/tesseract/wiki

###### pip install
`pip install pytesseract`

###### 경로 지정 (code 내에 삽입)
```
tesseract_path = 'C:/Program Files (x86)/Tesseract-OCR'
pytesseract.pytesseract.tesseract_cmd = tesseract_path + '/tesseract'
```