---
title: Github blog Chirpy 테마 적용 오류
author: arat5724
date: 2023-08-23 00:34:00 +0800
categories: [Other, Github blog]
tags: [Jeklly, Chirpy, Github blog]
---

방치해두던 Github blog를 새로운 테마와 함께 시작하려던 와중 오류를 만났다.

![image](https://github.com/Arat5724/arat5724.github.io/assets/79699284/fadf92df-ce06-41bc-a0dc-66e5dffdb361)

`-- layout: home # Index page -—`

시키는 대로 했다고 생각했는데...

찾아보니 Github Actions에서 build가 실패했다.

![image](https://github.com/Arat5724/arat5724.github.io/assets/79699284/25204d05-1ff7-461b-a469-550dd4e50659)
![image](https://github.com/Arat5724/arat5724.github.io/assets/79699284/10581a02-dbda-4ff5-8078-35ec5ccc965f)
```
_site/404.html
*  internal script /assets/js/dist/page.min.js does not exist (line 1)
```

`/assets/js/dist`에 js 파일이 없다는데, 이 파일들은 원래 npm build 과정에서 생겨야 한다.

`_config.yml`에 `include: [_javascript]`를 추가해서 [해결했다는 글](https://velog.io/@lzlko/github-%EB%B8%94%EB%A1%9C%EA%B7%B8)도 봤는데,

나는 Github Actions에서 npm build를 직접 실행해보기로 했다.

![image](https://github.com/Arat5724/arat5724.github.io/assets/79699284/ad6200f1-d42a-4e4d-86da-e583665fde41)

`.github\workflows\pages-deploy.yml`에
```
      - name: Npm build
        run: npm i && npm run build
```
를 추가하면 된다.

![image](https://github.com/Arat5724/arat5724.github.io/assets/79699284/4f8fcd45-54bb-4e06-ae13-5c5cf6f1109f)
![image](https://github.com/Arat5724/arat5724.github.io/assets/79699284/bfd636ae-aef2-49a7-afdd-b1e2b67016b0)

Npm build에서 성공적으로 build 완료 후에 /assets/js/dist에 js 파일들이 생성되었고, Test site도 오류가 발생하지 않고 완료됐다.

![image](https://github.com/Arat5724/arat5724.github.io/assets/79699284/334a8066-9e72-4e52-b41d-4b183ce8263b)

