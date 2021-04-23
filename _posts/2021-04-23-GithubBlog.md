---
title: "GithubBlog-1"
categories: githubBlog
tags: blog git github githubBlog
published: true

---

## Github Blog


#### GitHub Post

어디서부터 정리해야할지 모르겠다.<br>
하지만 일단 https://ansohxxn.github.io/blog/jekyll-directory-structure/#_layouts 이 블로그 덕에 살았다.<br>
여기서 구조들을 파악했고 하나씩 해보면서 문법을 익혔다. <br>
가장 먼저! jekyll ruby 언어로 구성된 블로그이고, Liquid 문법, yml (yaml?) 을 사용했다고 한다. <br>
이게 맞는지 모르겠다.. 더 자세히 공부하기 .. <br>

1. 먼저 includes 는 layout (html) 이나 post (md) 등에서 가져올 수 있는 아이템 같은 거라고 생각하면 될 것 같다. 

2. layout은 화면 구성의 전체적인 틀을 잡아준다. layout을 사용하고 content를 통해 그 위에 렌더링(?)한다.

	content 를 빼지말자!

3. splash layout <br>
	splash는 갤러리 식으로 티저 이미지를 먼저 보여준다. 이것을 활용해서 포스트로 들어갈 수 있게 만들면 될 것 같다. <br>
	코드 안에 이런게 있었다. <br>
	<article class="splash" itemscope itemtype="https://schema.org/CreativeWork">

	schema.org... 구글링 해보니까 데이터 구조화를 쉽게 하는 거라는데 잘 모르겠다...나는..  <br>

4. scss
전반적인 style을 담당해주는 것 같다. 쓰는게 css랑 비슷하다. <br>

<br>

++ 궁금 : <br>
1. post default는 config.yml로 만들던데 그거 어떻게 연결을 시켰는지 궁금하다.<br>
2. schema.org... 이해 안간다 뭔쓸모인지 ? <br>
3. liquid 문법은 html, md 둘 다 되던데 왜 그런걸까?<br>
4. liquid 문법에서 page.[name], site.[name], categories.[name] 은 무슨 기준으로 참조하는 것인가? <br>
	yml을 참조해서 가져오는 경우도 있는거 같은데 어떻게 연결한 것인가? <br>

5. {{% %}} 이거 왜 안됨..? 

