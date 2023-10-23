---
weight: 1
bookFlatSection: true
title: "下載YT影片"
---

# 使用pytube下載YT影片 


- 下載pytube套件
- 執行terminal
- 在終端機貼上網址
- 會自動下載到桌面


## 程式碼如下：

```tpl
#conda install -c conda-forge pytube 如果一直讀不到可能需要直接在conda裡pip
import os
from pytube import YouTube

def download_video(url, output_path):
    try:
        yt = YouTube(url)
        video = yt.streams.get_highest_resolution()
        video.download(output_path)
        print("下載完成！")
    except Exception as e:
        print("發生錯誤：", str(e))

# 輸入要下載的YouTube影片的URL
video_url = input("請輸入YouTube影片的URL_")

# 桌面路徑
desktop_path = os.path.expanduser("~/Desktop")

download_video(video_url, desktop_path)

```