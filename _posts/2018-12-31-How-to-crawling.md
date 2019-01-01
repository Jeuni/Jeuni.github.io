---
layout: post
title: [Python/BeautifulSoup4] 파이썬을 이용한 크롤링
---

### 크롤링이란?
크롤링(crawling)은 스크레이핑(scraping)은 웹 페이지를 그대로 가져와서 거기서 데이터를 추출해 내는 행위이다. 크롤링하는 소프트웨어는 크롤러(crawler)라고 부른다.


최근에는 비전공자들이 사용하기 쉽도록 라이브러리들이 발달했습니다. 대표적인 파이썬의 라이브러리에는 <code>BeautifulSoup</code>이 있습니다.

BeautifulSoup라이브러리를 이용하여서 크롤링 실습을 해보겠습니다.

먼저 웹페이지에서 크롤링을 하기 위해서는 <code>urllib</code>라이브러리를 이용합니다. <code>urllib</code>라이브러리는 파이썬에서 웹과 관련된 데이터를 쉽게 이용하게 도와주는 라이브러리입니다. 그 중에서 <code>request</code>모듈은 웹을 열어서 데이터를 읽어옵니다.

>import urllib.request
form bs4 import BeautifulSoup

url = "데이터를 가져 올 사이트 주소"
req = urllib.request.Request(url)
sourcecode = urllib.request.urlopen(url).read()
soup = BeautifulSoup(sourcecode, "html.parser")


웹에서 데이터를 가져올 준비가 되었습니다. 여기서 원하는 정보를 가져오기 위해서는 <code>find()</code> 또는 <code>find_all()</code>함수들을 이용합니다.

* <code>find(tag, attributes, recursive, string, \*\*kwargs)</code>
* <code>find_all(tag, attributes, revursive, string, limit, \*\*kwargs)</code>

함수를 사용해서 네이버의 인기검색어를 가져와 봅시다. 가져오고 싶은 소스의 TAG와 class를 찾아서 가져옵니다.

현재 네이버의 인기검색어 소스는 

![default](https://user-images.githubusercontent.com/39057061/50572517-c557c600-0e05-11e9-9b2a-8f25ef388566.PNG)
 

이렇게 되어있습니다. TAG는 span, class는 ah_k인 것을 확인할 수 있습니다. 인기 검색어 10위까지를 list에 넣어 출력해 보겠습니다. 

```
import urllib.request
from bs4 import BeautifulSoup

def main():
    
    # URL 데이터를 가져올 사이트 url 입력
    url = "http://www.naver.com"
        
    # URL 주소에 있는 HTML 코드를 soup에 저장합니다.
    soup = BeautifulSoup(urllib.request.urlopen(url).read(), "html.parser")
    
    
    list = []

    for naver_text in soup.find_all("span", class_="ah_k"):
        list.append(naver_text.get_text())

    print(list[:10])


if __name__ == "__main__":
    main()

```

<b>실행 결과</b>

![default](https://user-images.githubusercontent.com/39057061/50572516-c557c600-0e05-11e9-9277-23005065c8e1.PNG)
