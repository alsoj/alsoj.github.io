---
title: "[크롤링]Selenium WebDriver 사용법"
categories:
  - POST
tags:
  - crawling
  - webdriver
  - selenium
---

크롤링 프로그램을 제작할 때 가장 많이 사용하는 패키지가 바로 selenium이다. 크롬 브라우저를 이용하기 때문에 실제 웹사이트를 조회하는 것과 동일한 방식으로 진행할 수 있다. 이 포스팅에서는 selenium의 기본적인 사용법과 각종 사용 팁들을 정리해보았다.

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

## 팝창 or 탭으로 전환하기

`browser.window_handles`를 통해 해당 브라우저에서 다루고 있는 창을 조회할 수 있고, `switch_to` 함수를 통해 특정 창으로 이동할 수 있다.

```python
browser.window_handles

# 띄워진 순서대로 리스트가 담긴다.
#['CDwindow-916401BA0B7910D0C3129E6B471B5B19',
# 'CDwindow-FC884D80F1B7125B2E3CAE6319DAB659',
# 'CDwindow-A4FDB8CCE540E3BB888E973C594D71C6']
```

```python
# 마지막으로 띄워진 팝업 창 or 탭으로 이동
browser.switch_to.window(browser.window_handles[-1])

# 최초의 메인 창으로 이동
browser.switch_to.window(browser.window_handles[0])

# 새로운 탭으로 이동
browser.switch_to.new_window('tab')
```

## 최초 tab 외에 모두 닫기
```python
def close_new_tabs(browser):
  tabs = browser.window_handles
  while len(tabs) != 1 :
    browser.switch_to.window(tabs[1])
    browser.close()
    tabs = browser.window_handles
  browser.switch_to.window(tabs[0])
```

## 하위에 특정 Element가 존재하는지 확인

```python
# try / catch 블록을 이용한 방법
from Selenium.common.exceptions import NoSuchElementException

try:
  element = driver.find_element(by=By.TAG_NAME, value='a')
except NoSuchElementException:
  print("No element found")

# find_elements를 이용한 방법
elements = driver.driver.find_elements(by=By.TAG_NAME, value='a')
if not elements:
  print("No element found")
else:
  element = elements[0]
```
