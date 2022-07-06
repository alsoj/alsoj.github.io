---
title: "[크롤링]Selenium WebDriver 사용법"
categories:
  - POST
tags:
  - crawling
  - webdriver
  - selenium
---

## 셀레니움(Selenium) 사용법

필요 라이브러리 import

```python
from selenium import webdriver
```

크롬 브라우저 로드

```python
driver = webdriver.Chrome('chromedriver.exe')
```

해당 PC 또는 서버에 chromedriver.exe 파일이 존재해야 한다.

get 방식 request

```python
driver.get("https://alsoj.github.io/")
```

로드된 화면에서 특정한 컴포넌트를 찾고, 클릭

```python
nextButton = browser.find_element(by=By.XPATH, value='/html/body/div/main/div/div/div[2]/button/span')
nextButton.click()
```

Input 박스에 텍스트 입력

```python
nickName = browser.find_element(by=By.XPATH, value='/html/body/div/main/div/form/div[1]/div/input')
nickName.send_keys("하하하")
```

<br />

### 페이지에서 요소 찾기

```python
from selenium.webdriver.common.by import By

driver.find_element(By.XPATH, '//button[text()="Some text"]')
driver.find_elements(By.XPATH, '//button')
```

- find_element : 해당하는 첫번째 요소를 반환
- find_elements : 해당하는 요소들을 리스트로 반환

```python
# 해당 페이지 내에 a 태그로 연결된 url 추출
sub_pages = driver.find_elements(by=By.TAG_NAME, value='a')

for sub_page in sub_pages:
  print(sub_page.get_attribute('href'))

# https://www.naver.com/test/1/
# https://www.naver.com/test/2/
# https://www.naver.com/test/3/
# https://www.naver.com/test/4/
# https://www.naver.com/test/5/
```

<br />

By 클래스에 사용할 수 있는 속성은 페이지에서 요소를 찾는 데 사용됩니다. 다음은 클래스별에 사용할 수 있는 속성입니다

```python
ID = "id"
NAME = "name"
XPATH = "xpath"
LINK_TEXT = "link text"
PARTIAL_LINK_TEXT = "partial link text"
TAG_NAME = "tag name"
CLASS_NAME = "class name"
CSS_SELECTOR = "css selector"
```

<br />

다음은 속성이 페이지에서 요소를 찾는 데 사용되는 다양한 방법입니다.

```python
find_element(By.ID, "id")
find_element(By.NAME, "name")
find_element(By.XPATH, "xpath")
find_element(By.LINK_TEXT, "link text")
find_element(By.PARTIAL_LINK_TEXT, "partial link text")
find_element(By.TAG_NAME, "tag name")
find_element(By.CLASS_NAME, "class name")
find_element(By.CSS_SELECTOR, "css selector")
```

### iframe으로 전환하기

```python
browser.switch_to.frame('ID 또는 NAME')

# 사용예시 - videoarea라는 id를 가진 iframe으로 브라우저를 전환한다.
browser.switch_to.frame('videoarea')
```

## popup창으로 전환하기

```python
browser.switch_to.window(browser.window_handles[1])
```
