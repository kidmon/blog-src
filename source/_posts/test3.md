---
toc: true
widgets:
  - type: toc
    position: right
  - type: category
    position: right
sidebar:
  right:
    sticky: true
title: test3
date: 2019-10-10 01:11:33
categories: test
tags: test
---

Hexo를 이용해서 블로그를 만들고 관리 하다보니 문제점을 하나 발견했다.
바로 백업에 관한 문제인데 Hexo 블로그는 Github에 repository를 통해 구성되어 있으니
다른 곳에서 작업할때 그것을 clone해서 수정하면 된다고 생각했다.

그러나 다른 곳에서 clone을 해보고는 문제가 있음을 알수 있었다.
라이브되는 repository에 올라가는건 public 폴더의 내용이라 실제로 작업한 것은 올라가지 않는다는 것을 말이다.

그래서 해결책으로 별도의 repository 하나를 생성하여 별도로 백업을 하기로 했는데
이 방법도 문제가 있었다. Hexo의 테마들을 각자의 git을 가지고 있어서
git 안에 git이 있어 재대로 관리가 되어지지 않았다.

그래서 검색을 통해 알아보다가 git의 서브모듈(submodule)을 이용해서 백업 하기로 했다.

Hexo를 이용해서 블로그를 만들고 관리 하다보니 문제점을 하나 발견했다.
바로 백업에 관한 문제인데 Hexo 블로그는 Github에 repository를 통해 구성되어 있으니
다른 곳에서 작업할때 그것을 clone해서 수정하면 된다고 생각했다.

그러나 다른 곳에서 clone을 해보고는 문제가 있음을 알수 있었다.
라이브되는 repository에 올라가는건 public 폴더의 내용이라 실제로 작업한 것은 올라가지 않는다는 것을 말이다.

그래서 해결책으로 별도의 repository 하나를 생성하여 별도로 백업을 하기로 했는데
이 방법도 문제가 있었다. Hexo의 테마들을 각자의 git을 가지고 있어서
git 안에 git이 있어 재대로 관리가 되어지지 않았다.

그래서 검색을 통해 알아보다가 git의 서브모듈(submodule)을 이용해서 백업 하기로 했다.

<!-- more -->

Hexo를 이용해서 블로그를 만들고 관리 하다보니 문제점을 하나 발견했다.
바로 백업에 관한 문제인데 Hexo 블로그는 Github에 repository를 통해 구성되어 있으니
다른 곳에서 작업할때 그것을 clone해서 수정하면 된다고 생각했다.

그러나 다른 곳에서 clone을 해보고는 문제가 있음을 알수 있었다.
라이브되는 repository에 올라가는건 public 폴더의 내용이라 실제로 작업한 것은 올라가지 않는다는 것을 말이다.

그래서 해결책으로 별도의 repository 하나를 생성하여 별도로 백업을 하기로 했는데
이 방법도 문제가 있었다. Hexo의 테마들을 각자의 git을 가지고 있어서
git 안에 git이 있어 재대로 관리가 되어지지 않았다.

그래서 검색을 통해 알아보다가 git의 서브모듈(submodule)을 이용해서 백업 하기로 했다.

Hexo를 이용해서 블로그를 만들고 관리 하다보니 문제점을 하나 발견했다.
바로 백업에 관한 문제인데 Hexo 블로그는 Github에 repository를 통해 구성되어 있으니
다른 곳에서 작업할때 그것을 clone해서 수정하면 된다고 생각했다.

그러나 다른 곳에서 clone을 해보고는 문제가 있음을 알수 있었다.
라이브되는 repository에 올라가는건 public 폴더의 내용이라 실제로 작업한 것은 올라가지 않는다는 것을 말이다.

그래서 해결책으로 별도의 repository 하나를 생성하여 별도로 백업을 하기로 했는데
이 방법도 문제가 있었다. Hexo의 테마들을 각자의 git을 가지고 있어서
git 안에 git이 있어 재대로 관리가 되어지지 않았다.

그래서 검색을 통해 알아보다가 git의 서브모듈(submodule)을 이용해서 백업 하기로 했다.