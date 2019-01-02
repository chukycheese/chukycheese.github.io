---
title: GitHub 블로그에 Jupyter notebook 올리는 방법
date: 2019-01-02
category:
    - translation
    - GitHub
    - Jupyter Notebook
source: https://blomadam.github.io/tutorials/2017/04/09/ipynb-to-Jekyll-Post-tools.html
---

여러분의 GitHub 블로그에 Jupyter notebook 을 바꿔서 올릴 수 있도록 도와줄 글이다. 
직접 바꾸는 방법은 1회성 글들을 위해서 추가했고, 변환 과정과 파일 이동, 그리고 여러분의 블로그에 올리는 것까지
한 번에 할 수 있는 자동화 bash 를 만드는 자세한 방법도 추가했다.

## 직접 하는 방법

`notebook.ipynb` 라는 이름의 파일을 변한하기 위해 아래의 명령어를 터미널에서 실행하면 Jupyter notebook 형식을
여러분의 Jekyll 블로그에 맞는 markdown 형식으로 바꿔줄 것이다. 여러분이 변환하고자 하는 파일이 포함되어 있는
폴더에서 아래의 명렁어를 실행해야한다는 것을 명심하자.

```
jupyter nbconvert --to markdown notebook.ipynb
```

이 명령어는 Jupyter 가 제공하는 번역 기능을 실행해서 다음과 같은 두 아이템을 만들 것이다:
* `notebook.md` 는 여러분의 새로운 블로그 글을 위한 markdown 을 포함하고 있는 파일이다
* `notebook_files` 는 여러분의 새로운 블로그 글을 위한 모든 이미지를 포함하고 있는 폴더이다.

`notebook.md` 파일을 여러분의 블로그의 `_posts` 폴더 아래로 옮기고 일자(date) 와 제목(title) 을 포함하도록 이름을 바꿔준다.
뿐만 아니라 첫 부분에 적절한 front matter(Jekyll 용어의 YAML 부분)를 포함하는지 확인할 필요가 있다.
그리고 여러분의 블로그의 이미지 폴더를 향하도록 이미지 링크를 바꿔주어야 한다.
이 작업의 대부분을 자동화한 방법을 보려면 아래를 읽도록 하자.

`notebook_files` 폴더를 여러분 블로그의 "images" 폴더로 옮기자(이 작업 또한 자동화를 했다).

이 파일들을 git repository 에 추가하고 commit 한다. 그러고난 뒤 repo 를 서버에 push 하도록 하자.
축하한다, 조금만 기다리면 여러분의 업데이트가 사이트에 반영될 것이다!

## 자동화된 방법

**아래의 도구를 설치하고 난 뒤에 Jupyter notebook 을 여러분의 블로그에 새 글로 올리는 방법은 다음과 같다**

* `new_post notebook.ipynb`(notebook.ipynb 는 여러분이 변환해서 올리고자하는 파일의 이름이다)를 실행한다
* 새로운 글이 블로그 여러분의 블로그 페이지에 올라왔는지 쉴틈없이 새로고침을 연타한다

**notebook 파일의 어떤 아이템들은 최종 블로그 글에 올라오지 않을 수도 있다:**

* LaTeX 식은 제대로 변환되지 않을 수도 있다
* 직접 삽입한 이미지는 나중에 고쳐야한다
* YAML metadata(title, date, category 등과 같은) 은 첫 번째 셀의 타입이 **Raw NBConvert** 일 때만 제대로 작동한다

**new_post 함수가 하는 것들:**

* markdown 으로 변환하기
* 삽입된 도표 이미지 주소 수정하기
* git repository 에 새로운 글 추가하고 commit 하기
* repository 에 바뀐 것 서버에 push 하기

현재는 이 함수에 대한 무결성 검사가 존재하지 않는다. 그러니 실행하기 전에 이 함수가 작동하는 방법에 대해 이해하고, 사용에 주의를 기울이기 바란다.
여기에 [예제](https://blomadam.github.io/tutorials/2017/04/08/Example_post.html)를 만들어 두었다.

## 자동화 툴 설정하기

이 과정은 내가 수업 첫 주에 만든 도구와 매우 유사하다.
쉽게 말해서 우리는 새로운 터미널 창을 열 때마다 CLI 가 매번 불러오는 `.bash_profile` 스크립트에 바로가기를 추가하는 것과 같다.
나는 그 바로가기를 `new_post` 라고 이름 지었지만 여러분은 notebook 을 여러분의 블로그에 올릴 때 사용하고 싶은 명령어로 바꿔도 좋다.
설치는 아주 쉽다. 그냥 아래의 코드를 여러분의 `~/.bash_profile` 파일에 복붙하면 된다(CLI 에서 이 파일을 Sublime Text를 통해 바로 열고 싶다면 명령창에 `subl ~/.bash_profile`을 입력하라).
여러분의 컴퓨터의 설정에 따라 첫 부분의 몇 줄을 바꿔야함을 명심하길 바란다.

```
function new_post {
    #change these 3 lines to match your specific setup
    GH_USER="github_username"
    PC_USER="local_username"
    POST_PATH="/Users/${PC_USER}/dsi-nyc-5/${GH_USER}.github.io/_posts"
    IMG_PATH="/Users/${PC_USER}/dsi-nyc-5/${GH_USER}.github.io/images"

    FILE_NAME="$1"
    CURR_DIR=`pwd`
    FILE_BASE=`basename $FILE_NAME .ipynb`

    POST_NAME="${FILE_BASE}.md"
    IMG_NAME="${FILE_BASE}_files"

    POST_DATE_NAME=`date "+%Y-%m-%d-"`${POST_NAME}

    # convert the notebook
    jupyter nbconvert --to markdown $FILE_NAME

    # change image paths
    sed -i .bak "s:\[png\](:[png](/images/:" $POST_NAME

    # move everything to blog area
    mv  $POST_NAME "${POST_PATH}/${POST_DATE_NAME}"
    mv  $IMG_NAME "${IMG_PATH}/"

    # add files to git repo to be included in next commit
    cd $POST_PATH
    git add $POST_DATE_NAME
    cd $IMG_PATH
    git add $IMG_NAME

    # make git submission
    cd ..
    git commit -m "\"New blog entry ${FILE_BASE}\""

    # push changes to server
    git push

    cd $CURR_DIR
}
```

## 도표 보기 좋게 설정하기

여러분의 시스템이 블로그 글을 번역하도록 설정하면, Jekyll 이 Pandas DataFrame 표를 적절히 보여주기 위해 여러분의 html 템플릿에
약간의 CSS 코드를 추가해야한다. 
아래는 `<head>`의 마지막 부분에 CSS 코드를 포함하고 있는 나의 `<username>.github.io/_layouts/default.html` 에서 관련이 있는 부분이다.
여러분은 본인의 기본 파일을 아래와 비슷하게 바꿔야 한다.

```
  <head>
    <!-- Begin section for dataframe table formatting -->
    <style type="text/css">
    table.dataframe {
        width: 100%;
        height: 240px;
        display: block;
        overflow: auto;
        font-family: Arial, sans-serif;
        font-size: 13px;
        line-height: 20px;
        text-align: center;
    }
    table.dataframe th {
      font-weight: bold;
      padding: 4px;
    }
    table.dataframe td {
      padding: 4px;
    }
    table.dataframe tr:hover {
      background: #b8d1f3; 
    }
    </style>
    <!-- End section for dataframe table formatting -->
  </head>
```

추가된 CSS 코드가 하는 대략적인 기능은 아래와 같다. 본인의 입맛에 맞도록 수정해도 무방하다.

* 표의 넓이는 전체, 높이는 240px 로 설정
* 더 큰 표는 스크롤을 통해 볼 수 있도록 설정
* 서체는 Arial, 크기는 13, 그리고 모든 셀에서 가운데 정렬로 설정
* 표의 헤더(행, 열 둘 다)는 굵게 표시
* 각 셀에 4px 만큼 여백 설정
* 커서가 위치하는 행을 밝은 파란색(`#b8d1f3`) 으로 

**출처:**

<https://blomadam.github.io/tutorials/2017/04/09/ipynb-to-Jekyll-Post-tools.html>
