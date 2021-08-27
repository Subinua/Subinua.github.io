# 나의 블로그
## 준비
- ### Ruby 설치
  - 설치 마지막 ridk install
  - ruby -v
  - get -v
- ### Jekyll 설치
  - gem install jekyll bundler
    - jekyll -v
## 새 Jekyll site 생성
  - ./myFirstJekyllBlog
  - jekyll new myFirstJekyllBlog
  - cd myFirstJekyllBlog
  - bundle add webrick (Compile Error 제거)
  - bundle exec jekyll serve
  - http://localhost:4000 주소로 접속
## Pure Jekyll site 생성
  - ./__pureJekyllBlog
  - mkdir __pureJekyllBlog
  - cd __pureJekyllBlog
  - bundle init
  - gem "jekyll" 추가 (Gemfile 수정)
  - bundle add webrick (Compile Error 제거)
  - bundle (Gemfile.lock 생성)
  - index.html 생성 
  - jekyll build (static _site 생성)
  - jekyll serve (local web server)
  - http://localhost:4000 주소로 접속
## Jekyll site 수정
### Liquid
Jekyll이 사용하는 템플릿 언어
- Object
  - ```{{ page.title }}```
- Tag
  - ```Liquid
    {% if page.show_sidebar %}
      <div class="sidebar">sidebar content</div>
    {% endif %}
    ```
- Filter
  - ```{{ "hi" | capitalize }}```
