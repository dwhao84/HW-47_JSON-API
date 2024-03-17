from bs4 import BeautifulSoup
import json

# 假设HTML内容已经被读取到变量`html_content`中
# 例如：with open("你的HTML文件路径.html", "r") as file: html_content = file.read()

soup = BeautifulSoup(html_content, 'html.parser')

videos_data = {"videos": []}

for video in soup.find_all("li", class_="collection-item"):
    title = video.find("h4", class_="video-title").get_text(strip=True) if video.find("h4", class_="video-title") else None
    url_suffix = video.find("a", class_="video-image-link")["href"] if video.find("a", class_="video-image-link") else None
    duration = video.find("span", class_="video-duration").get_text(strip=True) if video.find("span", class_="video-duration") else None
    description = video.find("p", class_="description").get_text(strip=True) if video.find("p", class_="description") else None
    image_url = video.find("img", class_="video-image")["src"] if video.find("img", class_="video-image") else None
    tags = [tag.get_text(strip=True) for tag in video.find_all("span", class_="smaller")] if video.find_all("span", class_="smaller") else []

    video_info = {
        "title": title,
        "url": f"https://developer.apple.com{url_suffix}" if url_suffix else None,
        "duration": duration,
        "description": description,
        "image_url": image_url,
        "tags": tags
    }

    videos_data["videos"].append(video_info)

# 将Python字典转换为JSON字符串并打印出来
json_data = json.dumps(videos_data, indent=4, ensure_ascii=False)
print(json_data)

# 要将这些数据保存到文件，你可以使用：
# with open("videos_data.json", "w", encoding="utf-8") as json_file:
#     json.dump(videos_data, json_file, indent=4, ensure_ascii=False)
