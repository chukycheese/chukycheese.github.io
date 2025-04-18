---
layout: post
title: 초보자를 위한 RStudio 의 프로젝트 와 작업 디렉토리
date: 2020-01-24 00:30:00
toc: true
toc_sticky: true
category: data-analytics
tag:
    - translation
    - r-studio
mathjax: true
comment: true
---

원문: [RStudio Projects and Working Directories: A Beginner's Guide](https://martinctc.github.io/blog/rstudio-projects-and-working-directories-a-beginner%27s-guide/) by Martin Chan

## 시작하기

이 글은 RStudio 의 Projects 의 사용과 폴더를 구조화하는 방법에 대한 기초적인 소개글입니다. 여러분이 여전히 `setwd()` 를 사용하고 있다면 읽을만한 가치가 있는 글이죠!

비록 R 에서의 작업 디렉토리가 꽤나 기본적이고 잘 다뤄진 주제이긴 하지만, 이를 구조화하는 저만의 방법을 공유하는 게 여전히 가치가 있을 것이라 느꼈습니다. 작업 디렉토리를 구조화하는 이성적이고 유요한 여러가지 방법이 명백하게 있긴 합니다. 이 글에서 다룰 프로젝트 디렉토리의 구조는 제가 매일 사용하고 있는 것이며, 메모리에 데이터셋을 읽고, 작업 디렉토리 안에 저장하는 것과 같이 제가 주로 다루는 데이터 분석 업무에 가장 적절하다고 생각했기 때문입니다.

만약 여러분이 이제 막 R 을 배우기 시작했다면 RStudio 의 프로젝트(Project) 를 사용하고 작업 디렉토리를 구조화하는 것은 '필수 요소' 라는 것이 제 개인적인 조언입니다. RStudio 의 프로젝트를 사용하면 데이터를 읽고 내보는 작업에서의 수많은 초기의 어려움을 없앨 수 있습니다. 작업 디렉토리를 제대로 설정하는 것은 재현가능한 분석에 이바지하는 좋은 습관을 기를 수 있게 도와줍니다. 이는 제가 R 프로그래밍에서 코드와는 관계 없지만 알면 굉장히 유용하다고 생각하는 부분이며, 학습자에게는 틀림없이 GitHub을 사용하는 것보다 우선순위가 높다고 생각합니다.

## RStudio 프로젝트는 무엇이며 왜 사용해야할까요?

몇 년 전 제가 처음 R 을 사용하기 시작했을 때, 작업 디렉토리를 설정하는 교과서와 주된 방법은 `setwd()` 를 사용하는 것이었습니다. 이는 파일의 *절대* 주소를 받아서 이를 R 프로세스에서의 작업 디렉토리로 설정하는 방법입니다. 그러고 나서 `getwd()` 를 이용해서 현재 작업 디렉토리를 찾고, 제대로 설정이 되었는지를 알 수 있습니다.

이 접근법의 문제점은 `setwd()` 함수가 파일의 *절대* 주소에 의존하기 때문에 링크가 깨지기 굉장히 쉽고, 다른 사람들과 분석 결과를 공유하기 굉장히 어렵다는 점입니다. 전체 디렉토리를 다른 드라이브의 하위 폴더로 옮기는 것 같이 간단한 행위로도 링크가 깨져서 여러분의 스크립트는 작동하지 않습니다. [Jenny Bryan 이 지적했듯이](https://www.tidyverse.org/blog/2017/12/workflow-vs-script/) `setwd()` 방법은 원저자가 본인의 컴퓨터에서 직접 스크립트를 실행하는 게 아니라면 다른 모든 사람들은 이를 사용하는 게 거의 불가능하게 만듭니다.

> `setwd()` 명령어가 저자를 제외한 다른 사람의 컴퓨터에서 제대로 작동할 확률은 0% 입니다. 심지어 1-2년 뒤에는 저자의 컴퓨터에서도 제대로 작동하지 않을 수 있습니다. 그 프로젝트는 독립적이지도, 휴대 가능하지도 않습니다. 이 그림을 다시 만들거나 확장하기 위해서는 운이 좋은 수신자가 본인의 컴퓨터에 맞게 하나 이상의 주소를 직접 수정해야 할 것입니다. 만약 과제 때문에 이틀 동안 이 짓을 73번 정도 하고 나면 그 사람의 컴퓨터를 불살라버리는 환상에 빠지기 시작할 겁니다.

(원문을 보려면 위의 링크를 누르세요)

처음에는 저도 `setwd()` 의 전통을 전부 버리는 급진적으로 보이는 행위에 회의적이었습니다. 하지만 프로젝트 워크플로우를 사용하고 나서 파일의 절대 주소를 사용하는 것을 더이상 생각해보지 않았습니다. 그래서 저는 이에 대해서는 Jenny Bryan 에 전적으로 동의합니다.

## RStudio 프로젝트를 이용해서 쉽게 파일 주소 참조하기

RStudio 프로젝트는 파일 주소를 *상대적*으로 만들어서 '깨지기 쉬운' 파일 주소 문제를 해결했습니다. RStudio 프로젝트 파일은 .Rproj 확장자를 가진 루트 디렉토리 (root directory) 에 존재하는 파일입니다. 여러분의 RStudio 세션이 프로젝트 파일(.Rproj) 을 통해 실행되고 있는 동안은 현재 작업 디렉토리는 .Rproj 파일이 저장되어 있는 루트 디렉토리를 바라보고 있습니다.

예를 들어봅시다. 제 작업 디렉토리가 *SurveyAnalysis1* 이라는 이름의 폴더라고 가정해보죠. 전체 절대경로 주소를 *C:/Users/Martin/Documents/Analysis/SurveyAnalysis1/Data/Data1.xlsx* 와 같이 나열하는 대신 동일한 엑셀 파일을 *Data/Data1.xlsx* 와 같이 프로젝트를 사용하는 디렉토리 수준에서부터 참조할 수 있습니다. 만약 어느날 제가 *SurveyAnalysis1* 폴더를 다른 위치로 옮기거나 다른 컴퓨터에서 연다고 해도, 제가 .Rproj 파일을 이용해서 세션을 시작하기만 한다면 제 R 스크립트는 여전히 잘 작동할 것입니다.

이 .Rproj 파일은 RStudio 에서 **File > New Project...** 을 통해 만들 수 있으며, 특정 폴더 또는 디렉토리와 연계됩니다. 이제 그 디렉토리(전체 폴더와 하위 폴더, 그리고 모든 컨텐츠) 는 독립적이고 이동가능하다고 생각하시면 됩니다. 다시 말하면, 이 디렉토리 *밖에서* 파일을 읽거나 쓰면 안된다는 것입니다. 그 분석 또는 프로젝트와 관련이 있는 모든 것은 해당 디렉토리 안에서 일어나야만 합니다. 여러분의 분석이 웹 스크래핑이나 API 를 부르는 것처럼 인터넷 소스에서 불러오는 게 아니라면요. 존재하는 프로젝트를 열 때는 .Rproj 파일을 먼저 연 다음 R 스크립트(.R 확장자 파일) 를 열어야만 합니다. .Rproj 파일을 여는 것을 여러분이 이 세션에서 실행하는 모든 것이 해당 디렉토리 아래의 적합한 파일을 찾을 수 있도록 보장하는 RStudio 세션을 '시작하는' 단계라고 생각하시면 됩니다. RStudio 에는 .RData 와 .Rhistory 파일에 대한 보다 많은 정보를 담고 있는 [RStudio 프로젝트에 대한 보다 자세한 문서](https://support.rstudio.com/hc/en-us/articles/200526207-Using-Projects) 가 있으며, 읽어볼 가치가 충분히 있습니다. *R for Data Science* 책의 [8장 (Workflow: projects)](https://r4ds.had.co.nz/workflow-projects.html) 에는 RStudio 프로젝트에 대한 '처음 시작하는' 가이드가 있습니다.

## 작업 디렉토리 구조화하기

RStudio 프로젝트를 사용하는 것 외에도, 여러분과 협업하는 사람들, 또는 일부 분석을 재현하려는 미래의 본인이 쉽게 그 분석을 둘러볼 수 있도록 여러분의 디렉토리를 구조화하는 것 또한 좋은 습관입니다. 저는 아래의 기본적인 '시작' 디렉토리 설정을 추천합니다.

![a-basic-r-project-set-up](https://raw.githubusercontent.com/martinctc/blog/master/images/RPROJECT_2000dpi.png)

### 기본 구조

여러분의 작업 디렉토리에 다음과 같은 것들이 있어야 합니다.

* Data - 저는 제가 분석이나 시각화를 위해 읽어 오는 모든 파일을 이 하위폴더에 저장합니다. 이 데이터는 SPSS(*.sav) 파일, Excel / CSV 파일일 수도 있으며, .FST 또는 .RDS 일수도 있습니다. 핵심 아이디어는 이것들이 **원시 데이터 파일** 이며, 재현성을 위해서 R 이 이 파일들을 덮어쓰거나 편집해서는 안된다는 것입니다. 그 이유는 원시 데이터가 분석 과정에서 계속 바뀐다면 재현가능한 분석은 불가능하기 때문입니다 (스프레드시트에서 분석할 때를 생각해보세요). 여러분이 원시 데이터 파일을 바꿔야만 한다면 새로운 버전을 만들어서 파일 이름을 그 수정을 적절히 반영하는 이름으로 만들어야할 것입니다.
* Script - 이 폴더에 저는 R 스크립트와 RMarkdown 파일들을 저장합니다 (*.R, .Rmd* 확장자를 가진 파일들)
  * Analysis - 모든 제 주요 분석 R 스크립트는 여기에 저장합니다. 개인적인 생각이지만 만약 여러분이 서로 다른 작업을 하는 여러 개의 스크립트를 여기에 저장해놨다면 대부분의 경우 괜찮을 것입니다. 하나의 데이터셋을 가지고 20가지 이상의 다른 분석을 해야하는 경우가 생길 수도 있어서 저는 각각의 분석마다 새로운 프로젝트를 만들지는 않습니다. 한 분석을 나눌지 말지를 결정하기 위한 제 (비교적 간단한) 어림짐작법은 이 작업을 전혀 모르는 사람이 와서 디렉토리를 살펴보면서 어떤 작업을 수행하는지 파악할 수 있는지를 상상하는 것입니다. 추가적인 팁을 드리자면, 사려깊고 이치에 맞는 파일명을 붙이는 것이 엄청 도움이 된다는 것입니다!
  * Functions - 별도의 하위 폴더에 자신이 만든 함수를 저장하는 것은 여러분의 선택입니다. 저는 개인적으로 이 방법이 편리했는데, 제가 한 특정 프로젝트에서 작성한 함수를 재사용하고 싶은 경우가 생기면 그 프로젝트에서 작성한 함수들을 빠르게 살펴볼 수 있기 때문입니다. 함수를 따로 저장하면 이 함수들을 주된 분석 스크립트에 두는 것이 아니라 '주 분석 스크립트' 에 함수들을 불러오기 위해 `source()` 를 사용하는 워크플로우가 같이 따라오게 됩니다.
  * RMarkdonw files - RMarkdonw 파일은 파일 경로에 있어서 .R 파일과 조금은 다르게 작동되기 때문에 특수한 경우라고 볼 수 있습니다. 이 파일은 기본 작업 디렉토리가 파일이 저장된 경로이기 때문에 파일 자체가 작은 프로젝트처럼 행동한다고 보시면 됩니다. RMarkdown 파일을 이 셋업에서 저장하기ㅣ 위해서는 `{here}` 패키지와 그 워크플로우를 사용하기를 권장합니다. 그게 아니라면 `knitr::opts_knit$set(rood.dir = "../")` 를 사용해서 작업 디렉토리가 RMarkdown 파일이 저장된 하위 폴더가 아니라 루트 디렉토리라는 것을 알려주는 이 코드를 셋업 구문에서 실행시켜주셔도 됩니다(`{here}` 를 쓰는 것만큼 이상적이지는 않습니다). [제 다른 글](https://martinctc.github.io/blog/first-world-problems-very-long-rmarkdown-documents/)에서 다수의 RMarkdown 파일들을 하나의 긴 RMarkdown 문서로 합치는 디렉토리 구조에 대해서도 다룬 적이 있습니다.
* Output - 플랏, HTML, 그리고 내보낸 데이터 등을 포함해서 모든 결과물을 여기에 저장하세요.
  * Output 폴더를 만들면 다른 사람들로 하여금 코드의 **결과물** 이 어떤 파일들인지 파악하기 쉽게 해주며, 그 분석을 만들어내기 위해 사용한 소스 파일들과 구분해줍니다.
  * 여러분이 만든 하위 폴더들은 합리적이기만 한다면 크게 문제되지는 않습니다. 내보낸 파일의 종류보다는 분석과 결이 맞도록 하위 폴더를 구성하셔도 됩니다.
  * 제가 만든 패키지 [surveytoolbox](https://github.com/martinctc) (GitHub 에서 받으실 수 있습니다) 에 있는 `timed_fn()` 은 파일명에 타임스탬프를 만들어주는데, 반복적인 분석을 하는 경우에 결과물을 잃지 않도록 하기 위해서 종종 사용합니다.

이 디렉토리 구조 '템플릿' 은 프로젝트 워크 플로우가 생소하신 분들에게 프로젝트를 정리하는 좋은 시작점이 될 것입니다. 비록 일관성을 가지는 것이 좋다고는 하지만 프로젝트마다 필요한 부분이 다를 수 있습니다. 그러므로 여러분은 항상 어떤 것이 필요한지, 작업 디렉토리 구조를 설정할 때 어떤 일이 벌어질지를 항상 생각하시고 적절하게 변형하시기 바랍니다.

### 더 읽을거리

크리스 폰 체펄베이 (Chris Von Csefalvay) 도 R 프로젝트를 구조화할 때 고려할 사항에 대해 자세한 가이드를 제공해주는 [R 프로젝트 구조에 대한 좋은 글](https://chrisvoncsefalvay.com/2018/08/09/structuring-r-projects/) 을 썼습니다. 그는 각 프로젝트마다 (루트 디렉토리에) README 파일을 둘 것을 제언하였고, 더욱 복잡한 프로젝트일수록 특히 중요할 것이라고 했습니다.

늘 그렇듯이 여러분의 피드백, 댓글, 그리고 질문은 항상 환영합니다! 이 글이 마음에 드셨다면 https://martinctc.github.io/blog/ 에서 다른 글도 확인해주시기 바랍니다.

---

전에 다니던 회사에서 다른 사람들이 짜놓은 R 코드를 받아서 쓸 일이 있었는데 이 글에서 나온 폴더 구조는 어느 정도 고려는 되었지만 프로젝트 기능을 사용하지 않아서 다른 폴더나 컴퓨터로 옮기면 전체 프로세스가 와장창 깨지는 식이었다. 그래서 개선 작업을 하면서 주로 신경 썼던 부분이 그것이었고, 마침 이 글에서도 나왔던 Jenny Bryan 의 글을 보고 프로젝트 (Project) 에 대해서 알게된 후 적용했었고 아직까지도 프로젝트는 아주 잘 쓰고 있다 (전 회사의 코드가 아직까지 잘 돌아가는지는 잘 모르겠지만).

한동안 파이썬을 Jupyter Notebook, Google Colab 에서 사용하면서 셀 단위 실행에 익숙해졌고, R 로 넘어와서도 RMarkdown 에서 주로 작업을 했다. 보기는 편한데 전체를 실행하는 경우라면 데이터를 추출해오는 작업을 또 실행해야 해서 시간이 오래 걸리는 단점이 있었다. 그런데 이 글에서 말한 것처럼 분석 자체는 .R 파일에서 하고 RMarkdown 은 결과물을 가지고 분석 리포트를 만들기 위한 툴로만 사용하면 굉장히 시간을 단축시킬 수 있을 것 같다.

뿐만 아니라 지금은 분석 단위마다 별도의 프로젝트를 만들어서 진행하는데 20개 정도가 넘어가다보니 많이 헷갈리는 게 사실이다. 특히 재사용하는 DB 연결 관련 스크립트를 매번 가져와야하는데 여기서의 폴더 구조를 적용하면 그런 작업이 많이 줄어들지 않을까 싶다.
