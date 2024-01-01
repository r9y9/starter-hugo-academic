---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Hugo Academic を使ってウェブサイトをアップデートしました"
subtitle: ""
summary: "New: https://github.com/r9y9/website, old: https://github.com/r9y9/blog"
authors: ["admin"]
tags:
- Hugo
categories: []
date: 2022-01-18T20:59:28+09:00
lastmod: 2022-01-18T20:59:28+09:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

## Summary

- 新: {{< icon name="github" pack="fab" >}} https://github.com/r9y9/website
  - [トップページ]({{< relref "/" >}})
  - [ブログ一覧]({{< relref "/post/" >}})
  - [デモページ一覧]({{< relref "/project/" >}})
- 旧: {{< icon name="github" pack="fab" >}} https://github.com/r9y9/blog + {{< icon name="github" pack="fab" >}} https://github.com/r9y9/demos-src

これまで、ブログとデモページ[^1]をそれぞれ個別に [Hugo](https://gohugo.io/) で管理していましたが、それらを統合して一つの Hugo site として管理するように変更しました。
内部的に色々変わっていますが、URL はほぼ変わらないようにしています。

## はじめに

2年振りくらいにブログを書いています。大したことを書くわけではないのですが、ウェブサイト（ブログ含む）を大幅にアップデートしたので、その記録を残しておきます。

[^1]: 音声合成の論文を書くときに、読者や査読者が音声サンプルを聴取できるようにデモページを作ることがあります。例えば[こちら]({{< relref "/project/vuvd-pwg" >}})です。

## Why

なぜ大幅にアップデートをしたのか、理由は以下のとおりです。

- 経歴をまとめたプロフィールページなどコンテンツを追加したかった。ただし、これまでは、ブログとデモページをそれらに特化した個別の Hugo site として管理しており、それ以外の情報を追加することが容易ではなかった。プロフィール用に別の Hugo site を作ることも検討したが、管理のし易さの観点から一つの Hugo site にまとめたかった。
- Hugo の theme を修正してレイアウトを調整するのが大変だったので、いい感じレスポンシブにしてくれる、スマホで見てもレイアウトが崩れない Hugo theme を使いたくなった。
  - これまでは、minimal な theme をベースに自分で修正して使っていたが、限界がきた。

後者のレイアウトの問題は、theme を変えれば済む話とも言えますが、前者の問題を解決するためには、theme 変更に加えて複数のsiteを統合する必要がありました。

## アップデートに関してやったこと

### 基本方針

- Static site generator として Hugo を使う。速い。
- Hugo theme には https://github.com/wowchemy/starter-hugo-academic を使う。デザインがシンプルで好み、かつカスタマイズが柔軟にできそうだったので。

### 具体的な手順

- [starter-hugo-academic](https://github.com/wowchemy/starter-hugo-academic) をベースに、全体のレイアウトを作る。僕の場合、Home (トップページ) に `Profile`, `Posts`, `Projects`, `Talks` の4つのコンテンツを配置しました。このうち、`Profile` には、CV[^2]のリンクを貼るようにしました。
   - `Publications` コンテンツを作ることも考えましたが、Google Scholarで良くない？と思って作っていません。
- [ブログ](https://github.com/r9y9/blog) のコンテンツを `Posts` に移行する。一覧は[こちら]({{< relref "/post/" >}})
  - https://wowchemy.com/docs/content/front-matter/ にも書かれている通り、Hugo academic ならではの front matter がありますが、基本的には markdown + 必要なstatic filesをコピーするだけで移行はできました。
  - Hugo academic に `summary` を表示する機能があったので、すべてのブログ記事に `summary` を設定しました。
  - [Tableのレイアウトが崩れる問題](https://github.com/wowchemy/wowchemy-hugo-themes/issues/1404)があったので、微妙にcssを修正しました。
- [デモページ](https://github.com/r9y9/demos-src) のコンテンツを `Projects` に移行する。一覧は[こちら]({{< relref "/project/" >}})
  - blogを移行するのとまったく同じように移行できました
  - 論文に記載したデモページのURLが404にならないように、URLが変わらないようにする、あるいは リダイレクトを設定しました。Hugoだと、[`aliases`](https://gohugo.io/content-management/urls/#aliases) というパラメータを front matter に書くことでリダイレクトを実現できます。
  - これまでの取り組みを整理するいい機会だと思って、共著論文のデモページもコンテンツに追加しました。
- `Talks` のコンテンツをおまけで新しく追加しました。[LINE DEV DAYでの過去の発表]({{< relref "/event/linedevday2020pwg" >}})とか

[^2]: CVの提出を求められることがたまにあるので、これまでの実績を整理するいい機会かなと思って作りました https://github.com/r9y9/cv

## 雑感

### 良かったこと

- ウェブサイトはいい感じになった。プロフィールの追加ができたことはもちろん、モバイル端末で見てもレイアウトが崩れなくなったのは地味に嬉しい
- ブログとデモサイトを一つの Hugo site として管理することで、相互のコンテンツを行き来しやすくなった。具体的には、記事の終わりに、`Related` というセクションに関連するブログ記事やデモページのリンクが表示されるようになった。また、ページのヘッダーから、相互のコンテンツを行き来することもできる。
- 管理するリポジトリの数が4から2に減った。
  - 旧: {{< icon name="github" pack="fab" >}}[blog](https://github.com/r9y9/blog), {{< icon name="github" pack="fab" >}}[r9y9.github.io](https://github.com/r9y9/r9y9.github.io), {{< icon name="github" pack="fab" >}}[demos-src](https://github.com/r9y9/demos-src), {{< icon name="github" pack="fab" >}}[demos](https://github.com/r9y9/demos)
  - 新: {{< icon name="github" pack="fab" >}}[website](https://github.com/r9y9/website), {{< icon name="github" pack="fab" >}}[r9y9.github.io](https://github.com/r9y9/r9y9.github.io)


### 悪かったこと

- https://github.com/wowchemy/starter-hugo-academic はカスタマイズの自由度は高い一方で、適切に設定するのが難しかった。ドキュメントは豊富だが量が多く、全部読んで使いこなすのは大変に感じた。
- 大変だった・・・もうしばらくウェブサイトを大きく更新したくないなと思いました。

おわりです。ただの備忘録ですが、ここまで読んで頂きありがとうございました。
