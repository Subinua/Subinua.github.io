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
### Front Matter
문서의 상단에 있는 두 개의 --- 사이에 들어가는 YAML 조각
- ```
  ---
  # Front Matter
  my_number: 5
  ---
  {{ page.my_number }}
  ```
### Layouts
  - _layouts\default.html 제작
  - {{ content }} 는 호출된 페이지의 렌더링된 콘텐츠 값을 갖는 특수 변수
  - index.html에 ```layout: default``` 추가
  - about.md에 layout 적용해 보기
### Includes
  - _includes\navigation.html 제작
  - default layout에 적용해 보기
### Data Files
- Jekyll은 _data 디렉토리에 위치한 YAML, JSON, CSV 파일로부터 데이터를 가져오는 것을 지원한다.  
- 데이터 파일은 콘텐츠를 소스코드로부터 분리하여 사이트를 관리하기 쉽게 만들어주는 좋은 방법이다.
- 새로운 콘텐츠를 추가하거나 변경할 때 편리.
- 네비게이션의 콘텐츠를 데이터 파일로 보관하고, 네비게이션에 포함된 것들을 반복문을 이용해 사용해 보기
  - _data\navigation.yml 제작
  - navigation.yml에 있는 각각의 이름과 링크 쌍을 배열로 보관하여 사용
  - {{ site.data.navigation }}
  