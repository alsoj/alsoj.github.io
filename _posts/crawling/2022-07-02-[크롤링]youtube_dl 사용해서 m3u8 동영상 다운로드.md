---
title: "[크롤링]youtube_dl 사용해서 m3u8 동영상 다운로드."
categories:
  - POST
tags:
  - crawling
  - webdriver
  - selenium
---

## youtube_dl이란

> youtube-dl은 유튜브와 다른 사이트의 동영상을 다운로드하는 오픈 소스 소프트웨어이다. GitHub에서 현재도 활발히 개발되고 있으며, 성능 면에서는 타 소프트웨어의 추종을 불허한다.  
> 출처 : https://namu.wiki/w/youtube-dl

Python으로 동영상을 다운로드 하는 프로그램을 개발 중, m3u8 형식의 동영상을 다운받는 방법을 찾다가 알게 되었다. m3u8 형식 뿐만 아니라 다양한 형식의 동영상을 다운받을 수 있다. 패키지의 명칭과 달리 youtube뿐만 아니라 다양한 소스의 영상도 다운로드가 가능하다.

## youtube_dl 설치

PyCharm에서 다운로드 방법
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

## m3u8 다운로드시 주의사항!

위 소스 코드를 그대로 실행하면 FFmpeg가 없다고 오류가 발생한다. 아래 FFmpeg 공식 다운로드 사이트에 접속해서 OS에 맞는 파일을 다운로드 한다.

공식 다운로드 사이트 : https://ffmpeg.org/download.html

다운로드 된 파일들 중 bin 디렉터리에 있는 ffmpeg.exe, ffplay.exe, ffprobe.exe 세 파일을 실행하려는 .py 파일이 있는 경로에 복사한다. 이후 코드를 실행하면 정상적으로 다운로드가 진행된다.
