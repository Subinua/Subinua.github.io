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
### Assets
- Jekyll에서는 CSS, JS, 이미지, 다른 asset들을 직접적으로 사용할 수 있다. 
- 그것들을 Assets site 폴더에 넣으면 빌드된 사이트로 복사된다.
- _includes/navigation.html 에 사용된 인라인 스타일은 좋은 방법이 아니다.
  - 스타일을 클래스로 지정하는 방법으로 바꿔 본다.
  - 표준 CSS를 사용하는 것도 가능하지만 Sass를 이용한다.
  - Sass는 Jekyll에 CSS를 바로 올릴 수 있는 환상적인 확장이다.
  - assets\css\styles.scss 작성 => _site\assets\css\styles.css로 복사됨
  - _sass\main.css 작성 
  - default.html 에서 사용
    - ```
      <link rel="stylesheet" href="/assets/css/styles.css" />
      ```
### Blogging
Jekyll에선 데이터베이스없이 오로지 text 파일만으로 blogging하는 것이 가능하다.
- 블로그 포스트는 _posts 라는 폴더에 있다.
- 포스트의 파일명은 특별한 포맷을 가지는데 발행일, 제목, 확장자 이다.
- 첫 포스트를 _posts\2021-08-27-Test.md로 제작해 보기
- post layout 제작
- Jekyll에서는 포스트들을 site.posts 로 접근할 수 있다.
- blog.html을 루트 디렉토리에 제작하여 posts 관리
- _data\navigation.yml에 blog 엔트리 추가
### Collections
만약에 블로그의 저자들 각각을 위한 간단한 소개말과 그들의 포스트들을 볼 수 있는 저자들만의 페이지를 만들고 싶다면 어떻게 해야할까?
컬렉션은 콘텐츠를 날짜별로 그룹화하지 않아도 된다는 점을 제외하면 포스트와 유사하다.
- 컬렉션을 만들기 위해서 Jekyll에게 _config.yml 을 통해 알려주어야 한다.
  - 먼저 _config.yml 파일을 만든다.
  - _config.yml 파일을 수정한 후에 변경사항을 반영하기 위해서는 Jekyll 서버를 재시작해야 한다.
- 컬렉션에 있는 아이템들(문서들)은 루트 디렉토리에 있는 _*collection_name* 디렉토리에 만들면 된다.
  - 저자를 기준으로 컬렉션을 만들기 위해서는 _authors 로 만들면 적절할 것이다.
- 저자에 관한 문서들을 만들어보자.
  - _authors\jill.md 등
- 모든 저자들을 리스트해서 보여주는 페이지를 추가해보자.
  - Jekyll은 컬렉션을 site.authors 변수를 통해 이용할 수 있도록 해준다.
  - 루트 디렉토리에 staff.html 을 만든다.
- _data/navigation.yml 에 추가
- 기본적으로 컬렉션은 문서의 페이지를 출력하지 않는다.
  - 만약 각 저자 마다 페이지를 만들어주고 싶다면 _config.yml 파일을 살짝 수정해야 한다.
  - output: true 추가
- staff.html에 링크 추가
- post와 같이 authors를 위한 layout을 만든다.
  - _layouts/author.html 제작
  - 이렇게 만든 author 레이아웃을 author들, jill.md 와 ted.md 의 front matter에 표시해주어야 하지만 이것은 계속 반복되는 작업이다. 따라서 다른 방법을 사용해볼 수 있다.
    - 우리가 원하는 것은 자동적으로 포스트들은 post 레이아웃을 사용하고, author들은 author 레이아웃을 사용하는 것이다.
    - _config.yml에 front matter default를 적용
      - 기본값을 적용할 scope 를 정하고, 기본값으로 들어갈 front matter를 넣으면 된다.
    - 이제 모든 page 들과 post 들의 front matter에서 layout 에 관한 부분을 다 지워도 된다.
  - List author's posts
    - 각 author가 쓴 포스트들을 그들의 페이지에 필터링해서 보여주기.
    - author의 short_name 과 post의 author 가 매치될 필요가 있다.
  - Link to authors page
    - 각각의 포스트는 author의 페이지로 갈 수 있는 링크를 가져야할 것이다.
    - 위에서 한 것과 비슷한 필터링 기술을 사용해서 할 수 있다.
      - layouts/post.html 수정