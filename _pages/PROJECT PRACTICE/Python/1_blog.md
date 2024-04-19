---
title: "1. blog"
tags:
    - python
date: "2023-11-06"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

블로그를 만든 기념으로 파이썬을 이용해서 블로그가 운영되는 형식에 맞춰서 파이썬 사용법을 연습해봄

# **main.py**
---
{% highlight python %}
from module.Blog import Blog
from module.Post import Post

MAIN_TEXT = '''
-----------------
1. 블로그 글 작성
2. 블로그 글 리스트
3. 종료
-----------------
'''
MAIN1_TEXT = [
"타이틀: ",
"내용: "
]
MAIN2_TEXT = '''
-----------------
1. 블로그 보기
2. 블로그 편집
3. 뒤로 돌아가기
-----------------
'''
MAIN2_DETAIL_TEXT = 'id를 입력해주세요: '
MAIN1_END_TEXT = '''
작성 완료했습니다.
------------------
'''

class Main:
    def __init__(self, blog_data) -> None:
        self.blog_data = blog_data
        pass
    def __call__(self):
        while True:
            try:
                handler = Handler()
                post = Post()
                blog = Blog()
                (menu_num, input_data) = handler.get_input(text = MAIN_TEXT)
                input_data = int(input_data)
                if menu_num == "main":
                    if input_data == 1:
                        (menu_num, input_datas) = handler.get_input(text = MAIN1_TEXT)
                        self.blog_data = post.create(data= self.blog_data, title= input_datas[0], content= input_datas[1])
                        print(MAIN1_END_TEXT)
                    elif input_data == 2:
                        (menu_num, input_data) = handler.get_input(text = MAIN2_TEXT)
                        blog.view_all(data= self.blog_data, state="title")
                        input_data = int(input_data)
                        
                    elif input_data == 3:
                        break
                    else:
                        print("다시 선택해주세요.")
                if menu_num == "main2":
                    if input_data == 1:
                        (menu_num, input_data) = handler.get_input(text = MAIN2_DETAIL_TEXT)
                    elif input_data == 2:
                        pass
                    elif input_data == 3:
                        pass
                    else:
                        print("다시 선택해주세요.")
                if menu_num == "main2_1":
                    blog.view_all(data= self.blog_data, state="full", id=int(input_data))
                    (menu_num, input_data) = handler.get_input(text = "")
            except ValueError:
                print("숫자를 입력해주세요.")

class BlogDataSetting:
    def __init__(self) -> None:
        self.max_id = self.__get_default_id()
        self.posts = self.__get_posts()
        pass

    def __get_default_id(self):
        return 0

    def __get_posts(self):
        return []

class Handler:
    def get_input(self, text):
        if (text == MAIN_TEXT):
            print(text)
            return ("main", input())
        elif (text == MAIN1_TEXT):
            input_list = []
            for txt in text:
                input_list.append(input(txt))
            return ("main1", input_list)
        elif (text == MAIN2_TEXT):
            print(text)
            return ("main2", input())
        elif (text == MAIN2_DETAIL_TEXT):
            return ("main2_1", input(text))
        else:
            return ("main", input("돌아가기"))

if __name__ == "__main__":
    blog_data = BlogDataSetting()
    main = Main(blog_data)
    main()
{% endhighlight %}

# **module/Blog.py**
---
{% highlight python %}
class Blog():
    """
    전체 리스트 보기(id 기준), 태그 리스트 보기
    """
    def __init__(self) -> None:
        super().__init__()
        pass

    def view_all(self, data, state="title", id=False):
        posts = data.posts
        print("-------------")
        for post in posts:
            if id:
                if id == post['id']:
                    print(f"id: {post['id']}")
                    print(f"타이틀: {post['title']}")
                    if state == "full":
                        post['view_count'] += 1
                        print(f"내용: {post['content']}")
                        print(f"view: {post['view_count']}")
                        print(f"like: {post['like']}")
                    print(f"\t")
            else:
                print(f"id: {post['id']}")
                print(f"타이틀: {post['title']}")
                if state == "full":
                    print(f"내용: {post['content']}")
                    print(f"view: {post['view_count']}")
                    print(f"like: {post['like']}")
                print(f"\t")
        print("-------------")
{% endhighlight %}

# **module/Post.py**
---
{% highlight python %}
class Post():

    def __init__(self) -> None:
        super().__init__()
        pass

    def create(self, data, title, content):
        data.max_id += 1
        data.posts.append({
            "id": data.max_id,
            "title": title,
            "content": content,
            "view_count": 0,
            "like": 0
        })
        return data 

    def edit():
        pass
{% endhighlight %}
