# Convert Taaghche Books to PDF

This script is for creating a PDF out of [Taaghche's](https://taaghche.com/) books.

You need to have Python and Selenium installed on your system.

[Python installation](https://www.python.org/downloads/)

[Selenium installation](https://selenium-python.readthedocs.io/installation.html)

You also need to download chromedriver from [here](https://chromedriver.chromium.org/downloads).

Then you should open a Terminal and run Python. Inside the Python shell:

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
import time

driver = webdriver.Chrome('/Users/navid/chromedriver') #Path to the chromedriver
driver.set_window_size(800, 1200) #You can justify the window size to your preference
totalPages = 400 # Change to your book pages

driver.get("https://taaghche.com/")
```

After running these codes, a Chrome browser will be pop up and you will see Taaghche website. You now need to login to your account and open the book you want to convert to PDF. When you opened the book you should run this code inside Python shell:
```python
for pageNumber in range(totalPages):
   driver.save_screenshot(f'/Users/navid/Desktop/test/{pageNumber}.png') # Path to the folder where the screenshots should be saved
   driver.find_element(By.ID, '___nextPageMobile').click()
   time.sleep(2)
```

Now you have all the pages screenshots, you can use different tools to convert the images to a PDF. You can also use this script to convert them, just make sure you have PIL package [installed](https://pypi.org/project/Pillow/).
```python
from PIL import Image

images = []
for pageNumber in range(totalPages):
    image = Image.open(f'/Users/navid/Desktop/test/{pageNumber}.png') #Path to the screenshots folder
    if image.mode == 'RGBA':
        image = image.convert('RGB')
    images.append(image)

pdfPath = "/Users/navid/Desktop/test/test.pdf" #PDF path and name

images[0].save(
    pdfPath, "PDF", resolution=100.0, save_all=True, append_images=images[1:]
)
```
You can find the PDF in the path you defined. Current PDF you have is not searchable and you can't highlight it. You can use this [PDF OCR](https://tools.pdf24.org/en/ocr-pdf) tool to do so.