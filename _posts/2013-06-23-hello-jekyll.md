---
layout: post
title:  "JekyllとGitHub Pagesでブログを書き始めた"
categories: diary
tags: jekyll github gh-pages
---

Static Site Generator、流行ってますね。
僕も常々、「たかが個人が書くブログ程度にRDBMSはやりすぎ」と思っていたので、
このアプローチはとても気に入っています。

いままであまり使う機会に恵まれなかったんですが、しびれを切らして無理やり[Jekyll](http://jekyllrb.com)でブログを始めてみることにしました。
とりとめのない話は、しばらくこっちで更新してみようと思います。

以下、このサイトを作るまでのメモです。

なお、ホスティングには[GitHub Pages](http://pages.github.com/)を利用しています。
ユーザページ（ユーザ名.github.io）じゃなく、プロジェクトページ（ユーザ名.github.io/プロジェクト名）でやりました。

## GitHub上でRepositoryの準備

今回、tnantoka.github.comではなく、tobioka.github.comでやりたかったので、
[Organizations](https://github.com/settings/organizations)から、新たにOrganization（<https://github.com/tobioka>）を作成しました。

そして、Repository（<https://github.com/tobioka/blog>）を作ります。

一応、[README.md](https://github.com/tobioka/blog/blob/master/README.md)をコミットして、masterブランチをデフォルトにしておきました。
（gh-pagesだけにしてもよかったんですが、できるだけ「普通」の使い方をしたかったので）

### Jekyllでサイトを新規作成

{% highlight sh %}
$ git clone git@github.com:tobioka/blog.git
$ cd blog
$ git checkout -b gh-pages
$ git rm README.md # 空っぽじゃないとjekyll newできないので
$ jekyll new .
{% endhighlight %}


### 相対パスで動かせるように

今回、プロジェクトページでやるので「/プロジェクト名」で動作するように設定します。

参考：[ruby - Configuring Jekyll for github PROJECT pages - Stack Overflow](http://stackoverflow.com/questions/10585916/configuring-jekyll-for-github-project-pages)

{% highlight sh %}
$ vim _config.yml
baseurl: /blog

$ vim _layout/default.yml
<link rel="stylesheet" href="{{ "{{ site.baseurl " }}}}/css/syntax.css">
<link rel="stylesheet" href="{{ "{{ site.baseurl " }}}}/css/main.css">

$ vim index.html
<a href="{{ "{{ site.baseurl " }}}}{{ "{{ post.url " }}}}">{{ "{{ post.title " }}}}</a></li>
{% endhighlight %}


### 公開

{% highlight sh %}
$ git add .
$ git commit -am "Publish site"
$ git push origin gh-pages
{% endhighlight %}

あとは適当にサイト名とか記事とか編集しましたが、そこは省略します。

これで、今ご覧のブログが運営できる状態になりました。

