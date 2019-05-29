# Today I Learned
> 오늘 내가 배운 것을 정리하자  

## `190527` - [`walkWithPython`](../walkWithPython)
## 1교시
Pycharm, Python, Git Bash 설치  
Pycharm에 Git bash 연동

## 2교시
`.gitignore`
프로젝트 업로드
마크다운 작성
`Typora`

## 3교시
끝말잇기

> 점심시간 

## 4교시
`stirng_interpolation.py` : 문자열
1. 옛날 방식
2. `pyformat`
3. `f-string`

`lotto.py` : `random` 이용한 로또뽑기

`write_txt.py` : 파일 쓰기
1. `open()`
2. `with open()`  
2-1. `writelines`

`Escape Sequence`

## 5교시
`read_txt.py` : 파일 읽기
1. `open files()`
2. `with open()`

`reverse_content.py` : 파일 수정
1. `read file`
2. `reverse`
3. `write files`

`for` : `range` 종료시 매개변수 값

## 6교시
`naver_rank.py` : `bs4` 사용한 크롤링 활용
> `requests`, `bs4`, `datetime`, `encoding`, `enumerate`

## 7교시
`write_csv.py` : `csv` 파일 쓰기
1. `f-string`
2. `join()`
3. `csv`

`read_csv.py` : `csv` 파일 읽기
1. `string` `split`
2. `csv`

## 8교시
`melon_rank.py` : melon에서 실시간 차트 가져오자


## `190528` - [`Web`](../Web)

# 1교시 

`Static Web`

`Dynamic Web`

`URL` 구조 

`URL`과 `URI` 차이

`HTML` -> `HTTP`

# 2교시
`HTML Tag`

[`Semantic Tag`](https://www.w3schools.com/html/html5_semantic_elements.asp)
  - `header`
  - `nav`
  - `aside`
  - `section`
  - `article`
  - `footer`

`non-Semantic Tag`
  - `div`

`heading`

`paragraph`
  - `br`
  - `hr`

`font-style`
  - `b`, `strong`
  - `i`, `em`
  - `del`

`list`
  - `ol` + `li`
  - `ul` + `li`

# 3교시
`a`: 상대경로, 절대경로, `id`, `mailto`, `_blank`
`media`
  - `img`
  - `iframe`

`form`
  - `input` : text, password, submit

추가적인 학습 : [MDN HTML Tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element), [poiemaweb](https://poiemaweb.com/), [velopert](https://velopert.com)

`fake_naver.html` : `form`태그와 `query`를 활용해 fake 네이버 검색창 만들기

# 4교시
`css` 도입  

`css` 선언
  - external 
  - internal 
  - inline    

`css` 선택자
  - `tag`
  - `*`
  - `id`
  - `class`
  - `parent > child`

## 5교시
`css` 우선순위
  1. `!important`
  2. `css inline` 선언
  3. `id`
  4. `class`
  5. `tag`
  6. `parent`에 의해 상속
  
`font`
  - `font-size`
  - `font-style`
  - `font-weight`
  - `font-family`

`google font`
  

## 6교시
`Bootstrap`
  - `CDN`

실제로 써보자
  - `m-3`, `p-4`, `mx-3`, `py-4`
  - `text-center`, `text-primary`
  - `container`
  - `grid` = `row`, `column` + `emmet`
  - `border`
  - `btn`, `btn-primary`
  - `form`

## 7교시
[`Free Bootstrap Theme`](https://startbootstrap.com/)

수강자가 만드는 [`Github Pages`](https://pages.github.com/)   

## 8교시
[`Github Pages`](https://pages.github.com/) 실습 

## `190529` - `WebService`
# WebService
## 1교시
`Web Service` 도입  

`WWW` : World Wide Web  

현실세계의 `Service` -> `Web Service`  

`Client`, `Server`

`Get`, `Post`

`Python` + [`Flask`](http://flask.pocoo.org/)  

```bash
$ pip install Flask
$ FLASK_APP=hello.py flask run
```
```bash
$ FLASK_DEBUG=1 FLASK_APP=hello.py flask run
```

`hello.py`
```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

@app.route("/mulcam")
def mulcam():
    return "This is Multicampus"

# Flask를 쉽게 켜자
if __name__ == '__main__':
  app.run(debug=True)
```
명령어가 많이 줄어듬
```bash
$ python hello.py
```

## 2교시
`__name__`  

<del>`import`, `def`</del>  

`decorator`: `bye.py`

`variable routing`, `path variable`
  - `string`
  - `int`

사람 수 만큼 점심메뉴 뽑기
  - 메뉴 수 보다 많은 사람 수?
  - 중복 가능하도록?

`hello.py`
```python
from flask import Flask
from random import sample
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

@app.route("/mulcam")
def mulcam():
    return "This is Multicampus"

@app.route("/greeting/<string:name>")
def greeting(name):
  return f'반갑습니다. {name}!'

@app.route("/cube/<int:num>")
def cube(num):
  result = num ** 3 
  return f'{num}의 세제곱은 {result}'

# 사람 수 만큼 점심 메뉴 추천
@app.route("/lunch/<int:people>")
def lunch(people):
  menu = ["짜장면", "짬뽕", "라면", "브리또", "사과", "찜닭"]
  return f'{sample(menu, people)}'

# Flask를 쉽게 켜자
if __name__ == '__main__':
  app.run(debug=True)
```

## 3교시
랜더링
  - `html tag` 
    ```python
    @app.route("/html")
    def html():
      multiple_string = """
        <h1>This is HTML</h1>
        <p>This is p tag</p>
      """
      return multiple_string
    ```
  - `.html` + `/templates` + `render_template`
    ```python
    @app.route("/html_file")
    def html_file():
      return render_template('html_file.html')
    ```
  - `Template Variable` - `jinja`
    ```python
    @app.route("/hi/<string:name>")
    def hi(name):
      # Template Variable
      return render_template('hi.html', your_name=name)
    ```

`html`파일에서 파이썬 문법 사용하기
```html
{% for menu in menu_list %}
  <li>{{ menu }}</li>
{% endfor %}
```

## 4교시
`send` # `form` => `receive`

`request.arg.get`

## 5교시
[신이 나를 만들 때](https://kr.vonvon.me/quiz/329) 같이  
URL로 정보 넘기기 `실습`

## 6교시
`JSON`

`dict`
  1. dict 생성
  2. dict item 추가
  3. dict value 가져오기
  4. dict 반복문 활용
    4-1. 기본
    4-2. key 반복
    4-3. value 반복
    4-4. key, value 반복

[`lotto`](https://dhlottery.co.kr/)
`lotto API`, `requests`, `JSON`, `append`

## 7교시
`list comprehension`

`회차 입력`

```python
@app.route('/lotto_check')
def lotto_check():
  return render_template('lotto_check.html')

@app.route('/lotto_result')
def lotto_result():
  lotto_round = request.args.get('lotto_round')
  url = f"https://dhlottery.co.kr/common.do?method=getLottoNumber&drwNo={lotto_round}"
  response = requests.get(url)
  # response.text # => string
  lotto = response.json() # => dict
  winner = []
  
  # list comprehension
  # a = [n*2 for n in range(1, 7)] # => [2, 4, 6, 8, 10, 12]
  a = [lotto[f'drwtNo{n}'] for n in range(1, 7)]
  bonus = lotto['bnusNo']
  winner = f'{a} + {bonus}'
  return render_template('lotto_result.html', lotto=winner, bonus=bonus)
```

## 8교시
`등수 확인`

`Set` = `{요소1, 요소2, ...}` : 집합
  - `&`(합집합), `|`(교집합)

`in`, `len`



