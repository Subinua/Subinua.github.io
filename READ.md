# 나의 블로그
## 준비
- ### Ruby 설치
  - [루비 설치](https://subinua.github.io/mydoc_install_jekyll_on_windows.html)
  - [루비 Download](https://rubyinstaller.org/downloads/)
  - 설치 마지막에 "ridk install" 선택
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
[참고 Site](https://til.younho9.dev/docs/frontend/jekyll/jekyll-github-page%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%B4-%EA%B0%9C%EC%9D%B8%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0)
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
- ```Liquid
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
### 배포
- Gemfile을 루트 디렉토리에 만든다.
  - source 'https://rubygems.org'
  - gem 'jekyll'
- bundle install 실행 => Gemfile.lock 생성
- bundle exec jekyll serve
- 플러그인
  - ```
    group :jekyll_plugins do
      gem 'jekyll-sitemap'
      gem 'jekyll-feed'
      gem 'jekyll-seo-tag'
    end
    ```
  - _config.yml 에도 추가
    - ```
      plugins:
        - jekyll-feed
        - jekyll-sitemap
        - jekyll-seo-tag
      ```
- bundle update 실행
  -jekyll-feed 와 jekyll-seo-tag 를 사용하기 위해서는 _layouts/default.html 에 따로 태그를 추가해 주어야 한다. 
  - bundle exec jekyll serve 
- Environments
  - 때때로 사이트를 만들었을 때는 결과를 표시하고 싶지만, 개발 중일 때는 표시하지 않고 싶을 수 있다. disqus 또는 Google Analytics 등이 그러한데, 이것을 위해서는 environments를 사용할 수 있다.
  - JEKYLL_ENV 라는 환경 변수를 사용한다.
    - ```JEKYLL_ENV=production bundle exec jekyll build```
    - ```
      {% if jekyll.environment == "production" %}
      <script src="my-analytics-script.js"></script>
      {% endif %}
      ```
- 서버에 배포
  - JEKYLL_ENV=production bundle exec jekyll build
  - 이후 _site 디렉토리의 콘텐츠를 복사해 서버로 제공한다.
    - [Github Actions](https://jekyllrb.com/docs/continuous-integration/github-actions/)

## Jekyll Theme 사용
- [원본 Theme](https://github.com/mmistakes/minimal-mistakes)
- Clone: __minimal-mistakes
- [GitHub Page Source](https://Subinua.github.io)
  - main branch 사용
- [Target GitHub Page](https://Subinua.github.io/gh-pages)
### 설치
- git submodule 사용
- git submodule add https://github.com/mmistakes/minimal-mistakes __minimal-mistakes
- 작업 시, Submodule 포함 clone 방법
  - git clone --recurse-submodules https://github.com/Subinua/Subinua.github.io
    - git submodule init
    - git submodule update
  - Submodule Update
    - git submodule update --remote
      - __minimal-mistakes 폴더에서
      - git fetch
      - git update
### 수정
- __minimal-mistakes 파일 복사 
  - 제외 파일들:
    - .github, .git, .gitignore, .gitattributes, /docs, /test
    - .editorconfig, CHANGELOG.md, minimal-mistakes-jekyll.gemspec
    - README.md, screenshot-layouts.png, screenshot.png
- Gemfile 내용 변경
- Add jekyll-include-cache to the plugins array of your _config.yml (이미 수정되어 있음)
- bundle
- _config.yml 수정
  - remote_theme: "mmistakes/minimal-mistakes@4.24.0"
  - repository: "Subinua/Subinua.github.io"
- bundle update
- bundle add webrick
- bundle exec jekyll serve
