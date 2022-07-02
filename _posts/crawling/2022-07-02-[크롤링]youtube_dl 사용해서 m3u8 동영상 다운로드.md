---
title: "[크롤링]youtube_dl 사용해서 m3u8 동영상 다운로드."
categories:
  - POST
tags:
  - crawling
  - webdriver
  - selenium
---

## youtube_dl 설치

![image](/assets/images/youtube_dl%20install.png)

```python
# pip 설치
pip install youtube_dl

# conda 설치
conda install -c conda-forge youtube-dl
```

## m3u8 주소 확인

![image](/assets/images/youtube_dl%20m3u8.png)

## 동영상 다운로드

```python
# 위에서 조회한 m3u8 요청 URL
m3u8_url = 'https://k20.ciuxe2.xyz/k20/1996m1/index.m3u8'

# request header에 referer 추가
youtube_dl.utils.std_headers['Referer'] = "https://kfani.me/"

# youtube_dl 옵션 추가
ydl_opts = {
              # 동영상이 다운로드 될 경로 지정
              'outtmpl': '{}.mp4'.format(MOVIE_SAVE_PATH + movie_title)
            }

# 다운로드 진행
with youtube_dl.YoutubeDL(ydl_opts) as ydl:
  ydl.download([m3u8_url])
```
