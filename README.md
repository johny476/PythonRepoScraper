# PythonRepoScraper
一个基于Python的GitHub代码库爬虫
import requests
from bs4 import BeautifulSoup

def scrape_github_repositories():
    url = "https://github.com/explore"  # GitHub探索页面的URL

    # 发送HTTP GET请求
    response = requests.get(url)

    # 使用BeautifulSoup解析HTML
    soup = BeautifulSoup(response.text, "html.parser")

    # 查找代码库信息
    repositories = soup.find_all("article", {"class": "Box-row"})

    # 遍历每个代码库并提取信息
    for repo in repositories:
        name = repo.h1.text.strip()  # 代码库名称
        description = repo.find("p", {"class": "col-9"}).text.strip()  # 代码库描述
        topics = [topic.text.strip() for topic in repo.find_all("a", {"class": "topic-tag"})]  # 代码库主题
        stars = repo.find("a", {"class": "muted-link"}).text.strip()  # 星标数量

        print("名称:", name)
        print("描述:", description)
        print("主题:", ", ".join(topics))
        print("星标数量:", stars)
        print()

scrape_github_repositories()
