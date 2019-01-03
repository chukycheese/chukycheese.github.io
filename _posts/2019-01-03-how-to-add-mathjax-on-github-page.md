---
layout: post
title: GitHub Pages Jekyll Blog 에 MathJax 추가하기 (Adding MathJax to a GitHub Pages Jekyll Blog)
date: 2019-01-03 00:10:00
category:
    - translation
    - GitHub Pages
    - Jekyll
    - MathJax
tags: 
    - Jekyll
    - MathJax
    - GitHub Pages
mathjax: true
---

이 글은 MathJax 를 GitHub Pages Jekyll blog 에 추가하는 방법을 다룬다. *이탤릭체로 된 부분은 본문에는 없고 제가 따라하면서 고치거나 추가한 부분이니 참고하세요.*
 
## 절차

### 1. 아래의 코드를 **_includes/mathjax.html** 에 추가한다.
*따로 추가를 하지 않았다면 **_includes** 폴더에 **mathjax.html** 이라는 파일이 없을 겁니다.
그런 경우에는 파일을 추가해야 합니다.*

파일 주소 및 파일명: **_includes/mathjax.html**

```html
{% raw %}{% if page.mathjax %}{% endraw %} # post 의 front matter 에 mathjax 항목의 값에 따라 MathJax 를 불러올 지를 결정하는 부분
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ], # 어떤 기호로 수식을 적을지 정하는 부분
      processEscapes: true
    }
  });
</script>
<script
  type="text/javascript"
  charset="utf-8"
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
>
</script>
<script
  type="text/javascript"
  charset="utf-8"
  src="https://vincenttam.github.io/javascripts/MathJaxLocal.js"
>
</script>
{% raw %}{% endif %}{% endraw %}
```

### 2. 아래의 코드를 **_layouts/post.html** 또는 MathJax 를 사용하고자 하는 레이아웃에 추가한다.

*제 경우에는 _layouts/post**s**.html 이라는 이름의 파일이 있었어서 제가 참고한 글과 동일하게 post.html 로 바꾸었습니다.* 

```html
{% raw %}{% include mathjax.html %}{% endraw %}
```

*`post.html` 또는 `posts.html` 을 열어보면 아래와 같은 코드가 있을텐데 적절해보이는 위치에 위의 코드를 추가해주시면 됩니다.
저는 {{contents}} 의 바로 아랫줄에 추가했습니다.*

```html
{{ content }}

{% raw %}{% include mathjax.html %}{% endraw %} # mathjax.html 을 불러오는 부분

# 이하 생략
```

### 3. MathJax 를 사용하고자 하는 글의 YAML front matter 부분에 다음 코드 추가하기

```
mathjax: true
```

YAML front matter 부분에 아래와 같이 `mathjax` 를 추가하면 된다. [Disqus](https://disqus.com/) 또한 [동일한 방법](https://sgeos.github.io/jekyll/disqus/2016/02/14/adding-disqus-to-a-jekyll-blog.html)으로 추가했다.

```
---
layout: post
mathjax: true  # mathjax 의 사용 여부를 나타내는 부분
comments: true # Disqus 를 이용한 댓글 설정을 나타내는 부분
title:  "Adding MathJax to a GitHub Pages Jekyll Blog"
date:   2016-08-21 23:41:54 +0000
categories: github jekyll
---
```

모든 단계에서 문제가 없었다면 MathJax 를 inline 그리고 display 모드에서 사용할 수 있을 것이다.
[MathJax dynamic preview](https://cdn.mathjax.org/mathjax/latest/test/sample-dynamic-2.html) 를 이용하면 복잡한 공식도
보다 쉽게 만들 수 있을 것이다.

```
In N-dimensional simplex noise, the squared kernel summation radius $r^2$ is $\frac 1 2$
for all values of N. This is because the edge length of the N-simplex $s = \sqrt {\frac {N} {N + 1}}$
divides out of the N-simplex height $h = s \sqrt {\frac {N + 1} {2N}}$.
The kerel summation radius $r$ is equal to the N-simplex height $h$.

$$ r = h = \sqrt{\frac {1} {2}} = \sqrt{\frac {N} {N+1}} \sqrt{\frac {N+1} {2N}} $$
```

In N-dimensional simplex noise, the squared kernel summation radius $r^2$ is $\frac 1 2$
for all values of N. This is because the edge length of the N-simplex $s = \sqrt {\frac {N} {N + 1}}$
divides out of the N-simplex height $h = s \sqrt {\frac {N + 1} {2N}}$.
The kerel summation radius $r$ is equal to the N-simplex height $h$.

$$ r = h = \sqrt{\frac {1} {2}} = \sqrt{\frac {N} {N+1}} \sqrt{\frac {N+1} {2N}} $$

*한 가지 명심해야할 점은 GitHub 에서는 공식이 제대로 안 보일 수도 있다는 점입니다.
하지만 작성한 블로그 글로 가면 MathJax 를 통해 공식이 제대로 표시되는 것을 확인할 수 있습니다.*

**원문:**
[Adding MathJax to a GitHub Pages Jekyll Blog](http://sgeos.github.io/github/jekyll/2016/08/21/adding_mathjax_to_a_jekyll_github_pages_blog.html)
