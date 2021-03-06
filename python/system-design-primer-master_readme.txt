Contributing
============

Contributions are welcome!

**Please carefully read this page to make the code review process go as smoothly as possible and to maximize the likelihood of your contribution being merged.**

## Bug Reports

For bug reports or requests [submit an issue](https://github.com/donnemartin/system-design-primer/issues).

## Pull Requests

The preferred way to contribute is to fork the
[main repository](https://github.com/donnemartin/system-design-primer) on GitHub.

1. Fork the [main repository](https://github.com/donnemartin/system-design-primer).  Click on the 'Fork' button near the top of the page.  This creates a copy of the code under your account on the GitHub server.

2. Clone this copy to your local disk:

        $ git clone git@github.com:YourLogin/system-design-primer.git
        $ cd system-design-primer

3. Create a branch to hold your changes and start making changes. Don't work in the `master` branch!

        $ git checkout -b my-feature

4. Work on this copy on your computer using Git to do the version control. When you're done editing, run the following to record your changes in Git:

        $ git add modified_files
        $ git commit

5. Push your changes to GitHub with:

        $ git push -u origin my-feature

6. Finally, go to the web page of your fork of the `system-design-primer` repo and click 'Pull Request' to send your changes for review.

### GitHub Pull Requests Docs

If you are not familiar with pull requests, review the [pull request docs](https://help.github.com/articles/using-pull-requests/).

## Translations

We'd like for the guide to be available in many languages. Here is the process for maintaining translations:

* This original version and content of the guide is maintained in English.
* Translations follow the content of the original. Unfortunately, contributors must speak at least some English, so that translations do not diverge.
* Each translation has a maintainer to update the translation as the original evolves and to review others' changes. This doesn't require a lot of time, but review by the maintainer is important to maintain quality.

### Changes to translations

* Changes to content should be made to the English version first, and then translated to each other language.
* Changes that improve translations should be made directly on the file for that language. PRs should only modify one language at a time.
* Submit a PR with changes to the file in that language. Each language has a maintainer, who reviews changes in that language. Then the primary maintainer @donnemartin merges it in.
* Prefix PRs and issues with language codes if they are for that translation only, e.g. "es: Improve grammar", so maintainers can find them easily.

### Adding translations to new languages

Translations to new languages are always welcome, especially if you can maintain the translation!

* Check existing issues to see if a translation is in progress or stalled. If so, offer to help.
* If it is not in progress, file an issue for your language so people know you are working on it and we can arrange. Confirm you are native level in the language and are willing to maintain the translation, so it's not orphaned.
* To get it started, fork the repo, then submit a PR with the single file README-xx.md added, where xx is the language code. Use standard [IETF language tags](https://www.w3.org/International/articles/language-tags/), i.e. the same as is used by Wikipedia, *not* the code for a single country. These are usually just the two-letter lowercase code, for example, `fr` for French and `uk` for Ukrainian (not `ua`, which is for the country). For languages that have variations, use the shortest tag, such as `zh-Hant`.
* Invite friends to review if possible. If desired, feel free to invite friends to help your original translation by letting them fork your repo, then merging their PRs.
* Add links to your translation at the top of every README*.md file. (For consistency, the link should be added in alphabetical order by ISO code, and the anchor text should be in the native language.)
* When done, indicate on the PR that it's ready to be merged into the main repo.
* Once accepted, your PR will be squashed into a single commit into the `master` branch.

### Translation template credits

Thanks to [The Art of Command Line](https://github.com/jlevy/the-art-of-command-line) for the translation template.
I am providing code and resources in this repository to you under an open source
license.  Because this is my personal repository, the license you receive to my
code and resources is from me and not my employer (Facebook).

Copyright 2017 Donne Martin

Creative Commons Attribution 4.0 International License (CC BY 4.0)

http://creativecommons.org/licenses/by/4.0/
*[English](README.md) ∙ [日本語](README-ja.md) ∙ [简体中文](README-zh-Hans.md) ∙ [繁體中文](README-zh-TW.md) | [العَرَبِيَّة‎](https://github.com/donnemartin/system-design-primer/issues/170) ∙ [বাংলা](https://github.com/donnemartin/system-design-primer/issues/220) ∙ [Português do Brasil](https://github.com/donnemartin/system-design-primer/issues/40) ∙ [Deutsch](https://github.com/donnemartin/system-design-primer/issues/186) ∙ [ελληνικά](https://github.com/donnemartin/system-design-primer/issues/130) ∙ [עברית](https://github.com/donnemartin/system-design-primer/issues/272) ∙ [Italiano](https://github.com/donnemartin/system-design-primer/issues/104) ∙ [韓國語](https://github.com/donnemartin/system-design-primer/issues/102) ∙ [فارسی](https://github.com/donnemartin/system-design-primer/issues/110) ∙ [Polski](https://github.com/donnemartin/system-design-primer/issues/68) ∙ [русский язык](https://github.com/donnemartin/system-design-primer/issues/87) ∙ [Español](https://github.com/donnemartin/system-design-primer/issues/136) ∙ [ภาษาไทย](https://github.com/donnemartin/system-design-primer/issues/187) ∙ [Türkçe](https://github.com/donnemartin/system-design-primer/issues/39) ∙ [tiếng Việt](https://github.com/donnemartin/system-design-primer/issues/127) ∙ [Français](https://github.com/donnemartin/system-design-primer/issues/250) | [Add Translation](https://github.com/donnemartin/system-design-primer/issues/28)*

# システム設計入門

<p align="center">
  <img src="http://i.imgur.com/jj3A5N8.png"/>
  <br/>
</p>

## 動機・目的

> 大規模システムのシステム設計を学ぶ
>
> システム設計面接課題に備える

### 大規模システムの設計を学ぶ

スケーラブルなシステムのシステム設計を学ぶことは、より良いエンジニアになることに資するでしょう。

システム設計はとても広範なトピックを含みます。システム設計原理については **インターネット上には膨大な量の文献が散らばっています。**

このリポジトリは大規模システム構築に必要な知識を学ぶことができる **文献リストを体系的にまとめたもの** です。

### オープンソースコミュニティから学ぶ

このプロジェクトは、これからもずっと更新されていくオープンソースプロジェクトの初期段階にすぎません。

[Contributions](#contributing) は大歓迎です！

### システム設計面接課題に備える

コード技術面接に加えて、システム設計に関する知識は、多くのテック企業における **技術採用面接プロセス** で **必要不可欠な要素** です。

**システム設計面接での頻出質問に備え**、自分の解答と*模範解答*:ディスカッション、コードそして図表などを*比較*して学びましょう。

面接準備に役立つその他のトピック:

* [学習指針](#学習指針)
* [システム設計面接課題にどのように準備するか](#システム設計面接にどのようにして臨めばいいか)
* [システム設計課題例 **とその解答**](#システム設計課題例とその解答)
* [オブジェクト指向設計課題例、 **とその解答**](#オブジェクト指向設計問題と解答)
* [その他のシステム設計面接課題例](#他のシステム設計面接例題)

## 暗記カード

<p align="center">
  <img src="http://i.imgur.com/zdCAkB3.png"/>
  <br/>
</p>

この[Anki用フラッシュカードデッキ](https://apps.ankiweb.net/) は、間隔反復を活用して、システム設計のキーコンセプトの学習を支援します。

* [システム設計デッキ](resources/flash_cards/System%20Design.apkg)
* [システム設計練習課題デッキ](resources/flash_cards/System%20Design%20Exercises.apkg)
* [オブジェクト指向練習課題デッキ](resources/flash_cards/OO%20Design.apkg)

外出先や移動中の勉強に役立つでしょう。

### コーディング技術課題用の問題: 練習用インタラクティブアプリケーション

コード技術面接用の問題を探している場合は[**こちら**](https://github.com/donnemartin/interactive-coding-challenges)

<p align="center">
  <img src="http://i.imgur.com/b4YtAEN.png"/>
  <br/>
</p>

姉妹リポジトリの [**Interactive Coding Challenges**](https://github.com/donnemartin/interactive-coding-challenges)も見てみてください。追加の暗記デッキカードも入っています。

* [Coding deck](https://github.com/donnemartin/interactive-coding-challenges/tree/master/anki_cards/Coding.apkg)

## コントリビュート

> コミュニティから学ぶ

プルリクエスト等の貢献は積極的にお願いします:

* エラー修正
* セクション内容改善
* 新規セクション追加
* [翻訳する](https://github.com/donnemartin/system-design-primer/issues/28)

現在、内容の改善が必要な作業中のコンテンツは[こちら](#進行中の作業)です。

コントリビュートの前に[Contributing Guidelines](CONTRIBUTING.md)を読みましょう。

## システム設計目次

> 賛否も含めた様々なシステム設計の各トピックの概要。 **全てはトレードオフの関係にあります。**
>
> それぞれのセクションはより学びを深めるような他の文献へのリンクが貼られています。

<p align="center">
  <img src="http://i.imgur.com/jrUBAF7.png"/>
  <br/>
</p>

* [システム設計トピック: まずはここから](#システム設計トピックス-まずはここから)
    * [Step 1: スケーラビリティに関する動画を見る](#ステップ-1-スケーラビリティに関する動画を観て復習する)
    * [Step 2: スケーラビリティに関する記事を読む](#ステップ-2-スケーラビリティに関する資料を読んで復習する)
    * [次のステップ](#次のステップ)
* [パフォーマンス vs スケーラビリティ](#パフォーマンス-vs-スケーラビリティ)
* [レイテンシー vs スループット](#レイテンシー-vs-スループット)
* [可用性 vs 一貫性](#可用性-vs-一貫性)
    * [CAP理論](#cap-理論)
        * [CP - 一貫性(consistency)と分割性(partition)耐性](#cp---一貫性と分断耐性consistency-and-partition-tolerance)
        * [AP - 可用性(availability)と分割性(partition)耐性](#ap---可用性と分断耐性availability-and-partition-tolerance)
* [一貫性 パターン](#一貫性パターン)
    * [弱い一貫性](#弱い一貫性)
    * [結果整合性](#結果整合性)
    * [強い一貫性](#強い一貫性)
* [可用性 パターン](#可用性パターン)
    * [フェイルオーバー](#フェイルオーバー)
    * [レプリケーション](#レプリケーション)
* [ドメインネームシステム(DNS)](#ドメインネームシステム)
* [コンテンツデリバリーネットワーク(CDN)](#コンテンツデリバリーネットワークcontent-delivery-network)
    * [プッシュCDN](#プッシュcdn)
    * [プルCDN](#プルcdn)
* [ロードバランサー](#ロードバランサー)
    * [アクティブ/パッシブ構成](#アクティブパッシブ)
    * [アクティブ/アクティブ構成](#アクティブアクティブ)
    * [Layer 4 ロードバランシング](#layer-4-ロードバランシング)
    * [Layer 7 ロードバランシング](#layer-7-ロードバランシング)
    * [水平スケーリング](#水平スケーリング)
* [リバースプロキシ (WEBサーバー)](#リバースプロキシwebサーバー)
    * [ロードバランサー vs リバースプロキシ](#ロードバランサー-vs-リバースプロキシ)
* [アプリケーションレイヤー](#アプリケーション層)
    * [マイクロサービス](#マイクロサービス)
    * [サービスディスカバリー](#service-discovery)
* [データベース](#データベース)
    * [リレーショナルデータベースマネジメントシステム (RDBMS)](#リレーショナルデータベースマネジメントシステム-rdbms)
        * [マスター/スレーブ レプリケーション](#マスタースレーブ-レプリケーション)
        * [マスター/マスター レプリケーション](#マスターマスター-レプリケーション)
        * [フェデレーション](#federation)
        * [シャーディング](#シャーディング)
        * [デノーマライゼーション](#非正規化)
        * [SQL チューニング](#sqlチューニング)
    * [NoSQL](#nosql)
        * [キー/バリューストア](#キーバリューストア)
        * [ドキュメントストア](#ドキュメントストア)
        * [ワイドカラムストア](#ワイドカラムストア)
        * [グラフ データベース](#グラフデータベース)
    * [SQL or NoSQL](#sqlかnosqlか)
* [キャッシュ](#キャッシュ)
    * [クライアントキャッシング](#クライアントキャッシング)
    * [CDNキャッシング](#cdnキャッシング)
    * [Webサーバーキャッシング](#webサーバーキャッシング)
    * [データベースキャッシング](#データベースキャッシング)
    * [アプリケーションキャッシング](#アプリケーションキャッシング)
    * [データベースクエリレベルでキャッシングする](#データベースクエリレベルでのキャッシング)
    * [オブジェクトレベルでキャッシングする](#オブジェクトレベルでのキャッシング)
    * [いつキャッシュを更新するのか](#いつキャッシュを更新するか)
        * [キャッシュアサイド](#キャッシュアサイド)
        * [ライトスルー](#ライトスルー)
        * [ライトビハインド (ライトバック)](#ライトビハインド-ライトバック)
        * [リフレッシュアヘッド](#リフレッシュアヘッド)
* [非同期処理](#非同期処理)
    * [メッセージキュー](#メッセージキュー)
    * [タスクキュー](#タスクキュー)
    * [バックプレッシャー](#バックプレッシャー)
* [通信](#通信)
    * [伝送制御プロトコル (TCP)](#伝送制御プロトコル-tcp)
    * [ユーザデータグラムプロトコル (UDP)](#ユーザデータグラムプロトコル-udp)
    * [遠隔手続呼出 (RPC)](#遠隔手続呼出-rpc)
    * [Representational state transfer (REST)](#representational-state-transfer-rest)
* [セキュリティ](#セキュリティ)
* [補遺](#補遺)
    * [2の乗数表](#2の乗数表)
    * [全てのプログラマーが知るべきレイテンシー値](#全てのプログラマーが知るべきレイテンシー値)
    * [他のシステム設計面接例題](#他のシステム設計面接例題)
    * [実世界でのアーキテクチャ](#実世界のアーキテクチャ)
    * [各企業のアーキテクチャ](#各企業のアーキテクチャ)
    * [企業のエンジニアブログ](#企業のエンジニアブログ)
* [作業中](#進行中の作業)
* [クレジット](#クレジット)
* [連絡情報](#contact-info)
* [ライセンス](#license)

## 学習指針

> 学習スパンに応じてみるべきトピックス (short, medium, long)

![Imgur](http://i.imgur.com/OfVllex.png)

**Q: 面接のためには、ここにあるものすべてをやらないといけないのでしょうか？**

**A: いえ、ここにあるすべてをやる必要はありません。**

面接で何を聞かれるかは以下の条件によって変わってきます:

* どれだけの技術経験があるか
* あなたの技術背景が何であるか
* どのポジションのために面接を受けているか
* どの企業の面接を受けているか
* 運

より経験のある候補者は一般的にシステム設計についてより深い知識を有していることを要求されるでしょう。システムアーキテクトやチームリーダーは各メンバーの持つような知識よりは深い見識を持っているべきでしょう。一流テック企業では複数回の設計面接を課されることが多いです。

まずは広く始めて、そこからいくつかの分野に絞って深めていくのがいいでしょう。様々なシステム設計のトピックについて少しずつ知っておくことはいいことです。以下の学習ガイドを自分の学習に当てられる時間、技術経験、どの職位、どの会社に応募しているかなどを加味して自分用に調整して使うといいでしょう。

* **短期間** - **幅広く** システム設計トピックを学ぶ。**いくつかの** 面接課題を解くことで対策する。
* **中期間** - **幅広く** そして **それなりに深く**システム設計トピックを学ぶ。**多くの** 面接課題を解くことで対策する。
* **長期間** - **幅広く** そして **もっと深く**システム設計トピックを学ぶ。**ほぼ全ての** 面接課題を解くことで対策する。

| | 短期間 | 中期間 | 長期間 |
|---|---|---|---|
| [システム設計トピック](#システム設計目次) を読み、システム動作機序について広く知る | :+1: | :+1: | :+1: |
| 次のリンク先のいくつかのページを読んで [各企業のエンジニアリングブログ](#企業のエンジニアブログ) 応募する会社について知る | :+1: | :+1: | :+1: |
| 次のリンク先のいくつかのページを読む [実世界でのアーキテクチャ](#実世界のアーキテクチャ) | :+1: | :+1: | :+1: |
| 復習する [システム設計面接課題にどのように準備するか](#システム設計面接にどのようにして臨めばいいか) | :+1: | :+1: | :+1: |
| とりあえず一周する [システム設計課題例](#システム設計課題例とその解答) | Some | Many | Most |
| とりあえず一周する [オブジェクト指向設計問題と解答](#オブジェクト指向設計問題と解答) | Some | Many | Most |
| 復習する [その他システム設計面接での質問例](#他のシステム設計面接例題) | Some | Many | Most |

## システム設計面接にどのようにして臨めばいいか

> システム設計面接試験問題にどのように取り組むか

システム設計面接は **open-ended conversation(Yes/Noでは答えられない口頭質問)です**。 自分で会話を組み立てることを求められます。

以下のステップに従って議論を組み立てることができるでしょう。この過程を確かなものにするために、次のセクション[システム設計課題例とその解答](#system-design-interview-questions-with-solutions) を以下の指針に従って読み込むといいでしょう。

### ステップ 1: そのシステム使用例の概要、制約、推計値等を聞き出し、まとめる

システム仕様の要求事項を聞き出し、問題箇所を特定しましょう。使用例と制約を明確にするための質問を投げかけましょう。要求する推計値についても議論しておきましょう。

* 誰がそのサービスを使うのか？
* どのように使うのか？
* 何人のユーザーがいるのか？
* システムはどのような機能を果たすのか？
* システムへの入力と出力は？
* どれだけの容量のデータを捌く必要があるのか？
* 一秒間に何リクエストの送信が想定されるか？
* 読み書き比率の推定値はいくら程度か？

### ステップ 2: より高レベルのシステム設計を組み立てる

重要なコンポーネントを全て考慮した高レベルのシステム設計概要を組み立てる。

* 主要なコンポーネントと接続をスケッチして書き出す
* 考えの裏付けをする

### ステップ 3: 核となるコンポーネントを設計する

それぞれの主要なコンポーネントについての詳細を学ぶ。例えば、[url短縮サービス](solutions/system_design/pastebin/README.md)の設計を問われた際には次のようにするといいでしょう:

* 元のURLのハッシュ化したものを作り、それを保存する
    * [MD5](solutions/system_design/pastebin/README.md) と [Base62](solutions/system_design/pastebin/README.md)
    * ハッシュ衝突
    * SQL もしくは NoSQL
    * データベーススキーマ
* ハッシュ化されたURLを元のURLに再翻訳する
    * データベース参照
* API & オブジェクト指向の設計

### ステップ 4: システム設計のスケール

与えられた制約条件からボトルネックとなりそうなところを割り出し、明確化する。  例えば、スケーラビリティの問題解決のために以下の要素を考慮する必要があるだろうか？

* ロードバランサー
* 水平スケーリング
* キャッシング
* データベースシャーディング

取りうる解決策とそのトレードオフについて議論をしよう。全てのことはトレードオフの関係にある。ボトルネックについては[スケーラブルなシステム設計の原理](#システム設計目次)を読むといいでしょう。

### ちょっとした暗算問題

ちょっとした推計値を手計算ですることを求められることもあるかもしれません。[補遺](#補遺)の以下の項目が役に立つでしょう:

* [チラ裏計算でシステム設計する](http://highscalability.com/blog/2011/1/26/google-pro-tip-use-back-of-the-envelope-calculations-to-choo.html)
* [2の乗数表](#2の乗数表)
* [全てのプログラマーが知っておくべきレイテンシの参考値](#全てのプログラマーが知るべきレイテンシー値)

### 文献とその他の参考資料

以下のリンク先ページを見てどのような質問を投げかけられるか概要を頭に入れておきましょう:

* [システム設計面接で成功するには？](https://www.palantir.com/2011/10/how-to-rock-a-systems-design-interview/)
* [システム設計面接](http://www.hiredintech.com/system-design)
* [アーキテクチャ、システム設計面接への導入](https://www.youtube.com/watch?v=ZgdS0EUmn70)

## システム設計課題例とその解答

> 頻出のシステム設計面接課題と参考解答、コード及びダイアグラム
>
> 解答は `solutions/` フォルダ以下にリンクが貼られている

| 問題 | |
|---|---|
| Pastebin.com (もしくは Bit.ly) を設計する| [解答](solutions/system_design/pastebin/README.md) |
| Twitterタイムライン (もしくはFacebookフィード)を設計する<br/>Twitter検索(もしくはFacebook検索)機能を設計する | [解答](solutions/system_design/twitter/README.md) |
| ウェブクローラーを設計する | [解答](solutions/system_design/web_crawler/README.md) |
| Mint.comを設計する | [解答](solutions/system_design/mint/README.md) |
| SNSサービスのデータ構造を設計する | [解答](solutions/system_design/social_graph/README.md) |
| 検索エンジンのキー/バリュー構造を設計する | [解答](solutions/system_design/query_cache/README.md) |
| Amazonのカテゴリ毎の売り上げランキングを設計する | [解答](solutions/system_design/sales_rank/README.md) |
| AWS上で100万人規模のユーザーを捌くサービスを設計する | [解答](solutions/system_design/scaling_aws/README.md) |
| システム設計問題を追加する | [Contribute](#contributing) |

### Pastebin.com (もしくは Bit.ly) を設計する

[問題と解答を見る](solutions/system_design/pastebin/README.md)

![Imgur](http://i.imgur.com/4edXG0T.png)

### Twitterタイムライン&検索 (もしくはFacebookフィード&検索)を設計する

[問題と解答を見る](solutions/system_design/twitter/README.md)

![Imgur](http://i.imgur.com/jrUBAF7.png)

### ウェブクローラーの設計

[問題と解答を見る](solutions/system_design/web_crawler/README.md)

![Imgur](http://i.imgur.com/bWxPtQA.png)

### Mint.comの設計

[問題と解答を見る](solutions/system_design/mint/README.md)

![Imgur](http://i.imgur.com/V5q57vU.png)

### SNSサービスのデータ構造を設計する

[問題と解答を見る](solutions/system_design/social_graph/README.md)

![Imgur](http://i.imgur.com/cdCv5g7.png)

### 検索エンジンのキー/バリュー構造を設計する

[問題と解答を見る](solutions/system_design/query_cache/README.md)

![Imgur](http://i.imgur.com/4j99mhe.png)

### Amazonのカテゴリ毎の売り上げランキングを設計する

[問題と解答を見る](solutions/system_design/sales_rank/README.md)

![Imgur](http://i.imgur.com/MzExP06.png)

### AWS上で100万人規模のユーザーを捌くサービスを設計する

[問題と解答を見る](solutions/system_design/scaling_aws/README.md)

![Imgur](http://i.imgur.com/jj3A5N8.png)

## オブジェクト指向設計問題と解答

> 頻出のオブジェクト指向システム設計面接課題と参考解答、コード及びダイアグラム
>
> 解答は `solutions/` フォルダ以下にリンクが貼られている

>**備考: このセクションは作業中です**

| 問題 | |
|---|---|
| ハッシュマップの設計 | [解答](solutions/object_oriented_design/hash_table/hash_map.ipynb)  |
| LRUキャッシュの設計 | [解答](solutions/object_oriented_design/lru_cache/lru_cache.ipynb)  |
| コールセンターの設計 | [解答](solutions/object_oriented_design/call_center/call_center.ipynb)  |
| カードのデッキの設計 | [解答](solutions/object_oriented_design/deck_of_cards/deck_of_cards.ipynb)  |
| 駐車場の設計 | [解答](solutions/object_oriented_design/parking_lot/parking_lot.ipynb)  |
| チャットサーバーの設計 | [解答](solutions/object_oriented_design/online_chat/online_chat.ipynb)  |
| 円形配列の設計 | [Contribute](#contributing)  |
| オブジェクト指向システム設計問題を追加する | [Contribute](#contributing) |

## システム設計トピックス: まずはここから

システム設計の勉強は初めて？

まず初めに、よく使われる設計原理について、それらが何であるか、どのように用いられるか、長所短所について基本的な知識を得る必要があります

### ステップ 1: スケーラビリティに関する動画を観て復習する

[Harvardでのスケーラビリティの講義](https://www.youtube.com/watch?v=-W9F__D3oY4)

* ここで触れられているトピックス:
    * 垂直スケーリング
    * 水平スケーリング
    * キャッシング
    * ロードバランシング
    * データベースレプリケーション
    * データベースパーティション

### ステップ 2: スケーラビリティに関する資料を読んで復習する

[スケーラビリティ](http://www.lecloud.net/tagged/scalability/chrono)

* ここで触れられているトピックス:
    * [クローン](http://www.lecloud.net/post/7295452622/scalability-for-dummies-part-1-clones)
    * [データベース](http://www.lecloud.net/post/7994751381/scalability-for-dummies-part-2-database)
    * [キャッシュ](http://www.lecloud.net/post/9246290032/scalability-for-dummies-part-3-cache)
    * [非同期](http://www.lecloud.net/post/9699762917/scalability-for-dummies-part-4-asynchronism)

### 次のステップ

次に、ハイレベルでのトレードオフについてみていく:

* **パフォーマンス** vs **スケーラビリティ**
* **レイテンシ** vs **スループット**
* **可用性** vs **一貫性**

**全てはトレードオフの関係にある**というのを肝に命じておきましょう。

それから、より深い内容、DNSやCDNそしてロードバランサーなどについて学習を進めていきましょう。

## パフォーマンス vs スケーラビリティ

リソースが追加されるのにつれて **パフォーマンス** が向上する場合そのサービスは **スケーラブル** であると言えるでしょう。一般的に、パフォーマンスを向上させるというのはすなわち計算処理を増やすことを意味しますが、データセットが増えた時などより大きな処理を捌けるようになることでもあります。<sup><a href=http://www.allthingsdistributed.com/2006/03/a_word_on_scalability.html>1</a></sup>

パフォーマンスvsスケーラビリティをとらえる他の考え方:

* **パフォーマンス** での問題を抱えている時、あなたのシステムは一人のユーザーにとって遅いと言えるでしょう。
* **スケーラビリティ** での問題を抱えているとき、一人のユーザーにとっては速いですが、多くのリクエストがある時には遅くなってしまうでしょう。

### その他の参考資料、ページ

* [スケーラビリティについて](http://www.allthingsdistributed.com/2006/03/a_word_on_scalability.html)
* [スケーラビリティ、可用性、安定性、パターン](http://www.slideshare.net/jboner/scalability-availability-stability-patterns/)

## レイテンシー vs スループット

**レイテンシー** とはなにがしかの動作を行う、もしくは結果を算出するのに要する時間

**スループット** とはそのような動作や結果算出が単位時間に行われる回数

一般的に、 **最大限のスループット** を **許容範囲内のレイテンシー** で実現することを目指すのが普通だ。

### その他の参考資料、ページ

* [レイテンシー vs スループットを理解する](https://community.cadence.com/cadence_blogs_8/b/sd/archive/2010/09/13/understanding-latency-vs-throughput)

## 可用性 vs 一貫性

### CAP 理論

<p align="center">
  <img src="http://i.imgur.com/bgLMI2u.png"/>
  <br/>
  <i><a href=http://robertgreiner.com/2014/08/cap-theorem-revisited>Source: CAP theorem revisited</a></i>
</p>

分散型コンピュータシステムにおいては下の三つのうち二つまでしか同時に保証することはできない。:

* **一貫性** - 全ての読み込みは最新の書き込みもしくはエラーを受け取る
* **可用性** - 受け取る情報が最新のものだという保証はないが、全てのリクエストはレスポンスを必ず受け取る
* **分断耐性** - ネットワーク問題によって順不同の分断が起きてもシステムが動作を続ける

*ネットワークは信頼できないので、分断耐性は必ず保証しなければなりません。つまりソフトウェアシステムとしてのトレードオフは、一貫性を取るか、可用性を取るかを考えなければなりません。*

#### CP - 一貫性と分断耐性(consistency and partition tolerance)

分断されたノードからのレスポンスを待ち続けているとタイムアウトエラーに陥る可能性があります。CPはあなたのサービスがアトミックな読み書き（不可分操作）を必要とする際にはいい選択肢でしょう。

#### AP - 可用性と分断耐性(availability and partition tolerance)

レスポンスはノード上にあるデータで最新のものを返します。つまり、最新版のデータが返されるとは限りません。分断が解消された後も、書き込みが反映されるのには時間がかかります。

[結果整合性](#結果整合性)　を求めるサービスの際にはAPを採用するのがいいでしょう。もしくは、外部エラーに関わらずシステムが稼働する必要がある際にも同様です。

### その他の参考資料、ページ

* [CAP 理論を振り返る](http://robertgreiner.com/2014/08/cap-theorem-revisited/)
* [平易な英語でのCAP 理論のイントロ](http://ksat.me/a-plain-english-introduction-to-cap-theorem/)
* [CAP FAQ](https://github.com/henryr/cap-faq)

## 一貫性パターン

同じデータの複製が複数ある状態では、クライアントが一貫したデータ表示を受け取るために、どのようにそれらを同期すればいいのかという課題があります。 [CAP 理論](#cap-理論) における一貫性の定義を思い出してみましょう。全ての読み取りは最新の書き込みデータもしくはエラーを受け取るはずです。

### 弱い一貫性

書き込み後の読み取りでは、その最新の書き込みを読めたり読めなかったりする。ベストエフォート型のアプローチに基づく。

このアプローチはmemcachedなどのシステムに見られます。弱い一貫性はリアルタイム性が必要なユースケース、例えばVoIP、ビデオチャット、リアルタイムマルチプレイヤーゲームなどと相性がいいでしょう。例えば、電話に出ているときに数秒間音声が受け取れなくなったとしたら、その後に接続が回復してもその接続が切断されていた間に話されていたことは聞き取れないというような感じです。

### 結果整合性

書き込みの後、読み取りは最終的にはその結果を読み取ることができる(ミリ秒ほど遅れてというのが一般的です)。データは非同期的に複製されます。

このアプローチはDNSやメールシステムなどに採用されています。結果整合性は多くのリクエストを捌くサービスと相性がいいでしょう。

### 強い一貫性

書き込みの後、読み取りはそれを必ず読むことができます。データは同期的に複製されます。

このアプローチはファイルシステムやRDBMSなどで採用されています。トランザクションを扱うサービスでは強い一貫性が必要でしょう。

### その他の参考資料、ページ

* [データセンター間でのトランザクション](http://snarfed.org/transactions_across_datacenters_io.html)

## 可用性パターン

高い可用性を担保するには主に次の二つのパターンがあります: **フェイルオーバー** と **レプリケーション** です。

### フェイルオーバー

#### アクティブ・パッシブ

アクティブ・パッシブフェイルオーバーにおいては、周期信号はアクティブもしくはスタンバイ中のパッシブなサーバーに送られます。周期信号が中断された時には、パッシブだったサーバーがアクティブサーバーのIPアドレスを引き継いでサービスを再開します。

起動までのダウンタイムはパッシブサーバーが「ホット」なスタンバイ状態にあるか、「コールド」なスタンバイ状態にあるかで変わります。アクティブなサーバーのみがトラフィックを捌きます。

アクティブ・パッシブフェイルオーバーはマスター・スレーブフェイルオーバーと呼ばれることもあります。

#### アクティブ・アクティブ

アクティブアクティブ構成では両方のサーバーがトラフィックを捌くことで負荷を分散します。

これらのサーバーがパブリックなものの場合、DNSは両方のサーバーのパブリックIPを知っている必要があります。もし、プライベートなものな場合、アプリケーションロジックが両方のサーバーの情報について知っている必要があります。

アクティブ・アクティブなフェイルオーバーはマスター・マスターフェイルオーバーと呼ばれることもあります。

### 短所: フェイルオーバー

* フェイルオーバーではより多くのハードウェアを要し、複雑さが増します。
* 最新の書き込みがパッシブサーバーに複製される前にアクティブが落ちると、データ欠損が起きる潜在可能性があります。

### レプリケーション

#### マスター・スレーブ　と　マスター・マスター

このトピックは [データベース](#データベース) セクションにおいてより詳細に解説されています:

* [マスター・スレーブ レプリケーション](#マスタースレーブ-レプリケーション)
* [マスター・マスター レプリケーション](#マスターマスター-レプリケーション)

## ドメインネームシステム

<p align="center">
  <img src="http://i.imgur.com/IOyLj4i.jpg"/>
  <br/>
  <i><a href=http://www.slideshare.net/srikrupa5/dns-security-presentation-issa>Source: DNS security presentation</a></i>
</p>

ドメインネームシステム (DNS) は www.example.com などのドメインネームをIPアドレスへと翻訳します。

DNSは少数のオーソライズされたサーバーが上位に位置する階層的構造です。あなたのルーターもしくはISPは検索をする際にどのDNSサーバーに接続するかという情報を提供します。低い階層のDNSサーバーはその経路マップをキャッシュします。ただ、この情報は伝搬遅延によって陳腐化する可能性があります。DNSの結果はあなたのブラウザもしくはOSに一定期間（[time to live (TTL)](https://en.wikipedia.org/wiki/Time_to_live)に設定された期間）キャッシュされます。

* **NS record (name server)** - あなたのドメイン・サブドメインでのDNSサーバーを特定します。
* **MX record (mail exchange)** - メッセージを受け取るメールサーバーを特定します。
* **A record (address)** - IPアドレスに名前をつけます。
* **CNAME (canonical)** - 他の名前もしくは　`CNAME` (example.com を www.example.com) もしくは `A` recordへと名前を指し示す。

[CloudFlare](https://www.cloudflare.com/dns/) や [Route 53](https://aws.amazon.com/route53/) などのサービスはマネージドDNSサービスを提供しています。いくつかのDNSサービスでは様々な手法を使ってトラフィックを捌くことができます:

* [加重ラウンドロビン](http://g33kinfo.com/info/archives/2657)
    * トラフィックがメンテナンス中のサーバーに行くのを防ぎます
    * 様々なクラスターサイズに応じて調整します
    * A/B テスト
* レイテンシーベース
* 地理ベース

### 欠点: DNS

* 上記で示されているようなキャッシングによって緩和されているとはいえ、DNSサーバーへの接続には少し遅延が生じる。
* DNSサーバーは、[政府、ISP企業,そして大企業](http://superuser.com/questions/472695/who-controls-the-dns-servers/472729)に管理されているが、それらの管理は複雑である。
* DNSサービスは[DDoS attack](http://dyn.com/blog/dyn-analysis-summary-of-friday-october-21-attack/)の例で、IPアドレスなしにユーザーがTwitterなどにアクセスできなくなったように、攻撃を受ける可能性がある。

### その他の参考資料、ページ

* [DNS アーキテクチャ](https://technet.microsoft.com/en-us/library/dd197427(v=ws.10).aspx)
* [Wikipedia](https://en.wikipedia.org/wiki/Domain_Name_System)
* [DNS 記事](https://support.dnsimple.com/categories/dns/)

## コンテンツデリバリーネットワーク(Content delivery network)

<p align="center">
  <img src="http://i.imgur.com/h9TAuGI.jpg"/>
  <br/>
  <i><a href=https://www.creative-artworks.eu/why-use-a-content-delivery-network-cdn/>Source: Why use a CDN</a></i>
</p>

コンテンツデリバリーネットワーク(CDN)は世界中に配置されたプロキシサーバーのネットワークがユーザーに一番地理的に近いサーバーからコンテンツを配信するシステムのことです。AmazonのCloudFrontなどは例外的にダイナミックなコンテンツも配信しますが、一般的に、HTML/CSS/JS、写真、そして動画などの静的ファイルがCDNを通じて配信されます。そのサイトのDNSがクライアントにどのサーバーと交信するかという情報を伝えます。

CDNを用いてコンテンツを配信することで以下の二つの理由でパフォーマンスが劇的に向上します:

* ユーザーは近くにあるデータセンターから受信できる
* バックエンドサーバーはCDNが処理してくれるリクエストに関しては処理する必要がなくなります

### プッシュCDN

プッシュCDNではサーバーデータに更新があった時には必ず、新しいコンテンツを受け取る方式です。コンテンツを用意し、CDNに直接アップロードし、URLをCDNを指すように指定するところまで、全て自分で責任を負う形です。コンテンツがいつ期限切れになるのか更新されるのかを設定することができます。コンテンツは新規作成時、更新時のみアップロードされることでトラフィックは最小化される一方、ストレージは最大限消費されてしまいます。

トラフィックの少ない、もしくは頻繁にはコンテンツが更新されないサイトの場合にはプッシュCDNと相性がいいでしょう。コンテンツは定期的に再びプルされるのではなく、CDNに一度のみ配置されます。

### プルCDN

プルCDNでは一人目のユーザーがリクエストした時に、新しいコンテンツをサービスのサーバーから取得します。コンテンツは自分のサーバーに保存して、CDNを指すURLを書き換えます。結果として、CDNにコンテンツがキャッシュされるまではリクエスト処理が遅くなります。

[time-to-live (TTL)](https://en.wikipedia.org/wiki/Time_to_live) はコンテンツがどれだけの期間キャッシュされるかを規定します。プルCDNはCDN 上でのストレージスペースを最小化しますが、有効期限が切れたファイルが更新前にプルされてしまうことで冗長なトラフィックに繋がってしまう可能性があります。

大規模なトラフィックのあるサイトではプルCDNが相性がいいでしょう。というのも、トラフィックの大部分は最近リクエストされ、CDNに残っているコンテンツにアクセスするものであることが多いからです。

### 欠点: CDN

* CDNのコストはトラフィック量によって変わります。もちろん、CDNを使わない場合のコストと比較するべきでしょう。
* TTLが切れる前にコンテンツが更新されると陳腐化する恐れがあります。
* CDNでは静的コンテンツがCDNを指すようにURLを更新する必要があります。

### その他の参考資料、ページ

* [グローバルに分散されたコンテンツデリバリーネットワーク](http://repository.cmu.edu/cgi/viewcontent.cgi?article=2112&context=compsci)
* [プッシュCDNとプルCDNの違い](http://www.travelblogadvice.com/technical/the-differences-between-push-and-pull-cdns/)
* [Wikipedia](https://en.wikipedia.org/wiki/Content_delivery_network)

## ロードバランサー

<p align="center">
  <img src="http://i.imgur.com/h81n9iK.png"/>
  <br/>
  <i><a href=http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html>Source: Scalable system design patterns</a></i>
</p>

ロードバランサーは入力されるクライアントのリクエストをアプリケーションサーバーやデータベースへと分散させる。どのケースでもロードバランサーはサーバー等計算リソースからのレスポンスを適切なクライアントに返す。ロードバランサーは以下のことに効果的です:

* リクエストが状態の良くないサーバーに行くのを防ぐ
* リクエストを過剰に送るのを防ぐ
* 特定箇所の欠陥でサービスが落ちることを防ぐ

ロードバランサーは (費用の高い) ハードウェアもしくはHAProxyなどのソフトウェアで実現できる。

他の利点としては:

* **SSL termination** - 入力されるリクエストを解読する、また、サーバーレスポンスを暗号化することでバックエンドのサーバーがこのコストが高くつきがちな処理を請け負わなくていいように肩代わりします。
    * [X.509 certificates](https://en.wikipedia.org/wiki/X.509) をそれぞれのサーバーにインストールする必要をなくします
* **セッション管理** - クッキーを取り扱うウェブアプリがセッション情報を保持していない時などに、特定のクライアントのリクエストを同じインスタンスへと流します。

障害に対応するために、[アクティブ・パッシブ](#アクティブパッシブ) もしくは [アクティブ・アクティブ](#アクティブアクティブ) モードのどちらにおいても、複数のロードバランサーを配置するのが一般的です。

ロードバランサーは以下のような種々のメトリックを用いてトラフィックルーティングを行うことができます:

* ランダム
* Least loaded
* セッション/クッキー
* [ラウンドロビンもしくは加重ラウンドロビン](http://g33kinfo.com/info/archives/2657)
* [Layer 4](#layer-4-ロードバランシング)
* [Layer 7](#layer-7-ロードバランシング)

### Layer 4 ロードバランシング

Layer 4 ロードバランサーは [トランスポートレイヤー](#通信) を参照してどのようにリクエストを配分するか判断します。一般的に、トランスポートレイヤーとしては、ソース、送信先IPアドレス、ヘッダーに記述されたポート番号が含まれますが、パケットの中身のコンテンツは含みません。 Layer 4 ロードバランサーはネットワークパケットを上流サーバーへ届け、上流サーバーから配信することでネットワークアドレス変換 [Network Address Translation (NAT)](https://www.nginx.com/resources/glossary/layer-4-load-balancing/) を実現します。

### Layer 7 ロードバランシング

Layer 7 ロードバランサーは [アプリケーションレイヤー](#通信) を参照してどのようにリクエストを配分するか判断します。ヘッダー、メッセージ、クッキーなどのコンテンツのことです。Layer 7 ロードバランサーはネットワークトラフィックの終端を受け持ち メッセージを読み込み、ロードバランシングの判断をし、選択したサーバーとの接続を繋ぎます。例えば layer 7 ロードバランサーは動画のトラフィックを直接、そのデータをホストしているサーバーにつなぐと同時に、決済処理などのより繊細なトラフィックをセキュリティ強化されたサーバーに流すということもできる。

柔軟性とのトレードオフになりますが、 layer 4 ロードバランサーではLayer 7ロードバランサーよりも所要時間、計算リソースを少なく済ませることができます。ただし、昨今の汎用ハードウェアではパフォーマンスは最小限のみしか発揮できないでしょう。

### 水平スケーリング

ロードバランサーでは水平スケーリングによってパフォーマンスと可用性を向上させることができます。手頃な汎用マシンを追加することによってスケールアウトさせる方が、一つのサーバーをより高価なマシンにスケールアップする（**垂直スケーリング**）より費用対効果も高くなり、結果的に可用性も高くなります。また、汎用ハードウェアを扱える人材を雇う方が、特化型の商用ハードウェアを扱える人材を雇うよりも簡単でしょう。

#### 欠点: 水平スケーリング

* 水平的にスケーリングしていくと、複雑さが増す上に、サーバーのクローニングが必要になる。
    * サーバーはステートレスである必要がある: ユーザーに関連するセッションや、プロフィール写真などのデータを持ってはいけない
    * セッションは一元的な[データベース](#データベース) (SQL、 NoSQL)などのデータストアにストアされるか [キャッシュ](#キャッシュ) (Redis、 Memcached)に残す必要があります。
* キャッシュやデータベースなどの下流サーバーは上流サーバーがスケールアウトするにつれてより多くの同時接続を保たなければなりません。

### 欠点: ロードバランサー

* ロードバランサーはリソースが不足していたり、設定が適切でない場合、システム全体のボトルネックになる可能性があります。
* 単一障害点を除こうとしてロードバランサーを導入した結果、複雑さが増してしまうことになります。
* ロードバランサーが一つだけだとそこが単一障害点になってしまいます。一方で、ロードバランサーを複数にすると、さらに複雑さが増してしまいます。

### その他の参考資料、ページ

* [NGINX アーキテクチャ](https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/)
* [HAProxy アーキテクチャガイド](http://www.haproxy.org/download/1.2/doc/architecture.txt)
* [スケーラビリティ](http://www.lecloud.net/post/7295452622/scalability-for-dummies-part-1-clones)
* [Wikipedia](https://en.wikipedia.org/wiki/Load_balancing_(computing))
* [Layer 4 ロードバランシング](https://www.nginx.com/resources/glossary/layer-4-load-balancing/)
* [Layer 7 ロードバランシング](https://www.nginx.com/resources/glossary/layer-7-load-balancing/)
* [ELB listener config](http://docs.aws.amazon.com/elasticloadbalancing/latest/classic/elb-listener-config.html)

## リバースプロキシ(webサーバー)

<p align="center">
  <img src="http://i.imgur.com/n41Azff.png"/>
  <br/>
  <i><a href=https://upload.wikimedia.org/wikipedia/commons/6/67/Reverse_proxy_h2g2bob.svg>Source: Wikipedia</a></i>
  <br/>
</p>

リバースプロキシサーバーは内部サービスをまとめて外部に統一されたインターフェースを提供するウェブサーバーです。クライアントからのリクエストはそれに対応するサーバーに送られて、その後レスポンスをリバースプロキシがクライアントに返します。

他には以下のような利点があります:

* **より堅牢なセキュリティ** - バックエンドサーバーの情報を隠したり、IPアドレスをブラックリスト化したり、クライアントごとの接続数を制限したりできます。
* **スケーラビリティや柔軟性が増します** - クライアントはリバースプロキシのIPしか見ないので、裏でサーバーをスケールしたり、設定を変えやすくなります。
* **SSL termination** - 入力されるリクエストを解読し、サーバーのレスポンスを暗号化することでサーバーがこのコストのかかりうる処理をしなくて済むようになります。
    * [X.509 証明書](https://en.wikipedia.org/wiki/X.509) を各サーバーにインストールする必要がなくなります。
* **圧縮** - サーバーレスポンスを圧縮できます
* **キャッシング** - キャッシュされたリクエストに対して、レスポンスを返します
* **静的コンテンツ** - 静的コンテンツを直接送信することができます。
    * HTML/CSS/JS
    * 写真
    * 動画
    * などなど

### ロードバランサー vs リバースプロキシ

* 複数のサーバーがある時にはロードバランサーをデプロイすると役に立つでしょう。 しばしば、ロードバランサーは同じ機能を果たすサーバー群へのトラフィックを捌きます。
* リバースプロキシでは、上記に述べたような利点を、単一のウェブサーバーやアプリケーションレイヤーに対しても示すことができます。
* NGINX や HAProxy などの技術はlayer 7 リバースプロキシとロードバランサーの両方をサポートします。

### 欠点: リバースプロキシ

* リバースプロキシを導入するとシステムの複雑性が増します。
* 単一のリバースプロキシは単一障害点になりえます。一方で、複数のリバースプロキシを導入すると(例: [フェイルオーバー](https://en.wikipedia.org/wiki/Failover)) 複雑性はより増します。

### その他の参考資料、ページ

* [リバースプロキシ vs ロードバランサー](https://www.nginx.com/resources/glossary/reverse-proxy-vs-load-balancer/)
* [NGINX アーキテクチャ](https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/)
* [HAProxy アーキテクチャ ガイド](http://www.haproxy.org/download/1.2/doc/architecture.txt)
* [Wikipedia](https://en.wikipedia.org/wiki/Reverse_proxy)

## アプリケーション層

<p align="center">
  <img src="http://i.imgur.com/yB5SYwm.png"/>
  <br/>
  <i><a href=http://lethain.com/introduction-to-architecting-systems-for-scale/#platform_layer>Source: Intro to architecting systems for scale</a></i>
</p>

ウェブレイヤーをアプリケーション層 (プラットフォーム層とも言われる) と分離することでそれぞれの層を独立にスケール、設定することができるようになります。新しいAPIをアプリケーション層に追加する際に、不必要にウェブサーバーを追加する必要がなくなります。

 **単一責任の原則** では、小さい自律的なサービスが協調して動くように提唱しています。小さいサービスの小さいチームが急成長のためにより積極的な計画を立てられるようにするためです。

アプリケーション層は[非同期処理](#非同期処理)もサポートします。

### マイクロサービス

独立してデプロイできる、小規模なモジュール様式である[マイクロサービス](https://en.wikipedia.org/wiki/Microservices)もこの議論に関係してくる技術でしょう。それぞれのサービスは独自のプロセスを処理し、明確で軽量なメカニズムで通信して、その目的とする機能を実現します。<sup><a href=https://smartbear.com/learn/api-design/what-are-microservices>1</a></sup>

例えばPinterestでは以下のようなマイクロサービスに分かれています。ユーザープロフィール、フォロワー、フィード、検索、写真アップロードなどです。

### サービスディスカバリー

[Consul](https://www.consul.io/docs/index.html)、 [Etcd](https://coreos.com/etcd/docs/latest)、 [Zookeeper](http://www.slideshare.net/sauravhaloi/introduction-to-apache-zookeeper) などのシステムでは、登録されているサービスの名前、アドレス、ポートの情報を監視することで、サービス同士が互いを見つけやすくしています。サービスの完全性の確認には [Health checks](https://www.consul.io/intro/getting-started/checks.html) が便利で、これには [HTTP](#hypertext-transfer-protocol-http) エンドポイントがよく使われます。 Consul と Etcd のいずれも組み込みの [key-value store](#キーバリューストア) を持っており、設定データや共有データなどのデータを保存しておくことに使われます。

### 欠点: アプリケーション層

* アーキテクチャ、運用、そしてプロセスを考慮すると、緩く結び付けられたアプリケーション層を追加するには、モノリシックなシステムとは異なるアプローチが必要です。
* マイクロサービスはデプロイと運用の点から見ると複雑性が増すことになります。

### その他の参考資料、ページ

* [スケールするシステムアーキテクチャを設計するためのイントロ](http://lethain.com/introduction-to-architecting-systems-for-scale)
* [システム設計インタビューを紐解く](http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview)
* [サービス指向アーキテクチャ](https://en.wikipedia.org/wiki/Service-oriented_architecture)
* [Zookeeperのイントロダクション](http://www.slideshare.net/sauravhaloi/introduction-to-apache-zookeeper)
* [マイクロサービスを作るために知っておきたいこと](https://cloudncode.wordpress.com/2016/07/22/msa-getting-started/)

## データベース

<p align="center">
  <img src="http://i.imgur.com/Xkm5CXz.png"/>
  <br/>
  <i><a href=https://www.youtube.com/watch?v=w95murBkYmU>Source: Scaling up to your first 10 million users</a></i>
</p>

### リレーショナルデータベースマネジメントシステム (RDBMS)

SQLなどのリレーショナルデータベースはテーブルに整理されたデータの集合である。

**ACID** はリレーショナルデータベースにおける[トランザクション](https://en.wikipedia.org/wiki/Database_transaction)のプロパティの集合である

* **不可分性** - それぞれのトランザクションはあるかないかのいずれかである
* **一貫性** - どんなトランザクションもデータベースをある確かな状態から次の状態に遷移させる。
* **独立性** - 同時にトランザクションを処理することは、連続的にトランザクションを処理するのと同じ結果をもたらす。
* **永続性** - トランザクションが処理されたら、そのように保存される

リレーショナルデータベースをスケールさせるためにはたくさんの技術がある: **マスター・スレーブ レプリケーション**、 **マスター・マスター レプリケーション**、 **federation**、 **シャーディング**、 **非正規化**、 そして **SQL チューニング**

#### マスタースレーブ レプリケーション

マスターデータベースが読み取りと書き込みを処理し、書き込みを一つ以上のスレーブデータベースに複製します。スレーブデータベースは読み取りのみを処理します。スレーブデータベースは木構造のように追加のスレーブにデータを複製することもできます。マスターデータベースがオフラインになった場合には、いずれかのスレーブがマスターに昇格するか、新しいマスターデータベースが追加されるまでは読み取り専用モードで稼働します。

<p align="center">
  <img src="http://i.imgur.com/C9ioGtn.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>Source: Scalability, availability, stability, patterns</a></i>
</p>

##### 欠点: マスタースレーブ レプリケーション

* スレーブをマスターに昇格させるには追加のロジックが必要になる。
* マスタースレーブ レプリケーション、マスターマスター レプリケーションの **両方** の欠点は[欠点: レプリケーション](#欠点-マスタースレーブ-レプリケーション)を参照

#### マスターマスター レプリケーション

いずれのマスターも読み取り書き込みの両方に対応する。書き込みに関してはそれぞれ協調する。いずれかのマスターが落ちても、システム全体としては読み書き両方に対応したまま運用できる。

<p align="center">
  <img src="http://i.imgur.com/krAHLGg.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>Source: Scalability, availability, stability, patterns</a></i>
</p>

##### 欠点: マスターマスター レプリケーション

* ロードバランサーを導入するか、アプリケーションロジックを変更することでどこに書き込むかを指定しなければならない。
* 大体のマスターマスターシステムは、一貫性が緩い（ACID原理を守っていない）もしくは、同期する時間がかかるために書き込みのレイテンシーが増加してしまっている。
* 書き込みノードが追加され、レイテンシーが増加するにつれ書き込みの衝突の可能性が増える。
* マスタースレーブ レプリケーション、マスターマスター レプリケーションの **両方** の欠点は[欠点: レプリケーション](#欠点-マスタースレーブ-レプリケーション) を参照

##### 欠点: レプリケーション

* 新しいデータ書き込みを複製する前にマスターが落ちた場合にはそのデータが失われてしまう可能性がある。
* 書き込みは読み取りレプリカにおいてリプレイされる。書き込みが多い場合、複製ノードが書き込みの処理のみで行き詰まって、読み取りの処理を満足に行えない可能性がある。
* 読み取りスレーブノードの数が多ければ多いほど、複製しなければならない数も増え、複製時間が伸びてしまいます。
* システムによっては、マスターへの書き込みはマルチスレッドで並列処理できる一方、スレーブへの複製は単一スレッドで連続的に処理しなければならない場合があります。
* レプリケーションでは追加のハードウェアが必要になり、複雑性も増します。

##### その他の参考資料、ページ: レプリケーション

* [スケーラビリティ、 可用性、 スタビリティ パターン](http://www.slideshare.net/jboner/scalability-availability-stability-patterns/)
* [マルチマスター レプリケーション](https://en.wikipedia.org/wiki/Multi-master_replication)

#### Federation

<p align="center">
  <img src="http://i.imgur.com/U3qV33e.png"/>
  <br/>
  <i><a href=https://www.youtube.com/watch?v=w95murBkYmU>Source: Scaling up to your first 10 million users</a></i>
</p>

フェデレーション (もしくは機能分割化とも言う) はデータベースを機能ごとに分割する。例えば、モノリシックな単一データベースの代わりに、データベースを **フォーラム**、 **ユーザー**、 **プロダクト** のように三つにすることで、データベース一つあたりの書き込み・読み取りのトラフィックが減り、その結果レプリケーションのラグも短くなります。データベースが小さくなることで、メモリーに収まるデータが増えます。キャッシュの局所性が高まるため、キャッシュヒット率も上がります。単一の中央マスターで書き込みを直列化したりしないため、並列で書き込みを処理することができ、スループットの向上が期待できます。

##### 欠点: federation

* 大規模な処理やテーブルを要するスキーマの場合、フェデレーションは効果的とは言えないでしょう。
* どのデータベースに読み書きをするのかを指定するアプリケーションロジックを更新しなければなりません。
* [server link](http://stackoverflow.com/questions/5145637/querying-data-by-joining-two-tables-in-two-database-on-different-servers)で二つのデータベースからのデータを連結するのはより複雑になるでしょう。
* フェデレーションでは追加のハードウェアが必要になり、複雑性も増します。

##### その他の参考資料、ページ: federation

* [Scaling up to your first 10 million users](https://www.youtube.com/watch?v=w95murBkYmU)

#### シャーディング

<p align="center">
  <img src="http://i.imgur.com/wU8x5Id.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>Source: Scalability, availability, stability, patterns</a></i>
</p>

シャーディングでは異なるデータベースにそれぞれがデータのサブセット断片のみを持つようにデータを分割します。ユーザーデータベースを例にとると、ユーザー数が増えるにつれてクラスターにはより多くの断片が加えられることになります。

[federation](#federation)の利点に似ていて、シャーディングでは読み書きのトラフィックを減らし、レプリケーションを減らし、キャッシュヒットを増やすことができます。インデックスサイズも減らすことができます。一般的にはインデックスサイズを減らすと、パフォーマンスが向上しクエリ速度が速くなります。なにがしかのデータを複製する機能がなければデータロスにつながりますが、もし、一つのシャードが落ちても、他のシャードが動いていることになります。フェデレーションと同じく、単一の中央マスターが書き込みの処理をしなくても、並列で書き込みを処理することができ、スループットの向上が期待できます。

ユーザーテーブルをシャードする一般的な方法は、ユーザーのラストネームイニシャルでシャードするか、ユーザーの地理的配置でシャードするなどです。

##### 欠点: シャーディング

* シャードに対応するようにアプリケーションロジックを変更しなければなりません。結果としてSQLクエリが複雑になります。
* シャードではデータ配分がいびつになってしまう可能性があります。例えば、標準ユーザーの集合を持つシャードがある場合、そのシャードが他のシャードよりも重い負荷を負うことになります。
    * リバランシングをすると複雑性がより増します。[consistent hashing](http://www.paperplanes.de/2011/12/9/the-magic-of-consistent-hashing.html) に基づいたシャーディングでは、通信データを削減することもできます。
* 複数のシャードからのデータを連結するのはより複雑です。
* シャーディングでは追加のハードウェアが必要になり、複雑性も増します。

##### その他の参考資料、ページ: シャーディング

* [シャードの登場](http://highscalability.com/blog/2009/8/6/an-unorthodox-approach-to-database-design-the-coming-of-the.html)
* [シャードデータベースアーキテクチャ](https://en.wikipedia.org/wiki/Shard_(database_architecture))
* [Consistent hashing](http://www.paperplanes.de/2011/12/9/the-magic-of-consistent-hashing.html)

#### 非正規化

非正規化では、書き込みのパフォーマンスをいくらか犠牲にして読み込みのパフォーマンスを向上させようとします。計算的に重いテーブルの結合などをせずに、複数のテーブルに冗長なデータのコピーが書き込まれるのを許容します。いくつかのRDBMS例えば、[PostgreSQL](https://en.wikipedia.org/wiki/PostgreSQL) やOracleはこの冗長な情報を取り扱い、一貫性を保つための[materialized views](https://en.wikipedia.org/wiki/Materialized_view) という機能をサポートしています。

[フェデレーション](#federation) や [シャーディング](#シャーディング)などのテクニックによってそれぞれのデータセンターに分配されたデータを合一させることはとても複雑な作業です。非正規化によってそのような複雑な処理をしなくて済むようになります。

多くのシステムで、100対1あるいは1000対1くらいになるくらい読み取りの方が、書き込みのトラフィックよりも多いことでしょう。読み込みを行うために、複雑なデータベースのジョイン処理が含まれるものは計算的に高価につきますし、ディスクの処理時間で膨大な時間を費消してしまうことになります。

##### 欠点: 非正規化

* データが複製される。
* 冗長なデータの複製が同期されるように制約が存在し、そのことでデータベース全体の設計が複雑化する。
* 非正規化されたデータベースは過大な書き込みを処理しなければならない場合、正規化されているそれよりもパフォーマンスにおいて劣る可能性がある。

###### その他の参考資料、ページ: 非正規化

* [Denormalization](https://en.wikipedia.org/wiki/Denormalization)

#### SQLチューニング

SQLチューニングは広範な知識を必要とする分野で多くの [本](https://www.amazon.com/s/ref=nb_sb_noss_2?url=search-alias%3Daps&field-keywords=sql+tuning) が書かれています。

ボトルネックを明らかにし、シミュレートする上で、 **ベンチマーク** を定め、 **プロファイル** することはとても重要です。

* **ベンチマーク** - [ab](http://httpd.apache.org/docs/2.2/programs/ab.html)などのツールを用いて、高負荷の状況をシミュレーションしてみましょう。
* **プロファイル** - [slow query log](http://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html) などのツールを用いて、パフォーマンス状況の確認をしましょう。

ベンチマークとプロファイルをとることで以下のような効率化の選択肢をとることになるでしょう。

##### スキーマを絞る

* MySQLはアクセス速度向上のため、ディスク上の連続したブロックへデータを格納しています。
* 長さの決まったフィールドに対しては `VARCHAR` よりも `CHAR` を使うようにしましょう。
    * `CHAR` の方が効率的に速くランダムにデータにアクセスできます。 一方、 `VARCHAR` では次のデータに移る前にデータの末尾を検知しなければならないために速度が犠牲になります。
* ブログの投稿など、大きなテキストには TEXT を使いましょう。 TEXT ではブーリアン型の検索も可能です。 TEXT フィールドには、テキストブロックが配置されている、ディスク上の場所へのポインターが保存されます。
* 2の32乗や40億以下を超えない程度の大きな数には INT を使いましょう。
* 通貨に関しては小数点表示上のエラーを避けるために `DECIMAL` を使いましょう。
* 大きな `BLOBS` を保存するのは避けましょう。どこからそのオブジェクトを取ってくることができるかの情報を保存しましょう。
* `VARCHAR(255)` は8ビットで数えられる最大の文字数です。一部のDBMSでは、1バイトの利用効率を最大化するためにこの文字数がよく使われます。
* [検索性能向上のため](http://stackoverflow.com/questions/1017239/how-do-null-values-affect-performance-in-a-database-search) 、可能であれば `NOT NULL` 制約を設定しましょう。

##### インデックスを効果的に用いる

* クエリ(`SELECT`、 `GROUP BY`、 `ORDER BY`、 `JOIN`) の対象となる列にインデックスを使うことで速度を向上できるかもしれません。
* インデックスは通常、平衡探索木である[B木](https://en.wikipedia.org/wiki/B-tree)の形で表されます。B木によりデータは常にソートされた状態になります。また検索、順次アクセス、挿入、削除を対数時間で行えます。
* インデックスを配置することはデータをメモリーに残すことにつながりより容量を必要とします。
* インデックスの更新も必要になるため書き込みも遅くなります。
* 大量のデータをロードする際には、インデックスを切ってからデータをロードして再びインデックスをビルドした方が速いことがあります。

##### 高負荷なジョインを避ける

* パフォーマンス上必要なところには[非正規化](#非正規化)を適用する

##### テーブルのパーティション

* テーブルを分割し、ホットスポットを独立したテーブルに分離してメモリーに乗せられるようにする。

##### クエリキャッシュを調整する

* 場合によっては[クエリキャッシュ](http://dev.mysql.com/doc/refman/5.7/en/query-cache) が[パフォーマンス問題](https://www.percona.com/blog/2014/01/28/10-mysql-performance-tuning-settings-after-installation/) を引き起こす可能性がある

##### その他の参考資料、ページ: SQLチューニング

* [MySQLクエリを最適化するためのTips](http://20bits.com/article/10-tips-for-optimizing-mysql-queries-that-dont-suck)
* [VARCHAR(255)をやたらよく見かけるのはなんで？](http://stackoverflow.com/questions/1217466/is-there-a-good-reason-i-see-varchar255-used-so-often-as-opposed-to-another-l)
* [null値はどのようにパフォーマンスに影響するのか？](http://stackoverflow.com/questions/1017239/how-do-null-values-affect-performance-in-a-database-search)
* [Slow query log](http://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html)

### NoSQL

NoSQL は **key-value store**、 **document-store**、 **wide column store**、 もしくは **graph database**によって表現されるデータアイテムの集合です。データは一般的に正規化されておらず、アプリケーション側でジョインが行われます。大部分のNoSQLは真のACIDトランザクションを持たず、 [結果整合性](#結果整合性) 的な振る舞いの方を好みます。

**BASE** はしばしばNoSQLデータベースのプロパティを説明するために用いられます。[CAP Theorem](#cap-理論) と対照的に、BASEは一貫性よりも可用性を優先します。

* **Basically available** - システムは可用性を保証します。
* **Soft state** - システムの状態は入力がなくても時間経過とともに変化する可能性があります。
* **結果整合性** - システム全体は時間経過とともにその間に入力がないという前提のもと、一貫性が達成されます。

[SQLか？NoSQLか？](#sqlかnosqlか) を選択するのに加えて、どのタイプのNoSQLがどの使用例に最も適するかを理解するのはとても有益です。このセクションでは **キーバリューストア**、 **ドキュメントストア**、 **ワイドカラムストア**、 と **グラフデータベース** について触れていきます。

#### キーバリューストア

> 概要: ハッシュテーブル

キーバリューストアでは一般的にO(1)の読み書きができ、それらはメモリないしSSDで裏付けられています。データストアはキーを [辞書的順序](https://en.wikipedia.org/wiki/Lexicographical_order) で保持することでキーの効率的な取得を可能にしています。キーバリューストアではメタデータを値とともに保持することが可能です。

キーバリューストアはハイパフォーマンスな挙動が可能で、単純なデータモデルやインメモリーキャッシュレイヤーなどのデータが急速に変わる場合などに使われます。単純な処理のみに機能が制限されているので、追加の処理機能が必要な場合にはその複雑性はアプリケーション層に載せることになります。

キーバリューストアはもっと複雑なドキュメントストアや、グラフデータベースなどの基本です。

##### その他の参考資料、ページ: キーバリューストア

* [キーバリューデータベース](https://en.wikipedia.org/wiki/Key-value_database)
* [キーバリューストアの欠点](http://stackoverflow.com/questions/4056093/what-are-the-disadvantages-of-using-a-key-value-table-over-nullable-columns-or)
* [Redisアーキテクチャ](http://qnimate.com/overview-of-redis-architecture/)
* [メムキャッシュアーキテクチャ](https://www.adayinthelifeof.nl/2011/02/06/memcache-internals/)

#### ドキュメントストア

> 概要: ドキュメントがバリューとして保存されたキーバリューストア

ドキュメントストアはオブジェクトに関する全ての情報を持つドキュメント(XML、 JSON、 binaryなど)を中心に据えたシステムです。ドキュメントストアでは、ドキュメント自身の内部構造に基づいた、APIもしくはクエリ言語を提供します。 *メモ：多くのキーバリューストアでは、値のメタデータを扱う機能を含んでいますが、そのことによって二つドキュメントストアとの境界線が曖昧になってしまっています。*

以上のことを実現するために、ドキュメントはコレクション、タグ、メタデータやディレクトリなどとして整理されています。ドキュメント同士はまとめてグループにできるものの、それぞれで全く異なるフィールドを持つ可能性があります。

[MongoDB](https://www.mongodb.com/mongodb-architecture) や [CouchDB](https://blog.couchdb.org/2016/08/01/couchdb-2-0-architecture/) などのドキュメントストアも、複雑なクエリを処理するためのSQLのような言語を提供しています。[DynamoDB](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/decandia07dynamo.pdf) はキーバリューとドキュメントの両方をサポートしています。

ドキュメントストアは高い柔軟性を担保するので、頻繁に変化するデータを扱う時に用いられます。

##### その他の参考資料、ページ:  ドキュメントストア

* [ドキュメント指向 データベース](https://en.wikipedia.org/wiki/Document-oriented_database)
* [MongoDB アーキテクチャ](https://www.mongodb.com/mongodb-architecture)
* [CouchDB アーキテクチャ](https://blog.couchdb.org/2016/08/01/couchdb-2-0-architecture/)
* [Elasticsearch アーキテクチャ](https://www.elastic.co/blog/found-elasticsearch-from-the-bottom-up)

#### ワイドカラムストア

<p align="center">
  <img src="http://i.imgur.com/n16iOGk.png"/>
  <br/>
  <i><a href=http://blog.grio.com/2015/11/sql-nosql-a-brief-history.html>Source: SQL & NoSQL, a brief history</a></i>
</p>

> 概要: ネストされたマップ `カラムファミリー<行キー、 カラム<ColKey、 Value、 Timestamp>>`

ワイドカラムストアのデータの基本単位はカラム（ネーム・バリューのペア）です。それぞれのカラムはカラムファミリーとして（SQLテーブルのように）グループ化することができます。スーパーカラムファミリーはカラムファミリーの集合です。それぞれのカラムには行キーでアクセスすることができます。同じ行キーを持つカラムは同じ行として認識されます。それぞれの値は、バージョン管理とコンフリクトが起きた時のために、タイムスタンプを含みます。

Googleは[Bigtable](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/chang06bigtable.pdf)を初のワイドカラムストアとして発表しました。それがオープンソースでHadoopなどでよく使われる[HBase](https://www.mapr.com/blog/in-depth-look-hbase-architecture) やFacebookによる[Cassandra](http://docs.datastax.com/en/archived/cassandra/2.0/cassandra/architecture/architectureIntro_c.html) などのプロジェクトに影響を与えました。BigTable、HBaseやCassandraなどのストアはキーを辞書形式で保持することで選択したキーレンジでのデータ取得を効率的にします。

ワイドカラムストアは高い可用性とスケーラビリティを担保します。これらはとても大規模なデータセットを扱うことによく使われます。

##### その他の参考資料、ページ:  ワイドカラムストア

* [SQL & NoSQL簡単に歴史をさらう](http://blog.grio.com/2015/11/sql-nosql-a-brief-history.html)
* [Bigtable アーキテクチャ](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/chang06bigtable.pdf)
* [HBase アーキテクチャ](https://www.mapr.com/blog/in-depth-look-hbase-architecture)
* [Cassandra アーキテクチャ](http://docs.datastax.com/en/archived/cassandra/2.0/cassandra/architecture/architectureIntro_c.html)

#### グラフデータベース

<p align="center">
  <img src="http://i.imgur.com/fNcl65g.png"/>
  <br/>
  <i><a href=https://en.wikipedia.org/wiki/File:GraphDatabase_PropertyGraph.png>Source: Graph database</a></i>
</p>

> 概要: グラフ

グラフデータベースでは、それぞれのノードがレコードで、それぞれのアークは二つのノードを繋ぐ関係性として定義されます。グラフデータベースは多数の外部キーや多対多などの複雑な関係性を表すのに最適です。

グラフデータベースはSNSなどのサービスの複雑な関係性モデルなどについて高いパフォーマンスを発揮します。比較的新しく、まだ一般的には用いられていないので、開発ツールやリソースを探すのが他の方法に比べて難しいかもしれません。多くのグラフは[REST APIs](#representational-state-transfer-rest)を通じてのみアクセスできます。

##### その他の参考資料、ページ:  グラフ

* [Graphデータベース](https://en.wikipedia.org/wiki/Graph_database)
* [Neo4j](https://neo4j.com/)
* [FlockDB](https://blog.twitter.com/2010/introducing-flockdb)

#### その他の参考資料、ページ:  NoSQL

* [基本用語の説明](http://stackoverflow.com/questions/3342497/explanation-of-base-terminology)
* [NoSQLデータベースについて調査と選択ガイド](https://medium.com/baqend-blog/nosql-databases-a-survey-and-decision-guidance-ea7823a822d#.wskogqenq)
* [スケーラビリティ](http://www.lecloud.net/post/7994751381/scalability-for-dummies-part-2-database)
* [NoSQLのイントロダクション](https://www.youtube.com/watch?v=qI_g07C_Q5I)
* [NoSQLパターン](http://horicky.blogspot.com/2009/11/nosql-patterns.html)

### SQLか？NoSQLか？

<p align="center">
  <img src="http://i.imgur.com/wXGqG5f.png"/>
  <br/>
  <i><a href=https://www.infoq.com/articles/Transition-RDBMS-NoSQL/>Source: Transitioning from RDBMS to NoSQL</a></i>
</p>

**SQL** を選ぶ理由:

* 構造化されたデータ
* 厳格なスキーマ
* リレーショナルデータ
* 複雑なジョインをする必要性
* トランザクション
* スケールする際のパターンが明確なとき
* 開発者の数、コミュニティ、コード等がより充実している
* インデックスによるデータ探索はとても速い

**NoSQL** を選ぶ理由:

* 準構造化されたデータ
* ダイナミックないし、フレキシブルなスキーマ
* ノンリレーショナルなデータ
* 複雑なジョインをする必要がない
* データの多くのTB (もしくは PB) を保存する
* 集中的、大規模なデータ負荷に耐えられる
* IOPSについては極めて高いスループットを示す

NoSQLに適するサンプルデータ:

* 急激なクリックストリームやログデータの収集
* リーダーボードやスコアリングデータ
* ショッピングカートなどの一時的情報
* 頻繁にアクセスされる ('ホットな') テーブル
* メタデータやルックアップテーブル

##### その他の参考資料、ページ:  　SQLもしくはNoSQL

* [最初の1000万ユーザーにスケールアップするために](https://www.youtube.com/watch?v=w95murBkYmU)
* [SQLとNoSQLの違い](https://www.sitepoint.com/sql-vs-nosql-differences/)

## キャッシュ

<p align="center">
  <img src="http://i.imgur.com/Q6z24La.png"/>
  <br/>
  <i><a href=http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html>Source: Scalable system design patterns</a></i>
</p>

キャッシュはページの読み込み時間を削減し、サーバーやデータベースへの負荷を低減することができます。このモデルでは、実際の処理を保存するために、ディスパッチャーがまず以前にリクエストが送信されたかどうかを確認し、直前の結果を受け取ります。

データベースはそのパーティションに渡って統合された読み取り書き込みの分配を要求しますが、人気アイテムはその分配を歪めてシステム全体のボトルネックになってしまうことがあります。データベースの前にキャッシュを差し込むことでこのように、均一でない負荷やトラフィックの急激な増加を吸収することができます。

### クライアントキャッシング

キャッシュはOSやブラウザーなどのクライアントサイド、[サーバーサイド](#リバースプロキシwebサーバー) もしくは独立のキャッシュレイヤーに設置することができます。

### CDNキャッシング

[CDN](#コンテンツデリバリーネットワークcontent-delivery-network) もキャッシュの一つとして考えることができます。

### Webサーバーキャッシング

[リバースプロキシ](#リバースプロキシwebサーバー) や [Varnish](https://www.varnish-cache.org/) などのキャッシュは静的そして動的なコンテンツを直接配信することができます。 webサーバーもリクエストをキャッシュしてアプリケーションサーバーに接続することなしにレスポンスを返すことができます。

### データベースキャッシング

データベースは普通、一般的な使用状況に適するようなキャッシングの設定を初期状態で持っています。この設定を特定の仕様に合わせて調整することでパフォーマンスを向上させることができます。

### アプリケーションキャッシング

メムキャッシュなどのIn-memoryキャッシュやRedisはアプリケーションとデータストレージの間のキーバリューストアです。データはRAMで保持されるため、データがディスクで保存される一般的なデータベースよりもだいぶ速いです。RAM容量はディスクよりも限られているので、[least recently used (LRU)](https://en.wikipedia.org/wiki/Cache_algorithms#Least_Recently_Used)などの[cache invalidation](https://en.wikipedia.org/wiki/Cache_algorithms) アルゴリズムが 'コールド' なエントリを弾き、'ホット' なデータをRAMに保存します。

Redisはさらに以下のような機能を備えています:

* パージステンス設定
* ソート済みセット、リストなどの組み込みデータ構造

キャッシュには様々なレベルのものがありますが、いずれも大きく二つのカテゴリーのいずれかに分類することができます: **データベースクエリ** と **オブジェクト** です:

* 行レベル
* クエリレベル
* Fully-formed serializable objects
* Fully-rendered HTML

一般的に、ファイルベースキャッシングはクローンを作り出してオートスケーリングを難しくしてしまうので避けるべきです。

### データベースクエリレベルでのキャッシング

データベースをクエリする際には必ずクエリをキーとしてハッシュして結果をキャッシュに保存しましょう。この手法はキャッシュ期限切れ問題に悩むことになります:

* 複雑なクエリによりキャッシュされた結果を削除することが困難
* テーブルセルなどのデータ断片が変化した時に、その変化したセルを含むかもしれない全てのキャッシュされたクエリを削除する必要がある。

### オブジェクトレベルでのキャッシング

データをアプリケーションコードでそうするように、オブジェクトとして捉えてみましょう。アプリケーションに、データベースからのデータセットをクラスインスタンスやデータ構造として組み立てさせます。:

* そのデータが変更されたら、オブジェクトをキャッシュから削除すること
* 非同期処理を許容します: ワーカーがキャッシュされたオブジェクトの中で最新のものを集めてきます

何をキャッシュするか:

* ユーザーのセッション
* 完全にレンダーされたウェブページ
* アクテビティストリーム
* ユーザーグラフデータ

### いつキャッシュを更新するか

キャッシュに保存できる容量は限られているため、自分のケースではどのキャッシュ手法が一番いいかは検討する必要があります。

#### キャッシュアサイド

<p align="center">
  <img src="http://i.imgur.com/ONjORqk.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/tmatyashovsky/from-cache-to-in-memory-data-grid-introduction-to-hazelcast>Source: From cache to in-memory data grid</a></i>
</p>

アプリケーションはストレージへの読み書きの処理をします。キャッシュはストレージとは直接やりとりをしません。アプリケーションは以下のことをします:

* キャッシュの中のエントリを参照しますが、結果としてキャッシュミスになります
* データベースからエントリを取得します
* エントリをキャッシュに追加します
* エントリを返します

```python
def get_user(self, user_id):
    user = cache.get("user.{0}", user_id)
    if user is None:
        user = db.query("SELECT * FROM users WHERE user_id = {0}", user_id)
        if user is not None:
            key = "user.{0}".format(user_id)
            cache.set(key, json.dumps(user))
    return user
```

[Memcached](https://memcached.org/) は通常このように使われる。

その後のキャッシュデータ読み込みは速いです。キャッシュアサイドはレージーローディングであるとも言われます。リクエストされたデータのみがキャッシュされ、リクエストされていないデータでキャッシュが溢れるのを防止します。

##### 欠点: キャッシュアサイド

* 各キャッシュミスは三つのトリップを呼び出すことになり、体感できるほどの遅延が起きてしまいます。
* データベースのデータが更新されるとキャッシュデータは古いものになってしまいます。time-to-live (TTL)を設定することでキャッシュエントリの更新を強制的に行う、もしくはライトスルーを採用することでこの問題は緩和できます。
* ノードが落ちると、新規の空のノードで代替されることでレイテンシーが増加することになります。

#### ライトスルー

<p align="center">
  <img src="http://i.imgur.com/0vBc0hN.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>Source: Scalability, availability, stability, patterns</a></i>
</p>

アプリケーションはキャッシュをメインのデータストアとして使い、そこにデータの読み書きを行います。一方、キャッシュはデータベースへの読み書きを担当します。

* アプリケーションはキャッシュにあるエントリを追加・更新します
* キャッシュは同期的にデータストアに書き込みを行います
* エントリを返します

アプリケーションコード:

```
set_user(12345, {"foo":"bar"})
```

キャッシュコード:

```python
def set_user(user_id, values):
    user = db.query("UPDATE Users WHERE id = {0}", user_id, values)
    cache.set(user_id, user)
```

ライトスルーは書き込み処理のせいで全体としては遅いオペレーションですが、書き込まれたばかりのデータに関する読み込みは速いです。ユーザー側は一般的にデータ更新時の方が読み込み時よりもレイテンシーに許容的です。キャッシュ内のデータは最新版で保たれます。

##### 欠点: ライトスルー

* ノードが落ちたこと、もしくはスケーリングによって新しいノードが作成された時に、新しいノードはデータベース内のエントリーが更新されるまではエントリーをキャッシュしません。キャッシュアサイドとライトスルーを併用することでこの問題を緩和できます。
* 書き込まれたデータの大部分は一度も読み込まれることはありません。このデータはTTLによって圧縮することができます。

#### ライトビハインド (ライトバック)

<p align="center">
  <img src="http://i.imgur.com/rgSrvjG.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>Source: Scalability, availability, stability, patterns</a></i>
</p>

ライトビハインドではアプリケーションは以下のことをします:

* キャッシュのエントリーを追加・更新します
* データストアへの書き込みを非同期的に行うことで、書き込みパフォーマンスを向上させます。

##### 欠点: ライトビハインド

* キャッシュがデータストア内のコンテンツにヒットする前にキャッシュが落ちるとデータ欠損が起きる可能性があります。
* キャッシュアサイドやライトスルーよりも実装が複雑になります。

#### リフレッシュアヘッド

<p align="center">
  <img src="http://i.imgur.com/kxtjqgE.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/tmatyashovsky/from-cache-to-in-memory-data-grid-introduction-to-hazelcast>Source: From cache to in-memory data grid</a></i>
</p>

期限切れよりも前に、直近でアクセスされた全てのキャッシュエントリを自動的に更新するように設定することができます。

もしどのアイテムが将来必要になるのかを正確に予測することができるのならば、リードスルーよりもレイテンシーを削減することができます。

##### 欠点: リフレッシュアヘッド

* どのアイテムが必要になるかの予測が正確でない場合にはリフレッシュアヘッドがない方がレイテンシーは良いという結果になってしまいます。

### 欠点: キャッシュ

* [cache invalidation](https://en.wikipedia.org/wiki/Cache_algorithms)などを用いて、データベースなどの真のデータとキャッシュの間の一貫性を保つ必要があります。
* Redisやmemcachedを追加することでアプリケーション構成を変更する必要があります。
* Cache invalidationも難しいですがそれに加えて、いつキャッシュを更新するかという複雑な問題にも悩まされることになります。

### その他の参考資料、ページ

* [From cache to in-memory data grid](http://www.slideshare.net/tmatyashovsky/from-cache-to-in-memory-data-grid-introduction-to-hazelcast)
* [スケーラブルなシステムデザインパターン](http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html)
* [スケールできるシステムを設計するためのイントロダクション](http://lethain.com/introduction-to-architecting-systems-for-scale/)
* [スケーラビリティ、可用性、安定性、パターン](http://www.slideshare.net/jboner/scalability-availability-stability-patterns/)
* [スケーラビリティ](http://www.lecloud.net/post/9246290032/scalability-for-dummies-part-3-cache)
* [AWS ElastiCacheのストラテジー](http://docs.aws.amazon.com/AmazonElastiCache/latest/UserGuide/Strategies.html)
* [Wikipedia](https://en.wikipedia.org/wiki/Cache_(computing))

## 非同期処理

<p align="center">
  <img src="http://i.imgur.com/54GYsSx.png"/>
  <br/>
  <i><a href=http://lethain.com/introduction-to-architecting-systems-for-scale/#platform_layer>Source: Intro to architecting systems for scale</a></i>
</p>

非同期のワークフローはもし、連続的に行われるとリクエスト時間を圧迫してしまうような重い処理を別で処理する手法です。また、定期的にデータを集合させるなどの時間がかかるような処理を前もって処理しておくことにも役立ちます。

### メッセージキュー

メッセージキューはメッセージを受け取り、保存し、配信します。もし、処理がインラインで行うには遅すぎる場合、以下のようなワークフローでメッセージキューを用いるといいでしょう:

* アプリケーションはジョブをキューに配信し、ユーザーにジョブステータスを伝えます。
* ワーカーがジョブキューから受け取って、処理を行い、終了したらそのシグナルを返します。

ユーザーの処理が止まることはなく、ジョブはバックグラウンドで処理されます。この間に、クライアントはオプションとして、タスクが完了したかのように見せるために小規模の処理を行います。例えば、ツイートを投稿するときに、ツイートはすぐにあなたのタイムラインに反映されたように見えますが、そのツイートが実際に全てのフォロワーに配信されるまでにはもう少し時間がかかっているでしょう。

**Redis** はシンプルなメッセージ仲介としてはいいですが、メッセージが失われてしまう可能性があります。

**RabbitMQ** はよく使われていますが、'AMQP'プロトコルに対応して、自前のノードを立てる必要があります。

**Amazon SQS** という選択肢もありますが、レイテンシーが高く、メッセージが重複して配信されてしまう可能性があります。

### タスクキュー

タスクキューはタスクとその関連するデータを受け取り、処理した上でその結果を返します。スケジュール管理をできるほか、バックグラウンドでとても重いジョブをこなすこともできます。

**Celery** はスケジューリングとpythonのサポートがあります。

### バックプレッシャー

もし、キューが拡大しすぎると、メモリーよりもキューの方が大きくなりキャッシュミスが起こり、ディスク読み出しにつながり、パフォーマンスが低下することにつながります。[バックプレッシャー](http://mechanical-sympathy.blogspot.com/2012/05/apply-back-pressure-when-overloaded.html)はキューサイズを制限することで回避することができ、高いスループットを確保しキューにすでにあるジョブについてのレスポンス時間を短縮できます。キューがいっぱいになると、クライアントはサーバービジーもしくはHTTP 503をレスポンスとして受け取りまた後で時間をおいてアクセスするようにメッセージを受け取ります。クライアントは[exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff)などによって後ほど再度時間を置いてリクエストすることができます。

### 欠点: 非同期処理

* キューを用いることで遅延が起こり、複雑さも増すため、あまり重くない計算処理やリアルタイムワークフローにおいては同期処理の方がいいでしょう。

### その他の参考資料、ページ

* [It's all a numbers game](https://www.youtube.com/watch?v=1KRYH75wgy4)
* [オーバーロードした時にバックプレッシャーを適用する](http://mechanical-sympathy.blogspot.com/2012/05/apply-back-pressure-when-overloaded.html)
* [Little's law](https://en.wikipedia.org/wiki/Little%27s_law)
* [メッセージキューとタスクキューの違いとは？](https://www.quora.com/What-is-the-difference-between-a-message-queue-and-a-task-queue-Why-would-a-task-queue-require-a-message-broker-like-RabbitMQ-Redis-Celery-or-IronMQ-to-function)

## 通信

<p align="center">
  <img src="http://i.imgur.com/5KeocQs.jpg"/>
  <br/>
  <i><a href=http://www.escotal.com/osilayer.html>Source: OSI 7 layer model</a></i>
</p>

### Hypertext transfer protocol (HTTP)

HTTP はクライアントとサーバー間でのデータをエンコードして転送するための手法です。リクエスト・レスポンスに関わるプロトコルです。クライアントがリクエストをサーバーに投げ、サーバーがリクエストに関係するコンテンツと完了ステータス情報をレスポンスとして返します。HTTPは自己完結するので、間にロードバランサー、キャッシュ、エンクリプション、圧縮などのどんな中間ルーターが入っても動くようにできています。

基本的なHTTPリクエストはHTTP動詞(メソッド)とリソース(エンドポイント)で成り立っています。以下がよくあるHTTP動詞です。:

| 動詞 | 詳細 | 冪等性* | セーフ | キャッシュできるか |
|---|---|---|---|---|
| GET | リソースを読み取る | Yes | Yes | Yes |
| POST | リソースを作成するもしくはデータを処理するトリガー | No | No | Yes レスポンスが新しい情報を含む場合 |
| PUT | リソースを作成もしくは入れ替える | Yes | No | No |
| PATCH | リソースを部分的に更新する | No | No | Yes レスポンスが新しい情報を含む場合 |
| DELETE | リソースを削除する | Yes | No | No |

*何度呼んでも同じ結果が返ってくること*

HTTPは**TCP** や **UDP** などの低級プロトコルに依存しているアプリケーションレイヤーのプロトコルである。

#### その他の参考資料、ページ: HTTP

* [HTTPってなに?](https://www.nginx.com/resources/glossary/http/)
* [HTTP と TCPの違い](https://www.quora.com/What-is-the-difference-between-HTTP-protocol-and-TCP-protocol)
* [PUT と PATCHの違い](https://laracasts.com/discuss/channels/general-discussion/whats-the-differences-between-put-and-patch?page=1)

### 伝送制御プロトコル (TCP)

<p align="center">
  <img src="http://i.imgur.com/JdAsdvG.jpg"/>
  <br/>
  <i><a href=http://www.wildbunny.co.uk/blog/2012/10/09/how-to-make-a-multi-player-game-part-1/>Source: How to make a multiplayer game</a></i>
</p>

TCPは[IP network](https://en.wikipedia.org/wiki/Internet_Protocol)の上で成り立つ接続プロトコルです。接続は[handshake](https://en.wikipedia.org/wiki/Handshaking)によって開始、解除されます。全ての送信されたパケットは欠損なしで送信先に送信された順番で到達するように以下の方法で保証されています:

* シーケンス番号と[checksum fields](https://en.wikipedia.org/wiki/Transmission_Control_Protocol#Checksum_computation)が全てのパケットに用意されている
* [Acknowledgement](https://en.wikipedia.org/wiki/Acknowledgement_(data_networks))パケットと自動再送信

もし送信者が正しいレスポンスを受け取らなかったとき、パケットを再送信します。複数のタイムアウトがあったとき、接続は解除されます。TCP は[フロー制御](https://en.wikipedia.org/wiki/Flow_control_(data)) と [輻輳制御](https://en.wikipedia.org/wiki/Network_congestion#Congestion_control)も実装しています。これらの機能によって速度は低下し、一般的にUDPよりも非効率な転送手段になっています。

ハイスループットを実現するために、ウェブサーバーはかなり大きな数のTCP接続を開いておくことがあり、そのことでメモリー使用が圧迫されます。ウェブサーバスレッドと例えば[memcached](#memcached) サーバーの間で多数のコネクションを保っておくことは高くつくかもしれません。可能なところではUDPに切り替えるだけでなく[コネクションプーリング](https://en.wikipedia.org/wiki/Connection_pool)なども役立つかもしれません。

TCPは高い依存性を要し、時間制約が厳しくないものに適しているでしょう。ウェブサーバー、データベース情報、SMTP、FTPやSSHなどの例に適用されます。

以下の時にUDPよりもTCPを使うといいでしょう:

* 全てのデータが欠損することなしに届いてほしい
* ネットワークスループットの最適な自動推測をしてオペレーションしたい

### ユーザデータグラムプロトコル (UDP)

<p align="center">
  <img src="http://i.imgur.com/yzDrJtA.jpg"/>
  <br/>
  <i><a href=http://www.wildbunny.co.uk/blog/2012/10/09/how-to-make-a-multi-player-game-part-1/>Source: How to make a multiplayer game</a></i>
</p>

UDPはコネクションレスです。データグラム（パケットのようなもの）はデータグラムレベルでの保証しかされません。データグラムは順不同で受け取り先に到着したりそもそも着かなかったりします。UDPは輻輳制御をサポートしません。TCPにおいてはサポートされているこれらの保証がないため、UDPは一般的に、TCPよりも効率的です。

UDPはサブネット上のすべての機器にデータグラムを送信することができます。これは[DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol) において役に立ちます。というのも、クライアントはまだIPアドレスを取得していないので、IPアドレスを必要とするTCPによるストリームができないからです。

UDPは信頼性の面では劣りますが、VoIP、ビデオチャット、ストリーミングや同時通信マルチプレイヤーゲームなどのリアルタイム性が重視される時にはとても効果的です。

TCPよりもUDPを使うのは:

* レイテンシーを最低限に抑えたい時
* データ欠損よりも、データ遅延を重視するとき
* エラー修正を自前で実装したいとき

#### その他の参考資料、ページ: TCP と UDP

* [ゲームプログラミングのためのネットワーク](http://gafferongames.com/networking-for-game-programmers/udp-vs-tcp/)
* [TCP と UDP プロトコルの主な違い](http://www.cyberciti.biz/faq/key-differences-between-tcp-and-udp-protocols/)
* [TCP と UDPの違い](http://stackoverflow.com/questions/5970383/difference-between-tcp-and-udp)
* [Transmission control protocol](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)
* [User datagram protocol](https://en.wikipedia.org/wiki/User_Datagram_Protocol)
* [Facebookのメムキャッシュスケーリング](http://www.cs.bu.edu/~jappavoo/jappavoo.github.com/451/papers/memcache-fb.pdf)

### 遠隔手続呼出 (RPC)

<p align="center">
  <img src="http://i.imgur.com/iF4Mkb5.png"/>
  <br/>
  <i><a href=http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview>Source: Crack the system design interview</a></i>
</p>

RPCではクライアントがリモートサーバーなどの異なるアドレス空間でプロシージャーが処理されるようにします。プロシージャーはローカルでのコールのように、クライアントからサーバーにどのように通信するかという詳細を省いた状態でコードが書かれます。リモートのコールは普通、ローカルのコールよりも遅く、信頼性に欠けるため、RPCコールをローカルコールと区別させておくことが好ましいでしょう。人気のRPCフレームワークは以下です。[Protobuf](https://developers.google.com/protocol-buffers/)、 [Thrift](https://thrift.apache.org/)、[Avro](https://avro.apache.org/docs/current/)

RPC は リクエストレスポンスプロトコル:

* **クライアントプログラム** - クライアントスタブプロシージャーを呼び出します。パラメータはローカルでのプロシージャーコールのようにスタックへとプッシュされていきます。
* **クライアントスタブプロシージャー** - プロシージャIDとアーギュメントをパックしてリクエストメッセージにします。
* **クライアント通信モジュール** - OSがクライアントからサーバーへとメッセージを送ります。
* **サーバー通信モジュール** - OSが受け取ったパケットをサーバースタブプロシージャーに受け渡します。
* **サーバースタブプロシージャー** -  結果を展開し、プロシージャーIDにマッチするサーバープロシージャーを呼び出し、結果を返します。
* サーバーレスポンスは上記のステップを逆順で繰り返します。

Sample RPC calls:

```
GET /someoperation?data=anId

POST /anotheroperation
{
  "data":"anId";
  "anotherdata": "another value"
}
```

RPCは振る舞いを公開することに焦点を当てています。RPCは内部通信パフォーマンスを理由として使われることが多いです。というのも、使用する状況に合わせてネイティブコールを自作することができるからです。

ネイティブライブラリー (aka SDK) を呼ぶのは以下の時:

* ターゲットのプラットフォームを知っている時
* ロジックがどのようにアクセスされるのかを管理したいとき
* ライブラリー外でエラーがどのようにコントロールされるかを管理したい時
* パフォーマンスとエンドユーザーエクスペリエンスが最優先の時

**REST** プロトコルに従うHTTP APIはパブリックAPIにおいてよく用いられます。

#### 欠点: RPC

* RPCクライアントとはサービス実装により厳密に左右されることになります。
* 新しいオペレーション、使用例があるたびに新しくAPIが定義されなければなりません。
* RPCをデバッグするのは難しい可能性があります。
* 既存のテクノロジーをそのまま使ってサービスを構築することはできないかもしれません。例えば、[Squid](http://www.squid-cache.org/)などのサーバーに[RPCコールが正しくキャッシュ](http://etherealbits.com/2012/12/debunking-the-myths-of-rpc-rest/) されるように追加で骨を折る必要があるかもしれません。

### Representational state transfer (REST)

RESTは、クライアントがサーバーによってマネージされるリソースに対して処理を行うクライアント・サーバーモデルを支持するアーキテキチャスタイルです。サーバーは操作できるもしくは新しいリソースレプレゼンテーションを受け取ることができるようなリソースやアクションのレプレゼンテーションを提供します。すべての通信はステートレスでキャッシュ可能でなければなりません。

RESTful なインターフェースには次の四つの特徴があります:

* **特徴的なリソース (URI in HTTP)** - どのオペレーションであっても同じURIを使う。
* **HTTP動詞によって変わる (Verbs in HTTP)** - 動詞、ヘッダー、ボディを使う
* **自己説明的なエラーメッセージ (status response in HTTP)** - ステータスコードを使い、新しく作ったりしないこと。
* **[HATEOAS](http://restcookbook.com/Basics/hateoas/) (HTML interface for HTTP)** - 自分のwebサービスがブラウザで完全にアクセスできること。

サンプル REST コール:

```
GET /someresources/anId

PUT /someresources/anId
{"anotherdata": "another value"}
```

RESTはデータを公開することに焦点を当てています。クライアントとサーバーのカップリングを最小限にするもので、パブリックAPIなどによく用いられます。RESTはURI、 [representation through headers](https://github.com/for-GET/know-your-http-well/blob/master/headers.md)、そして、GET、POST、PUT、 DELETE、PATCHなどのHTTP動詞等のよりジェネリックで統一されたメソッドを用います。ステートレスであるのでRESTは水平スケーリングやパーティショニングに最適です。

#### 欠点: REST

* RESTはデータ公開に焦点を当てているので、リソースが自然に整理されていなかったり、シンプルなヒエラルキーで表せられない時にはよい選択肢とは言えないかもしれません。例えば、とあるイベントのセットにマッチするすべての更新情報を返すと言った処理は簡単にはパスで表現することができません。RESTでは、URIパス、クエリパラメータ、そして場合によってはリクエストボディなどによって実装されることが多いでしょう。
* RESTは少数の動詞に依存しています(GET、POST、PUT、DELETE、そして PATCH) が時には使いたい事例に合わないことがあります。例えば、期限の切れたドキュメントをアーカイブに移したい場合などはこれらの動詞の中には綺麗にはフィットしません。
* ネストされたヒエラルキーの中にあるリソースをとってくるのはシングルビューを描画するのにクライアントとサーバー間で数回やりとりしなければなりません。例として、ブログエントリーのコンテンツとそれに対するコメントを表示する場合などです。様々なネットワーク環境で動作する可能性が考えられるモバイルアプリケーションにおいてはこのような複数のやり取りは好ましくありません。
* 時が経つにつれて、APIレスポンスにより多くのフィールドが与えられて、古いクライアントはすでにいらないものも含めてすべてのデータフィールドを受け取ることになります。そのことで、ペイロードが大きくなりすぎて、レイテンシーも拡大することになります。

### RPCとREST比較

| Operation | RPC | REST |
|---|---|---|
| サインアップ	| **POST** /signup | **POST** /persons |
| リザイン	| **POST** /resign<br/>{<br/>"personid": "1234"<br/>} | **DELETE** /persons/1234 |
| Person読み込み | **GET** /readPerson?personid=1234 | **GET** /persons/1234 |
| Personのアイテムリスト読み込み | **GET** /readUsersItemsList?personid=1234 | **GET** /persons/1234/items |
| Personのアイテムへのアイテム追加 | **POST** /addItemToUsersItemsList<br/>{<br/>"personid": "1234";<br/>"itemid": "456"<br/>} | **POST** /persons/1234/items<br/>{<br/>"itemid": "456"<br/>} |
| アイテム更新	| **POST** /modifyItem<br/>{<br/>"itemid": "456";<br/>"key": "value"<br/>} | **PUT** /items/456<br/>{<br/>"key": "value"<br/>} |
| アイテム削除 | **POST** /removeItem<br/>{<br/>"itemid": "456"<br/>} | **DELETE** /items/456 |

<p align="center">
  <i><a href=https://apihandyman.io/do-you-really-know-why-you-prefer-rest-over-rpc/>Source: Do you really know why you prefer REST over RPC</a></i>
</p>

#### その他の参考資料、ページ: REST と RPC

* [Do you really know why you prefer REST over RPC](https://apihandyman.io/do-you-really-know-why-you-prefer-rest-over-rpc/)
* [When are RPC-ish approaches more appropriate than REST?](http://programmers.stackexchange.com/a/181186)
* [REST vs JSON-RPC](http://stackoverflow.com/questions/15056878/rest-vs-json-rpc)
* [Debunking the myths of RPC and REST](http://etherealbits.com/2012/12/debunking-the-myths-of-rpc-rest/)
* [What are the drawbacks of using REST](https://www.quora.com/What-are-the-drawbacks-of-using-RESTful-APIs)
* [Crack the system design interview](http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview)
* [Thrift](https://code.facebook.com/posts/1468950976659943/)
* [Why REST for internal use and not RPC](http://arstechnica.com/civis/viewtopic.php?t=1190508)

## セキュリティ

このセクションは更新が必要です。[contributing](#contributing)してください！

セキュリティは幅広いトピックです。十分な経験、セキュリティ分野のバックグラウンドがなくても、セキュリティの知識を要する職に応募するのでない限り、基本以上のことを知る必要はないでしょう。

* 情報伝達、保存における暗号化
* [XSS](https://en.wikipedia.org/wiki/Cross-site_scripting) や [SQL injection](https://en.wikipedia.org/wiki/SQL_injection)を防ぐために、全てのユーザー入力もしくはユーザーに露出される入力パラメーターをサニタイズする
* SQL injectionを防ぐためにパラメータ化されたクエリを用いる。
* [least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege)の原理を用いる

### その他の参考資料、ページ:

* [開発者のためのセキュリティガイド](https://github.com/FallibleInc/security-guide-for-developers)
* [OWASP top ten](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet)

## 補遺

暗算で、推計値を求める必要があることも時にはあります。例えば、ディスクから100枚イメージ分のサムネイルを作る時間を求めたり、その時にどれだけディスクメモリーが消費されるかなどの値です。**2の乗数表** と **全てのプログラマーが知るべきレイテンシー値** は良い参考になるでしょう。

### 2の乗数表

```
乗数           厳密な値         約        Bytes
---------------------------------------------------------------
7                             128
8                             256
10                           1024   1 thousand           1 KB
16                         65,536                       64 KB
20                      1,048,576   1 million            1 MB
30                  1,073,741,824   1 billion            1 GB
32                  4,294,967,296                        4 GB
40              1,099,511,627,776   1 trillion           1 TB
```

#### その他の参考資料、ページ:

* [2の乗数表](https://en.wikipedia.org/wiki/Power_of_two)

### 全てのプログラマーが知るべきレイテンシー値

```
Latency Comparison Numbers
--------------------------
L1 cache reference                           0.5 ns
Branch mispredict                            5   ns
L2 cache reference                           7   ns                      14x L1 cache
Mutex lock/unlock                           25   ns
Main memory reference                      100   ns                      20x L2 cache, 200x L1 cache
Compress 1K bytes with Zippy            10,000   ns       10 us
Send 1 KB bytes over 1 Gbps network     10,000   ns       10 us
Read 4 KB randomly from SSD*           150,000   ns      150 us          ~1GB/sec SSD
Read 1 MB sequentially from memory     250,000   ns      250 us
Round trip within same datacenter      500,000   ns      500 us
Read 1 MB sequentially from SSD*     1,000,000   ns    1,000 us    1 ms  ~1GB/sec SSD, 4X memory
Disk seek                           10,000,000   ns   10,000 us   10 ms  20x datacenter roundtrip
Read 1 MB sequentially from 1 Gbps  10,000,000   ns   10,000 us   10 ms  40x memory, 10X SSD
Read 1 MB sequentially from disk    30,000,000   ns   30,000 us   30 ms 120x memory, 30X SSD
Send packet CA->Netherlands->CA    150,000,000   ns  150,000 us  150 ms

Notes
-----
1 ns = 10^-9 seconds
1 us = 10^-6 seconds = 1,000 ns
1 ms = 10^-3 seconds = 1,000 us = 1,000,000 ns
```

上記表に基づいた役に立つ数値:

* ディスクからの連続読み取り速度 30 MB/s
* 1 Gbps Ethernetからの連続読み取り速度　100 MB/s
* SSDからの連続読み取り速度 1 GB/s
* main memoryからの連続読み取り速度 4 GB/s
* 1秒で地球6-7周できる
* 1秒でデータセンターと2000周やりとりできる

#### レイテンシーの視覚的表

![](https://camo.githubusercontent.com/77f72259e1eb58596b564d1ad823af1853bc60a3/687474703a2f2f692e696d6775722e636f6d2f6b307431652e706e67)

#### その他の参考資料、ページ:

* [全てのプログラマーが知るべきレイテンシー値 - 1](https://gist.github.com/jboner/2841832)
* [全てのプログラマーが知るべきレイテンシー値 - 2](https://gist.github.com/hellerbarde/2843375)
* [Designs, lessons, and advice from building large distributed systems](http://www.cs.cornell.edu/projects/ladis2009/talks/dean-keynote-ladis2009.pdf)
* [Software Engineering Advice from Building Large-Scale Distributed Systems](https://static.googleusercontent.com/media/research.google.com/en//people/jeff/stanford-295-talk.pdf)

### 他のシステム設計面接例題

> 頻出のシステム設計面接課題とその解答へのリンク

| 質問 | 解答 |
|---|---|
| Dropboxのようなファイル同期サービスを設計する | [youtube.com](https://www.youtube.com/watch?v=PE4gwstWhmc) |
| Googleのような検索エンジンの設計 | [queue.acm.org](http://queue.acm.org/detail.cfm?id=988407)<br/>[stackexchange.com](http://programmers.stackexchange.com/questions/38324/interview-question-how-would-you-implement-google-search)<br/>[ardendertat.com](http://www.ardendertat.com/2012/01/11/implementing-search-engines/)<br/>[stanford.edu](http://infolab.stanford.edu/~backrub/google.html) |
| Googleのようなスケーラブルなwebクローラーの設計 | [quora.com](https://www.quora.com/How-can-I-build-a-web-crawler-from-scratch) |
| Google docsの設計 | [code.google.com](https://code.google.com/p/google-mobwrite/)<br/>[neil.fraser.name](https://neil.fraser.name/writing/sync/) |
| Redisのようなキーバリューストアの設計 | [slideshare.net](http://www.slideshare.net/dvirsky/introduction-to-redis) |
| Memcachedのようなキャッシュシステムの設計 | [slideshare.net](http://www.slideshare.net/oemebamo/introduction-to-memcached) |
| Amazonのようなレコメンデーションシステムの設計 | [hulu.com](http://tech.hulu.com/blog/2011/09/19/recommendation-system.html)<br/>[ijcai13.org](http://ijcai13.org/files/tutorial_slides/td3.pdf) |
| BitlyのようなURL短縮サービスの設計 | [n00tc0d3r.blogspot.com](http://n00tc0d3r.blogspot.com/) |
| WhatsAppのようなチャットアプリの設計 | [highscalability.com](http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html)
| Instagramのような写真共有サービスの設計 | [highscalability.com](http://highscalability.com/flickr-architecture)<br/>[highscalability.com](http://highscalability.com/blog/2011/12/6/instagram-architecture-14-million-users-terabytes-of-photos.html) |
| Facebookニュースフィードの設計 | [quora.com](http://www.quora.com/What-are-best-practices-for-building-something-like-a-News-Feed)<br/>[quora.com](http://www.quora.com/Activity-Streams/What-are-the-scaling-issues-to-keep-in-mind-while-developing-a-social-network-feed)<br/>[slideshare.net](http://www.slideshare.net/danmckinley/etsy-activity-feeds-architecture) |
| Facebookタイムラインの設計 | [facebook.com](https://www.facebook.com/note.php?note_id=10150468255628920)<br/>[highscalability.com](http://highscalability.com/blog/2012/1/23/facebook-timeline-brought-to-you-by-the-power-of-denormaliza.html) |
| Facebookチャットの設計 | [erlang-factory.com](http://www.erlang-factory.com/upload/presentations/31/EugeneLetuchy-ErlangatFacebook.pdf)<br/>[facebook.com](https://www.facebook.com/note.php?note_id=14218138919&id=9445547199&index=0) |
| Facebookのようなgraph検索の設計 | [facebook.com](https://www.facebook.com/notes/facebook-engineering/under-the-hood-building-out-the-infrastructure-for-graph-search/10151347573598920)<br/>[facebook.com](https://www.facebook.com/notes/facebook-engineering/under-the-hood-indexing-and-ranking-in-graph-search/10151361720763920)<br/>[facebook.com](https://www.facebook.com/notes/facebook-engineering/under-the-hood-the-natural-language-interface-of-graph-search/10151432733048920) |
| CloudFlareのようなCDNの設計 | [cmu.edu](http://repository.cmu.edu/cgi/viewcontent.cgi?article=2112&context=compsci) |
| Twitterのトレンド機能の設計 | [michael-noll.com](http://www.michael-noll.com/blog/2013/01/18/implementing-real-time-trending-topics-in-storm/)<br/>[snikolov .wordpress.com](http://snikolov.wordpress.com/2012/11/14/early-detection-of-twitter-trends/) |
| ランダムID発行システムの設計 | [blog.twitter.com](https://blog.twitter.com/2010/announcing-snowflake)<br/>[github.com](https://github.com/twitter/snowflake/) |
| 一定のインターバル時間での上位k件を返す | [ucsb.edu](https://icmi.cs.ucsb.edu/research/tech_reports/reports/2005-23.pdf)<br/>[wpi.edu](http://davis.wpi.edu/xmdv/docs/EDBT11-diyang.pdf) |
| 複数のデータセンターからデータを配信するサービスの設計 | [highscalability.com](http://highscalability.com/blog/2009/8/24/how-google-serves-data-from-multiple-datacenters.html) |
| オンラインの複数プレイヤーカードゲームの設計 | [indieflashblog.com](http://www.indieflashblog.com/how-to-create-an-asynchronous-multiplayer-game.html)<br/>[buildnewgames.com](http://buildnewgames.com/real-time-multiplayer/) |
| ガーベッジコレクションシステムの設計 | [stuffwithstuff.com](http://journal.stuffwithstuff.com/2013/12/08/babys-first-garbage-collector/)<br/>[washington.edu](http://courses.cs.washington.edu/courses/csep521/07wi/prj/rick.pdf) |
| システム設計例題を追加する | [Contribute](#contributing) |

### 実世界のアーキテクチャ

> 世の中のシステムがどのように設計されているかについての記事

<p align="center">
  <img src="http://i.imgur.com/TcUo2fw.png"/>
  <br/>
  <i><a href=https://www.infoq.com/presentations/Twitter-Timeline-Scalability>Source: Twitter timelines at scale</a></i>
</p>

**以下の記事の重箱の隅をつつくような細かい詳細にこだわらないこと。むしろ**

* 共通の原理、技術、パターンを探ること
* それぞれのコンポーネントでどんな問題が解決され、コンポーネントはどこでうまく使えもしくは使えないかを知ること
* 学んだことを復習すること

|種類 | システム | 参考ページ |
|---|---|---|
| データ処理 | **MapReduce** - Googleの分散データ処理システム | [research.google.com](http://static.googleusercontent.com/media/research.google.com/zh-CN/us/archive/mapreduce-osdi04.pdf) |
| データ処理 | **Spark** - Databricksの分散データ処理システム | [slideshare.net](http://www.slideshare.net/AGrishchenko/apache-spark-architecture) |
| データ処理 | **Storm** - Twitterの分散データ処理システム | [slideshare.net](http://www.slideshare.net/previa/storm-16094009) |
| | | |
| データストア | **Bigtable** - Googleのカラム指向分散データベース | [harvard.edu](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/chang06bigtable.pdf) |
| データストア | **HBase** - Bigtableのオープンソース実装 | [slideshare.net](http://www.slideshare.net/alexbaranau/intro-to-hbase) |
| データストア | **Cassandra** - Facebookのカラム指向分散データベース | [slideshare.net](http://www.slideshare.net/planetcassandra/cassandra-introduction-features-30103666)
| データストア | **DynamoDB** - Amazonのドキュメント指向分散データベース | [harvard.edu](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/decandia07dynamo.pdf) |
| データストア | **MongoDB** - ドキュメント指向分散データベース | [slideshare.net](http://www.slideshare.net/mdirolf/introduction-to-mongodb) |
| データストア | **Spanner** - Googleのグローバル分散データベース | [research.google.com](http://research.google.com/archive/spanner-osdi2012.pdf) |
| データストア | **Memcached** - 分散メモリーキャッシングシステム | [slideshare.net](http://www.slideshare.net/oemebamo/introduction-to-memcached) |
| データストア | **Redis** - 永続性とバリュータイプを兼ね備えた分散メモリーキャッシングシステム | [slideshare.net](http://www.slideshare.net/dvirsky/introduction-to-redis) |
| | | |
| ファイルシステム | **Google File System (GFS)** - 分散ファイルシステム | [research.google.com](http://static.googleusercontent.com/media/research.google.com/zh-CN/us/archive/gfs-sosp2003.pdf) |
| ファイルシステム | **Hadoop File System (HDFS)** - GFSのオープンソース実装 | [apache.org](https://hadoop.apache.org/docs/r1.2.1/hdfs_design.html) |
| | | |
| Misc | **Chubby** - 疎結合の分散システムをロックするGoogleのサービス | [research.google.com](http://static.googleusercontent.com/external_content/untrusted_dlcp/research.google.com/en/us/archive/chubby-osdi06.pdf) |
| Misc | **Dapper** - 分散システムを追跡するインフラ | [research.google.com](http://static.googleusercontent.com/media/research.google.com/en//pubs/archive/36356.pdf)
| Misc | **Kafka** - LinkedInによるPub/subメッセージキュー | [slideshare.net](http://www.slideshare.net/mumrah/kafka-talk-tri-hug) |
| Misc | **Zookeeper** - 同期を可能にする中央集権インフラとサービス | [slideshare.net](http://www.slideshare.net/sauravhaloi/introduction-to-apache-zookeeper) |
| | アーキテクチャを追加する | [Contribute](#contributing) |

### 各企業のアーキテクチャ

| 企業 | 参考ページ |
|---|---|
| Amazon | [Amazon architecture](http://highscalability.com/amazon-architecture) |
| Cinchcast | [Producing 1,500 hours of audio every day](http://highscalability.com/blog/2012/7/16/cinchcast-architecture-producing-1500-hours-of-audio-every-d.html) |
| DataSift | [Realtime datamining At 120,000 tweets per second](http://highscalability.com/blog/2011/11/29/datasift-architecture-realtime-datamining-at-120000-tweets-p.html) |
| DropBox | [How we've scaled Dropbox](https://www.youtube.com/watch?v=PE4gwstWhmc) |
| ESPN | [Operating At 100,000 duh nuh nuhs per second](http://highscalability.com/blog/2013/11/4/espns-architecture-at-scale-operating-at-100000-duh-nuh-nuhs.html) |
| Google | [Google architecture](http://highscalability.com/google-architecture) |
| Instagram | [14 million users, terabytes of photos](http://highscalability.com/blog/2011/12/6/instagram-architecture-14-million-users-terabytes-of-photos.html)<br/>[What powers Instagram](http://instagram-engineering.tumblr.com/post/13649370142/what-powers-instagram-hundreds-of-instances) |
| Justin.tv | [Justin.Tv's live video broadcasting architecture](http://highscalability.com/blog/2010/3/16/justintvs-live-video-broadcasting-architecture.html) |
| Facebook | [Scaling memcached at Facebook](https://cs.uwaterloo.ca/~brecht/courses/854-Emerging-2014/readings/key-value/fb-memcached-nsdi-2013.pdf)<br/>[TAO: Facebook’s distributed data store for the social graph](https://cs.uwaterloo.ca/~brecht/courses/854-Emerging-2014/readings/data-store/tao-facebook-distributed-datastore-atc-2013.pdf)<br/>[Facebook’s photo storage](https://www.usenix.org/legacy/event/osdi10/tech/full_papers/Beaver.pdf) |
| Flickr | [Flickr architecture](http://highscalability.com/flickr-architecture) |
| Mailbox | [From 0 to one million users in 6 weeks](http://highscalability.com/blog/2013/6/18/scaling-mailbox-from-0-to-one-million-users-in-6-weeks-and-1.html) |
| Pinterest | [From 0 To 10s of billions of page views a month](http://highscalability.com/blog/2013/4/15/scaling-pinterest-from-0-to-10s-of-billions-of-page-views-a.html)<br/>[18 million visitors, 10x growth, 12 employees](http://highscalability.com/blog/2012/5/21/pinterest-architecture-update-18-million-visitors-10x-growth.html) |
| Playfish | [50 million monthly users and growing](http://highscalability.com/blog/2010/9/21/playfishs-social-gaming-architecture-50-million-monthly-user.html) |
| PlentyOfFish | [PlentyOfFish architecture](http://highscalability.com/plentyoffish-architecture) |
| Salesforce | [How they handle 1.3 billion transactions a day](http://highscalability.com/blog/2013/9/23/salesforce-architecture-how-they-handle-13-billion-transacti.html) |
| Stack Overflow | [Stack Overflow architecture](http://highscalability.com/blog/2009/8/5/stack-overflow-architecture.html) |
| TripAdvisor | [40M visitors, 200M dynamic page views, 30TB data](http://highscalability.com/blog/2011/6/27/tripadvisor-architecture-40m-visitors-200m-dynamic-page-view.html) |
| Tumblr | [15 billion page views a month](http://highscalability.com/blog/2012/2/13/tumblr-architecture-15-billion-page-views-a-month-and-harder.html) |
| Twitter | [Making Twitter 10000 percent faster](http://highscalability.com/scaling-twitter-making-twitter-10000-percent-faster)<br/>[Storing 250 million tweets a day using MySQL](http://highscalability.com/blog/2011/12/19/how-twitter-stores-250-million-tweets-a-day-using-mysql.html)<br/>[150M active users, 300K QPS, a 22 MB/S firehose](http://highscalability.com/blog/2013/7/8/the-architecture-twitter-uses-to-deal-with-150m-active-users.html)<br/>[Timelines at scale](https://www.infoq.com/presentations/Twitter-Timeline-Scalability)<br/>[Big and small data at Twitter](https://www.youtube.com/watch?v=5cKTP36HVgI)<br/>[Operations at Twitter: scaling beyond 100 million users](https://www.youtube.com/watch?v=z8LU0Cj6BOU) |
| Uber | [How Uber scales their real-time market platform](http://highscalability.com/blog/2015/9/14/how-uber-scales-their-real-time-market-platform.html) |
| WhatsApp | [The WhatsApp architecture Facebook bought for $19 billion](http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html) |
| YouTube | [YouTube scalability](https://www.youtube.com/watch?v=w5WVu624fY8)<br/>[YouTube architecture](http://highscalability.com/youtube-architecture) |

### 企業のエンジニアブログ

> 面接を受ける企業のアーキテクチャ
>
> 投げられる質問は同じ分野から来ることもあるでしょう

* [Airbnb Engineering](http://nerds.airbnb.com/)
* [Atlassian Developers](https://developer.atlassian.com/blog/)
* [Autodesk Engineering](http://cloudengineering.autodesk.com/blog/)
* [AWS Blog](https://aws.amazon.com/blogs/aws/)
* [Bitly Engineering Blog](http://word.bitly.com/)
* [Box Blogs](https://www.box.com/blog/engineering/)
* [Cloudera Developer Blog](http://blog.cloudera.com/blog/)
* [Dropbox Tech Blog](https://tech.dropbox.com/)
* [Engineering at Quora](http://engineering.quora.com/)
* [Ebay Tech Blog](http://www.ebaytechblog.com/)
* [Evernote Tech Blog](https://blog.evernote.com/tech/)
* [Etsy Code as Craft](http://codeascraft.com/)
* [Facebook Engineering](https://www.facebook.com/Engineering)
* [Flickr Code](http://code.flickr.net/)
* [Foursquare Engineering Blog](http://engineering.foursquare.com/)
* [GitHub Engineering Blog](http://githubengineering.com/)
* [Google Research Blog](http://googleresearch.blogspot.com/)
* [Groupon Engineering Blog](https://engineering.groupon.com/)
* [Heroku Engineering Blog](https://engineering.heroku.com/)
* [Hubspot Engineering Blog](http://product.hubspot.com/blog/topic/engineering)
* [High Scalability](http://highscalability.com/)
* [Instagram Engineering](http://instagram-engineering.tumblr.com/)
* [Intel Software Blog](https://software.intel.com/en-us/blogs/)
* [Jane Street Tech Blog](https://blogs.janestreet.com/category/ocaml/)
* [LinkedIn Engineering](http://engineering.linkedin.com/blog)
* [Microsoft Engineering](https://engineering.microsoft.com/)
* [Microsoft Python Engineering](https://blogs.msdn.microsoft.com/pythonengineering/)
* [Netflix Tech Blog](http://techblog.netflix.com/)
* [Paypal Developer Blog](https://devblog.paypal.com/category/engineering/)
* [Pinterest Engineering Blog](http://engineering.pinterest.com/)
* [Quora Engineering](https://engineering.quora.com/)
* [Reddit Blog](http://www.redditblog.com/)
* [Salesforce Engineering Blog](https://developer.salesforce.com/blogs/engineering/)
* [Slack Engineering Blog](https://slack.engineering/)
* [Spotify Labs](https://labs.spotify.com/)
* [Twilio Engineering Blog](http://www.twilio.com/engineering)
* [Twitter Engineering](https://engineering.twitter.com/)
* [Uber Engineering Blog](http://eng.uber.com/)
* [Yahoo Engineering Blog](http://yahooeng.tumblr.com/)
* [Yelp Engineering Blog](http://engineeringblog.yelp.com/)
* [Zynga Engineering Blog](https://www.zynga.com/blogs/engineering)

#### その他の参考資料、ページ:

* [kilimchoi/engineering-blogs](https://github.com/kilimchoi/engineering-blogs)

ここにあるリストは比較的小規模なものにとどめ、[kilimchoi/engineering-blogs](https://github.com/kilimchoi/engineering-blogs)により詳細に記すことで重複しないようにしておくことにする。エンジニアブログへのリンクを追加する場合はここではなく、engineering-blogsレボジトリに追加することを検討してください。

## 進行中の作業

セクションの追加や、進行中の作業を手伝っていただける場合は[こちら](#contributing)!

* MapReduceによる分散コンピューティング
* Consistent hashing
* Scatter gather
* [Contribute](#contributing)

## クレジット

クレジット及び、参照ページは適時このリポジトリ内に記載してあります

Special thanks to:

* [Hired in tech](http://www.hiredintech.com/system-design/the-system-design-process/)
* [Cracking the coding interview](https://www.amazon.com/dp/0984782850/)
* [High scalability](http://highscalability.com/)
* [checkcheckzz/system-design-interview](https://github.com/checkcheckzz/system-design-interview)
* [shashank88/system_design](https://github.com/shashank88/system_design)
* [mmcgrana/services-engineering](https://github.com/mmcgrana/services-engineering)
* [System design cheat sheet](https://gist.github.com/vasanthk/485d1c25737e8e72759f)
* [A distributed systems reading list](http://dancres.github.io/Pages/)
* [Cracking the system design interview](http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview)

## Contact info

Feel free to contact me to discuss any issues, questions, or comments.

My contact info can be found on my [GitHub page](https://github.com/donnemartin).

## License

*I am providing code and resources in this repository to you under an open source license.  Because this is my personal repository, the license you receive to my code and resources is from me and not my employer (Facebook).*

    Copyright 2017 Donne Martin

    Creative Commons Attribution 4.0 International License (CC BY 4.0)

    http://creativecommons.org/licenses/by/4.0/
> * 原文地址：[github.com/donnemartin/system-design-primer](https://github.com/donnemartin/system-design-primer)
> * 译文出自：[掘金翻译计划](https://github.com/xitu/gold-miner)
> * 译者：[XatMassacrE](https://github.com/XatMassacrE)、[L9m](https://github.com/L9m)、[Airmacho](https://github.com/Airmacho)、[xiaoyusilen](https://github.com/xiaoyusilen)、[jifaxu](https://github.com/jifaxu)
> * 这个 [链接](https://github.com/xitu/system-design-primer/compare/master...donnemartin:master) 用来查看本翻译与英文版是否有差别（如果你没有看到 README.md 发生变化，那就意味着这份翻译文档是最新的）。

*[English](README.md) ∙ [日本語](README-ja.md) ∙ [简体中文](README-zh-Hans.md) ∙ [繁體中文](README-zh-TW.md) | [العَرَبِيَّة‎](https://github.com/donnemartin/system-design-primer/issues/170) ∙ [বাংলা](https://github.com/donnemartin/system-design-primer/issues/220) ∙ [Português do Brasil](https://github.com/donnemartin/system-design-primer/issues/40) ∙ [Deutsch](https://github.com/donnemartin/system-design-primer/issues/186) ∙ [ελληνικά](https://github.com/donnemartin/system-design-primer/issues/130) ∙ [עברית](https://github.com/donnemartin/system-design-primer/issues/272) ∙ [Italiano](https://github.com/donnemartin/system-design-primer/issues/104) ∙ [韓國語](https://github.com/donnemartin/system-design-primer/issues/102) ∙ [فارسی](https://github.com/donnemartin/system-design-primer/issues/110) ∙ [Polski](https://github.com/donnemartin/system-design-primer/issues/68) ∙ [русский язык](https://github.com/donnemartin/system-design-primer/issues/87) ∙ [Español](https://github.com/donnemartin/system-design-primer/issues/136) ∙ [ภาษาไทย](https://github.com/donnemartin/system-design-primer/issues/187) ∙ [Türkçe](https://github.com/donnemartin/system-design-primer/issues/39) ∙ [tiếng Việt](https://github.com/donnemartin/system-design-primer/issues/127) ∙ [Français](https://github.com/donnemartin/system-design-primer/issues/250) | [Add Translation](https://github.com/donnemartin/system-design-primer/issues/28)*

# 系统设计入门

<p align="center">
  <img src="http://i.imgur.com/jj3A5N8.png"/>
  <br/>
</p>

## 翻译

有兴趣参与[翻译](https://github.com/donnemartin/system-design-primer/issues/28)?  以下是正在进行中的翻译:

* [巴西葡萄牙语](https://github.com/donnemartin/system-design-primer/issues/40)
* [简体中文](https://github.com/donnemartin/system-design-primer/issues/38)
* [土耳其语](https://github.com/donnemartin/system-design-primer/issues/39)

## 目的

> 学习如何设计大型系统。
>
> 为系统设计的面试做准备。

### 学习如何设计大型系统

学习如何设计可扩展的系统将会有助于你成为一个更好的工程师。

系统设计是一个很宽泛的话题。在互联网上，**关于系统设计原则的资源也是多如牛毛。**

这个仓库就是这些资源的**组织收集**，它可以帮助你学习如何构建可扩展的系统。

### 从开源社区学习

这是一个不断更新的开源项目的初期的版本。

欢迎[贡献](#贡献)！

### 为系统设计的面试做准备

在很多科技公司中，除了代码面试，系统设计也是**技术面试过程**中的一个**必要环节**。

**实践常见的系统设计面试题**并且把你的答案和**例子的解答**进行**对照**：讨论，代码和图表。

面试准备的其他主题：

* [学习指引](#学习指引)
* [如何处理一个系统设计的面试题](#如何处理一个系统设计的面试题)
* [系统设计的面试题，**含解答**](#系统设计的面试题和解答)
* [面向对象设计的面试题，**含解答**](#面向对象设计的面试问题及解答)
* [其它的系统设计面试题](#其它的系统设计面试题)

## 抽认卡

<p align="center">
  <img src="http://i.imgur.com/zdCAkB3.png"/>
  <br/>
</p>

这里提供的[抽认卡堆](https://apps.ankiweb.net/)使用间隔重复的方法，帮助你记忆关键的系统设计概念。

* [系统设计的卡堆](resources/flash_cards/System%20Design.apkg)
* [系统设计的练习卡堆](resources/flash_cards/System%20Design%20Exercises.apkg)
* [面向对象设计的练习卡堆](resources/flash_cards/OO%20Design.apkg)

随时随地都可使用。

### 代码资源：互动式编程挑战

你正在寻找资源以准备[**编程面试**](https://github.com/donnemartin/interactive-coding-challenges)吗？

<p align="center">
  <img src="http://i.imgur.com/b4YtAEN.png"/>
  <br/>
</p>

请查看我们的姐妹仓库[**互动式编程挑战**](https://github.com/donnemartin/interactive-coding-challenges)，其中包含了一个额外的抽认卡堆：

* [代码卡堆](https://github.com/donnemartin/interactive-coding-challenges/tree/master/anki_cards/Coding.apkg)

## 贡献

> 从社区中学习。

欢迎提交 PR 提供帮助：

* 修复错误
* 完善章节
* 添加章节

一些还需要完善的内容放在了[正在完善中](#正在完善中)。

请查看[贡献指南](CONTRIBUTING.md)。

## 系统设计主题的索引

> 各种系统设计主题的摘要，包括优点和缺点。**每一个主题都面临着取舍和权衡**。
>
> 每个章节都包含着更多的资源的链接。


<p align="center">
  <img src="http://i.imgur.com/jrUBAF7.png"/>
  <br/>
</p>

* [系统设计主题：从这里开始](#系统设计主题从这里开始)
    * [第一步：回顾可扩展性的视频讲座](#第一步回顾可扩展性scalability的视频讲座)
    * [第二步：回顾可扩展性的文章](#第二步回顾可扩展性文章)
    * [接下来的步骤](#接下来的步骤)
* [性能与拓展性](#性能与可扩展性)
* [延迟与吞吐量](#延迟与吞吐量)
* [可用性与一致性](#可用性与一致性)
    * [CAP 理论](#cap-理论)
        * [CP - 一致性和分区容错性](#cp--一致性和分区容错性)
        * [AP - 可用性和分区容错性](#ap--可用性与分区容错性)
* [一致模式](#一致性模式)
    * [弱一致性](#弱一致性)
    * [最终一致性](#最终一致性)
    * [强一致性](#强一致性)
* [可用模式](#可用性模式)
    * [故障切换](#故障切换)
    * [复制](#复制)
* [域名系统](#域名系统)
* [CDN](#内容分发网络cdn)
    * [CDN 推送](#cdn-推送push)
    * [CDN 拉取](#cdn-拉取pull)
* [负载均衡器](#负载均衡器)
    * [工作到备用切换（Active-passive）](#工作到备用切换active-passive)
    * [双工作切换（Active-active）](#双工作切换active-active)
    * [四层负载均衡](#四层负载均衡)
    * [七层负载均衡](#七层负载均衡器)
    * [水平扩展](#水平扩展)
* [反向代理（web 服务器）](#反向代理web-服务器)
    * [负载均衡与反向代理](#负载均衡器与反向代理)
* [应用层](#应用层)
    * [微服务](#微服务)
    * [服务发现](#服务发现)
* [数据库](#数据库)
    * [关系型数据库管理系统（RDBMS）](#关系型数据库管理系统rdbms)
        * [Master-slave 复制集](#主从复制)
        * [Master-master 复制集](#主主复制)
        * [联合](#联合)
        * [分片](#分片)
        * [非规范化](#非规范化)
        * [SQL 调优](#sql-调优)
    * [NoSQL](#nosql)
        * [Key-value 存储](#键-值存储)
        * [文档存储](#文档类型存储)
        * [宽列存储](#列型存储)
        * [图数据库](#图数据库)
    * [SQL 还是 NoSQL](#sql-还是-nosql)
* [缓存](#缓存)
    * [客户端缓存](#客户端缓存)
    * [CDN 缓存](#cdn-缓存)
    * [Web 服务器缓存](#web-服务器缓存)
    * [数据库缓存](#数据库缓存)
    * [应用缓存](#应用缓存)
    * [数据库查询级别的缓存](#数据库查询级别的缓存)
    * [对象级别的缓存](#对象级别的缓存)
    * [何时更新缓存](#何时更新缓存)
        * [缓存模式](#缓存模式)
        * [直写模式](#直写模式)
        * [回写模式](#回写模式)
        * [刷新](#刷新)
* [异步](#异步)
    * [消息队列](#消息队列)
    * [任务队列](#任务队列)
    * [背压机制](#背压)
* [通讯](#通讯)
    * [传输控制协议（TCP）](#传输控制协议tcp)
    * [用户数据报协议（UDP）](#用户数据报协议udp)
    * [远程控制调用协议（RPC）](#远程过程调用协议rpc)
    * [表述性状态转移（REST）](#表述性状态转移rest)
* [安全](#安全)
* [附录](#附录)
    * [2 的次方表](#2-的次方表)
    * [每个程序员都应该知道的延迟数](#每个程序员都应该知道的延迟数)
    * [其它的系统设计面试题](#其它的系统设计面试题)
    * [真实架构](#真实架构)
    * [公司的系统架构](#公司的系统架构)
    * [公司工程博客](#公司工程博客)
* [正在完善中](#正在完善中)
* [致谢](#致谢)
* [联系方式](#联系方式)
* [许可](#许可)

## 学习指引

> 基于你面试的时间线（短、中、长）去复习那些推荐的主题。

![Imgur](http://i.imgur.com/OfVllex.png)

**问：对于面试来说，我需要知道这里的所有知识点吗？**

**答：不，如果只是为了准备面试的话，你并不需要知道所有的知识点。**

在一场面试中你会被问到什么取决于下面这些因素：

* 你的经验
* 你的技术背景
* 你面试的职位
* 你面试的公司
* 运气

那些有经验的候选人通常会被期望了解更多的系统设计的知识。架构师或者团队负责人则会被期望了解更多除了个人贡献之外的知识。顶级的科技公司通常也会有一次或者更多的系统设计面试。

面试会很宽泛的展开并在几个领域深入。这会帮助你了解一些关于系统设计的不同的主题。基于你的时间线，经验，面试的职位和面试的公司对下面的指导做出适当的调整。

* **短期** - 以系统设计主题的**广度**为目标。通过解决**一些**面试题来练习。
* **中期** - 以系统设计主题的**广度**和**初级深度**为目标。通过解决**很多**面试题来练习。
* **长期** - 以系统设计主题的**广度**和**高级深度**为目标。通过解决**大部分**面试题来练习。

|                                          | 短期   | 中期   | 长期   |
| ---------------------------------------- | ---- | ---- | ---- |
| 阅读 [系统设计主题](#系统设计主题的索引) 以获得一个关于系统如何工作的宽泛的认识 | :+1: | :+1: | :+1: |
| 阅读一些你要面试的[公司工程博客](#公司工程博客)的文章            | :+1: | :+1: | :+1: |
| 阅读 [真实架构](#真实架构)                   | :+1: | :+1: | :+1: |
| 复习 [如何处理一个系统设计面试题](#如何处理一个系统设计面试题)       | :+1: | :+1: | :+1: |
| 完成 [系统设计的面试题和解答](#系统设计的面试题和解答)             | 一些   | 很多   | 大部分  |
| 完成 [面向对象设计的面试题和解答](#面向对象设计的面试问题及解答)        | 一些   | 很多   | 大部分  |
| 复习 [其它的系统设计面试题](#其它的系统设计面试题)          | 一些   | 很多   | 大部分  |

## 如何处理一个系统设计的面试题

系统设计面试是一个**开放式的对话**。他们期望你去主导这个对话。

你可以使用下面的步骤来指引讨论。为了巩固这个过程，请使用下面的步骤完成[系统设计的面试题和解答](#系统设计的面试题和解答)这个章节。

### 第一步：描述使用场景，约束和假设

把所有需要的东西聚集在一起，审视问题。不停的提问，以至于我们可以明确使用场景和约束。讨论假设。

* 谁会使用它？
* 他们会怎样使用它？
* 有多少用户？
* 系统的作用是什么？
* 系统的输入输出分别是什么？
* 我们希望处理多少数据？
* 我们希望每秒钟处理多少请求？
* 我们希望的读写比率？

### 第二步：创造一个高层级的设计

使用所有重要的组件来描绘出一个高层级的设计。

* 画出主要的组件和连接
* 证明你的想法

### 第三步：设计核心组件

对每一个核心组件进行详细深入的分析。举例来说，如果你被问到[设计一个 url 缩写服务](solutions/system_design/pastebin/README.md)，开始讨论：

* 生成并储存一个完整 url 的 hash
    * [MD5](solutions/system_design/pastebin/README.md) 和 [Base62](solutions/system_design/pastebin/README.md)
    * Hash 碰撞
    * SQL 还是 NoSQL
    * 数据库模型
* 将一个 hashed url 翻译成完整的 url
    * 数据库查找
* API 和面向对象设计

### 第四步：扩展设计

确认和处理瓶颈以及一些限制。举例来说就是你需要下面的这些来完成扩展性的议题吗？

* 负载均衡
* 水平扩展
* 缓存
* 数据库分片

论述可能的解决办法和代价。每件事情需要取舍。可以使用[可扩展系统的设计原则](#系统设计主题的索引)来处理瓶颈。

### 预估计算量

你或许会被要求通过手算进行一些估算。[附录](#附录)涉及到的是下面的这些资源：

* [使用预估计算量](http://highscalability.com/blog/2011/1/26/google-pro-tip-use-back-of-the-envelope-calculations-to-choo.html)
* [2 的次方表](#2-的次方表)
* [每个程序员都应该知道的延迟数](#每个程序员都应该知道的延迟数)

### 相关资源和延伸阅读

查看下面的链接以获得我们期望的更好的想法：

* [怎样通过一个系统设计的面试](https://www.palantir.com/2011/10/how-to-rock-a-systems-design-interview/)
* [系统设计的面试](http://www.hiredintech.com/system-design)
* [系统架构与设计的面试简介](https://www.youtube.com/watch?v=ZgdS0EUmn70)

## 系统设计的面试题和解答

> 普通的系统设计面试题和相关事例的论述，代码和图表。
>

> 与内容有关的解答在 `solutions/` 文件夹中。

| 问题                                       |                                          |
| ---------------------------------------- | ---------------------------------------- |
| 设计 Pastebin.com (或者 Bit.ly)              | [解答](solutions/system_design/pastebin/README-zh-Hans.md) |
| 设计 Twitter 时间线和搜索 (或者 Facebook feed 和搜索) | [解答](solutions/system_design/twitter/README.md) |
| 设计一个网页爬虫                                 | [解答](solutions/system_design/web_crawler/README.md) |
| 设计 Mint.com                              | [解答](solutions/system_design/mint/README.md) |
| 为一个社交网络设计数据结构                            | [解答](solutions/system_design/social_graph/README.md) |
| 为搜索引擎设计一个 key-value 储存                   | [解答](solutions/system_design/query_cache/README.md) |
| 通过分类特性设计 Amazon 的销售排名                    | [解答](solutions/system_design/sales_rank/README.md) |
| 在 AWS 上设计一个百万用户级别的系统                     | [解答](solutions/system_design/scaling_aws/README.md) |
| 添加一个系统设计问题                               | [贡献](#贡献)                                |

### 设计 Pastebin.com (或者 Bit.ly)

[查看实践与解答](solutions/system_design/pastebin/README.md)

![Imgur](http://i.imgur.com/4edXG0T.png)

### 设计 Twitter 时间线和搜索 (或者 Facebook feed 和搜索)

[查看实践与解答](solutions/system_design/twitter/README.md)

![Imgur](http://i.imgur.com/jrUBAF7.png)

### 设计一个网页爬虫

[查看实践与解答](solutions/system_design/web_crawler/README.md)

![Imgur](http://i.imgur.com/bWxPtQA.png)

### 设计 Mint.com

[查看实践与解答](solutions/system_design/mint/README.md)

![Imgur](http://i.imgur.com/V5q57vU.png)

### 为一个社交网络设计数据结构

[查看实践与解答](solutions/system_design/social_graph/README.md)

![Imgur](http://i.imgur.com/cdCv5g7.png)

### 为搜索引擎设计一个 key-value 储存

[查看实践与解答](solutions/system_design/query_cache/README.md)

![Imgur](http://i.imgur.com/4j99mhe.png)

### 设计按类别分类的 Amazon 销售排名

[查看实践与解答](solutions/system_design/sales_rank/README.md)

![Imgur](http://i.imgur.com/MzExP06.png)

### 在 AWS 上设计一个百万用户级别的系统

[查看实践与解答](solutions/system_design/scaling_aws/README.md)

![Imgur](http://i.imgur.com/jj3A5N8.png)

## 面向对象设计的面试问题及解答

> 常见面向对象设计面试问题及实例讨论，代码和图表演示。
>
> 与内容相关的解决方案在 `solutions/` 文件夹中。

>**注：此节还在完善中**

| 问题           |                                          |
| ------------ | ---------------------------------------- |
| 设计 hash map  | [解决方案](solutions/object_oriented_design/hash_table/hash_map.ipynb) |
| 设计 LRU 缓存    | [解决方案](solutions/object_oriented_design/lru_cache/lru_cache.ipynb) |
| 设计一个呼叫中心     | [解决方案](solutions/object_oriented_design/call_center/call_center.ipynb) |
| 设计一副牌        | [解决方案](solutions/object_oriented_design/deck_of_cards/deck_of_cards.ipynb) |
| 设计一个停车场      | [解决方案](solutions/object_oriented_design/parking_lot/parking_lot.ipynb) |
| 设计一个聊天服务     | [解决方案](solutions/object_oriented_design/online_chat/online_chat.ipynb) |
| 设计一个环形数组     | [待解决](#贡献)                     |
| 添加一个面向对象设计问题 | [待解决](#贡献)                     |

## 系统设计主题：从这里开始

不熟悉系统设计？

首先，你需要对一般性原则有一个基本的认识，知道它们是什么，怎样使用以及利弊。

### 第一步：回顾可扩展性（scalability）的视频讲座

[哈佛大学可扩展性讲座](https://www.youtube.com/watch?v=-W9F__D3oY4)

* 主题涵盖
    * 垂直扩展（Vertical scaling）
    * 水平扩展（Horizontal scaling）
    * 缓存
    * 负载均衡
    * 数据库复制
    * 数据库分区

### 第二步：回顾可扩展性文章

[可扩展性](http://www.lecloud.net/tagged/scalability/chrono)

* 主题涵盖：
    * [Clones](http://www.lecloud.net/post/7295452622/scalability-for-dummies-part-1-clones)
    * [数据库](http://www.lecloud.net/post/7994751381/scalability-for-dummies-part-2-database)
    * [缓存](http://www.lecloud.net/post/9246290032/scalability-for-dummies-part-3-cache)
    * [异步](http://www.lecloud.net/post/9699762917/scalability-for-dummies-part-4-asynchronism)

### 接下来的步骤

接下来，我们将看看高阶的权衡和取舍:

* **性能**与**可扩展性**
* **延迟**与**吞吐量**
* **可用性**与**一致性**

记住**每个方面都面临取舍和权衡**。

然后，我们将深入更具体的主题，如 DNS、CDN 和负载均衡器。

## 性能与可扩展性

如果服务**性能**的增长与资源的增加是成比例的，服务就是可扩展的。通常，提高性能意味着服务于更多的工作单元，另一方面，当数据集增长时，同样也可以处理更大的工作单位。<sup><a href="http://www.allthingsdistributed.com/2006/03/a_word_on_scalability.html">1</a></sup>

另一个角度来看待性能与可扩展性:

* 如果你的系统有**性能**问题，对于单个用户来说是缓慢的。
* 如果你的系统有**可扩展性**问题，单个用户较快但在高负载下会变慢。

### 来源及延伸阅读

* [简单谈谈可扩展性](http://www.allthingsdistributed.com/2006/03/a_word_on_scalability.html)
* [可扩展性，可用性，稳定性和模式](http://www.slideshare.net/jboner/scalability-availability-stability-patterns/)

## 延迟与吞吐量

**延迟**是执行操作或运算结果所花费的时间。

**吞吐量**是单位时间内（执行）此类操作或运算的数量。

通常，你应该以**可接受级延迟**下**最大化吞吐量**为目标。

### 来源及延伸阅读

* [理解延迟与吞吐量](https://community.cadence.com/cadence_blogs_8/b/sd/archive/2010/09/13/understanding-latency-vs-throughput)

## 可用性与一致性

### CAP 理论

<p align="center">
  <img src="http://i.imgur.com/bgLMI2u.png"/>
  <br/>
  <strong><a href="http://robertgreiner.com/2014/08/cap-theorem-revisited">来源：再看 CAP 理论</a></strong>
</p>

在一个分布式计算系统中，只能同时满足下列的两点:

* **一致性** ─ 每次访问都能获得最新数据但可能会收到错误响应
* **可用性** ─ 每次访问都能收到非错响应，但不保证获取到最新数据
* **分区容错性** ─ 在任意分区网络故障的情况下系统仍能继续运行

**网络并不可靠，所以你应要支持分区容错性，并需要在软件可用性和一致性间做出取舍。**

#### CP ─ 一致性和分区容错性

等待分区节点的响应可能会导致延时错误。如果你的业务需求需要原子读写，CP 是一个不错的选择。

#### AP ─ 可用性与分区容错性

响应节点上可用数据的最近版本可能并不是最新的。当分区解析完后，写入（操作）可能需要一些时间来传播。

如果业务需求允许[最终一致性](#最终一致性)，或当有外部故障时要求系统继续运行，AP 是一个不错的选择。

### 来源及延伸阅读

* [再看 CAP 理论](http://robertgreiner.com/2014/08/cap-theorem-revisited/)
* [通俗易懂地介绍 CAP 理论](http://ksat.me/a-plain-english-introduction-to-cap-theorem/)
* [CAP FAQ](https://github.com/henryr/cap-faq)

## 一致性模式

有同一份数据的多份副本，我们面临着怎样同步它们的选择，以便让客户端有一致的显示数据。回想 [CAP 理论](#cap-理论)中的一致性定义 ─ 每次访问都能获得最新数据但可能会收到错误响应


### 弱一致性

在写入之后，访问可能看到，也可能看不到（写入数据）。尽力优化之让其能访问最新数据。

这种方式可以 memcached 等系统中看到。弱一致性在 VoIP，视频聊天和实时多人游戏等真实用例中表现不错。打个比方，如果你在通话中丢失信号几秒钟时间，当重新连接时你是听不到这几秒钟所说的话的。

### 最终一致性

在写入后，访问最终能看到写入数据（通常在数毫秒内）。数据被异步复制。

DNS 和 email 等系统使用的是此种方式。最终一致性在高可用性系统中效果不错。

### 强一致性

在写入后，访问立即可见。数据被同步复制。

文件系统和关系型数据库（RDBMS）中使用的是此种方式。强一致性在需要记录的系统中运作良好。

### 来源及延伸阅读

* [Transactions across data centers](http://snarfed.org/transactions_across_datacenters_io.html)

## 可用性模式

有两种支持高可用性的模式: **故障切换（fail-over）**和**复制（replication）**。

### 故障切换

#### 工作到备用切换（Active-passive）

关于工作到备用的故障切换流程是，工作服务器发送周期信号给待机中的备用服务器。如果周期信号中断，备用服务器切换成工作服务器的 IP 地址并恢复服务。

宕机时间取决于备用服务器处于“热”待机状态还是需要从“冷”待机状态进行启动。只有工作服务器处理流量。

工作到备用的故障切换也被称为主从切换。

#### 双工作切换（Active-active）

在双工作切换中，双方都在管控流量，在它们之间分散负载。

如果是外网服务器，DNS 将需要对两方都了解。如果是内网服务器，应用程序逻辑将需要对两方都了解。

双工作切换也可以称为主主切换。

### 缺陷：故障切换

* 故障切换需要添加额外硬件并增加复杂性。
* 如果新写入数据在能被复制到备用系统之前，工作系统出现了故障，则有可能会丢失数据。

### 复制

#### 主─从复制和主─主复制

这个主题进一步探讨了[数据库](#数据库)部分:

* [主─从复制](#主从复制)
* [主─主复制](#主主复制)

## 域名系统

<p align="center">
  <img src="http://i.imgur.com/IOyLj4i.jpg"/>
  <br/>
  <strong><a href="http://www.slideshare.net/srikrupa5/dns-security-presentation-issa">来源：DNS 安全介绍</a></strong>
</p>

域名系统是把 www.example.com 等域名转换成 IP 地址。

域名系统是分层次的，一些 DNS 服务器位于顶层。当查询（域名） IP 时，路由或 ISP 提供连接 DNS 服务器的信息。较底层的 DNS 服务器缓存映射，它可能会因为 DNS 传播延时而失效。DNS 结果可以缓存在浏览器或操作系统中一段时间，时间长短取决于[存活时间 TTL](https://en.wikipedia.org/wiki/Time_to_live)。

* **NS 记录（域名服务）** ─ 指定解析域名或子域名的 DNS 服务器。
* **MX 记录（邮件交换）** ─ 指定接收信息的邮件服务器。
* **A 记录（地址）** ─ 指定域名对应的 IP 地址记录。
* **CNAME（规范）** ─ 一个域名映射到另一个域名或 `CNAME` 记录（ example.com 指向 www.example.com ）或映射到一个 `A` 记录。

[CloudFlare](https://www.cloudflare.com/dns/) 和 [Route 53](https://aws.amazon.com/route53/) 等平台提供管理 DNS 的功能。某些 DNS 服务通过集中方式来路由流量:

* [加权轮询调度](http://g33kinfo.com/info/archives/2657)
    * 防止流量进入维护中的服务器
    * 在不同大小集群间负载均衡
    * A/B 测试
* 基于延迟路由
* 基于地理位置路由

### 缺陷:DNS

* 虽说缓存可以减轻 DNS 延迟，但连接 DNS 服务器还是带来了轻微的延迟。
* 虽然它们通常由[政府，网络服务提供商和大公司](http://superuser.com/questions/472695/who-controls-the-dns-servers/472729)管理，但 DNS 服务管理仍可能是复杂的。
* DNS 服务最近遭受 [DDoS 攻击](http://dyn.com/blog/dyn-analysis-summary-of-friday-october-21-attack/)，阻止不知道 Twitter IP 地址的用户访问 Twitter。

### 来源及延伸阅读

* [DNS 架构](https://technet.microsoft.com/en-us/library/dd197427(v=ws.10).aspx)
* [Wikipedia](https://en.wikipedia.org/wiki/Domain_Name_System)
* [关于 DNS 的文章](https://support.dnsimple.com/categories/dns/)

## 内容分发网络（CDN）

<p align="center">
  <img src="http://i.imgur.com/h9TAuGI.jpg"/>
  <br/>
  <strong><a href="https://www.creative-artworks.eu/why-use-a-content-delivery-network-cdn/">来源：为什么使用 CDN</a></strong>
</p>

内容分发网络（CDN）是一个全球性的代理服务器分布式网络，它从靠近用户的位置提供内容。通常，HTML/CSS/JS，图片和视频等静态内容由 CDN 提供，虽然亚马逊 CloudFront 等也支持动态内容。CDN 的 DNS 解析会告知客户端连接哪台服务器。

将内容存储在 CDN 上可以从两个方面来提供性能:

* 从靠近用户的数据中心提供资源
* 通过 CDN 你的服务器不必真的处理请求

### CDN 推送（push）

当你服务器上内容发生变动时，推送 CDN 接受新内容。直接推送给 CDN 并重写 URL 地址以指向你的内容的 CDN 地址。你可以配置内容到期时间及何时更新。内容只有在更改或新增是才推送，流量最小化，但储存最大化。

### CDN 拉取（pull）

CDN 拉取是当第一个用户请求该资源时，从服务器上拉取资源。你将内容留在自己的服务器上并重写 URL 指向 CDN 地址。直到内容被缓存在 CDN 上为止，这样请求只会更慢，

[存活时间（TTL）](https://en.wikipedia.org/wiki/Time_to_live)决定缓存多久时间。CDN 拉取方式最小化 CDN 上的储存空间，但如果过期文件并在实际更改之前被拉取，则会导致冗余的流量。

高流量站点使用 CDN 拉取效果不错，因为只有最近请求的内容保存在 CDN 中，流量才能更平衡地分散。

### 缺陷：CDN

* CDN 成本可能因流量而异，可能在权衡之后你将不会使用 CDN。
* 如果在 TTL 过期之前更新内容，CDN 缓存内容可能会过时。
* CDN 需要更改静态内容的 URL 地址以指向 CDN。

### 来源及延伸阅读

* [全球性内容分发网络](http://repository.cmu.edu/cgi/viewcontent.cgi?article=2112&context=compsci)
* [CDN 拉取和 CDN 推送的区别](http://www.travelblogadvice.com/technical/the-differences-between-push-and-pull-cdns/)
* [Wikipedia](https://en.wikipedia.org/wiki/Content_delivery_network)

## 负载均衡器

<p align="center">
  <img src="http://i.imgur.com/h81n9iK.png"/>
  <br/>
  <strong><a href="http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html">来源：可扩展的系统设计模式</a></strong>
</p>

负载均衡器将传入的请求分发到应用服务器和数据库等计算资源。无论哪种情况，负载均衡器将从计算资源来的响应返回给恰当的客户端。负载均衡器的效用在于:

* 防止请求进入不好的服务器
* 防止资源过载
* 帮助消除单一的故障点

负载均衡器可以通过硬件（昂贵）或 HAProxy 等软件来实现。
增加的好处包括:

* **SSL 终结** ─ 解密传入的请求并加密服务器响应，这样的话后端服务器就不必再执行这些潜在高消耗运算了。
    * 不需要再每台服务器上安装 [X.509 证书](https://en.wikipedia.org/wiki/X.509)。
* **Session 留存** ─ 如果 Web 应用程序不追踪会话，发出 cookie 并将特定客户端的请求路由到同一实例。

通常会设置采用[工作─备用](#工作到备用切换active-passive) 或 [双工作](#双工作切换active-active) 模式的多个负载均衡器，以免发生故障。

负载均衡器能基于多种方式来路由流量:

* 随机
* 最少负载
* Session/cookie
* [轮询调度或加权轮询调度算法](http://g33kinfo.com/info/archives/2657)
* [四层负载均衡](#四层负载均衡)
* [七层负载均衡](#七层负载均衡)

### 四层负载均衡

四层负载均衡根据监看[传输层](#通讯)的信息来决定如何分发请求。通常，这会涉及来源，目标 IP 地址和请求头中的端口，但不包括数据包（报文）内容。四层负载均衡执行[网络地址转换（NAT）](https://www.nginx.com/resources/glossary/layer-4-load-balancing/)来向上游服务器转发网络数据包。

### 七层负载均衡器

七层负载均衡器根据监控[应用层](#通讯)来决定怎样分发请求。这会涉及请求头的内容，消息和 cookie。七层负载均衡器终结网络流量，读取消息，做出负载均衡判定，然后传送给特定服务器。比如，一个七层负载均衡器能直接将视频流量连接到托管视频的服务器，同时将更敏感的用户账单流量引导到安全性更强的服务器。

以损失灵活性为代价，四层负载均衡比七层负载均衡花费更少时间和计算资源，虽然这对现代商用硬件的性能影响甚微。

### 水平扩展

负载均衡器还能帮助水平扩展，提高性能和可用性。使用商业硬件的性价比更高，并且比在单台硬件上**垂直扩展**更贵的硬件具有更高的可用性。相比招聘特定企业系统人才，招聘商业硬件方面的人才更加容易。

#### 缺陷：水平扩展

* 水平扩展引入了复杂度并涉及服务器复制
    * 服务器应该是无状态的:它们也不该包含像 session 或资料图片等与用户关联的数据。
    * session 可以集中存储在数据库或持久化[缓存](#缓存)（Redis、Memcached）的数据存储区中。
* 缓存和数据库等下游服务器需要随着上游服务器进行扩展，以处理更多的并发连接。

### 缺陷：负载均衡器

* 如果没有足够的资源配置或配置错误，负载均衡器会变成一个性能瓶颈。
* 引入负载均衡器以帮助消除单点故障但导致了额外的复杂性。
* 单个负载均衡器会导致单点故障，但配置多个负载均衡器会进一步增加复杂性。

### 来源及延伸阅读

* [NGINX 架构](https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/)
* [HAProxy 架构指南](http://www.haproxy.org/download/1.2/doc/architecture.txt)
* [可扩展性](http://www.lecloud.net/post/7295452622/scalability-for-dummies-part-1-clones)
* [Wikipedia](https://en.wikipedia.org/wiki/Load_balancing_(computing))
* [四层负载平衡](https://www.nginx.com/resources/glossary/layer-4-load-balancing/)
* [七层负载平衡](https://www.nginx.com/resources/glossary/layer-7-load-balancing/)
* [ELB 监听器配置](http://docs.aws.amazon.com/elasticloadbalancing/latest/classic/elb-listener-config.html)

## 反向代理（web 服务器）

<p align="center">
  <img src="http://i.imgur.com/n41Azff.png"/>
  <br/>
  <strong><a href="https://upload.wikimedia.org/wikipedia/commons/6/67/Reverse_proxy_h2g2bob.svg">资料来源：维基百科</a></strong>
  <br/>
</p>

反向代理是一种可以集中地调用内部服务，并提供统一接口给公共客户的 web 服务器。来自客户端的请求先被反向代理服务器转发到可响应请求的服务器，然后代理再把服务器的响应结果返回给客户端。

带来的好处包括：

- **增加安全性** - 隐藏后端服务器的信息，屏蔽黑名单中的 IP，限制每个客户端的连接数。
- **提高可扩展性和灵活性** - 客户端只能看到反向代理服务器的 IP，这使你可以增减服务器或者修改它们的配置。
- **本地终结 SSL 会话** - 解密传入请求，加密服务器响应，这样后端服务器就不必完成这些潜在的高成本的操作。
  - 免除了在每个服务器上安装 [X.509](https://en.wikipedia.org/wiki/X.509) 证书的需要
- **压缩** - 压缩服务器响应
- **缓存** - 直接返回命中的缓存结果
- **静态内容** - 直接提供静态内容
  - HTML/CSS/JS
  - 图片
  - 视频
  - 等等

### 负载均衡器与反向代理

- 当你有多个服务器时，部署负载均衡器非常有用。通常，负载均衡器将流量路由给一组功能相同的服务器上。
- 即使只有一台 web 服务器或者应用服务器时，反向代理也有用，可以参考上一节介绍的好处。
- NGINX 和 HAProxy 等解决方案可以同时支持第七层反向代理和负载均衡。

### 不利之处：反向代理

- 引入反向代理会增加系统的复杂度。
- 单独一个反向代理服务器仍可能发生单点故障，配置多台反向代理服务器（如[故障转移](https://en.wikipedia.org/wiki/Failover)）会进一步增加复杂度。

### 来源及延伸阅读


- [反向代理与负载均衡](https://www.nginx.com/resources/glossary/reverse-proxy-vs-load-balancer/)
- [NGINX 架构](https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/)
- [HAProxy 架构指南](http://www.haproxy.org/download/1.2/doc/architecture.txt)
- [Wikipedia](https://en.wikipedia.org/wiki/Reverse_proxy)

## 应用层

<p align="center">
  <img src="http://i.imgur.com/yB5SYwm.png"/>
  <br/>
  <strong><a href="http://lethain.com/introduction-to-architecting-systems-for-scale/#platform_layer">资料来源：可缩放系统构架介绍</a></strong>
</p>

将 Web 服务层与应用层（也被称作平台层）分离，可以独立缩放和配置这两层。添加新的 API 只需要添加应用服务器，而不必添加额外的 web 服务器。

**单一职责原则**提倡小型的，自治的服务共同合作。小团队通过提供小型的服务，可以更激进地计划增长。

应用层中的工作进程也有可以实现[异步化](#异步)。

### 微服务

与此讨论相关的话题是 [微服务](https://en.wikipedia.org/wiki/Microservices)，可以被描述为一系列可以独立部署的小型的，模块化服务。每个服务运行在一个独立的线程中，通过明确定义的轻量级机制通讯，共同实现业务目标。<sup><a href=https://smartbear.com/learn/api-design/what-are-microservices>1</a></sup>

例如，Pinterest 可能有这些微服务： 用户资料、关注者、Feed 流、搜索、照片上传等。

### 服务发现

像 [Consul](https://www.consul.io/docs/index.html)，[Etcd](https://coreos.com/etcd/docs/latest) 和 [Zookeeper](http://www.slideshare.net/sauravhaloi/introduction-to-apache-zookeeper) 这样的系统可以通过追踪注册名、地址、端口等信息来帮助服务互相发现对方。[Health checks](https://www.consul.io/intro/getting-started/checks.html) 可以帮助确认服务的完整性和是否经常使用一个 [HTTP](#超文本传输协议http) 路径。Consul 和 Etcd 都有一个内建的 [key-value 存储](#键-值存储) 用来存储配置信息和其他的共享信息。

### 不利之处：应用层

- 添加由多个松耦合服务组成的应用层，从架构、运营、流程等层面来讲将非常不同（相对于单体系统）。
- 微服务会增加部署和运营的复杂度。


### 来源及延伸阅读

- [可缩放系统构架介绍](http://lethain.com/introduction-to-architecting-systems-for-scale)
- [破解系统设计面试](http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview)
- [面向服务架构](https://en.wikipedia.org/wiki/Service-oriented_architecture)
- [Zookeeper 介绍](http://www.slideshare.net/sauravhaloi/introduction-to-apache-zookeeper)
- [构建微服务，你所需要知道的一切](https://cloudncode.wordpress.com/2016/07/22/msa-getting-started/)

## 数据库

<p align="center">
  <img src="http://i.imgur.com/Xkm5CXz.png"/>
  <br/>
  <strong><a href="https://www.youtube.com/watch?v=w95murBkYmU">资料来源：扩展你的用户数到第一个一千万</a></strong>
</p>

### 关系型数据库管理系统（RDBMS）

像 SQL 这样的关系型数据库是一系列以表的形式组织的数据项集合。

> 校对注：这里作者 SQL 可能指的是 MySQL

**ACID** 用来描述关系型数据库[事务](https://en.wikipedia.org/wiki/Database_transaction)的特性。

- **原子性** - 每个事务内部所有操作要么全部完成，要么全部不完成。
- **一致性** - 任何事务都使数据库从一个有效的状态转换到另一个有效状态。
- **隔离性** - 并发执行事务的结果与顺序执行事务的结果相同。
- **持久性** - 事务提交后，对系统的影响是永久的。

关系型数据库扩展包括许多技术：**主从复制**、**主主复制**、**联合**、**分片**、**非规范化**和 **SQL调优**。

<p align="center">
  <img src="http://i.imgur.com/C9ioGtn.png"/>
  <br/>
  <strong><a href="http://www.slideshare.net/jboner/scalability-availability-stability-patterns/">资料来源：可扩展性、可用性、稳定性、模式</a></strong>
</p>

#### 主从复制

主库同时负责读取和写入操作，并复制写入到一个或多个从库中，从库只负责读操作。树状形式的从库再将写入复制到更多的从库中去。如果主库离线，系统可以以只读模式运行，直到某个从库被提升为主库或有新的主库出现。

##### 不利之处：主从复制

- 将从库提升为主库需要额外的逻辑。
- 参考[不利之处：复制](#不利之处复制)中，主从复制和主主复制**共同**的问题。

<p align="center">
  <img src="http://i.imgur.com/krAHLGg.png"/>
  <br/>
  <strong><a href="http://www.slideshare.net/jboner/scalability-availability-stability-patterns/">资料来源：可扩展性、可用性、稳定性、模式</a></strong>
</p>

#### 主主复制

两个主库都负责读操作和写操作，写入操作时互相协调。如果其中一个主库挂机，系统可以继续读取和写入。

##### 不利之处： 主主复制

- 你需要添加负载均衡器或者在应用逻辑中做改动，来确定写入哪一个数据库。
- 多数主-主系统要么不能保证一致性（违反 ACID），要么因为同步产生了写入延迟。
- 随着更多写入节点的加入和延迟的提高，如何解决冲突显得越发重要。
- 参考[不利之处：复制](#不利之处复制)中，主从复制和主主复制**共同**的问题。

##### 不利之处：复制


- 如果主库在将新写入的数据复制到其他节点前挂掉，则有数据丢失的可能。
- 写入会被重放到负责读取操作的副本。副本可能因为过多写操作阻塞住，导致读取功能异常。
- 读取从库越多，需要复制的写入数据就越多，导致更严重的复制延迟。
- 在某些数据库系统中，写入主库的操作可以用多个线程并行写入，但读取副本只支持单线程顺序地写入。
- 复制意味着更多的硬件和额外的复杂度。


##### 来源及延伸阅读


- [扩展性，可用性，稳定性模式](http://www.slideshare.net/jboner/scalability-availability-stability-patterns/)
- [多主复制](https://en.wikipedia.org/wiki/Multi-master_replication)

#### 联合

<p align="center">
  <img src="http://i.imgur.com/U3qV33e.png"/>
  <br/>
  <strong><a href="https://www.youtube.com/watch?v=w95murBkYmU">资料来源：扩展你的用户数到第一个一千万</a></strong>
</p>

联合（或按功能划分）将数据库按对应功能分割。例如，你可以有三个数据库：**论坛**、**用户**和**产品**，而不仅是一个单体数据库，从而减少每个数据库的读取和写入流量，减少复制延迟。较小的数据库意味着更多适合放入内存的数据，进而意味着更高的缓存命中几率。没有只能串行写入的中心化主库，你可以并行写入，提高负载能力。

##### 不利之处：联合


- 如果你的数据库模式需要大量的功能和数据表，联合的效率并不好。
- 你需要更新应用程序的逻辑来确定要读取和写入哪个数据库。
- 用 [server link](http://stackoverflow.com/questions/5145637/querying-data-by-joining-two-tables-in-two-database-on-different-servers) 从两个库联结数据更复杂。
- 联合需要更多的硬件和额外的复杂度。

##### 来源及延伸阅读：联合

- [扩展你的用户数到第一个一千万](https://www.youtube.com/watch?v=w95murBkYmU)

#### 分片

<p align="center">
  <img src="http://i.imgur.com/wU8x5Id.png"/>
  <br/>
  <strong><a href="http://www.slideshare.net/jboner/scalability-availability-stability-patterns/">资料来源：可扩展性、可用性、稳定性、模式</a></strong>
</p>

分片将数据分配在不同的数据库上，使得每个数据库仅管理整个数据集的一个子集。以用户数据库为例，随着用户数量的增加，越来越多的分片会被添加到集群中。

类似[联合](#联合)的优点，分片可以减少读取和写入流量，减少复制并提高缓存命中率。也减少了索引，通常意味着查询更快，性能更好。如果一个分片出问题，其他的仍能运行，你可以使用某种形式的冗余来防止数据丢失。类似联合，没有只能串行写入的中心化主库，你可以并行写入，提高负载能力。

常见的做法是用户姓氏的首字母或者用户的地理位置来分隔用户表。

##### 不利之处：分片

- 你需要修改应用程序的逻辑来实现分片，这会带来复杂的 SQL 查询。
- 分片不合理可能导致数据负载不均衡。例如，被频繁访问的用户数据会导致其所在分片的负载相对其他分片高。
  - 再平衡会引入额外的复杂度。基于[一致性哈希](http://www.paperplanes.de/2011/12/9/the-magic-of-consistent-hashing.html)的分片算法可以减少这种情况。
- 联结多个分片的数据操作更复杂。
- 分片需要更多的硬件和额外的复杂度。

#### 来源及延伸阅读：分片

- [分片时代来临](http://highscalability.com/blog/2009/8/6/an-unorthodox-approach-to-database-design-the-coming-of-the.html)
- [数据库分片架构](https://en.wikipedia.org/wiki/Shard_(database_architecture))
- [一致性哈希](http://www.paperplanes.de/2011/12/9/the-magic-of-consistent-hashing.html)

#### 非规范化

非规范化试图以写入性能为代价来换取读取性能。在多个表中冗余数据副本，以避免高成本的联结操作。一些关系型数据库，比如 [PostgreSQL](https://en.wikipedia.org/wiki/PostgreSQL) 和 Oracle 支持[物化视图](https://en.wikipedia.org/wiki/Materialized_view)，可以处理冗余信息存储和保证冗余副本一致。

当数据使用诸如[联合](#联合)和[分片](#分片)等技术被分割，进一步提高了处理跨数据中心的联结操作复杂度。非规范化可以规避这种复杂的联结操作。

在多数系统中，读取操作的频率远高于写入操作，比例可达到 100:1，甚至 1000:1。需要复杂的数据库联结的读取操作成本非常高，在磁盘操作上消耗了大量时间。

##### 不利之处：非规范化

- 数据会冗余。
- 约束可以帮助冗余的信息副本保持同步，但这样会增加数据库设计的复杂度。
- 非规范化的数据库在高写入负载下性能可能比规范化的数据库差。

##### 来源及延伸阅读：非规范化

- [非规范化](https://en.wikipedia.org/wiki/Denormalization)

#### SQL 调优

SQL 调优是一个范围很广的话题，有很多相关的[书](https://www.amazon.com/s/ref=nb_sb_noss_2?url=search-alias%3Daps&field-keywords=sql+tuning)可以作为参考。

利用**基准测试**和**性能分析**来模拟和发现系统瓶颈很重要。

- **基准测试** - 用 [ab](http://httpd.apache.org/docs/2.2/programs/ab.html) 等工具模拟高负载情况。
- **性能分析** - 通过启用如[慢查询日志](http://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html)等工具来辅助追踪性能问题。

基准测试和性能分析可能会指引你到以下优化方案。

##### 改进模式

- 为了实现快速访问，MySQL 在磁盘上用连续的块存储数据。
- 使用 `CHAR` 类型存储固定长度的字段，不要用 `VARCHAR`。
  - `CHAR` 在快速、随机访问时效率很高。如果使用 `VARCHAR`，如果你想读取下一个字符串，不得不先读取到当前字符串的末尾。
- 使用 `TEXT` 类型存储大块的文本，例如博客正文。`TEXT` 还允许布尔搜索。使用 `TEXT` 字段需要在磁盘上存储一个用于定位文本块的指针。
- 使用 `INT` 类型存储高达 2^32 或 40 亿的较大数字。
- 使用 `DECIMAL` 类型存储货币可以避免浮点数表示错误。
- 避免使用 `BLOBS` 存储实际对象，而是用来存储存放对象的位置。
- `VARCHAR(255)` 是以 8 位数字存储的最大字符数，在某些关系型数据库中，最大限度地利用字节。
- 在适用场景中设置 `NOT NULL` 约束来[提高搜索性能](http://stackoverflow.com/questions/1017239/how-do-null-values-affect-performance-in-a-database-search)。

##### 使用正确的索引

- 你正查询（`SELECT`、`GROUP BY`、`ORDER BY`、`JOIN`）的列如果用了索引会更快。
- 索引通常表示为自平衡的 [B 树](https://en.wikipedia.org/wiki/B-tree)，可以保持数据有序，并允许在对数时间内进行搜索，顺序访问，插入，删除操作。
- 设置索引，会将数据存在内存中，占用了更多内存空间。
- 写入操作会变慢，因为索引需要被更新。
- 加载大量数据时，禁用索引再加载数据，然后重建索引，这样也许会更快。

##### 避免高成本的联结操作

- 有性能需要，可以进行非规范化。

##### 分割数据表

- 将热点数据拆分到单独的数据表中，可以有助于缓存。

##### 调优查询缓存

- 在某些情况下，[查询缓存](http://dev.mysql.com/doc/refman/5.7/en/query-cache)可能会导致[性能问题](https://www.percona.com/blog/2014/01/28/10-mysql-performance-tuning-settings-after-installation/)。

##### 来源及延伸阅读

- [MySQL 查询优化小贴士](http://20bits.com/article/10-tips-for-optimizing-mysql-queries-that-dont-suck)
- [为什么 VARCHAR(255) 很常见？](http://stackoverflow.com/questions/1217466/is-there-a-good-reason-i-see-varchar255-used-so-often-as-opposed-to-another-l)
- [Null 值是如何影响数据库性能的？](http://stackoverflow.com/questions/1017239/how-do-null-values-affect-performance-in-a-database-search)
- [慢查询日志](http://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html)

### NoSQL

NoSQL 是**键-值数据库**、**文档型数据库**、**列型数据库**或**图数据库**的统称。数据库是非规范化的，表联结大多在应用程序代码中完成。大多数 NoSQL 无法实现真正符合 ACID 的事务，支持[最终一致](#最终一致性)。

**BASE** 通常被用于描述 NoSQL 数据库的特性。相比 [CAP 理论](#cap-理论)，BASE 强调可用性超过一致性。

- **基本可用** - 系统保证可用性。
- **软状态** - 即使没有输入，系统状态也可能随着时间变化。
- **最终一致性** - 经过一段时间之后，系统最终会变一致，因为系统在此期间没有收到任何输入。

除了在 [SQL 还是 NoSQL](#sql-还是-nosql) 之间做选择，了解哪种类型的 NoSQL 数据库最适合你的用例也是非常有帮助的。我们将在下一节中快速了解下 **键-值存储**、**文档型存储**、**列型存储**和**图存储**数据库。

#### 键-值存储

> 抽象模型：哈希表

键-值存储通常可以实现 O(1) 时间读写，用内存或 SSD 存储数据。数据存储可以按[字典顺序](https://en.wikipedia.org/wiki/Lexicographical_order)维护键，从而实现键的高效检索。键-值存储可以用于存储元数据。

键-值存储性能很高，通常用于存储简单数据模型或频繁修改的数据，如存放在内存中的缓存。键-值存储提供的操作有限，如果需要更多操作，复杂度将转嫁到应用程序层面。

键-值存储是如文档存储，在某些情况下，甚至是图存储等更复杂的存储系统的基础。

#### 来源及延伸阅读

- [键-值数据库](https://en.wikipedia.org/wiki/Key-value_database)
- [键-值存储的劣势](http://stackoverflow.com/questions/4056093/what-are-the-disadvantages-of-using-a-key-value-table-over-nullable-columns-or)
- [Redis 架构](http://qnimate.com/overview-of-redis-architecture/)
- [Memcached 架构](https://www.adayinthelifeof.nl/2011/02/06/memcache-internals/)

#### 文档类型存储

> 抽象模型：将文档作为值的键-值存储

文档类型存储以文档（XML、JSON、二进制文件等）为中心，文档存储了指定对象的全部信息。文档存储根据文档自身的内部结构提供 API 或查询语句来实现查询。请注意，许多键-值存储数据库有用值存储元数据的特性，这也模糊了这两种存储类型的界限。

基于底层实现，文档可以根据集合、标签、元数据或者文件夹组织。尽管不同文档可以被组织在一起或者分成一组，但相互之间可能具有完全不同的字段。

MongoDB 和 CouchDB 等一些文档类型存储还提供了类似 SQL 语言的查询语句来实现复杂查询。DynamoDB 同时支持键-值存储和文档类型存储。

文档类型存储具备高度的灵活性，常用于处理偶尔变化的数据。

#### 来源及延伸阅读：文档类型存储

- [面向文档的数据库](https://en.wikipedia.org/wiki/Document-oriented_database)
- [MongoDB 架构](https://www.mongodb.com/mongodb-architecture)
- [CouchDB 架构](https://blog.couchdb.org/2016/08/01/couchdb-2-0-architecture/)
- [Elasticsearch 架构](https://www.elastic.co/blog/found-elasticsearch-from-the-bottom-up)

#### 列型存储

<p align="center">
  <img src="http://i.imgur.com/n16iOGk.png"/>
  <br/>
  <strong><a href="http://blog.grio.com/2015/11/sql-nosql-a-brief-history.html">资料来源: SQL 和 NoSQL，一个简短的历史</a></strong>
</p>

> 抽象模型：嵌套的 `ColumnFamily<RowKey, Columns<ColKey, Value, Timestamp>>` 映射

类型存储的基本数据单元是列（名／值对）。列可以在列族（类似于 SQL 的数据表）中被分组。超级列族再分组普通列族。你可以使用行键独立访问每一列，具有相同行键值的列组成一行。每个值都包含版本的时间戳用于解决版本冲突。

Google 发布了第一个列型存储数据库 [Bigtable](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/chang06bigtable.pdf)，它影响了 Hadoop 生态系统中活跃的开源数据库 [HBase](https://www.mapr.com/blog/in-depth-look-hbase-architecture) 和 Facebook 的 [Cassandra](http://docs.datastax.com/en/archived/cassandra/2.0/cassandra/architecture/architectureIntro_c.html)。像 BigTable，HBase 和 Cassandra 这样的存储系统将键以字母顺序存储，可以高效地读取键列。

列型存储具备高可用性和高可扩展性。通常被用于大数据相关存储。

##### 来源及延伸阅读：列型存储

- [SQL 与 NoSQL 简史](http://blog.grio.com/2015/11/sql-nosql-a-brief-history.html)
- [BigTable 架构](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/chang06bigtable.pdf)
- [Hbase 架构](https://www.mapr.com/blog/in-depth-look-hbase-architecture)
- [Cassandra 架构](http://docs.datastax.com/en/archived/cassandra/2.0/cassandra/architecture/architectureIntro_c.html)

#### 图数据库

<p align="center">
  <img src="http://i.imgur.com/fNcl65g.png"/>
  <br/>
  <strong><a href="https://en.wikipedia.org/wiki/File:GraphDatabase_PropertyGraph.png"/>资料来源：图数据库</a></strong>
</p>

> 抽象模型： 图

在图数据库中，一个节点对应一条记录，一个弧对应两个节点之间的关系。图数据库被优化用于表示外键繁多的复杂关系或多对多关系。

图数据库为存储复杂关系的数据模型，如社交网络，提供了很高的性能。它们相对较新，尚未广泛应用，查找开发工具或者资源相对较难。许多图只能通过 [REST API](#表述性状态转移rest) 访问。

##### 相关资源和延伸阅读：图
- [图数据库](https://en.wikipedia.org/wiki/Graph_database)
- [Neo4j](https://neo4j.com/)
- [FlockDB](https://blog.twitter.com/2010/introducing-flockdb)

#### 来源及延伸阅读：NoSQL

- [数据库术语解释](http://stackoverflow.com/questions/3342497/explanation-of-base-terminology)
- [NoSQL 数据库 - 调查及决策指南](https://medium.com/baqend-blog/nosql-databases-a-survey-and-decision-guidance-ea7823a822d#.wskogqenq)
- [可扩展性](http://www.lecloud.net/post/7994751381/scalability-for-dummies-part-2-database)
- [NoSQL 介绍](https://www.youtube.com/watch?v=qI_g07C_Q5I)
- [NoSQL 模式](http://horicky.blogspot.com/2009/11/nosql-patterns.html)

### SQL 还是 NoSQL

<p align="center">
  <img src="http://i.imgur.com/wXGqG5f.png"/>
  <br/>
  <strong><a href="https://www.infoq.com/articles/Transition-RDBMS-NoSQL/">资料来源：从 RDBMS 转换到 NoSQL</a></strong>
</p>

选取 **SQL** 的原因:

- 结构化数据
- 严格的模式
- 关系型数据
- 需要复杂的联结操作
- 事务
- 清晰的扩展模式
- 既有资源更丰富：开发者、社区、代码库、工具等
- 通过索引进行查询非常快

选取 **NoSQL** 的原因：

- 半结构化数据
- 动态或灵活的模式
- 非关系型数据
- 不需要复杂的联结操作
- 存储 TB （甚至 PB）级别的数据
- 高数据密集的工作负载
- IOPS 高吞吐量

适合 NoSQL 的示例数据：

- 埋点数据和日志数据
- 排行榜或者得分数据
- 临时数据，如购物车
- 频繁访问的（“热”）表
- 元数据／查找表

##### 来源及延伸阅读：SQL 或 NoSQL

- [扩展你的用户数到第一个千万](https://www.youtube.com/watch?v=w95murBkYmU)
- [SQL 和 NoSQL 的不同](https://www.sitepoint.com/sql-vs-nosql-differences/)
## 缓存

<p align="center">
  <img src="http://i.imgur.com/Q6z24La.png"/>
  <br/>
  <strong><a href="http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html">资料来源：可扩展的系统设计模式</a></strong>
</p>

缓存可以提高页面加载速度，并可以减少服务器和数据库的负载。在这个模型中，分发器先查看请求之前是否被响应过，如果有则将之前的结果直接返回，来省掉真正的处理。

数据库分片均匀分布的读取是最好的。但是热门数据会让读取分布不均匀，这样就会造成瓶颈，如果在数据库前加个缓存，就会抹平不均匀的负载和突发流量对数据库的影响。

### 客户端缓存

缓存可以位于客户端（操作系统或者浏览器），[服务端](#反向代理web-服务器)或者不同的缓存层。

### CDN 缓存

[CDN](#内容分发网络cdn) 也被视为一种缓存。

### Web 服务器缓存

[反向代理](#反向代理web-服务器)和缓存（比如 [Varnish](https://www.varnish-cache.org/)）可以直接提供静态和动态内容。Web 服务器同样也可以缓存请求，返回相应结果而不必连接应用服务器。

### 数据库缓存

数据库的默认配置中通常包含缓存级别，针对一般用例进行了优化。调整配置，在不同情况下使用不同的模式可以进一步提高性能。

### 应用缓存

基于内存的缓存比如 Memcached 和 Redis 是应用程序和数据存储之间的一种键值存储。由于数据保存在 RAM 中，它比存储在磁盘上的典型数据库要快多了。RAM 比磁盘限制更多，所以例如 [least recently used (LRU)](https://en.wikipedia.org/wiki/Cache_algorithms#Least_Recently_Used) 的[缓存无效算法](https://en.wikipedia.org/wiki/Cache_algorithms)可以将「热门数据」放在 RAM 中，而对一些比较「冷门」的数据不做处理。

Redis 有下列附加功能：

- 持久性选项
- 内置数据结构比如有序集合和列表

有多个缓存级别，分为两大类：**数据库查询**和**对象**：

- 行级别
- 查询级别
- 完整的可序列化对象
- 完全渲染的 HTML

一般来说，你应该尽量避免基于文件的缓存，因为这使得复制和自动缩放很困难。

### 数据库查询级别的缓存

当你查询数据库的时候，将查询语句的哈希值与查询结果存储到缓存中。这种方法会遇到以下问题：

- 很难用复杂的查询删除已缓存结果。
- 如果一条数据比如表中某条数据的一项被改变，则需要删除所有可能包含已更改项的缓存结果。

### 对象级别的缓存

将您的数据视为对象，就像对待你的应用代码一样。让应用程序将数据从数据库中组合到类实例或数据结构中：

- 如果对象的基础数据已经更改了，那么从缓存中删掉这个对象。
- 允许异步处理：workers 通过使用最新的缓存对象来组装对象。

建议缓存的内容：

- 用户会话
- 完全渲染的 Web 页面
- 活动流
- 用户图数据

### 何时更新缓存

由于你只能在缓存中存储有限的数据，所以你需要选择一个适用于你用例的缓存更新策略。

#### 缓存模式

<p align="center">
  <img src="http://i.imgur.com/ONjORqk.png"/>
  <br/>
  <strong><a href="http://www.slideshare.net/tmatyashovsky/from-cache-to-in-memory-data-grid-introduction-to-hazelcast">资料来源：从缓存到内存数据网格</a></strong>
</p>

应用从存储器读写。缓存不和存储器直接交互，应用执行以下操作：

- 在缓存中查找记录，如果所需数据不在缓存中
- 从数据库中加载所需内容
- 将查找到的结果存储到缓存中
- 返回所需内容

```python
def get_user(self, user_id):
    user = cache.get("user.{0}", user_id)
    if user is None:
        user = db.query("SELECT * FROM users WHERE user_id = {0}", user_id)
        if user is not None:
            key = "user.{0}".format(user_id)
            cache.set(key, json.dumps(user))
    return user
```

[Memcached](https://memcached.org/) 通常用这种方式使用。

添加到缓存中的数据读取速度很快。缓存模式也称为延迟加载。只缓存所请求的数据，这避免了没有被请求的数据占满了缓存空间。

##### 缓存的缺点：

- 请求的数据如果不在缓存中就需要经过三个步骤来获取数据，这会导致明显的延迟。
- 如果数据库中的数据更新了会导致缓存中的数据过时。这个问题需要通过设置 TTL 强制更新缓存或者直写模式来缓解这种情况。
- 当一个节点出现故障的时候，它将会被一个新的节点替代，这增加了延迟的时间。

#### 直写模式

<p align="center">
  <img src="http://i.imgur.com/0vBc0hN.png"/>
  <br/>
  <strong><a href="http://www.slideshare.net/jboner/scalability-availability-stability-patterns/">资料来源：可扩展性、可用性、稳定性、模式</a></strong>
</p>

应用使用缓存作为主要的数据存储，将数据读写到缓存中，而缓存负责从数据库中读写数据。

- 应用向缓存中添加/更新数据
- 缓存同步地写入数据存储
- 返回所需内容

应用代码：

```
set_user(12345, {"foo":"bar"})
```

缓存代码：

```python
def set_user(user_id, values):
    user = db.query("UPDATE Users WHERE id = {0}", user_id, values)
    cache.set(user_id, user)
```

由于存写操作所以直写模式整体是一种很慢的操作，但是读取刚写入的数据很快。相比读取数据，用户通常比较能接受更新数据时速度较慢。缓存中的数据不会过时。

##### 直写模式的缺点：

- 由于故障或者缩放而创建的新的节点，新的节点不会缓存，直到数据库更新为止。缓存应用直写模式可以缓解这个问题。
- 写入的大多数数据可能永远都不会被读取，用 TTL 可以最小化这种情况的出现。

#### 回写模式

<p align="center">
  <img src="http://i.imgur.com/rgSrvjG.png"/>
  <br/>
  <strong><a href="http://www.slideshare.net/jboner/scalability-availability-stability-patterns/">资料来源：可扩展性、可用性、稳定性、模式</a></strong>
</p>

在回写模式中，应用执行以下操作：

- 在缓存中增加或者更新条目
- 异步写入数据，提高写入性能。

##### 回写模式的缺点：

- 缓存可能在其内容成功存储之前丢失数据。
- 执行直写模式比缓存或者回写模式更复杂。

#### 刷新

<p align="center">
  <img src="http://i.imgur.com/kxtjqgE.png"/>
  <br/>
  <strong><a href=http://www.slideshare.net/tmatyashovsky/from-cache-to-in-memory-data-grid-introduction-to-hazelcast>资料来源：从缓存到内存数据网格</a></strong>
</p>

你可以将缓存配置成在到期之前自动刷新最近访问过的内容。

如果缓存可以准确预测将来可能请求哪些数据，那么刷新可能会导致延迟与读取时间的降低。

##### 刷新的缺点：

- 不能准确预测到未来需要用到的数据可能会导致性能不如不使用刷新。

### 缓存的缺点：

- 需要保持缓存和真实数据源之间的一致性，比如数据库根据[缓存无效](https://en.wikipedia.org/wiki/Cache_algorithms)。
- 需要改变应用程序比如增加 Redis 或者 memcached。
- 无效缓存是个难题，什么时候更新缓存是与之相关的复杂问题。

### 相关资源和延伸阅读

- [从缓存到内存数据](http://www.slideshare.net/tmatyashovsky/from-cache-to-in-memory-data-grid-introduction-to-hazelcast)
- [可扩展系统设计模式](http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html)
- [可缩放系统构架介绍](http://lethain.com/introduction-to-architecting-systems-for-scale/)
- [可扩展性，可用性，稳定性和模式](http://www.slideshare.net/jboner/scalability-availability-stability-patterns/)
- [可扩展性](http://www.lecloud.net/post/9246290032/scalability-for-dummies-part-3-cache)
- [AWS ElastiCache 策略](http://docs.aws.amazon.com/AmazonElastiCache/latest/UserGuide/Strategies.html)
- [维基百科](https://en.wikipedia.org/wiki/Cache_(computing))

## 异步

<p align="center">
  <img src="http://i.imgur.com/54GYsSx.png"/>
  <br/>
  <strong><a href=http://lethain.com/introduction-to-architecting-systems-for-scale/#platform_layer>资料来源：可缩放系统构架介绍</a></strong>
</p>

异步工作流有助于减少那些原本顺序执行的请求时间。它们可以通过提前进行一些耗时的工作来帮助减少请求时间，比如定期汇总数据。

### 消息队列

消息队列接收，保留和传递消息。如果按顺序执行操作太慢的话，你可以使用有以下工作流的消息队列：

- 应用程序将作业发布到队列，然后通知用户作业状态
- 一个 worker 从队列中取出该作业，对其进行处理，然后显示该作业完成

不去阻塞用户操作，作业在后台处理。在此期间，客户端可能会进行一些处理使得看上去像是任务已经完成了。例如，如果要发送一条推文，推文可能会马上出现在你的时间线上，但是可能需要一些时间才能将你的推文推送到你的所有关注者那里去。

**Redis** 是一个令人满意的简单的消息代理，但是消息有可能会丢失。

**RabbitMQ** 很受欢迎但是要求你适应「AMQP」协议并且管理你自己的节点。

**Amazon SQS** 是被托管的，但可能具有高延迟，并且消息可能会被传送两次。

### 任务队列

任务队列接收任务及其相关数据，运行它们，然后传递其结果。 它们可以支持调度，并可用于在后台运行计算密集型作业。

**Celery** 支持调度，主要是用 Python 开发的。

### 背压

如果队列开始明显增长，那么队列大小可能会超过内存大小，导致高速缓存未命中，磁盘读取，甚至性能更慢。[背压](http://mechanical-sympathy.blogspot.com/2012/05/apply-back-pressure-when-overloaded.html)可以通过限制队列大小来帮助我们，从而为队列中的作业保持高吞吐率和良好的响应时间。一旦队列填满，客户端将得到服务器忙或者 HTTP 503 状态码，以便稍后重试。客户端可以在稍后时间重试该请求，也许是[指数退避](https://en.wikipedia.org/wiki/Exponential_backoff)。

### 异步的缺点：

- 简单的计算和实时工作流等用例可能更适用于同步操作，因为引入队列可能会增加延迟和复杂性。

### 相关资源和延伸阅读

- [这是一个数字游戏](https://www.youtube.com/watch?v=1KRYH75wgy4)
- [超载时应用背压](http://mechanical-sympathy.blogspot.com/2012/05/apply-back-pressure-when-overloaded.html)
- [利特尔法则](https://en.wikipedia.org/wiki/Little%27s_law)
- [消息队列与任务队列有什么区别？](https://www.quora.com/What-is-the-difference-between-a-message-queue-and-a-task-queue-Why-would-a-task-queue-require-a-message-broker-like-RabbitMQ-Redis-Celery-or-IronMQ-to-function)

## 通讯

<p align="center">
  <img src="http://i.imgur.com/5KeocQs.jpg"/>
  <br/>
  <strong><a href=http://www.escotal.com/osilayer.html>资料来源：OSI 7层模型</a></strong>
</p>

### 超文本传输协议（HTTP）

HTTP 是一种在客户端和服务器之间编码和传输数据的方法。它是一个请求/响应协议：客户端和服务端针对相关内容和完成状态信息的请求和响应。HTTP 是独立的，允许请求和响应流经许多执行负载均衡，缓存，加密和压缩的中间路由器和服务器。

一个基本的 HTTP 请求由一个动词（方法）和一个资源（端点）组成。 以下是常见的 HTTP 动词：

| 动词     | 描述             | *幂等  | 安全性  | 可缓存            |
| ------ | -------------- | ---- | ---- | -------------- |
| GET    | 读取资源           | Yes  | Yes  | Yes            |
| POST   | 创建资源或触发处理数据的进程 | No   | No   | Yes，如果回应包含刷新信息 |
| PUT    | 创建或替换资源        | Yes  | No   | No             |
| PATCH  | 部分更新资源         | No   | No   | Yes，如果回应包含刷新信息 |
| DELETE | 删除资源           | Yes  | No   | No             |



**多次执行不会产生不同的结果**。

HTTP 是依赖于较低级协议（如 **TCP** 和 **UDP**）的应用层协议。

#### 来源及延伸阅读：HTTP

* [README](https://www.quora.com/What-is-the-difference-between-HTTP-protocol-and-TCP-protocol)    +
* [HTTP 是什么？](https://www.nginx.com/resources/glossary/http/)
* [HTTP 和 TCP 的区别](https://www.quora.com/What-is-the-difference-between-HTTP-protocol-and-TCP-protocol)
* [PUT 和 PATCH的区别](https://laracasts.com/discuss/channels/general-discussion/whats-the-differences-between-put-and-patch?page=1)

### 传输控制协议（TCP）

<p align="center">
  <img src="http://i.imgur.com/JdAsdvG.jpg"/>
  <br/>
  <strong><a href="http://www.wildbunny.co.uk/blog/2012/10/09/how-to-make-a-multi-player-game-part-1/">资料来源：如何制作多人游戏</a></strong>
</p>

TCP 是通过 [IP 网络](https://en.wikipedia.org/wiki/Internet_Protocol)的面向连接的协议。 使用[握手](https://en.wikipedia.org/wiki/Handshaking)建立和断开连接。 发送的所有数据包保证以原始顺序到达目的地，用以下措施保证数据包不被损坏：

- 每个数据包的序列号和[校验码](https://en.wikipedia.org/wiki/Transmission_Control_Protocol#Checksum_computation)。
- [确认包](https://en.wikipedia.org/wiki/Acknowledgement_(data_networks))和自动重传

如果发送者没有收到正确的响应，它将重新发送数据包。如果多次超时，连接就会断开。TCP 实行[流量控制](https://en.wikipedia.org/wiki/Flow_control_(data))和[拥塞控制](https://en.wikipedia.org/wiki/Network_congestion#Congestion_control)。这些确保措施会导致延迟，而且通常导致传输效率比 UDP 低。

为了确保高吞吐量，Web 服务器可以保持大量的 TCP 连接，从而导致高内存使用。在 Web 服务器线程间拥有大量开放连接可能开销巨大，消耗资源过多，也就是说，一个 [memcached](#memcached) 服务器。[连接池](https://en.wikipedia.org/wiki/Connection_pool) 可以帮助除了在适用的情况下切换到 UDP。

TCP  对于需要高可靠性但时间紧迫的应用程序很有用。比如包括 Web 服务器，数据库信息，SMTP，FTP 和 SSH。

以下情况使用 TCP 代替 UDP：

- 你需要数据完好无损。
- 你想对网络吞吐量自动进行最佳评估。

### 用户数据报协议（UDP）

<p align="center">
  <img src="http://i.imgur.com/yzDrJtA.jpg"/>
  <br/>
  <strong><a href="http://www.wildbunny.co.uk/blog/2012/10/09/how-to-make-a-multi-player-game-part-1">资料来源：如何制作多人游戏</a></strong>
</p>

UDP 是无连接的。数据报（类似于数据包）只在数据报级别有保证。数据报可能会无序的到达目的地，也有可能会遗失。UDP 不支持拥塞控制。虽然不如 TCP 那样有保证，但 UDP 通常效率更高。

UDP 可以通过广播将数据报发送至子网内的所有设备。这对 [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol) 很有用，因为子网内的设备还没有分配 IP 地址，而 IP 对于 TCP 是必须的。

UDP 可靠性更低但适合用在网络电话、视频聊天，流媒体和实时多人游戏上。

以下情况使用 UDP 代替 TCP：

* 你需要低延迟
* 相对于数据丢失更糟的是数据延迟
* 你想实现自己的错误校正方法

#### 来源及延伸阅读：TCP 与 UDP

* [游戏编程的网络](http://gafferongames.com/networking-for-game-programmers/udp-vs-tcp/)
* [TCP 与 UDP 的关键区别](http://www.cyberciti.biz/faq/key-differences-between-tcp-and-udp-protocols/)
* [TCP 与 UDP 的不同](http://stackoverflow.com/questions/5970383/difference-between-tcp-and-udp)
* [传输控制协议](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)
* [用户数据报协议](https://en.wikipedia.org/wiki/User_Datagram_Protocol)
* [Memcache 在 Facebook 的扩展](http://www.cs.bu.edu/~jappavoo/jappavoo.github.com/451/papers/memcache-fb.pdf)

### 远程过程调用协议（RPC）

<p align="center">
  <img src="http://i.imgur.com/iF4Mkb5.png"/>
  <br/>
  <strong><a href="http://www.puncsky.com/blog/2016/02/14/crack-the-system-design-interview">Source: Crack the system design interview</a></strong>
</p>

在 RPC 中，客户端会去调用另一个地址空间（通常是一个远程服务器）里的方法。调用代码看起来就像是调用的是一个本地方法，客户端和服务器交互的具体过程被抽象。远程调用相对于本地调用一般较慢而且可靠性更差，因此区分两者是有帮助的。热门的 RPC 框架包括 [Protobuf](https://developers.google.com/protocol-buffers/)、[Thrift](https://thrift.apache.org/) 和 [Avro](https://avro.apache.org/docs/current/)。

RPC 是一个“请求-响应”协议：

* **客户端程序** ── 调用客户端存根程序。就像调用本地方法一样，参数会被压入栈中。
* **客户端 stub 程序** ── 将请求过程的 id 和参数打包进请求信息中。
* **客户端通信模块** ── 将信息从客户端发送至服务端。
* **服务端通信模块** ── 将接受的包传给服务端存根程序。
* **服务端 stub 程序** ── 将结果解包，依据过程 id 调用服务端方法并将参数传递过去。

RPC 调用示例：

```
GET /someoperation?data=anId

POST /anotheroperation
{
  "data":"anId";
  "anotherdata": "another value"
}
```

RPC 专注于暴露方法。RPC 通常用于处理内部通讯的性能问题，这样你可以手动处理本地调用以更好的适应你的情况。


当以下情况时选择本地库（也就是 SDK）：

* 你知道你的目标平台。
* 你想控制如何访问你的“逻辑”。
* 你想对发生在你的库中的错误进行控制。
* 性能和终端用户体验是你最关心的事。

遵循 **REST** 的 HTTP API 往往更适用于公共 API。

#### 缺点：RPC

* RPC 客户端与服务实现捆绑地很紧密。
* 一个新的 API 必须在每一个操作或者用例中定义。
* RPC 很难调试。
* 你可能没办法很方便的去修改现有的技术。举个例子，如果你希望在 [Squid](http://www.squid-cache.org/) 这样的缓存服务器上确保 [RPC 被正确缓存](http://etherealbits.com/2012/12/debunking-the-myths-of-rpc-rest/)的话可能需要一些额外的努力了。

### 表述性状态转移（REST）

REST 是一种强制的客户端/服务端架构设计模型，客户端基于服务端管理的一系列资源操作。服务端提供修改或获取资源的接口。所有的通信必须是无状态和可缓存的。

RESTful 接口有四条规则：

* **标志资源（HTTP 里的 URI）** ── 无论什么操作都使用同一个 URI。
* **表示的改变（HTTP 的动作）** ── 使用动作, headers 和 body。
* **可自我描述的错误信息（HTTP 中的 status code）** ── 使用状态码，不要重新造轮子。
* **[HATEOAS](http://restcookbook.com/Basics/hateoas/)（HTTP 中的HTML 接口）** ── 你的 web 服务器应该能够通过浏览器访问。

REST 请求的例子：

```
GET /someresources/anId

PUT /someresources/anId
{"anotherdata": "another value"}
```

REST 关注于暴露数据。它减少了客户端／服务端的耦合程度，经常用于公共 HTTP API 接口设计。REST 使用更通常与规范化的方法来通过 URI 暴露资源，[通过 header 来表述](https://github.com/for-GET/know-your-http-well/blob/master/headers.md)并通过 GET、POST、PUT、DELETE 和 PATCH 这些动作来进行操作。因为无状态的特性，REST 易于横向扩展和隔离。

#### 缺点：REST

* 由于 REST 将重点放在暴露数据，所以当资源不是自然组织的或者结构复杂的时候它可能无法很好的适应。举个例子，返回过去一小时中与特定事件集匹配的更新记录这种操作就很难表示为路径。使用 REST，可能会使用 URI 路径，查询参数和可能的请求体来实现。
* REST 一般依赖几个动作（GET、POST、PUT、DELETE 和 PATCH），但有时候仅仅这些没法满足你的需要。举个例子，将过期的文档移动到归档文件夹里去，这样的操作可能没法简单的用上面这几个 verbs 表达。
* 为了渲染单个页面，获取被嵌套在层级结构中的复杂资源需要客户端，服务器之间多次往返通信。例如，获取博客内容及其关联评论。对于使用不确定网络环境的移动应用来说，这些多次往返通信是非常麻烦的。
* 随着时间的推移，更多的字段可能会被添加到 API 响应中，较旧的客户端将会接收到所有新的数据字段，即使是那些它们不需要的字段，结果它会增加负载大小并引起更大的延迟。

### RPC 与 REST 比较

| 操作          | RPC                                      | REST                                     |
| ----------- | ---------------------------------------- | ---------------------------------------- |
| 注册          | **POST** /signup                         | **POST** /persons                        |
| 注销          | **POST** /resign<br/>{<br/>"personid": "1234"<br/>} | **DELETE** /persons/1234                 |
| 读取用户信息      | **GET** /readPerson?personid=1234        | **GET** /persons/1234                    |
| 读取用户物品列表    | **GET** /readUsersItemsList?personid=1234 | **GET** /persons/1234/items              |
| 向用户物品列表添加一项 | **POST** /addItemToUsersItemsList<br/>{<br/>"personid": "1234";<br/>"itemid": "456"<br/>} | **POST** /persons/1234/items<br/>{<br/>"itemid": "456"<br/>} |
| 更新一个物品      | **POST** /modifyItem<br/>{<br/>"itemid": "456";<br/>"key": "value"<br/>} | **PUT** /items/456<br/>{<br/>"key": "value"<br/>} |
| 删除一个物品      | **POST** /removeItem<br/>{<br/>"itemid": "456"<br/>} | **DELETE** /items/456                    |

<p align="center">
  <strong><a href="https://apihandyman.io/do-you-really-know-why-you-prefer-rest-over-rpc">资料来源：你真的知道你为什么更喜欢 REST 而不是 RPC 吗</a></strong>
</p>

#### 来源及延伸阅读：REST 与 RPC

* [你真的知道你为什么更喜欢 REST 而不是 RPC 吗](https://apihandyman.io/do-you-really-know-why-you-prefer-rest-over-rpc/)
* [什么时候 RPC 比 REST 更合适？](http://programmers.stackexchange.com/a/181186)
* [REST vs JSON-RPC](http://stackoverflow.com/questions/15056878/rest-vs-json-rpc)
* [揭开 RPC 和 REST 的神秘面纱](http://etherealbits.com/2012/12/debunking-the-myths-of-rpc-rest/)
* [使用 REST 的缺点是什么](https://www.quora.com/What-are-the-drawbacks-of-using-RESTful-APIs)
* [破解系统设计面试](http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview)
* [Thrift](https://code.facebook.com/posts/1468950976659943/)
* [为什么在内部使用 REST 而不是 RPC](http://arstechnica.com/civis/viewtopic.php?t=1190508)

## 安全

这一部分需要更多内容。[一起来吧](#贡献)！

安全是一个宽泛的话题。除非你有相当的经验、安全方面背景或者正在申请的职位要求安全知识，你不需要了解安全基础知识以外的内容：

* 在运输和等待过程中加密
* 对所有的用户输入和从用户那里发来的参数进行处理以防止 [XSS](https://en.wikipedia.org/wiki/Cross-site_scripting) 和 [SQL 注入](https://en.wikipedia.org/wiki/SQL_injection)。
* 使用参数化的查询来防止 SQL 注入。
* 使用[最小权限原则](https://en.wikipedia.org/wiki/Principle_of_least_privilege)。

### 来源及延伸阅读

* [为开发者准备的安全引导](https://github.com/FallibleInc/security-guide-for-developers)
* [OWASP top ten](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet)

## 附录

一些时候你会被要求做出保守估计。比如，你可能需要估计从磁盘中生成 100 张图片的缩略图需要的时间或者一个数据结构需要多少的内存。**2 的次方表**和**每个开发者都需要知道的一些时间数据**（译注：OSChina 上有这篇文章的[译文](https://www.oschina.net/news/30009/every-programmer-should-know)）都是一些很方便的参考资料。

### 2 的次方表

```
Power           Exact Value         Approx Value        Bytes
---------------------------------------------------------------
7                             128
8                             256
10                           1024   1 thousand           1 KB
16                         65,536                       64 KB
20                      1,048,576   1 million            1 MB
30                  1,073,741,824   1 billion            1 GB
32                  4,294,967,296                        4 GB
40              1,099,511,627,776   1 trillion           1 TB
```

#### 来源及延伸阅读

* [2 的次方](https://en.wikipedia.org/wiki/Power_of_two)

### 每个程序员都应该知道的延迟数

```
Latency Comparison Numbers
--------------------------
L1 cache reference                           0.5 ns
Branch mispredict                            5   ns
L2 cache reference                           7   ns                      14x L1 cache
Mutex lock/unlock                           25   ns
Main memory reference                      100   ns                      20x L2 cache, 200x L1 cache
Compress 1K bytes with Zippy            10,000   ns       10 us
Send 1 KB bytes over 1 Gbps network     10,000   ns       10 us
Read 4 KB randomly from SSD*           150,000   ns      150 us          ~1GB/sec SSD
Read 1 MB sequentially from memory     250,000   ns      250 us
Round trip within same datacenter      500,000   ns      500 us
Read 1 MB sequentially from SSD*     1,000,000   ns    1,000 us    1 ms  ~1GB/sec SSD, 4X memory
Disk seek                           10,000,000   ns   10,000 us   10 ms  20x datacenter roundtrip
Read 1 MB sequentially from 1 Gbps  10,000,000   ns   10,000 us   10 ms  40x memory, 10X SSD
Read 1 MB sequentially from disk    30,000,000   ns   30,000 us   30 ms 120x memory, 30X SSD
Send packet CA->Netherlands->CA    150,000,000   ns  150,000 us  150 ms

Notes
-----
1 ns = 10^-9 seconds
1 us = 10^-6 seconds = 1,000 ns
1 ms = 10^-3 seconds = 1,000 us = 1,000,000 ns
```

基于上述数字的指标：
* 从磁盘以 30 MB/s 的速度顺序读取
* 以 100 MB/s 从 1 Gbps 的以太网顺序读取
* 从 SSD 以 1 GB/s 的速度读取
* 以 4 GB/s 的速度从主存读取
* 每秒能绕地球 6-7 圈
* 数据中心内每秒有 2,000 次往返

#### 延迟数可视化

![](https://camo.githubusercontent.com/77f72259e1eb58596b564d1ad823af1853bc60a3/687474703a2f2f692e696d6775722e636f6d2f6b307431652e706e67)

#### 来源及延伸阅读

* [每个程序员都应该知道的延迟数 — 1](https://gist.github.com/jboner/2841832)
* [每个程序员都应该知道的延迟数 — 2](https://gist.github.com/hellerbarde/2843375)
* [关于建设大型分布式系统的的设计方案、课程和建议](http://www.cs.cornell.edu/projects/ladis2009/talks/dean-keynote-ladis2009.pdf)
* [关于建设大型可拓展分布式系统的软件工程咨询](https://static.googleusercontent.com/media/research.google.com/en//people/jeff/stanford-295-talk.pdf)

### 其它的系统设计面试题

> 常见的系统设计面试问题，给出了如何解决的方案链接

| 问题                      | 引用                                       |
| ----------------------- | ---------------------------------------- |
| 设计类似于 Dropbox 的文件同步服务   | [youtube.com](https://www.youtube.com/watch?v=PE4gwstWhmc) |
| 设计类似于 Google 的搜索引擎      | [queue.acm.org](http://queue.acm.org/detail.cfm?id=988407)<br/>[stackexchange.com](http://programmers.stackexchange.com/questions/38324/interview-question-how-would-you-implement-google-search)<br/>[ardendertat.com](http://www.ardendertat.com/2012/01/11/implementing-search-engines/)<br/>[stanford.edu](http://infolab.stanford.edu/~backrub/google.html) |
| 设计类似于 Google 的可扩展网络爬虫   | [quora.com](https://www.quora.com/How-can-I-build-a-web-crawler-from-scratch) |
| 设计 Google 文档            | [code.google.com](https://code.google.com/p/google-mobwrite/)<br/>[neil.fraser.name](https://neil.fraser.name/writing/sync/) |
| 设计类似 Redis 的键值存储        | [slideshare.net](http://www.slideshare.net/dvirsky/introduction-to-redis) |
| 设计类似 Memcached 的缓存系统    | [slideshare.net](http://www.slideshare.net/oemebamo/introduction-to-memcached) |
| 设计类似亚马逊的推荐系统            | [hulu.com](http://tech.hulu.com/blog/2011/09/19/recommendation-system.html)<br/>[ijcai13.org](http://ijcai13.org/files/tutorial_slides/td3.pdf) |
| 设计类似 Bitly 的短链接系统       | [n00tc0d3r.blogspot.com](http://n00tc0d3r.blogspot.com/) |
| 设计类似 WhatsApp 的聊天应用     | [highscalability.com](http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html) |
| 设计类似 Instagram 的图片分享系统  | [highscalability.com](http://highscalability.com/flickr-architecture)<br/>[highscalability.com](http://highscalability.com/blog/2011/12/6/instagram-architecture-14-million-users-terabytes-of-photos.html) |
| 设计 Facebook 的新闻推荐方法     | [quora.com](http://www.quora.com/What-are-best-practices-for-building-something-like-a-News-Feed)<br/>[quora.com](http://www.quora.com/Activity-Streams/What-are-the-scaling-issues-to-keep-in-mind-while-developing-a-social-network-feed)<br/>[slideshare.net](http://www.slideshare.net/danmckinley/etsy-activity-feeds-architecture) |
| 设计 Facebook 的时间线系统      | [facebook.com](https://www.facebook.com/note.php?note_id=10150468255628920)<br/>[highscalability.com](http://highscalability.com/blog/2012/1/23/facebook-timeline-brought-to-you-by-the-power-of-denormaliza.html) |
| 设计 Facebook 的聊天系统       | [erlang-factory.com](http://www.erlang-factory.com/upload/presentations/31/EugeneLetuchy-ErlangatFacebook.pdf)<br/>[facebook.com](https://www.facebook.com/note.php?note_id=14218138919&id=9445547199&index=0) |
| 设计类似 Facebook 的图表搜索系统   | [facebook.com](https://www.facebook.com/notes/facebook-engineering/under-the-hood-building-out-the-infrastructure-for-graph-search/10151347573598920)<br/>[facebook.com](https://www.facebook.com/notes/facebook-engineering/under-the-hood-indexing-and-ranking-in-graph-search/10151361720763920)<br/>[facebook.com](https://www.facebook.com/notes/facebook-engineering/under-the-hood-the-natural-language-interface-of-graph-search/10151432733048920) |
| 设计类似 CloudFlare 的内容传递网络 | [cmu.edu](http://repository.cmu.edu/cgi/viewcontent.cgi?article=2112&context=compsci) |
| 设计类似 Twitter 的热门话题系统    | [michael-noll.com](http://www.michael-noll.com/blog/2013/01/18/implementing-real-time-trending-topics-in-storm/)<br/>[snikolov .wordpress.com](http://snikolov.wordpress.com/2012/11/14/early-detection-of-twitter-trends/) |
| 设计一个随机 ID 生成系统          | [blog.twitter.com](https://blog.twitter.com/2010/announcing-snowflake)<br/>[github.com](https://github.com/twitter/snowflake/) |
| 返回一定时间段内次数前 k 高的请求      | [ucsb.edu](https://icmi.cs.ucsb.edu/research/tech_reports/reports/2005-23.pdf)<br/>[wpi.edu](http://davis.wpi.edu/xmdv/docs/EDBT11-diyang.pdf) |
| 设计一个数据源于多个数据中心的服务系统     | [highscalability.com](http://highscalability.com/blog/2009/8/24/how-google-serves-data-from-multiple-datacenters.html) |
| 设计一个多人网络卡牌游戏            | [indieflashblog.com](http://www.indieflashblog.com/how-to-create-an-asynchronous-multiplayer-game.html)<br/>[buildnewgames.com](http://buildnewgames.com/real-time-multiplayer/) |
| 设计一个垃圾回收系统              | [stuffwithstuff.com](http://journal.stuffwithstuff.com/2013/12/08/babys-first-garbage-collector/)<br/>[washington.edu](http://courses.cs.washington.edu/courses/csep521/07wi/prj/rick.pdf) |
| 添加更多的系统设计问题             | [贡献](#贡献)              |

### 真实架构

> 关于现实中真实的系统是怎么设计的文章。

<p align="center">
  <img src="http://i.imgur.com/TcUo2fw.png"/>
  <br/>
  <strong><a href="https://www.infoq.com/presentations/Twitter-Timeline-Scalability">Source: Twitter timelines at scale</a></strong>
</p>

**不要专注于以下文章的细节，专注于以下方面：**

* 发现这些文章中的共同的原则、技术和模式。
* 学习每个组件解决哪些问题，什么情况下使用，什么情况下不适用
* 复习学过的文章

| 类型              | 系统                                       | 引用                                       |
| --------------- | ---------------------------------------- | ---------------------------------------- |
| Data processing | **MapReduce** - Google的分布式数据处理 | [research.google.com](http://static.googleusercontent.com/media/research.google.com/zh-CN/us/archive/mapreduce-osdi04.pdf) |
| Data processing | **Spark** - Databricks 的分布式数据处理 | [slideshare.net](http://www.slideshare.net/AGrishchenko/apache-spark-architecture) |
| Data processing | **Storm** - Twitter 的分布式数据处理 | [slideshare.net](http://www.slideshare.net/previa/storm-16094009) |
|                 |                                          |                                          |
| Data store      | **Bigtable** - Google 的列式数据库 | [harvard.edu](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/chang06bigtable.pdf) |
| Data store      | **HBase** - Bigtable 的开源实现 | [slideshare.net](http://www.slideshare.net/alexbaranau/intro-to-hbase) |
| Data store      | **Cassandra** - Facebook 的列式数据库 | [slideshare.net](http://www.slideshare.net/planetcassandra/cassandra-introduction-features-30103666) |
| Data store      | **DynamoDB** - Amazon 的文档数据库 | [harvard.edu](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/decandia07dynamo.pdf) |
| Data store      | **MongoDB** - 文档数据库 | [slideshare.net](http://www.slideshare.net/mdirolf/introduction-to-mongodb) |
| Data store      | **Spanner** - Google 的全球分布数据库 | [research.google.com](http://research.google.com/archive/spanner-osdi2012.pdf) |
| Data store      | **Memcached** - 分布式内存缓存系统 | [slideshare.net](http://www.slideshare.net/oemebamo/introduction-to-memcached) |
| Data store      | **Redis** - 能够持久化及具有值类型的分布式内存缓存系统 | [slideshare.net](http://www.slideshare.net/dvirsky/introduction-to-redis) |
|                 |                                          |                                          |
| File system     | **Google File System (GFS)** - 分布式文件系统 | [research.google.com](http://static.googleusercontent.com/media/research.google.com/zh-CN/us/archive/gfs-sosp2003.pdf) |
| File system     | **Hadoop File System (HDFS)** - GFS 的开源实现 | [apache.org](https://hadoop.apache.org/docs/r1.2.1/hdfs_design.html) |
|                 |                                          |                                          |
| Misc            | **Chubby** - Google 的分布式系统的低耦合锁服务 | [research.google.com](http://static.googleusercontent.com/external_content/untrusted_dlcp/research.google.com/en/us/archive/chubby-osdi06.pdf) |
| Misc            | **Dapper** - 分布式系统跟踪基础设施 | [research.google.com](http://static.googleusercontent.com/media/research.google.com/en//pubs/archive/36356.pdf) |
| Misc            | **Kafka** - LinkedIn 的发布订阅消息系统 | [slideshare.net](http://www.slideshare.net/mumrah/kafka-talk-tri-hug) |
| Misc            | **Zookeeper** - 集中的基础架构和协调服务 | [slideshare.net](http://www.slideshare.net/sauravhaloi/introduction-to-apache-zookeeper) |
|                 | 添加更多                      | [贡献](#贡献)              |

### 公司的系统架构

| Company        | Reference(s)                             |
| -------------- | ---------------------------------------- |
| Amazon         | [Amazon 的架构](http://highscalability.com/amazon-architecture) |
| Cinchcast      | [每天产生 1500 小时的音频](http://highscalability.com/blog/2012/7/16/cinchcast-architecture-producing-1500-hours-of-audio-every-d.html) |
| DataSift       | [每秒实时挖掘 120000 条 tweet](http://highscalability.com/blog/2011/11/29/datasift-architecture-realtime-datamining-at-120000-tweets-p.html) |
| DropBox        | [我们如何缩放 Dropbox](https://www.youtube.com/watch?v=PE4gwstWhmc) |
| ESPN           | [每秒操作 100000 次](http://highscalability.com/blog/2013/11/4/espns-architecture-at-scale-operating-at-100000-duh-nuh-nuhs.html) |
| Google         | [Google 的架构](http://highscalability.com/google-architecture) |
| Instagram      | [1400 万用户，达到兆级别的照片存储](http://highscalability.com/blog/2011/12/6/instagram-architecture-14-million-users-terabytes-of-photos.html)<br/>[是什么在驱动 Instagram](http://instagram-engineering.tumblr.com/post/13649370142/what-powers-instagram-hundreds-of-instances) |
| Justin.tv      | [Justin.Tv 的直播广播架构](http://highscalability.com/blog/2010/3/16/justintvs-live-video-broadcasting-architecture.html) |
| Facebook       | [Facebook 的可扩展 memcached](https://cs.uwaterloo.ca/~brecht/courses/854-Emerging-2014/readings/key-value/fb-memcached-nsdi-2013.pdf)<br/>[TAO: Facebook 社交图的分布式数据存储](https://cs.uwaterloo.ca/~brecht/courses/854-Emerging-2014/readings/data-store/tao-facebook-distributed-datastore-atc-2013.pdf)<br/>[Facebook 的图片存储](https://www.usenix.org/legacy/event/osdi10/tech/full_papers/Beaver.pdf) |
| Flickr         | [Flickr 的架构](http://highscalability.com/flickr-architecture) |
| Mailbox        | [在 6 周内从 0 到 100 万用户](http://highscalability.com/blog/2013/6/18/scaling-mailbox-from-0-to-one-million-users-in-6-weeks-and-1.html) |
| Pinterest      | [从零到每月数十亿的浏览量](http://highscalability.com/blog/2013/4/15/scaling-pinterest-from-0-to-10s-of-billions-of-page-views-a.html)<br/>[1800 万访问用户，10 倍增长，12 名员工](http://highscalability.com/blog/2012/5/21/pinterest-architecture-update-18-million-visitors-10x-growth.html) |
| Playfish       | [月用户量 5000 万并在不断增长](http://highscalability.com/blog/2010/9/21/playfishs-social-gaming-architecture-50-million-monthly-user.html) |
| PlentyOfFish   | [PlentyOfFish 的架构](http://highscalability.com/plentyoffish-architecture) |
| Salesforce     | [他们每天如何处理 13 亿笔交易](http://highscalability.com/blog/2013/9/23/salesforce-architecture-how-they-handle-13-billion-transacti.html) |
| Stack Overflow | [Stack Overflow 的架构](http://highscalability.com/blog/2009/8/5/stack-overflow-architecture.html) |
| TripAdvisor    | [40M 访问者，200M 页面浏览量，30TB 数据](http://highscalability.com/blog/2011/6/27/tripadvisor-architecture-40m-visitors-200m-dynamic-page-view.html) |
| Tumblr         | [每月 150 亿的浏览量](http://highscalability.com/blog/2012/2/13/tumblr-architecture-15-billion-page-views-a-month-and-harder.html) |
| Twitter        | [Making Twitter 10000 percent faster](http://highscalability.com/scaling-twitter-making-twitter-10000-percent-faster)<br/>[每天使用 MySQL 存储2.5亿条 tweet](http://highscalability.com/blog/2011/12/19/how-twitter-stores-250-million-tweets-a-day-using-mysql.html)<br/>[150M 活跃用户，300K QPS，22 MB/S 的防火墙](http://highscalability.com/blog/2013/7/8/the-architecture-twitter-uses-to-deal-with-150m-active-users.html)<br/>[可扩展时间表](https://www.infoq.com/presentations/Twitter-Timeline-Scalability)<br/>[Twitter 的大小数据](https://www.youtube.com/watch?v=5cKTP36HVgI)<br/>[Twitter 的行为：规模超过 1 亿用户](https://www.youtube.com/watch?v=z8LU0Cj6BOU) |
| Uber           | [Uber 如何扩展自己的实时化市场](http://highscalability.com/blog/2015/9/14/how-uber-scales-their-real-time-market-platform.html) |
| WhatsApp       | [Facebook 用 190 亿美元购买 WhatsApp 的架构](http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html) |
| YouTube        | [YouTube 的可扩展性](https://www.youtube.com/watch?v=w5WVu624fY8)<br/>[YouTube 的架构](http://highscalability.com/youtube-architecture) |

### 公司工程博客

> 你即将面试的公司的架构
>
> 你面对的问题可能就来自于同样领域

* [Airbnb Engineering](http://nerds.airbnb.com/)
* [Atlassian Developers](https://developer.atlassian.com/blog/)
* [Autodesk Engineering](http://cloudengineering.autodesk.com/blog/)
* [AWS Blog](https://aws.amazon.com/blogs/aws/)
* [Bitly Engineering Blog](http://word.bitly.com/)
* [Box Blogs](https://www.box.com/blog/engineering/)
* [Cloudera Developer Blog](http://blog.cloudera.com/blog/)
* [Dropbox Tech Blog](https://tech.dropbox.com/)
* [Engineering at Quora](http://engineering.quora.com/)
* [Ebay Tech Blog](http://www.ebaytechblog.com/)
* [Evernote Tech Blog](https://blog.evernote.com/tech/)
* [Etsy Code as Craft](http://codeascraft.com/)
* [Facebook Engineering](https://www.facebook.com/Engineering)
* [Flickr Code](http://code.flickr.net/)
* [Foursquare Engineering Blog](http://engineering.foursquare.com/)
* [GitHub Engineering Blog](http://githubengineering.com/)
* [Google Research Blog](http://googleresearch.blogspot.com/)
* [Groupon Engineering Blog](https://engineering.groupon.com/)
* [Heroku Engineering Blog](https://engineering.heroku.com/)
* [Hubspot Engineering Blog](http://product.hubspot.com/blog/topic/engineering)
* [High Scalability](http://highscalability.com/)
* [Instagram Engineering](http://instagram-engineering.tumblr.com/)
* [Intel Software Blog](https://software.intel.com/en-us/blogs/)
* [Jane Street Tech Blog](https://blogs.janestreet.com/category/ocaml/)
* [LinkedIn Engineering](http://engineering.linkedin.com/blog)
* [Microsoft Engineering](https://engineering.microsoft.com/)
* [Microsoft Python Engineering](https://blogs.msdn.microsoft.com/pythonengineering/)
* [Netflix Tech Blog](http://techblog.netflix.com/)
* [Paypal Developer Blog](https://devblog.paypal.com/category/engineering/)
* [Pinterest Engineering Blog](http://engineering.pinterest.com/)
* [Quora Engineering](https://engineering.quora.com/)
* [Reddit Blog](http://www.redditblog.com/)
* [Salesforce Engineering Blog](https://developer.salesforce.com/blogs/engineering/)
* [Slack Engineering Blog](https://slack.engineering/)
* [Spotify Labs](https://labs.spotify.com/)
* [Twilio Engineering Blog](http://www.twilio.com/engineering)
* [Twitter Engineering](https://engineering.twitter.com/)
* [Uber Engineering Blog](http://eng.uber.com/)
* [Yahoo Engineering Blog](http://yahooeng.tumblr.com/)
* [Yelp Engineering Blog](http://engineeringblog.yelp.com/)
* [Zynga Engineering Blog](https://www.zynga.com/blogs/engineering)

#### 来源及延伸阅读

* [kilimchoi/engineering-blogs](https://github.com/kilimchoi/engineering-blogs)

## 正在完善中

有兴趣加入添加一些部分或者帮助完善某些部分吗？[加入进来吧](#贡献)！

* 使用 MapReduce 进行分布式计算
* 一致性哈希
* 直接存储器访问（DMA）控制器
* [贡献](#贡献)

## 致谢

整个仓库都提供了证书和源

特别鸣谢：

* [Hired in tech](http://www.hiredintech.com/system-design/the-system-design-process/)
* [Cracking the coding interview](https://www.amazon.com/dp/0984782850/)
* [High scalability](http://highscalability.com/)
* [checkcheckzz/system-design-interview](https://github.com/checkcheckzz/system-design-interview)
* [shashank88/system_design](https://github.com/shashank88/system_design)
* [mmcgrana/services-engineering](https://github.com/mmcgrana/services-engineering)
* [System design cheat sheet](https://gist.github.com/vasanthk/485d1c25737e8e72759f)
* [A distributed systems reading list](http://dancres.github.io/Pages/)
* [Cracking the system design interview](http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview)

## 联系方式

欢迎联系我讨论本文的不足、问题或者意见。

可以在我的 [GitHub 主页](https://github.com/donnemartin)上找到我的联系方式

## 许可

    Creative Commons Attribution 4.0 International License (CC BY 4.0)

    http://creativecommons.org/licenses/by/4.0/
*[English](README.md) ∙ [日本語](README-ja.md) ∙ [简体中文](README-zh-Hans.md) ∙ [繁體中文](README-zh-TW.md) | [العَرَبِيَّة‎](https://github.com/donnemartin/system-design-primer/issues/170) ∙ [বাংলা](https://github.com/donnemartin/system-design-primer/issues/220) ∙ [Português do Brasil](https://github.com/donnemartin/system-design-primer/issues/40) ∙ [Deutsch](https://github.com/donnemartin/system-design-primer/issues/186) ∙ [ελληνικά](https://github.com/donnemartin/system-design-primer/issues/130) ∙ [עברית](https://github.com/donnemartin/system-design-primer/issues/272) ∙ [Italiano](https://github.com/donnemartin/system-design-primer/issues/104) ∙ [韓國語](https://github.com/donnemartin/system-design-primer/issues/102) ∙ [فارسی](https://github.com/donnemartin/system-design-primer/issues/110) ∙ [Polski](https://github.com/donnemartin/system-design-primer/issues/68) ∙ [русский язык](https://github.com/donnemartin/system-design-primer/issues/87) ∙ [Español](https://github.com/donnemartin/system-design-primer/issues/136) ∙ [ภาษาไทย](https://github.com/donnemartin/system-design-primer/issues/187) ∙ [Türkçe](https://github.com/donnemartin/system-design-primer/issues/39) ∙ [tiếng Việt](https://github.com/donnemartin/system-design-primer/issues/127) ∙ [Français](https://github.com/donnemartin/system-design-primer/issues/250) | [Add Translation](https://github.com/donnemartin/system-design-primer/issues/28)*

# 系統設計入門

<p align="center">
  <img src="http://i.imgur.com/jj3A5N8.png"/>
  <br/>
</p>

## 動機

> 學習如何設計大型系統。
>
> 準備系統設計的面試。

### 學習如何設計大型系統

學習如何設計可擴展的系統會幫助你成為一個更好的工程師。

系統設計是一個廣泛的主題。在網路上，關於**系統設計的資源也是不計其數**。

本專案將**許多資源進行分門別類**，幫助你學習如何建構可擴展的系統。

### 從開放原始碼社群中學習

這是一個早期、持續不斷更新的開放原始碼專案。

[任何貢獻](#如何貢獻) 都相當歡迎！

### 準備系統設計的面試

除了程式的面試外，系統設計在許多科技公司的**面試流程**中都是**必要**的一環。

**練習常見的系統設計問題**，並且將你的設計結果和**參考答案**進行**比對**：討論、程式碼和圖表。

關於面試的其他主題：

* [學習指南](#學習指南)
* [如何解決一個系統設計的面試題目](#如何解決一個系統設計的面試題目)
* [系統設計面試問題與**解答**](#系統設計面試問題與解答)
* [物件導向設計問題與**解答**](#物件導向設計面試問題與解答)
* [其他的系統設計面試問題](#其他的系統設計面試問題)

## 學習單字卡

<p align="center">
  <img src="http://i.imgur.com/zdCAkB3.png"/>
  <br/>
</p>

底下提供的[學習單字卡](https://apps.ankiweb.net/)以每隔一段時間間隔出現的方式，幫助你學習系統設計的概念。

* [系統設計單字卡](resources/flash_cards/System%20Design.apkg)
* [系統設計練習單字卡](resources/flash_cards/System%20Design%20Exercises.apkg)
* [物件導向設計練習單字卡](resources/flash_cards/OO%20Design.apkg)

這些是非常棒的學習資源，隨時都可以使用。

### 程式設計學習資源：互動式程式學習設計

你正在尋找資源來面對[**程式語言面試**](https://github.com/donnemartin/interactive-coding-challenges)嗎？

<p align="center">
  <img src="http://i.imgur.com/b4YtAEN.png"/>
  <br/>
</p>

請參考 [**互動程式語言學習挑戰**](https://github.com/donnemartin/interactive-coding-challenges)，當中還包含了底下的學習單字卡：

* [程式語言學習單卡](https://github.com/donnemartin/interactive-coding-challenges/tree/master/anki_cards/Coding.apkg)

## 如何貢獻

> 從社群中學習

隨時歡迎提交 Pull Request：

* 修正錯誤
* 改善章節內容
* 增加新的章節
* [翻譯](https://github.com/donnemartin/system-design-primer/issues/28)

某些還需要再完善的章節放在 [修正中](#仍在進行中)。

請參考 [貢獻指南](CONTRIBUTING.md)。

## 系統設計主題的索引

> 底下是數個系統設計的主題，包含了優點及缺點。**要記得，每一個系統設計的考量都包含著某種取捨**。
>
> 每一章節都包含更深入資源的連結。

<p align="center">
  <img src="http://i.imgur.com/jrUBAF7.png"/>
  <br/>
</p>

* [系統設計主題：從這裡開始](#系統設計主題從這裡開始)
    * [第一步：複習關於可擴展性的影片講座](#第一步複習關於可擴展性的影片講座)
    * [第二步：複習關於可擴展性的文章](#第二步複習關於可擴展性的文章)
    * [下一步](#下一步)
* [效能與可擴展性](#效能與可擴展性)
* [延遲與吞吐量](#延遲與吞吐量)
* [可用性與一致性](#可用性與一致性)
    * [CAP 理論](#cap-理論)
        * [CP-一致性與部分容錯性](#cp-一致性與部分容錯性)
        * [AP-可用性與部分容錯性](#ap-可用性與部分容錯性)
* [一致性模式](#一致性模式)
    * [弱一致性](#弱一致性)
    * [最終一致性](#最終一致性)
    * [強一致性](#強一致性)
* [可用性模式](#可用性模式)
    * [容錯轉移](#容錯轉移)
    * [複寫機制](#複寫機制)
* [域名系統](#域名系統)
* [內容傳遞網路(CDN)](#內容傳遞網路cdn)
    * [推送式 CDNs](#推送式-cdns)
    * [拉取式 CDNs](#拉取式-cdns)
* [負載平衡器](#負載平衡器)
    * [主動到備用切換模式(AP Mode)](#主動到備用切換模式ap-mode)
    * [雙主動切換模式(AA Mode)](#雙主動切換模式aa-mode)
    * [第四層負載平衡](#第四層負載平衡)
    * [第七層負載平衡](#第七層負載平衡)
    * [水平擴展](#水平擴展)
* [反向代理(網頁伺服器)](#反向代理網頁伺服器)
    * [負載平衡器與反向代理伺服器](#負載平衡器與反向代理伺服器)
* [應用層](#應用層)
    * [微服務](#微服務)
    * [服務發現](#服務發現)
* [資料庫](#資料庫)
    * [關連式資料庫管理系統(RDBMS)](#關連式資料庫管理系統rdbms)
        * [主從複寫](#主從複寫)
        * [主動模式複寫](#主動模式複寫)
        * [聯邦式資料庫](#聯邦式資料庫)
        * [分片](#分片)
        * [反正規化](#反正規化)
        * [SQL 優化](#sql-優化)
    * [NoSQL](#nosql)
        * [鍵-值對的資料庫](#鍵-值對的資料庫)
        * [文件類型資料庫](#文件類型資料庫)
        * [列儲存型資料庫](#列儲存型資料庫)
        * [圖形資料庫](#圖形資料庫)
    * [SQL 或 NoSQL](#sql-或-nosql)
* [快取](#快取)
    * [客戶端快取](#客戶端快取)
    * [CDN 快取](#cdn-快取)
    * [網站伺服器快取](#網站伺服器快取)
    * [資料庫快取](#資料庫快取)
    * [應用程式快取](#應用程式快取)
    * [資料庫查詢級別的快取](#資料庫查詢級別的快取)
    * [物件級別的快取](#物件級別的快取)
    * [什麼時候要更新快取](#什麼時候要更新快取)
        * [快取模式](#快取模式)
        * [寫入模式](#寫入模式)
        * [事後寫入(回寫)](#事後寫入回寫)
        * [更新式快取](#更新式快取)
* [非同步機制](#非同步機制)
    * [訊息佇列](#訊息佇列)
    * [工作佇列](#工作佇列)
    * [背壓機制](#背壓機制)
* [通訊](#通訊)
    * [傳輸控制通訊協定(TCP)](#傳輸控制通訊協定tcp)
    * [使用者資料流通訊協定 (UDP)](#使用者資料流通訊協定-udp)
    * [遠端程式呼叫 (RPC)](#遠端程式呼叫-rpc)
    * [具象狀態轉移 (REST)](#具象狀態轉移-rest)
* [資訊安全](#資訊安全)
* [附錄](#附錄)
    * [2 的次方表](#2-的次方表)
    * [每個開發者都應該知道的延遲數量級](#每個開發者都應該知道的延遲數量級)
    * [其他的系統設計面試問題](#其他的系統設計面試問題)
    * [真實世界的架構](#真實世界的架構)
    * [公司的系統架構](#公司的系統架構)
    * [公司的工程部落格](#公司的工程部落格)
* [仍在進行中](#仍在進行中)
* [致謝](#致謝)
* [聯絡資訊](#聯絡資訊)
* [授權](#授權)

## 學習指南

> 基於你面試的時間 (短、中、長) 來複習這些建議的主題。

![Imgur](http://i.imgur.com/OfVllex.png)

**Q: 對於面試者來說，我需要知道這裡所有的知識嗎？**

**A: 不，如果是為了面試，你不需要知道這裡所有的知識**。

在一場面試中，你會被問到什麼問題取決於以下幾點：

* 你有多少經驗
* 你的技術背景
* 你面試什麼職位
* 你面試什麼公司
* 你的幸運程度

越有經驗的面試者通常被期望瞭解更多系統設計的知識。如果是架構師或團隊負責人則被預期瞭解更多除了個人貢獻以外的知識。頂尖的科技公司通常也會有一次或多次的系統設計面試。

面試時，會很廣泛地展開，並在幾個特定領域深入探討。這裡會幫助你了解一些系統設計不同的主題，基於你面試的時間、經驗、職位和公司來調整你所需要涉獵的知識內容。

* **短期** - 以系統設計的**廣度**為目標。通過解決**一些**面試題目來練習。
* **中期** - 以系統設計的**廣度**和**初級深度**為目標。通過解決**很多**面試題目來練習。
* **長期** - 以系統設計主題的**廣度**和**高級深度**為目標。通過解決**大部分**面試題目來練習。

|                                                                                 | 短期 | 中期 | 長期   |
|---------------------------------------------------------------------------------|------|------|--------|
| 閱讀 [系統設計主題的索引](#系統設計主題的索引) 來取得關於系統如何運作的廣泛知識 | :+1: | :+1: | :+1:   |
| 閱讀一些你要面試的 [公司的工程部落格](#公司的工程部落格) 文章                   | :+1: | :+1: | :+1:   |
| 閱讀關於 [真實世界的架構](#真實世界的架構)                                      | :+1: | :+1: | :+1:   |
| 複習 [如何解決一個系統設計的面試題目](#如何解決一個系統設計的面試題目)          | :+1: | :+1: | :+1:   |
| 完成 [系統設計面試題目與解答](#系統設計面試問題與解答)                          | 一些 | 很多 | 大部分 |
| 完成 [物件導向設計與解答](#物件導向設計面試問題與解答)                          | 一些 | 很多 | 大部分 |
| 複習 [其他的系統設計面試問題](#其他的系統設計面試問題)                          | 一些 | 很多 | 大部分 |

## 如何解決一個系統設計的面試題目

> 如何面對一個系統設計的面試題目

系統設計是一個**開放式的對話過程**，面試官會期望由你來主導這個對話。

你可以使用下面的步驟來引導整個討論過程。為了鞏固這個流程，請使用下面的步驟完成 [系統設計面試題目與解答](#系統設計面試問題與解答) 這個章節。

### 第一步：描述使用的場景、限制及假設

把問題的需求和範圍等資訊搜集起來。詢問以下問題，讓我們可以明確的定義使用場景和限制，對於提出的假設進行討論：

* 誰會使用這個系統？
* 他們怎麼使用系統？
* 有多少使用者？
* 系統的作用是什麼？
* 系統的輸入和輸出是什麼？
* 我們預期希望處理多少資料？
* 我們希望每秒處理多少請求？
* 預期的讀、寫比例為何？

### 第二步：建立一個高階的設計

使用重要的元件來建立一個高階的設計。

* 畫出主要的元件與其相互連接情況
* 證明你的想法

### 第三步： 設計核心的元件

對每一個核心元件進行深入的分析。舉例來說， 如果你被問到 [設計一個短網址的服務](solutions/system_design/pastebin/README.md) ，可以開始討論以下內容：

* 產生並儲存一個完整網址的 Hash
    * [MD5](solutions/system_design/pastebin/README.md) 和 [Base62](solutions/system_design/pastebin/README.md)
    * Hash 碰撞
    * SQL 或 NoSQL
    * 資料庫的模型
* 將一個 hash 過後的網址轉換為完整的網址
    * 資料庫查詢
* API 和物件導向設計

### 第四步：評估你的設計

確認及指出你的設計的瓶頸與限制，舉例來說，你需要底下幾個元件來擴展你的設計嗎？

* 負載平衡
* 水平擴展
* 快取
* 資料庫切片

針對你的設計討論可能的解決方法與代價。每個設計都有取捨。使用 [可擴展的設計原則](#系統設計主題：從這裡開始) 來處理系統瓶頸。

### 快速有效的進行估算

你可能被要求針對你的設計進行一些估算，可以參考 [附錄](#附錄) 的一些資源：

* [使用快速估算法](http://highscalability.com/blog/2011/1/26/google-pro-tip-use-back-of-the-envelope-calculations-to-choo.html)
* [2 的次方表](#2-的次方表)
* [每個開發者都應該知道的延遲數量級](#每個開發者都應該知道的延遲數量級)

### 相關資源與延伸閱讀

查看以下的連結獲得更好的做法：

* [如何在系統設計的面試中勝出](https://www.palantir.com/2011/10/how-to-rock-a-systems-design-interview/)
* [系統設計的面試](http://www.hiredintech.com/system-design)
* [系統架構與設計的面試介紹](https://www.youtube.com/watch?v=ZgdS0EUmn70)

## 系統設計面試問題與解答

> 常見的系統設計面試問題與相關範例的討論、程式碼以及圖表。
>
> 相關的解答位於 `解答/` 的資料夾中。

| 問題                                                                                                |                                                        |
|-----------------------------------------------------------------------------------------------------|--------------------------------------------------------|
| 設計 Pastebin.com (或 Bit.ly)                                                                       | [解答](solutions/system_design/pastebin/README.md)     |
| 設計一個像是 Twitter 的 timeline (或 Facebook feed)設計一個 Twitter 搜尋功能 (or Facebook 搜尋功能) | [解答](solutions/system_design/twitter/README.md)      |
| 設計一個爬蟲系統                                                                                    | [解答](solutions/system_design/web_crawler/README.md)  |
| 設計 Mint.com 網站                                                                                  | [解答](solutions/system_design/mint/README.md)         |
| 設計一個社交網站的資料結構                                                                          | [解答](solutions/system_design/social_graph/README.md) |
| 設計一個搜尋引擎使用的鍵值儲存資料結構                                                              | [解答](solutions/system_design/query_cache/README.md)  |
| 設計一個根據產品分類的亞馬遜銷售排名                                                                | [解答](solutions/system_design/sales_rank/README.md)   |
| 在 AWS 上設計一個百萬用戶等級的系統                                                                 | [解答](solutions/system_design/scaling_aws/README.md)  |
| 增加一個系統設計的問題                                                                              | [貢獻](#如何貢獻)                                      |

### 設計 Pastebin.com (或 Bit.ly)

[閱讀練習與解答](solutions/system_design/pastebin/README.md)

![Imgur](http://i.imgur.com/4edXG0T.png)

### 設計一個像是 Twitter 的 timeline (或 Facebook feed)設計一個 Twitter 搜尋功能 (or Facebook 搜尋功能)

[閱讀練習與解答](solutions/system_design/twitter/README.md)

![Imgur](http://i.imgur.com/jrUBAF7.png)

### 設計一個爬蟲系統

[閱讀練習與解答](solutions/system_design/web_crawler/README.md)

![Imgur](http://i.imgur.com/bWxPtQA.png)

### 設計 Mint.com 網站

[閱讀練習與解答](solutions/system_design/mint/README.md)

![Imgur](http://i.imgur.com/V5q57vU.png)

### 設計一個社交網站的資料結構

[閱讀練習與解答](solutions/system_design/social_graph/README.md)

![Imgur](http://i.imgur.com/cdCv5g7.png)

### 設計一個搜尋引擎使用的鍵值儲存資料結構

[閱讀練習與解答](solutions/system_design/query_cache/README.md)

![Imgur](http://i.imgur.com/4j99mhe.png)

### 設計一個根據產品分類的亞馬遜銷售排名

[閱讀練習與解答](solutions/system_design/sales_rank/README.md)

![Imgur](http://i.imgur.com/MzExP06.png)

### 在 AWS 上設計一個百萬用戶等級的系統

[閱讀練習與解答](solutions/system_design/scaling_aws/README.md)

![Imgur](http://i.imgur.com/jj3A5N8.png)

## 物件導向設計面試問題與解答

> 常見的物件導向面試問題與案例探討、程式碼與圖表。
>
> 相關的答案為在 `解答/` 目錄中。

>**注意: 本章節仍在完善內容中**

| 問題                     |                                                                            |
|--------------------------|----------------------------------------------------------------------------|
| 設計一個 hash map        | [解答](solutions/object_oriented_design/hash_table/hash_map.ipynb)         |
| 設計一個 LRU 快取        | [解答](solutions/object_oriented_design/lru_cache/lru_cache.ipynb)         |
| 設計一個客服系統         | [解答](solutions/object_oriented_design/call_center/call_center.ipynb)     |
| 設計一副牌               | [解答](solutions/object_oriented_design/deck_of_cards/deck_of_cards.ipynb) |
| 設計一個停車場           | [解答](solutions/object_oriented_design/online_chat/online_chat.ipynb)     |
| 設計一個環形陣列         | [如何貢獻](#如何貢獻)                                                      |
| 增加一個物件導向設計問題 | [如何貢獻](#如何貢獻)                                                      |

## 系統設計主題：從這裡開始

你是系統設計的新手嗎？

首先，你需要對於基本的原則有一定的認識，知道他們是什麼，如何使用，以及他們的優缺點。

### 第一步：複習關於可擴展性的影片講座

[哈佛大學可擴展性的影片](https://www.youtube.com/watch?v=-W9F__D3oY4)

* 包含以下主題：
    * 垂直擴展
    * 水平擴展
    * 快取
    * 負載平衡
    * 資料庫複寫
    * 資料庫分割

### 第二步：複習關於可擴展性的文章

[可擴展性](http://www.lecloud.net/tagged/scalability/chrono)

* 包含以下主題：
    * [複製](http://www.lecloud.net/post/7295452622/scalability-for-dummies-part-1-clones)
    * [資料庫](http://www.lecloud.net/post/7994751381/scalability-for-dummies-part-2-database)
    * [快取](http://www.lecloud.net/post/9246290032/scalability-for-dummies-part-3-cache)
    * [非同步](http://www.lecloud.net/post/9699762917/scalability-for-dummies-part-4-asynchronism)

### 下一步

接下來，我們需要看看某些取捨：

* **效能** vs **可擴展性**
* **延遲** vs **吞吐量**
* **可用性** vs **一致性**

記住，任何設計都是取捨。

接著，我們將會深入更具體的主題，包含 DNS、CDN 和負載平衡。

## 效能與可擴展性

如果服務**性能**的增加和資源的投入是成正比時，代表服務是可擴展的。一般來說，增加性能代表服務更多的工作單元，也可以處理更多的資料。<sup><a href="http://www.allthingsdistributed.com/2006/03/a_word_on_scalability.html">1</a></sup>

從另一方面來看看性能與可擴展性：

* 如果你的系統存在**性能**問題時，對單一使用者來說的感覺是慢的。
* 如果你的系統存在**可擴展性**問題時，對於單一使用者來說感覺較快，但在高負載的時候就會變慢。

### 來源及延伸閱讀

* [簡談可擴展性](http://www.allthingsdistributed.com/2006/03/a_word_on_scalability.html)
* [可擴展性、可用性、穩定性與相關模式](http://www.slideshare.net/jboner/scalability-availability-stability-patterns/)

## 延遲與吞吐量

**延遲** 指執行一個操作或運算結果所花費的時間。

**吞吐量** 指單位時間內執行此類型操作或運算的數量。

一般來說，你應該以**可接受的延遲**數量下的**最大化吞吐量**為設計目標。

### 來源及延伸閱讀

* [了解延遲與吞吐量](https://community.cadence.com/cadence_blogs_8/b/sd/archive/2010/09/13/understanding-latency-vs-throughput)

## 可用性與一致性

### CAP 理論

<p align="center">
  <img src="http://i.imgur.com/bgLMI2u.png"/>
  <br/>
  <i><a href=http://robertgreiner.com/2014/08/cap-theorem-revisited>來源：再看 CAP 理論</a></i>
</p>

在一個分散式系統中，只能滿足以下三個項目的任兩項：

* **一致性** - 每次讀取都可以得到最新的資料，但偶爾會拿到錯誤
* **可用性** - 每次讀取都可以得到非錯誤的回應，但不能保證可以得到最新的資料
* **部分容錯性** - 在任意分區的網路故障情況下，系統仍然能夠持續運行

*網路是不可靠的，你的設計必須要確保部分容錯性，所以你只能夠在一致性與可用性中做出取捨。*

#### CP-一致性與部分容錯性

等待分區的節點回覆可能會導致超時錯誤，如果你的系統的需求是需要保證原子讀寫時，CP 是一個不錯的選擇。

#### AP-可用性與部分容錯性

每個進行回覆的節點中的最新版本可能不是最新的，當分區節點解析完畢後，寫入的操作可能需要一些時間來傳播資料。

當你的系統需求需要保證 [最終一致性](#最終一致性) ，或當外部系統故障時，系統要能夠繼續運作時，AP 是一個不錯的選擇。

### 來源及延伸閱讀

* [複習 CAP 理論](http://robertgreiner.com/2014/08/cap-theorem-revisited/)
* [簡單的介紹 CAP 理論](http://ksat.me/a-plain-english-introduction-to-cap-theorem/)
* [CAP 問與答](https://github.com/henryr/cap-faq)

## 一致性模式

當你的資料有多個副本時，要考慮怎麼同步他們，以便讓使用者有一致的資料顯示。想想 [CAP 理論](#cap-理論) 中的一致性定律 - 每次的訪問都可以得到最新的資料，但可能也會收到錯誤的回應。

### 弱一致性

在寫入之後，任何的存取不一定可以拿到資料，弱一致性將盡力確保能存取到最新的資料。

這種方式可以在 memcached 等系統中看到。弱一致性可以在 VoIP、視訊聊天或其他即時多人線上遊戲中看到相關的使用案例。比方說，如果你在通話中遺失幾秒鐘時間的資料，再重新連接後，你是無法聽到這幾秒鐘的內容。

### 最終一致性

在寫入後的讀取操作最終可以看到被寫入的資料(通常在數毫秒內)。資料透過非同步的方式被複製。

DNS 或是電子郵件系統使用的就是這種方式，最終一致性在高可用的系統中效果很好。

### 強一致性

在寫入後，讀取將立刻取得資料，資料是透過同步的方式寫入。

檔案系統或資料庫系統就是使用這種方式，強一致性在需要紀錄的系統中表現很好。

### 來源及延伸閱讀

* [資料中心的記錄行為](http://snarfed.org/transactions_across_datacenters_io.html)

## 可用性模式

關於可用性有兩種模式：**容錯轉移** 和 **複寫**。

### 容錯轉移

#### 主動到備用切換模式(AP Mode)

在這個模式下，heartbeat 訊號會在主動和備用的機器中發送，當 heartbeat 中斷時，備用的機器就會切換為主動機器的 IP 位置接替服務。

當機的時間取決於備用的機器是在「熱」待機狀態還是「冷」待機狀態。只有處於主動的機器會處理使用者來的流量。

這個模式的切換也被稱為主從的切換模式。

#### 雙主動切換模式(AA Mode)

在此模式下，兩台伺服器都會負責處理流量，流量會在他們之間進行分散負載。

如果是外部網路的伺服器，DNS 需要知道兩台機器的 IP 位置，如果是內部網路的伺服器，應用程式邏輯需要知道這兩台機器。

雙主動切換模式也被稱為 master-master 切換。

### 缺點：容錯轉移

* 容錯轉移會需要增加額外的硬體與複雜度。
* 如果在新寫入的資料被複製到備用的機器前系統就發生故障，那有可能會遺失資料。

### 複寫機制

#### 主動到備用複寫與雙主動複寫

這一個主題進一步討論了 [資料庫](#資料庫) 部分：

* [主動到備用複寫](#主動到備用複寫)
* [雙主動複寫](#雙主動複寫)

## 域名系統

<p align="center">
  <img src="http://i.imgur.com/IOyLj4i.jpg"/>
  <br/>
  <i><a href=http://www.slideshare.net/srikrupa5/dns-security-presentation-issa>資料來源：DNS 安全介紹</a></i>
</p>

DNS 是將域名轉換為 IP 地址的系統。

DNS 是階層式的架構，一部分的 DNS 伺服器位於頂層，當查詢域名時，你的路由器或 ISP 業者會提供連接到 DNS 伺服器的資訊。較底層的 DNS 伺服器會快取查詢的結果，而這些快取資訊會因為 DNS 的傳遞而逐漸更新。DNS 的結果可以暫存在瀏覽器或操作系統中一段時間，時間的長短取決於 [存活時間(TTL)](https://en.wikipedia.org/wiki/Time_to_live) 的設定。

* **NS 記錄 (域名伺服器)** - 指定解析域名或子域名的 DNS 伺服器。
* **MX 記錄 (電子郵件交換伺服器)** - 指定接收電子郵件的伺服器。
* **A 記錄 (地址)** - 指向要對應的 IP 位置。
* **CNAME (別名)** - 從一個域名指向另外一個域名，或是 `CNAME` (example.com 指向 www.example.com) 或指向一個 `A` 記錄。

[CloudFlare](https://www.cloudflare.com/dns/) 和 [Route 53](https://aws.amazon.com/route53/) 提供了 DNS 的服務。而這些 DNS 服務商透過以下幾種方式來決定流量如何被分派：

* [加權輪詢](http://g33kinfo.com/info/archives/2657)
    * 防止流量進入正在維修中的伺服器
    * 在不同大小的集群中進行負載平衡
    * A/B 測試
* 基於延遲來路由請求
* 基於地理位置來路由請求

### DNS 的缺點

* 儘管可以透過快取來減輕 DNS 的延遲，但連接 DNS 伺服器還是帶來了些許的延遲。
* DNS 伺服器的管理是複雜的，儘管他通常由 [政府、ISP 業者或大公司](http://superuser.com/questions/472695/who-controls-the-dns-servers/472729) 來處理。
* DNS 伺服器會有 [DDoS 攻擊](http://dyn.com/blog/dyn-analysis-summary-of-friday-october-21-attack/) ，讓不知道 Twitter IP 的使用者無法訪問 Twitter 網站。

### 來源及延伸閱讀

* [DNS 架構](https://technet.microsoft.com/en-us/library/dd197427(v=ws.10).aspx)
* [維基百科](https://en.wikipedia.org/wiki/Domain_Name_System)
* [DNS 文章](https://support.dnsimple.com/categories/dns/)

## 內容傳遞網路(CDN)

<p align="center">
  <img src="http://i.imgur.com/h9TAuGI.jpg"/>
  <br/>
  <i><a href=https://www.creative-artworks.eu/why-use-a-content-delivery-network-cdn/>來源：為什麼要使用 CDN</a></i>
</p>

內容傳遞網路(CDN)是一種全球性的分散式代理伺服器，它透過靠近使用者的伺服器來提供檔案。通常 HTML/CSS/JS、圖片或影片等檔案會靜態檔案會透過 CDN 來提供，儘管 Amazon 的 CloudFront 也支援了動態內容的 CDN 服務。而 CDN 的 DNS 服務會告知使用者要連接哪一台伺服器。

透過 CDN 來取得檔案可以大幅度地增加請求的效率，因為：

* 從靠近使用者的伺服器來拿檔案
* 透過 CDN 來回應使用者，你的原始伺服器不需要處理請求

### 推送式 CDNs

當你的伺服器有檔案變動時，推送 CDN 會接收到新的變動內容，並重寫 URL 位置指向新的內容。你可以設定檔案內容什麼時候過期以及何時更新，檔案內容只有在變更或新增的時候才會推送，最小化流量，但最大化儲存。

流量較小的網站，或是內容不是經常更新的網站使用推送式的 CDN 相當適合，因為內容會被經常放置在 CDN 內，而不是常常需要重新抓取新檔案。

### 拉取式 CDNs

拉取式的 CDN 指的是當地一個使用者來請求該資源時，才從伺服器上抓取對應檔案。將檔案留在伺服器上並且重寫指向 CDN 的 URL，直到檔案被快取在 CDN 上為止，請求都會比較慢。

[存活時間 (TTL)](https://en.wikipedia.org/wiki/Time_to_live) 決定檔案要被緩存多久的時間。拉取式 CDN 可以節省儲存空間，但在過期的文件被更新之前，則會導致多餘的流量。

拉取式的 CDN 適合高流量的網站，因為檔案會被平均的分散在各個結點伺服器中。

### CDN 的缺點

* CDN 的成本取決於流量，在權衡評估後，你可能會因為成本而放棄使用。
* 如果在 TTL 過期之前就更新內容，CDN 的緩存內容可能會過期。
* 需要改變靜態內容的網址來指向 CDN。

### 來源及延伸閱讀

* [全球性的 CDN](http://repository.cmu.edu/cgi/viewcontent.cgi?article=2112&context=compsci)
* [拉取式和推拉式 CDN 的差別](http://www.travelblogadvice.com/technical/the-differences-between-push-and-pull-cdns/)
* [維基百科](https://en.wikipedia.org/wiki/Content_delivery_network)

## 負載平衡器

<p align="center">
  <img src="http://i.imgur.com/h81n9iK.png"/>
  <br/>
  <i><a href=http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html>來源：可擴展的系統設計模式</a></i>
</p>

負載平衡將使用者的請求分發到後端伺服器和資料庫，不管是哪種情況，負載平衡器會將回應返回給對應的使用者。而負載平衡器之所以有效在於以下幾點：

* 避免請求被轉到非正常運作的伺服器
* 避免資源過載
* 避免單點失敗

負載平衡器可以透過硬體(較昂貴)或 HAProxy 等軟體來實現。

其餘額外的好處有：

* **SSL 終結** - 將傳入的請求解密，並且加密伺服器的回應，如此一來後端伺服器就不需要進行這些高度消耗資源的運算
    * 不需要在每一台機器上安裝 [X.509 憑證](https://en.wikipedia.org/wiki/X.509)。
* **Session 保存** - 發行 cookie，並將特定使用者的請求路由到同樣的後端伺服器上。

為了避免故障，通常會採用 [主動到備用切換模式](#主動到備用切換模式(AP Mode)) 或 [雙主動切換模式](#雙主動切換模式(AA Mode)) 這樣多個負載平衡器的模式。

負載平衡器會基於多種方法來路由請求：

* 隨機
* 最少負載
* Session/cookies
* [輪詢調度或加權輪詢調度](http://g33kinfo.com/info/archives/2657)
* [第四層負載平衡](#第四層負載平衡)
* [第七層負載平衡](#第七層負載平衡)

### 第四層負載平衡

第四層的負載平衡器會監看 [傳輸層](#傳輸層) 的資訊來決定如何分發請求。一般來說，這包含了來源、目標 IP 位置，以及在 header 中的 port，但不包含資料本身的內容。第四層的負載平衡器會透過 [網路地址轉換(NAT)](https://www.nginx.com/resources/glossary/layer-4-load-balancing/) 來向上游的伺服器轉發資料。

### 第七層負載平衡

第七層的負載平衡器會監看 [應用層](#應用層) 來決定如何分發請求。這包含了請求的 header、訊息和 cookies。這種負載平衡器會終結網路的流量、讀取訊息並做出如何轉發訊息的決定，並把流量轉往對應的伺服器。舉例來說，一個第七層的負載平衡器可以將影音的流量轉往負責影音流量的伺服器，而將更敏感的使用者帳單的請求轉往安全性更強的伺服器。

第四層的負載平衡比起第七層的所要花費的時間和計算資源更低，雖然這對於現代商用硬體的性能影響已經微乎其微了。

### 水平擴展

負載平衡器一樣可以幫助水平擴展，提高性能與可用性。使用這種方式的擴展比起在單一機器的**垂直擴展**來說性價比更高，同時，聘請商用硬體的人才比起特定企業級系統人才來的更加容易。

#### 水平擴展的缺點

* 水平擴展會增加複雜性，同時也涉及了多台伺服器的議題
    * 伺服器應該是無狀態的：不應該包括像是 session 或資料圖片等和使用者相關的內容
    * Session 可以集中儲存在資料庫或 [快取](#快取)(Redis、Memcached) 等資料儲存中。
* 快取伺服器或資料庫需要隨著伺服器的增加而進行擴展，以便處理更多的請求。

### 負載平衡器的缺點

* 當負載平衡器資源不夠或沒有正確設定時，他可能會成為效能的瓶頸
* 使用負載平衡器來避免單點失敗會增加架構的複雜性
* 只有一台負載平衡器時，一樣有單點失敗的問題。而多台的負載平衡器一樣增加了架構的複雜性。

### 來源及延伸閱讀

* [NGINX 架構](https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/)
* [HAProxy 架構指南](http://www.haproxy.org/download/1.2/doc/architecture.txt)
* [可擴展性](http://www.lecloud.net/post/7295452622/scalability-for-dummies-part-1-clones)
* [維基百科](https://en.wikipedia.org/wiki/Load_balancing_(computing))
* [第四層負載平衡](https://www.nginx.com/resources/glossary/layer-4-load-balancing/)
* [第七層負載平衡](https://www.nginx.com/resources/glossary/layer-7-load-balancing/)
* [ELB 監聽器設定](http://docs.aws.amazon.com/elasticloadbalancing/latest/classic/elb-listener-config.html)

## 反向代理(網頁伺服器)

<p align="center">
  <img src="http://i.imgur.com/n41Azff.png"/>
  <br/>
  <i><a href=https://upload.wikimedia.org/wikipedia/commons/6/67/Reverse_proxy_h2g2bob.svg>來源：維基百科</a></i>
  <br/>
</p>

反向代理伺服器是一個集中內部服務，並提供統一個介面給公開使用者的伺服器。來自客戶端的請求會先被反向代理伺服器轉發到可以接收服務的伺服器，然後再由代理伺服器將結果返回給客戶端。

這樣做的好處有：

* **增加安全性** - 隱藏後端伺服器的資訊、可以設定 IP 的黑名單、限制每個客戶端的連線數量等。
* **增加可擴展性與靈活性** - 客戶端只會看到反向代理伺服器的 IP 或域名，這樣你就可以增加背後伺服器的數量或設定而不影響客戶端。
* **SSL 終止** - 解密傳入的請求、加密伺服器的回應，這樣後端伺服器就不需要進行這些高成本的操作
    * 不需要在每一台伺服器安裝 [X.509 憑證](https://en.wikipedia.org/wiki/X.509)。
* **壓縮** - 壓縮伺服器的回應
* **快取** - 直接在代理伺服器回應命中快取的結果
* **靜態檔案** - 直接提供靜態內容
    * HTML/CSS/JS
    * 圖片
    * 影片
    * 等等

### 負載平衡器與反向代理伺服器

* 當有多台伺服器時，使用負載平衡非常有用，一般來說，負載平衡器會將流量路由給一組功能相同的伺服器上。
* 即使只有一台伺服器或應用伺服器，反向代理也是有用的。可以參考上述的好處。
* Nginx 或 HAProxy 等解決方案可以同時支援第七層的反向代理與負載平衡

### 反向代理伺服器的缺點

* 引入反向代理伺服器會增加系統複雜度。
* 只有一台反向代理伺服器會有單點失效的問題，而設定多台的反向代理伺服器(如 [故障轉移](https://en.wikipedia.org/wiki/Failover) )同樣會增加系統複雜度。

### 來源與延伸閱讀

* [反向代理伺服器與負載平衡](https://www.nginx.com/resources/glossary/reverse-proxy-vs-load-balancer/)
* [NGINX 架構](https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/)
* [HAProxy 架構指南](http://www.haproxy.org/download/1.2/doc/architecture.txt)
* [維基百科](https://en.wikipedia.org/wiki/Reverse_proxy)

## 應用層

<p align="center">
  <img src="http://i.imgur.com/yB5SYwm.png"/>
  <br/>
  <i><a href=http://lethain.com/introduction-to-architecting-systems-for-scale/#platform_layer>資料來源：可縮放式系統架構介紹</a></i>
</p>

將 Web 服務層與應用層(也被稱為平台層)分離，如此一來這兩層就可以獨立縮放與設定，增加新的 API 服務只需要增加應用伺服器，而不需要增加額外的 Web 伺服器。

**單一職責原則**鼓勵小型、自治的服務與共同合作，小型團隊透過提供小型的服務可以更有效率地讓計畫成長。

在應用層中的工作程式可以實作 [非同步機制](#非同步機制)

### 微服務

相關的主題還有 [微服務](https://en.wikipedia.org/wiki/Microservices) ，指的是可以獨立運作、小型的模組化服務。每個服務會透過明確定義好的輕量級溝通機制，運作在一個獨立的流程中來共同實現一個目標。<sup><a href=https://smartbear.com/learn/api-design/what-are-microservices>1</a></sup>

舉例來說，Pinterest 可能有以下這些微服務：使用者資料、跟隨者、Feed、搜尋、照片上傳等等。

### 服務發現

[Consul](https://www.consul.io/docs/index.html)、[Etcd](https://coreos.com/etcd/docs/latest), 或是 [Zookeeper](http://www.slideshare.net/sauravhaloi/introduction-to-apache-zookeeper) 等系統可以透過註冊的名稱、位置、Port 等資訊來幫助各個服務發現彼此。[Health checks](https://www.consul.io/intro/getting-started/checks.html) 可以幫助確認服務的完整性以及是否經常使用一個 [HTTP](#hypertext-transfer-protocol-http) 的路徑。[鍵-值對的資料庫](#鍵-值對的資料庫) 則用來儲存設定的資訊與其他共享的資料。

### 應用層的缺點

* 設計多個鬆耦合微服務所組成的應用層，必須從架構、維運、流程等多個面向來考量，相對於單系統而言會非常不同。
* 微服務會增加部署與維運的複雜度。

### 來源與延伸閱讀

* [可擴展式系統架構介紹](http://lethain.com/introduction-to-architecting-systems-for-scale)
* [破解系統設計面試](http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview)
* [面向服務架構](https://en.wikipedia.org/wiki/Service-oriented_architecture)
* [Zookeeper 介紹](http://www.slideshare.net/sauravhaloi/introduction-to-apache-zookeeper)
* [建構微服務系統你所需要知道的一切](https://cloudncode.wordpress.com/2016/07/22/msa-getting-started/)

## 資料庫

<p align="center">
  <img src="http://i.imgur.com/Xkm5CXz.png"/>
  <br/>
  <i><a href=https://www.youtube.com/watch?v=vg5onp8TU6Q>來源：擴展你的使用者數量到第一個一千萬量級</a></i>
</p>

### 關連式資料庫管理系統(RDBMS)

像 SQL 這種關連式資料庫是以一組表格的形式存在的資料集合。

**ACID** 是用來描述資料庫 [事務](https://en.wikipedia.org/wiki/Database_transaction) 的特性。

* **原子性** - 每一個資料庫事務操作要不就是全部完成，要不就是全部不完成。
* **一致性** - 任何一個資料庫事務操作都會讓資料庫從一個有效的狀態轉換到另外一個有效狀態。
* **隔離性** - 併發執行資料庫事務操作的結果會和循序執行的結果一致。
* **持久性** - 一旦一個事務被資料庫執行後，他的結果與影響是擁永久保存的。

要針對關聯式資料庫系統進行擴展有許多方法： **主從複寫**, **主動模式複寫**, **聯邦式資料庫**, **分片**, **反正規化**, 和 **SQL 優化**.

#### 主從複寫

主資料庫負責讀和寫，並且將寫入的資料複寫至一或多個從屬資料庫中，從屬資料庫只負責讀取。而從屬資料庫可以再將寫入複製到更多以樹狀結構的其他資料庫中。如果主資料庫離線了，系統可以以只讀模式運行，直到某個從屬資料庫被提升為主資料庫，或有新的主資料庫出現。

<p align="center">
  <img src="http://i.imgur.com/C9ioGtn.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>來源： 可擴展性、可用性、穩定性及其模式</a></i>
</p>

##### 主從複寫的缺點

* 需要額外的處理邏輯來將從屬資料庫提升為主要資料庫。
* 參考 [複寫的缺點](#複寫的缺點) 章節，你可以看到主動模式複寫與主從模式**共同**的缺點。

#### 主動模式複寫

兩個主要的資料庫都負責讀取和寫入，並且兩者互相協調。如果其中一個主要資料庫離線，系統可以繼續運作。

<p align="center">
  <img src="http://i.imgur.com/krAHLGg.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>來源： 可擴展性、可用性、穩定性及其模式</a></i>
</p>

##### 主動模式的缺點

* 你需要一個負載平衡器來或是在你的應用程式邏輯中做修改來決定要寫入哪個資料庫。
* 大多數的主動模式資料庫無法保證一致性(違反 ACID)，或是會因為同步而產生了寫入延遲。
* 隨著更多寫入節點的增加和延遲的提高，如何解決衝突就顯得更加重要。
* 參考 [複寫的缺點](#複寫的缺點) 章節，你可以看到主動模式複寫與主從模式**共同**的缺點。

##### 複寫的缺點

* 如果在主要資料庫複製到其他結點前系統就失效，則會有資料丟失的可能。
* 當有過多寫入時，讀取的資料庫可能會因為過多寫入操作而被阻塞，導致讀取功能異常。
* 當讀取的資料庫越多時，需要複寫的資料越多，將會導致較為嚴重的延遲。
* 在某些資料庫系統中，寫入主資料庫的操作可以用多執行緒來並行寫入，但讀取的資料庫只支援單一執行緒來循序寫入。
* 複寫意味著更多的硬體以及更高的複雜度。

##### 來源及延伸閱讀

* [可擴展性、可用性、穩定性及其模式](http://www.slideshare.net/jboner/scalability-availability-stability-patterns/)
* [多主要資料庫複寫](https://en.wikipedia.org/wiki/Multi-master_replication)

#### 聯邦式資料庫

<p align="center">
  <img src="http://i.imgur.com/U3qV33e.png"/>
  <br/>
  <i><a href=https://www.youtube.com/watch?v=vg5onp8TU6Q>來源：擴展你的使用者數量到第一個一千萬量級</a></i>
</p>

聯邦式資料庫(或是指功能式切分)是將資料庫按照對應的功能進行分割。例如：你可以三個資料庫，分別是：**論壇**、**使用者**和**產品**，而不僅僅是單一資料庫。這樣會減少每個資料庫寫入與讀取的流量，進而降低複製的延遲。較少的資料意味者更多適合放入記憶體中的資料，進而增加快取命中率。因為沒有循序寫入的中央式主資料庫，你可以並行寫入以增加吞吐量。

##### 聯邦式資料庫的缺點

* 如果你的資料表需要大量的功能和資料表，聯邦式資料庫的效率並不好。
* 需要更新應用程式的邏輯來決定如何讀取和寫入到哪個資料庫。
* 透過 [server link](http://stackoverflow.com/questions/5145637/querying-data-by-joining-two-tables-in-two-database-on-different-servers) 從兩個資料庫中關資料更加複雜。
* 聯邦式資料庫需要更多的硬體和額外的複雜度。

##### 來源及延伸閱讀

* [來源：擴展你的使用者數量到第一個一千萬量級](https://www.youtube.com/watch?v=vg5onp8TU6Q)

#### 分片

<p align="center">
  <img src="http://i.imgur.com/wU8x5Id.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>來源： 可擴展性、可用性、穩定性及其模式</a></i>
</p>

分片是指將資料分配在不同的資料庫上，使每個資料庫只管理整個資料的部分子集。以使用者資料庫為例，隨著使用者數量的增加，越來越多的分片會被加入到群集當中。

類似於 [聯邦式資料庫](#聯邦式資料庫) 的優點，分片可以減少讀取和寫入的流量、減少複製並提高快取命中率。索引的容量也會減少，如此一來可以改善查詢的效能。當一個分片出現問題時，其餘的仍然可以正常運作，而為了避免資料遺失，你可能需要思考其他複寫的機制。如同聯邦式資料庫，分片的機制並沒有中央式的資料庫，你可以並行寫入以增加吞吐量。

以使用者資料庫為例，常見的做法是用使用者姓氏的部首或使用者地理問位置來區隔使用者資料表。

##### 分片的缺點

* 你需要修改應用程式的邏輯來實作分片，這可能會導致 SQL 變得複雜。
* 不合理的分片可能會導致資料負載不均，例如，頻繁被訪問的使用者資料如果被放置在同一個分片中，會導致該分片負載相對較高。
    * 再平衡會需要額外的複雜度。基於 [一致性 hash](http://www.paperplanes.de/2011/12/9/the-magic-of-consistent-hashing.html) 的分片演算法可以減少這種情形。
* 從多個分片中操作資料會很複雜。
* 分片需要額外的硬體和複雜度。

##### 來源及延伸閱讀

* [分片時代來臨](http://highscalability.com/blog/2009/8/6/an-unorthodox-approach-to-database-design-the-coming-of-the.html)
* [分片資料庫架構](https://en.wikipedia.org/wiki/Shard_(database_architecture))
* [一致性 hashing](http://www.paperplanes.de/2011/12/9/the-magic-of-consistent-hashing.html)

#### 反正規化

反正規化嘗試以寫入的性能作為代價來改善讀取性能。透過在不同資料表中的重複資料來避免高成本的 Join 操作。

某些關連式資料庫，例如 [PostgreSQL](https://en.wikipedia.org/wiki/PostgreSQL) 和 Oracle 支援 [materialized views](https://en.wikipedia.org/wiki/Materialized_view) ，可以用來處理重複資料的儲存，以及保證這些資料的一致性。

一旦資料使用如 [聯合](#聯合) 或 [切片](#切片) 等技術被分割，處理跨資料中心 Join 操作的複雜度。反正規化可以避免這種複雜的操作。

在多數系統中，讀取的操作頻率會遠高於寫入的頻率，比例可能會到 100:1 甚至 1000:1。進行複雜讀取操作的成本很高，會在硬碟上消耗大量的時間。

##### 反正規化的缺點

* 資料會重複存取
* Constraints 的機制可以讓重複的資料保持同步，但這樣會增加資料庫設計的複雜度。
* 反正規化的資料庫在大量寫入負載的情況下，性能表現可能會比正規化的資料庫差。

###### 來源及延伸閱讀

* [反正規化](https://en.wikipedia.org/wiki/Denormalization)

#### SQL 優化

SQL 優化是一個涵蓋範圍很廣的主題，有許多相關的 [參考書籍](https://www.amazon.com/s/ref=nb_sb_noss_2?url=search-alias%3Daps&field-keywords=sql+tuning) 可以做為參考。

透過 **效能測試** 和 **效能分析** 來模擬並發現系統的瓶頸是很重要的。

* **效能測試** - 透過 [ab](http://httpd.apache.org/docs/2.2/programs/ab.html) 等工具來測試高負載的情況。
* **效能分析** - 使用 [slow query log](http://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html) 等工具來追蹤性能問題。

效能測試和效能分析可能會引導你到以下的優化方案。

##### 使用較為精準的 schema

* 為了加快存取速度，MySQL 會在硬碟上使用連續的 block 來儲存資料。
* 使用 `CHAR` 來儲存固定長度的資料，不要使用 `VARCHAR`。
    * `CHAR` 在快速、隨機存取時效率很高。如果使用 `VARCHAR`，想要讀取下一個字元時，需要先讀取到目前字元的尾端。
* 使用 `TEXT` 來儲存大量的文字，例如部落格文章。`TEXT` 還可以使用布林搜尋。使用 `TEXT` 時，會在硬碟上保存一個指向硬碟區塊的指標。
* 使用 `INT` 來儲存數量級達到 2^32 或 40 億等較大的數字。
* 使用 `DECIMAL` 來儲存貨幣資料可以避免浮點數表達錯誤。
* 避免儲存龐大的 `BLOBS`，取而代之的，應該儲存存放該對象的位置。
* `VARCHAR(255)` 是使用 8 位數來儲存時的最大表示法，在某些關連式資料庫中，要最大限度地使用它。
* 在適用的情況下設定 `NOT NULL` 來 [提高搜尋性能](http://stackoverflow.com/questions/1017239/how-do-null-values-affect-performance-in-a-database-search)。

##### 使用正確的索引

* 當你使用 (`SELECT`, `GROUP BY`, `ORDER BY`, `JOIN`) 這些操作的對應欄位如果有使用索引就會查詢更快。
* 索引通常是使用平衡 [B 樹](https://en.wikipedia.org/wiki/B-tree) 表示，這樣可以保證資料是有序的，並允許在對數時間內進行搜尋、循序訪問以及插入、刪除等操作。
* 設定索引時，會將資料放置於記憶體中，會佔用更多記憶體空間。
* 寫入操作會變慢，因為索引會需要更新。
* 當讀取大量資料時，禁用索引再讀取，之後再重新建立索引，這樣也許會更快。

##### 避免高成本的 Join 操作

* 有性能需求時，可以進行 [反正規化](#反正規化)。

##### 分割資料表

* 將熱門的資料拆分到單獨的資料表中可以增加快取。

##### 調整查詢的快取

* 在某些情況下，[查詢快取](http://dev.mysql.com/doc/refman/5.7/en/query-cache) 可能會導致 [性能問題](https://www.percona.com/blog/2014/01/28/10-mysql-performance-tuning-settings-after-installation/)。

##### 來源及延伸閱讀

* [MySQL 查詢優化小提示](http://20bits.com/article/10-tips-for-optimizing-mysql-queries-that-dont-suck)
* [為什麼使用 VARCHAR(255) 很常見](http://stackoverflow.com/questions/1217466/is-there-a-good-reason-i-see-varchar255-used-so-often-as-opposed-to-another-l)
* [Null 值是如何影響資料庫性能](http://stackoverflow.com/questions/1017239/how-do-null-values-affect-performance-in-a-database-search)
* [慢 SQL log 查詢](http://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html)

### NoSQL

NoSQL 指的是 **鍵-值對的資料庫**、**文件類型資料庫**、**列儲存型資料庫** 和 **圖形資料庫** 等的統稱。資料是非正規化的，Join 大部分在應用端完成。大多數的 NoSQL 資料庫無法真正實現 ACID 的 transaction，他們通常會支援 [最終一致性](#最終一致性)。

**BASE** 通常被用來描述 NoSQL 資料庫的特性。  跟 [CAP 理論](#cap 理論) 相比，BASE 強調可用性而非一致性。

* **基本可用** - 系統保證可用性。
* **軟狀態** - 系統的狀態可能隨著時間改變，即使在沒有輸入的情況下也是如此。
* **最終一致性** - 經過一段時間之後，在沒有收到任何輸入的情況下，系統最終會達到一致。

除了在 [SQL 或 NoSQL](#sql-或-nosql) 之間做選擇，了解哪種類型的 NoSQL 資料庫最適合你的需求也是很有幫助的。我們會在下一節中快速瞭解一下 **鍵-值對的資料庫**、**文件類型資料庫**、**列儲存型資料庫** 和 **圖形資料庫** 等資料庫。

#### 鍵-值對的資料庫

> 抽象模型：hash table

一個鍵值對的資料庫通常可以實現 O(1) 時間內的讀寫，同時，它的背後通常使用記憶體或 SSD 當作儲存媒介。資料在儲存時，可以按照 [字典順序](https://en.wikipedia.org/wiki/Lexicographical_order) 來維護鍵的數值，進而實踐鍵數值的高效率檢索。鍵值對的資料庫也可以用來儲存值的 metadata。

鍵值對資料庫的效能很好，通常用來儲存簡單的資料模型或是頻繁修改的資料，如放在記憶體中的快取層。鍵值對資料庫所提供的操作有限，如果要進行更多操作，會將其放在應用端進行。

鍵值對的資料庫在某些情況下，是更複雜系統的基礎，例如圖形資料庫或是文件類型的資料庫。

##### 來源及延伸閱讀

* [鍵值對資料庫](https://en.wikipedia.org/wiki/Key-value_database)
* [鍵值對資料庫的缺點](http://stackoverflow.com/questions/4056093/what-are-the-disadvantages-of-using-a-key-value-table-over-nullable-columns-or)
* [Redis 架構](http://qnimate.com/overview-of-redis-architecture/)
* [Memcached 架構](https://www.adayinthelifeof.nl/2011/02/06/memcache-internals/)

#### 文件類型資料庫

> 抽象模型：將文件當做值的鍵值對資料庫

文件類型的資料庫是以文件 (XML、JSON、二進制檔案等) 為核心，文件本身儲存了對應物件的所有資訊。這種類型的資料庫提供了 API 或相關的查詢方法來根據儲存物件本身的特性來實現查詢功能。請注意，許多鍵值對資料庫有儲存 metadata 的特性，這也模糊了這兩種資料庫之間的界線。

根據底層實作的不同，文件資料庫可以根據集合、標籤、metadata 或目錄等來組織而成。儘管不同的文件可以被組織在一起或是分成一組，但彼此之間可能具有完全不同的內容。

某些文件型資料庫，例如 [MongoDB](https://www.mongodb.com/mongodb-architecture) 和 [CouchDB](https://blog.couchdb.org/2016/08/01/couchdb-2-0-architecture/) 同樣提供了類似於 SQL 查詢語句的功能來實現複雜的查詢。[DynamoDB](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/decandia07dynamo.pdf)則同時支援了鍵值對儲存和文件類型儲存的功能。

文件類型的資料庫具備高度靈活性，通常用於處理偶爾變化的資料。

##### 延伸閱讀

* [文件類型的資料庫](https://en.wikipedia.org/wiki/Document-oriented_database)
* [MongoDB 架構](https://www.mongodb.com/mongodb-architecture)
* [CouchDB 架構](https://blog.couchdb.org/2016/08/01/couchdb-2-0-architecture/)
* [Elasticsearch 架構](https://www.elastic.co/blog/found-elasticsearch-from-the-bottom-up)

#### 列儲存型資料庫

<p align="center">
  <img src="http://i.imgur.com/n16iOGk.png"/>
  <br/>
  <i><a href=http://blog.grio.com/2015/11/sql-nosql-a-brief-history.html>來源：SQL 和 NoSQL，簡短的歷史介紹</a></i>
</p>

> 抽象模型： 巢狀的 Map `ColumnFamily<RowKey, Columns<ColKey, Value, Timestamp>>`

列儲存型資料庫的基本單元是一列 (名稱/值為一組)。每一列可以被分到一個列的族群中(類似於 SQL 中的資料表)。而每個列族群之上還可以有一個超級列群。你可以透過列的鍵值來存取每一列，每個值都有一個時間戳記來解決版本問題。

Google 發表了第一個列儲存型資料庫 [Bigtable](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/chang06bigtable.pdf)，這影響了用於 Hadoop 系統中開源的 [HBase](https://www.mapr.com/blog/in-depth-look-hbase-architecture) often-used in the Hadoop ecosystem, 和 Facebook 的 [Cassandra](http://docs.datastax.com/en/archived/cassandra/2.0/cassandra/architecture/architectureIntro_c.html)。這些資料庫的儲存系統把鍵值利用字母順序來儲存，可以有效率的來讀取。

列儲存型態的資料的提供了高可用和高擴展性，通常被用在大量資料的儲存上。

##### 來源及延伸閱讀

* [SQL 和 NoSQL 歷史簡介](http://blog.grio.com/2015/11/sql-nosql-a-brief-history.html)
* [Bigtable 架構](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/chang06bigtable.pdf)
* [HBase 架構](https://www.mapr.com/blog/in-depth-look-hbase-architecture)
* [Cassandra 架構](http://docs.datastax.com/en/archived/cassandra/2.0/cassandra/architecture/architectureIntro_c.html)

#### 圖形資料庫

<p align="center">
  <img src="http://i.imgur.com/fNcl65g.png"/>
  <br/>
  <i><a href=https://en.wikipedia.org/wiki/File:GraphDatabase_PropertyGraph.png>來源： 圖形化資料庫</a></i>
</p>

> 抽象模型：圖

在圖形資料庫中，每一個節點會對應一條紀錄，而每個邊描述兩個節點之間的關係。圖形資料庫針對表示外來鍵(Foreign Key)眾多的複雜關聯或多對多關聯進行優化。

圖形資料庫為了儲存複雜的資料結構，例如社群網路，提供了很高的性能。他們相對較新，尚未被廣泛使用，查詢工具或資源比較難取得，許多這種類型的資料庫只能透過 [REST API](#representational-state-transfer-rest) 來存取。

##### 來源及延伸閱讀

* [圖形資料庫](https://en.wikipedia.org/wiki/Graph_database)
* [Neo4j](https://neo4j.com/)
* [FlockDB](https://blog.twitter.com/2010/introducing-flockdb)

#### 來源及延伸閱讀：NoSQL

* [資料庫術語解釋](http://stackoverflow.com/questions/3342497/explanation-of-base-terminology)
* [NoSQL 資料庫：調查與決策指南](https://medium.com/baqend-blog/nosql-databases-a-survey-and-decision-guidance-ea7823a822d#.wskogqenq)
* [可擴展性](http://www.lecloud.net/post/7994751381/scalability-for-dummies-part-2-database)
* [NoSQL 介紹](https://www.youtube.com/watch?v=qI_g07C_Q5I)
* [NoSQL 模式](http://horicky.blogspot.com/2009/11/nosql-patterns.html)

### SQL 或 NoSQL

<p align="center">
  <img src="http://i.imgur.com/wXGqG5f.png"/>
  <br/>
  <i><a href=https://www.infoq.com/articles/Transition-RDBMS-NoSQL/>來源：從 RDBMS 轉換到 NoSQL</a></i>
</p>

選擇 **SQL** 的原因：

* 結構化資料
* 嚴格的 schema
* 關連式資料
* 需要複雜的 join
* 事務
* 清晰的擴展模式
* 既有資源更豐富：開發者、社群、原始碼、工具等
* 透過索引查詢很快

選擇 **NoSQL** 的原因：

* 半結構化資料
* 動態或具有彈性的 schema
* 非關連式資料
* 不需要複雜的 joins
* 儲存 TB (或 PB) 等級的資料
* 高資料密集量的工作負載
* IOPS 的高吞吐量

適合使用 NoSQL 的範例：

* 快速地得到點擊的日誌資料
* 排行榜或得分資料
* 暫時性的資料，像是購物車
* 經常頻繁存取的資料表
* Metadata 或 查找資料表

##### 來源及延伸閱讀： SQL 或 NoSQL

* [擴展你的使用者到第一個一千萬等級](https://www.youtube.com/watch?v=vg5onp8TU6Q)
* [SQL 和 NoSQL 的不同](https://www.sitepoint.com/sql-vs-nosql-differences/)

## 快取

<p align="center">
  <img src="http://i.imgur.com/Q6z24La.png"/>
  <br/>
  <i><a href=http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html>來源：可擴展的系統設計模式</a></i>
</p>

快取可以提高頁面讀取速度，並且減少伺服器和資料庫的負載。在這種模型中，分派器會先檢查該次請求之前是否曾經被回應過，如果有的話，則直接拿之前的結果返回，避免真正執行處理的程序。

資料庫在資料均勻分布的情況下，讀取和寫入的效能是最好的。但是熱門的資料會讓讀取分佈不均，如此一來就會造成效能瓶頸。在資料庫前增加一個快取，就可以減少負載不均和突發流量所造成的影響。

### 客戶端快取

快取可以在客戶端(作業系統或瀏覽器)、[伺服器端](#反向代理伺服器) 或不同的緩存層等。

### CDN 快取

[內容傳遞網路(CDN)](#內容傳遞網路(CDN)) 也被視為一種快取。

### 網站伺服器快取

[反向代理](#反向代理網站伺服器) 以及像是 [Varnish](https://www.varnish-cache.org/) 等的快取服務可以提供靜態和動態內容。網站伺服器也可以快取使用者請求，返回結果，而不需要真正的處理這些請求。

### 資料庫快取

資料庫的預設設定中通常包含了快取的級別，針對一般的使用進行了優化。你可以針對不同的情況調整這些設定來進一步提高效能。

### 應用程式快取

基於記憶體的快取，像是 Memcached 和 Redis 是一種在應用層和資料庫之間的鍵值對快取。由於資料保存在記憶體中，比起存放在硬碟中的資料庫在存取上要快得多。記憶體的限制也比硬碟更多，所以像是 [least recently used (LRU)](https://en.wikipedia.org/wiki/Cache_algorithms#Least_Recently_Used) 的 [cache invalidation](https://en.wikipedia.org/wiki/Cache_algorithms) 方法可以讓 '熱門資料' 放在記憶體中，而比較 '冷門' 的資料在記憶體中失效。

Redis 還有以下額外的功能：

* 持久性的設定
* 內建一些資料結構，像是 Set 或 List

你可以快取的級別有好幾種，大致上分為兩類：**資料庫查詢** 和 **物件**：

* 記錄級別
* 查詢級別
* 完整的可序列化物件
* 完整的 HTML

一般來說，你應該避免文件檔案的快取，因為這會讓複製和自動擴展變得困難。

### 資料庫查詢級別的快取

當你將查詢資料庫的查詢語句的 hash 值和查詢結果儲存到快取中時，這種方法會遇到以下問題：

* 當你的查詢很複雜時，很難刪除快取內容
* 如果某個資料表中的某個欄位值改變時，需要刪除所有可能包含該欄位值的快取結果。

### 物件級別的快取

將資料視為物件，就像對待你的程式碼一樣。讓應用程式將資料從資料庫中組合到類別實例或資料結構中：

* 如果物件內的基本資料已經改變，那應該要從快取中刪除這個物件
* 允許異步處理：workers 透過使用最新的快取來組裝物件

建議快取的資料：

* 使用者 sessions
* 完整渲染的頁面
* 活動資訊
* 使用者資料圖表

### 什麼時候要更新快取

由於你只能在快取中儲存有限的資料，所以你需要選擇一個適用的快取策略。

#### 快取模式

<p align="center">
  <img src="http://i.imgur.com/ONjORqk.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/tmatyashovsky/from-cache-to-in-memory-data-grid-introduction-to-hazelcast>資料來源：從快取到記憶體資料網格</a></i>
</p>

應用程式負責從儲存裝置中進行讀取及寫入。快取不直接和儲存裝置進行互動，應用程式會執行以下操作：

* 從快取中尋找紀錄，如果所需要的紀錄在快取中找不到時
* 從資料庫中讀取紀錄
* 將該筆記錄儲存到快取
* 將資料返回

```python
def get_user(self, user_id):
    user = cache.get("user.{0}", user_id)
    if user is None:
        user = db.query("SELECT * FROM users WHERE user_id = {0}", user_id)
        if user is not None:
            key = "user.{0}".format(user_id)
            cache.set(key, json.dumps(user))
    return user
```

[Memcached](https://memcached.org/) 通常被用在快取上。

加入快取中的資料讀取速度很快，快取的模式也被稱為延遲讀取。只有被請求過的資料會被加入到快取中，避免沒有被請求的資料佔滿了快取空間。

##### 快取的缺點

* 當請求的資料不在快取中時，就需要經過三個步驟來獲得資料，這會導致明顯的延遲。
* 如果資料庫中的資料被更新了，會導致快取中的資料過時，這需要透過設定 TTL 強制更新快取，或透過直接更新模式來解決這種問題。
* 當快取的某個節點發生故障時，會需要被一個新的節點取代，這會導致延遲。

#### 寫入模式

<p align="center">
  <img src="http://i.imgur.com/0vBc0hN.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>資料來源：可獲展性、可用性、穩定性與模式</a></i>
</p>

應用程式使用快取當作主要的資料儲存服務，將資料寫入/讀取到快取中，由快取服務負責向資料庫讀寫資料。

* 應用程式向快取寫入/讀取資料
* 快取同步的將資料寫到資料庫進行儲存
* 返回所需要的內容

應用程式程式碼：

```
set_user(12345, {"foo":"bar"})
```

快取程式碼：

```python
def set_user(user_id, values):
    user = db.query("UPDATE Users WHERE id = {0}", user_id, values)
    cache.set(user_id, user)
```

直寫模式因為寫入操作的緣故，是一種較慢的操作，但讀取剛剛寫入的資料會很快，使用者通常比較能接受更新較慢，但讀取快速的情況。在快取中的資料不會過時。

##### 寫入模式的缺點

* 當發生故障或因為水平擴展而產生新的節點時，新的節點中將不會有快取資料，直到資料庫更新為止。將快取模式和寫入模式一起使用可以減緩這種現象。
* 被寫入多數的資料可能永遠都不會被讀取，你可以設定 TTL 來解決這種問題。

#### 事後寫入(回寫)

<p align="center">
  <img src="http://i.imgur.com/rgSrvjG.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>資料來源：可獲展性、可用性、穩定性與模式</a></i>
</p>

在事後寫入的模式中，應用程式會執行以下步驟：

* 在快取中新增/更新資料
* 非同步的寫入資料到資料儲存單元，提高寫入的性能

##### 事後寫入的缺點

* 快取可能在資料成功寫入到儲存單元前就丟失
* 事後寫入比起快取模式或是直寫模式在實作上更為複雜

#### 更新式快取

<p align="center">
  <img src="http://i.imgur.com/kxtjqgE.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/tmatyashovsky/from-cache-to-in-memory-data-grid-introduction-to-hazelcast>來源：從快取到記憶體資料網格技術</a></i>
</p>

你可以將快取設定為在到期之前就自動更新為最新存取的內容。

如果快取可以準確的預測將來可能會存取哪些資料，那自動更新可以降低讀取的延遲。

##### 更新式快取的缺點

* 無法準確預測未來會使用的資料時，會導致性能降低，還不如使用其他模式。

### 快取的缺點

* 需要保持快取和資料庫之間資料的一致性，比如說要如何設定 [快取無效](https://en.wikipedia.org/wiki/Cache_algorithms)。
* 需要更改應用程式程式碼來支援像是 Redis 或 Memcached 等快取服務。
* 快取的無效性是個難題，而什麼時候要更新快取就是個對應的複雜問題。

### 來源及延伸閱讀

* [從快取到記憶體資料網格技術](http://www.slideshare.net/tmatyashovsky/from-cache-to-in-memory-data-grid-introduction-to-hazelcast)
* [可擴展的系統設計模式](http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html)
* [可擴展的系統架構介紹](http://lethain.com/introduction-to-architecting-systems-for-scale/)
* [可擴展性、可用性、穩定性與模式](http://www.slideshare.net/jboner/scalability-availability-stability-patterns/)
* [可擴展性](http://www.lecloud.net/post/9246290032/scalability-for-dummies-part-3-cache)
* [AWS ElastiCache 策略](http://docs.aws.amazon.com/AmazonElastiCache/latest/UserGuide/Strategies.html)
* [維基百科](https://en.wikipedia.org/wiki/Cache_(computing))

## 非同步機制

<p align="center">
  <img src="http://i.imgur.com/54GYsSx.png"/>
  <br/>
  <i><a href=http://lethain.com/introduction-to-architecting-systems-for-scale/#platform_layer>資料來源：可縮放性系統架構介紹</a></i>
</p>

非同步的工作流程有助於減少原本按照同步順序進行請求的時間，透過提前進行一些耗時操作來將降低整體請求時間，比如說：定期的彙整資料。

### 訊息佇列

訊息佇列用來接收、保留以及傳遞訊息。如果一個操作按照順序執行太慢的時候，你可以透過訊息佇列和以下的流程搭配來完成此工作：

* 應用程式將訊息發送到佇列中，並通知使用者對應的狀態
* 一個 worker 從佇列中拿出該訊息並進行處理，然後完成後顯示對應資訊

這樣的工作流程，使用者不會被阻塞，同時工作會在背景完成。在這段期間，客戶端可以進行一些處理讓此任務看起來已經完成了。例如，當你要發送一則推文訊息時，此訊息可以馬上出現在你的時間軸上，但可能需要一段時間才會發送到你的追蹤者上面。

**Redis** 是一個簡單且令人滿意的訊息佇列服務，但訊息有可能會丟失。

**RabbitMQ** 很受歡迎，但你必須要使用 AMQP 通訊協定，並且要自己管理節點。

**Amazon SQS** 是一個被 AWS 託管的服務，但可能會有高延遲，並且訊息可能會被傳送兩次。

### 工作佇列

工作佇列會接收工作和對應的資料，執行它們，並且傳送其結果。他們可以支援排程，並且可以在背景運作計算密集型的工作。

**Celery** 支援排程，主要是使用 Python 開發。

### 背壓機制

當佇列開始明顯成長時，佇列的大小可能會超過記憶體，這會導致無法命中快取，降低整體效能。[背壓](http://mechanical-sympathy.blogspot.com/2012/05/apply-back-pressure-when-overloaded.html) 可以用來限制佇列的大小，讓佇列保持高吞吐率和良好的回應時間。一旦佇列滿了，客戶端將會得到 HTTP 503 的回應碼，以便讓他們在稍後重新嘗試。客戶端可以透過 [指數後退演算法](https://en.wikipedia.org/wiki/Exponential_backoff) 這種方式來進行重試。

### 非同步的缺點

* 簡單的運算和需要即時的工作可能更適合使用同步運算，導入佇列可能會增加延遲或系統複雜度。

### 來源及延伸閱讀

* [這是一個數字遊戲](https://www.youtube.com/watch?v=1KRYH75wgy4)
* [當過載時，使用背壓](http://mechanical-sympathy.blogspot.com/2012/05/apply-back-pressure-when-overloaded.html)
* [利特爾法則](https://en.wikipedia.org/wiki/Little%27s_law)
* [訊息佇列和工作佇列有什麼不同？](https://www.quora.com/What-is-the-difference-between-a-message-queue-and-a-task-queue-Why-would-a-task-queue-require-a-message-broker-like-RabbitMQ-Redis-Celery-or-IronMQ-to-function)

## 通訊

<p align="center">
  <img src="http://i.imgur.com/5KeocQs.jpg"/>
  <br/>
  <i><a href=http://www.escotal.com/osilayer.html>來源：OSI 七層模型</a></i>
</p>

### 超文件通訊協定 (HTTP)

HTTP 是一種在客戶端和伺服器端傳輸資料和定義編碼的方法。它是基於請求/回應的協議：客戶端發出請求，而伺服器端則針對請求內容完成對應的行為並進行回應。HTTP 是獨立的，它允許請求和回應經過許多負載平衡、快取、加密和壓縮的中間路由器和伺服器。

一個基本的 HTTP 請求是由一個動詞(方法)和一個資源(端點)所組成。以下是常見的 HTTP 動詞：

| 動詞   | 描述                             | 冪等* | 安全性 | 可快取性                                |
|--------|----------------------------------|-------|--------|-----------------------------------------|
| GET    | 讀取資源                         | Yes   | Yes    | Yes                                     |
| POST   | 建立資源，或是驅動處理資料的流程 | No    | No     | Yes，如果回應包含更新的資訊             |
| PUT    | 建立或更新資源                   | Yes   | No     | No                                      |
| PATCH  | 更新部分資料                     | No    | No     | Yes if response contains freshness info |
| DELETE | 刪除資料                         | Yes   | No     | No                                      |

*指的是當進行多次相同請求時，結果是相同的。

HTTP 是依賴於較底層的協議(例如：**TCP** 和 **UDP**) 的應用層協議。

#### 來源及延伸閱讀

* [什麼是 HTTP?](https://www.nginx.com/resources/glossary/http/)
* [HTTP 和 TCP 的差別](https://www.quora.com/What-is-the-difference-between-HTTP-protocol-and-TCP-protocol)
* [PUT 和 PATCH 的差別](https://laracasts.com/discuss/channels/general-discussion/whats-the-differences-between-put-and-patch?page=1)

### 傳輸控制通訊協定(TCP)

<p align="center">
  <img src="http://i.imgur.com/JdAsdvG.jpg"/>
  <br/>
  <i><a href=http://www.wildbunny.co.uk/blog/2012/10/09/how-to-make-a-multi-player-game-part-1/>來源：如何開發多人遊戲</a></i>
</p>

TCP 是透過 [IP 網路](https://en.wikipedia.org/wiki/Internet_Protocol) 面向連線的通訊協定。連線是透過 [握手](https://en.wikipedia.org/wiki/Handshaking) 的方式來建立和斷開連接，所有發送的資料在接收時會保證順序，另外透過以下的機制來保證資料不會損毀：

* 每個資料的序列號碼和 [校驗碼](https://en.wikipedia.org/wiki/Transmission_Control_Protocol#Checksum_computation)
* [確認訊息](https://en.wikipedia.org/wiki/Acknowledgement_(data_networks)) 和自動重傳

如果發送端沒有收到正確的回應，會重新發送資料，如果有多次的逾期時，連線就會斷開。TCP 實作了 [流量控制](https://en.wikipedia.org/wiki/Flow_control_(data)) 和 [阻塞控制](https://en.wikipedia.org/wiki/Network_congestion#Congestion_control)，這些機制會導致延遲，而且通常傳輸的效率會比 UDP 來得低。

為了確保高吞吐量，Web 伺服器會保持大量的 TCP 連線，進而導致記憶體用量變大。在 Web 伺服器之間使用大量的開放連線可能是昂貴的，更別說是在 memcached 快取中做這些事情。[連線池](https://en.wikipedia.org/wiki/Connection_pool) 可以幫助在適合的情況下切換到 UDP。

TCP 對於需要高可靠、低時間急迫性的應用來說很有用，比如說：Web 伺服器、資料庫、SMTP、FTP 和 SSH。

以下的情況請使用 TCP 而不是 UDP：

* 你需要資料完整無缺
* 你想要自動地對網路的流量進行最佳評估

### 使用者資料流通訊協定 (UDP)

<p align="center">
  <img src="http://i.imgur.com/yzDrJtA.jpg"/>
  <br/>
  <i><a href=http://www.wildbunny.co.uk/blog/2012/10/09/how-to-make-a-multi-player-game-part-1/>資料來源：如何製作多人遊戲</a></i>
</p>

UDP 是非連線型的通訊協定。資料流(類似於封包)只在資料流級別進行確保。資料可能會不按照順序地到達目的地，也可能會遺失。UDP 並不支援阻塞處理，儘管 UDP 不像 TCP 一樣可靠，但通常效率更好。

UDP 可以透過廣播來傳送資料流到所有子網路中的所有裝置，這對於 [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol) 來說很有用，因為所有子網路中的設備還沒有分配到 IP 位置，而對 TCP 來說，IP 是必須的。

UDP 的可靠性較低，但適合用在像是網路電話、視訊聊天、串流和多人線上即時遊戲中。

針對以下的案例，請使用 UDP 來代替 TCP：

* 你需要低延遲
* 資料延遲的成本比資料遺失還高
* 你想要自己實作錯誤校正方法

#### 來源及延伸閱讀

* [遊戲程式撰寫的網路架構](http://gafferongames.com/networking-for-game-programmers/udp-vs-tcp/)
* [TCP 和 UDP 的關鍵區別](http://www.cyberciti.biz/faq/key-differences-between-tcp-and-udp-protocols/)
* [TCP 和 UDP 的差別](http://stackoverflow.com/questions/5970383/difference-between-tcp-and-udp)
* [傳輸控制協議(TCP)](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)
* [使用者資料流協議(UDP)](https://en.wikipedia.org/wiki/User_Datagram_Protocol)
* [Memcache 在 Facebook 中的可擴展性設計](http://www.cs.bu.edu/~jappavoo/jappavoo.github.com/451/papers/memcache-fb.pdf)

### 遠端程式呼叫 (RPC)

<p align="center">
  <img src="http://i.imgur.com/iF4Mkb5.png"/>
  <br/>
  <i><a href=http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview>資料來源：破解系統設計面試</a></i>
</p>

在一個 RPC 中，客戶端會去呼叫另外一個位置空間(通常是在遠端的伺服器)的方法。呼叫的方式就像是呼叫本地端的一個方法一樣，客戶端和伺服器溝通的具體過程被抽象化，而遠端呼叫相較於本地端呼叫來說一般較慢，而且可靠性較差，因此了解如何區別這兩種方法是必要的。熱門的 RPC 框架包含了 [Protobuf](https://developers.google.com/protocol-buffers/)、[Thrift](https://thrift.apache.org/) 和 [Avro](https://avro.apache.org/docs/current/)。

RPC 是一個請求-回應的通訊協定：

* **客戶端程序** - 呼叫客戶端的 stub 程序，就像呼叫本地端方法一樣，參數會被放入堆疊當中
* **客戶端 stub 程序** - 將請求過程的 id 和參數打包放入請求資訊中
* **客戶端通訊模組** - 作業系統將資訊從客戶端發送到伺服器端
* **伺服器端通訊模組** - 作業系統將收到的資訊傳送到伺服器端的 stub 程序
* **伺服器端 stub 程序** -  將結果解開後，依照過程中的 ID 來呼叫伺服器
* 伺服器回覆的順序會按照以上相反的順序來回覆

RPC 使用範例：

```
GET /someoperation?data=anId

POST /anotheroperation
{
  "data":"anId";
  "anotherdata": "another value"
}
```

RPC 專注於揭露行為，它通常用來處理內部通訊的效能問題，通常你可以手動處理本地端的呼叫來更加符合你的使用案例。

當遇到以下情況時，使用本地端函式庫（也就是 SDK）：

* 你知道你的目標平台
* 你想要控制如何訪問你的 "邏輯"
* 當你的函式庫發生錯誤時，你想要進行控制
* 效能和使用者體驗是你最關注的事情

遵守 **REST** 規範的 HTTP API 往往更適合用在公用的 API。

#### RPC 的缺點

* RPC 的客戶端會變得和伺服器的實作綁得更死
* 一個新的 API 必須在每個操作或使用案例中進行定義
* RPC 很難抓錯誤
* 你很難方便的修改現有的技術，舉例來說，如果你希望在 [Squid](http://www.squid-cache.org/) 這樣的快取伺服器上確保 [RPC 呼叫被正確的快取](http://etherealbits.com/2012/12/debunking-the-myths-of-rpc-rest/)，你可以需要多費額外的努力了。

### 具象狀態轉移 (REST)

REST 是一個規範客戶端/伺服器端架構設計的模型。客戶端基於伺服器管理的系列操作，伺服器提供修改或取得資源的介面，所有的通訊必須是無狀態、可快取的。

Restful 的設計有四個原則：

* **標示資源 (HTTP 中的 URI)** - 無論任何操作都使用相同的 URI
* **表示層的改變 (HTTP 中的動作)** - 使用 HTTP 動詞、Headers 和 body
* **可自我描述的錯誤訊息 (HTTP 中的狀態碼)** - 使用狀態碼，不要重複造輪子
* **[HATEOAS](http://restcookbook.com/Basics/hateoas/) (HTTP 中的 HTML 介面)** - 你的 Web 伺服器應該要能夠透過瀏覽器訪問

REST 請求範例：

```
GET /someresources/anId

PUT /someresources/anId
{"anotherdata": "another value"}
```

REST 關注於揭露資料，減少客戶端/伺服器之間耦合的程度，並且經常用在公共的 HTTP API 設計上。REST 使用更通用和受規範的方法來透過 URI 來揭露資源，[透過 Headers 來描述](https://github.com/for-GET/know-your-http-well/blob/master/headers.md)，並透過 GET、POST、PUT、DELETE 和 PATCH 等動作來進行操作，因為無狀態的特性，REST 易於橫向擴展和分片。

#### REST 的缺點

* 因為 REST 的重點是放在如何揭露資料，所以當資料不是以自然的形式組成時，或是結構相當複雜時，REST 可能無法很好的處理他們。舉個範例，回傳過去一小時中與特定事件吻合的更新操作就很難透過路徑來表示，使用 REST，可能會使用 URI、查詢參數和請求本身來實現。
* REST 一般依賴於幾個動詞操作(GET、POST、PUT、DELETE 和 PATCH)，但有時候這些操作無法滿足你的需求，舉個範例，將過期的文件移動到歸檔文件資料庫中這樣的操作，可能就沒辦法簡單的使用以上幾個動詞操作來完成。
* 對於那些多層複雜的資源來說，需要在客戶端和伺服器端進行多次請求，例如：獲得部落格頁面及相關評論，而對於網路環境較不穩定的行動端應用來說，這些多次往返的請求是非常麻煩的。
* 隨著時間的增加，API 的回應中可能會增加更多的欄位，比較舊的客戶端還是會收到所有新的回應內容，即時他們不需要這些回應，這會造成他們的負擔，並且造成更大的延遲。

### RPC 和 REST 呼叫的比較

| 操作                       | RPC                                                                   | REST                                          |
|----------------------------|-----------------------------------------------------------------------|-----------------------------------------------|
| 註冊                       | **POST** /signup                                                      | **POST** /persons                             |
| 取消                       | **POST** /resign{"personid": "1234"}                                  | **DELETE** /persons/1234                      |
| 讀取使用者資訊             | **GET** /readPerson?personid=1234                                     | **GET** /persons/1234                         |
| 讀取使用者物品清單         | **GET** /readUsersItemsList?personid=1234                             | **GET** /persons/1234/items                   |
| 增加一個物品到使用者的清單 | **POST** /addItemToUsersItemsList{"personid": "1234";"itemid": "456"} | **POST** /persons/1234/items{"itemid": "456"} |
| 更新一個物品               | **POST** /modifyItem{"itemid": "456";"key": "value"}                  | **PUT** /items/456{"key": "value"}            |
| 刪除一個物品               | **POST** /removeItem{"itemid": "456"}                                 | **DELETE** /items/456                         |

<p align="center">
  <i><a href=https://apihandyman.io/do-you-really-know-why-you-prefer-rest-over-rpc/>資料來源：你真的知道為什麼你更喜歡 REST 而不是 RPC 嗎？</a></i>
</p>

#### 來源及延伸閱讀

* [你真的知道為什麼你更喜歡 REST 而不是 RPC 嗎？](https://apihandyman.io/do-you-really-know-why-you-prefer-rest-over-rpc/)
* [什麼時候 RPC 比 REST 更適合](http://programmers.stackexchange.com/a/181186)
* [REST 和 JSON-RPC](http://stackoverflow.com/questions/15056878/rest-vs-json-rpc)
* [揭開 RPC 和 REST 的神秘面紗](http://etherealbits.com/2012/12/debunking-the-myths-of-rpc-rest/)
* [使用 REST 的缺點](https://www.quora.com/What-are-the-drawbacks-of-using-RESTful-APIs)
* [破解系統設計面試](http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview)
* [Thrift](https://code.facebook.com/posts/1468950976659943/)
* [為什麼在內部要使用 REST 而不是 RPC](http://arstechnica.com/civis/viewtopic.php?t=1190508)

## 資訊安全

這一章節需要更多的貢獻，一起[加入](#如何貢獻)吧！

資訊安全是一個廣泛的議題，除非你有相當的經驗、資訊安全的背景或正在申請相關的職位要求對應的知識，否則了解以下的基礎內容即可：

*在傳輸和等待的過程中進行加密
* 對所有使用者輸入和從使用者得到的參數進行處理，以避免 [XSS](https://en.wikipedia.org/wiki/Cross-site_scripting) 和 [SQL injection](https://en.wikipedia.org/wiki/SQL_injection)
* 使用參數化輸入來避免 SQL injection
* 使用 [最小權限原則](https://en.wikipedia.org/wiki/Principle_of_least_privilege)

### 來源及延伸閱讀

* [為開發者準備的資訊安全指南](https://github.com/FallibleInc/security-guide-for-developers)
* [OWASP top ten](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet)

## 附錄

某些時候你可能會被要求做一些保守估計，比如說，你可能需要預估從硬碟中生成 100 張圖片約略需要多少時間，或一個資料結構需要多少記憶體等。**2 的次方表** 和 **每個開發者都需要知道的一些時間資料** 都是一些很方便的參考料。

### 2 的次方表

```
次方           實際值         近似值        位元組
---------------------------------------------------------------
7                             128
8                             256
10                           1024   1 thousand           1 KB
16                         65,536                       64 KB
20                      1,048,576   1 million            1 MB
30                  1,073,741,824   1 billion            1 GB
32                  4,294,967,296                        4 GB
40              1,099,511,627,776   1 trillion           1 TB
```

#### 來源及延伸閱讀

* [2 的次方](https://en.wikipedia.org/wiki/Power_of_two)

### 每個開發者都應該知道的延遲數量級

```
延遲比較數量級
--------------------------
L1 快取參考數量級                           0.5 ns
Branch mispredict                            5   ns
L2 快取參考數量級                             7   ns                      14x L1 cache
Mutex lock/unlock                          25   ns
主記憶體參考數量級                      100   ns                      20x L2 cache, 200x L1 cache
Compress 1K bytes with Zippy            10,000   ns       10 us
Send 1 KB bytes over 1 Gbps network     10,000   ns       10 us
Read 4 KB randomly from SSD*           150,000   ns      150 us          ~1GB/sec SSD
Read 1 MB sequentially from memory     250,000   ns      250 us
Round trip within same datacenter      500,000   ns      500 us
Read 1 MB sequentially from SSD*     1,000,000   ns    1,000 us    1 ms  ~1GB/sec SSD, 4X memory
Disk seek                           10,000,000   ns   10,000 us   10 ms  20x datacenter roundtrip
Read 1 MB sequentially from 1 Gbps  10,000,000   ns   10,000 us   10 ms  40x memory, 10X SSD
Read 1 MB sequentially from disk    30,000,000   ns   30,000 us   30 ms 120x memory, 30X SSD
Send packet CA->Netherlands->CA    150,000,000   ns  150,000 us  150 ms

Notes
-----
1 ns = 10^-9 seconds
1 us = 10^-6 seconds = 1,000 ns
1 ms = 10^-3 seconds = 1,000 us = 1,000,000 ns
```

一些基於上述數字的指標：

* 循序的從硬碟讀取資料大約 30 MB/s
* 循序的從 1 Gbps 坪寬的乙太網路讀取約 100 MB/s
* 循序的從 SSD 讀取大約 1 GB/s
* 循序的從主記憶體中讀取大約 4 GB/s
* 每秒大約可以繞地球 6-7 圈
* 資料中心內每秒約有 2000 次的往返

#### 視覺化延遲數

![](https://camo.githubusercontent.com/77f72259e1eb58596b564d1ad823af1853bc60a3/687474703a2f2f692e696d6775722e636f6d2f6b307431652e706e67)

#### 來源及延伸閱讀

* [每個程式設計師都應該知道的延遲數量級 - 1](https://gist.github.com/jboner/2841832)
* [每個程式設計師都應該知道的延遲數量級 - 2](https://gist.github.com/hellerbarde/2843375)
* [關於建置大型分散式系統所需要知道的設計方案、課程和建議](http://www.cs.cornell.edu/projects/ladis2009/talks/dean-keynote-ladis2009.pdf)
* [從軟體工程師的角度來看建置大型分散式系統](https://static.googleusercontent.com/media/research.google.com/en//people/jeff/stanford-295-talk.pdf)

### 其他的系統設計面試問題

> 常見的系統設計問題，同時提供如何解決該問題的連結

| 問題                                   | 來源                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 設計一個類似於 Dropbox 的文件同步系統  | [youtube.com](https://www.youtube.com/watch?v=PE4gwstWhmc)                                                                                                                                                                                                                                                                                                                                                                                        |
| 設計一個類似於 Google 的搜尋引擎       | [queue.acm.org](http://queue.acm.org/detail.cfm?id=988407)<br/>[stackexchange.com](http://programmers.stackexchange.com/questions/38324/interview-question-how-would-you-implement-google-search)<br/>[ardendertat.com](http://www.ardendertat.com/2012/01/11/implementing-search-engines/)<br/>[stanford.edu](http://infolab.stanford.edu/~backrub/google.html)                                                                                                 |
| 設計一個像 Google 一樣可擴展的網路爬蟲 | [quora.com](https://www.quora.com/How-can-I-build-a-web-crawler-from-scratch)                                                                                                                                                                                                                                                                                                                                                                     |
| 設計一個 Google Docs                   | [code.google.com](https://code.google.com/p/google-mobwrite/)<br/>[neil.fraser.name](https://neil.fraser.name/writing/sync/)                                                                                                                                                                                                                                                                                                                           |
| 設計一個像 Redis 一樣的鍵值對系統      | [slideshare.net](http://www.slideshare.net/dvirsky/introduction-to-redis)                                                                                                                                                                                                                                                                                                                                                                         |
| 設計一個像 Memcached 的快取系統        | [slideshare.net](http://www.slideshare.net/oemebamo/introduction-to-memcached)                                                                                                                                                                                                                                                                                                                                                                    |
| 設計一個像 Amazon 一樣的推薦系統       | [hulu.com](http://tech.hulu.com/blog/2011/09/19/recommendation-system.html)[ijcai13.org](http://ijcai13.org/files/tutorial_slides/td3.pdf)                                                                                                                                                                                                                                                                                                        |
| 設計一個像 Bitly 一樣的短網址服務      | [n00tc0d3r.blogspot.com](http://n00tc0d3r.blogspot.com/)                                                                                                                                                                                                                                                                                                                                                                                          |
| 設計一個像 WhatsApp 一樣的即時訊息系統 | [highscalability.com](http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html)                                                                                                                                                                                                                                                                                                                    |
| 設計一個像 Instagram 一樣的相片服務    | [highscalability.com](http://highscalability.com/flickr-architecture)<br/>[highscalability.com](http://highscalability.com/blog/2011/12/6/instagram-architecture-14-million-users-terabytes-of-photos.html)                                                                                                                                                                                                                                            |
| 設計一個像 Facebook 的新聞推薦方法     | [quora.com](http://www.quora.com/What-are-best-practices-for-building-something-like-a-News-Feed)<br/>[quora.com](http://www.quora.com/Activity-Streams/What-are-the-scaling-issues-to-keep-in-mind-while-developing-a-social-network-feed)<br/>[slideshare.net](http://www.slideshare.net/danmckinley/etsy-activity-feeds-architecture)                                                                                                                    |
| 設計一個 Facebook 時間軸功能           | [facebook.com](https://www.facebook.com/note.php?note_id=10150468255628920)<br/>[highscalability.com](http://highscalability.com/blog/2012/1/23/facebook-timeline-brought-to-you-by-the-power-of-denormaliza.html)                                                                                                                                                                                                                                     |
| 設計 Facebook 的聊天功能               | [erlang-factory.com](http://www.erlang-factory.com/upload/presentations/31/EugeneLetuchy-ErlangatFacebook.pdf)<br/>[facebook.com](https://www.facebook.com/note.php?note_id=14218138919&id=9445547199&index=0)                                                                                                                                                                                                                                         |
| 設計一個像 Facebook 的圖形化搜尋系統   | [facebook.com](https://www.facebook.com/notes/facebook-engineering/under-the-hood-building-out-the-infrastructure-for-graph-search/10151347573598920)<br/>[facebook.com](https://www.facebook.com/notes/facebook-engineering/under-the-hood-indexing-and-ranking-in-graph-search/10151361720763920)<br/>[facebook.com](https://www.facebook.com/notes/facebook-engineering/under-the-hood-the-natural-language-interface-of-graph-search/10151432733048920) |
| 設計一個像 CloudFlare 的內容傳輸網路   | [cmu.edu](http://repository.cmu.edu/cgi/viewcontent.cgi?article=2112&context=compsci)                                                                                                                                                                                                                                                                                                                                                             |
| 設計一個像 Twitter 的微網誌服務        | [michael-noll.com](http://www.michael-noll.com/blog/2013/01/18/implementing-real-time-trending-topics-in-storm/)<br/>[snikolov .wordpress.com](http://snikolov.wordpress.com/2012/11/14/early-detection-of-twitter-trends/)                                                                                                                                                                                                                            |
| 設計一個隨機 ID 生成系統               | [blog.twitter.com](https://blog.twitter.com/2010/announcing-snowflake)<br/>[github.com](https://github.com/twitter/snowflake/)                                                                                                                                                                                                                                                                                                                         |
| 給定一段時間，回傳次數排名前 K 的請求  | [ucsb.edu](https://icmi.cs.ucsb.edu/research/tech_reports/reports/2005-23.pdf)<br/>[wpi.edu](http://davis.wpi.edu/xmdv/docs/EDBT11-diyang.pdf)                                                                                                                                                                                                                                                                                                         |
| 設計一個資料來源在多個資料中心的系統   | [highscalability.com](http://highscalability.com/blog/2009/8/24/how-google-serves-data-from-multiple-datacenters.html)                                                                                                                                                                                                                                                                                                                            |
| 設計一個線上多人卡牌遊戲               | [indieflashblog.com](http://www.indieflashblog.com/how-to-create-an-asynchronous-multiplayer-game.html)<br/>[buildnewgames.com](http://buildnewgames.com/real-time-multiplayer/)                                                                                                                                                                                                                                                                       |
| 設計一個垃圾回收系統                   | [stuffwithstuff.com](http://journal.stuffwithstuff.com/2013/12/08/babys-first-garbage-collector/)<br/>[washington.edu](http://courses.cs.washington.edu/courses/csep521/07wi/prj/rick.pdf)                                                                                                                                                                                                                                                             |
| 貢獻更多系統設計問題                   | [Contribute](#如何貢獻)                                                                                                                                                                                                                                                                                                                                                                                                                           |

### 真實世界的架構

> 底下是關於真實世界的系統架構是如何設計的文章

<p align="center">
  <img src="http://i.imgur.com/TcUo2fw.png"/>
  <br/>
  <i><a href=https://www.infoq.com/presentations/Twitter-Timeline-Scalability>資料來源：可擴展式的 Twitter 時間軸設計</a></i>
</p>

**不要關注以下文章的細節，而是注意以下幾點：**

* 找到這些文章中共通的原則、技術和模式
* 學習每個元件負責解決哪些問題、在什麼情況下使用、什麼情況下不適用
* 複習學習過的文章

| 種類     | 系統                                                     | 參考來源                                                                                                                                       |
|----------|----------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| 資料處理 | **MapReduce** - Google 的分散式資料處理                  | [research.google.com](http://static.googleusercontent.com/media/research.google.com/zh-CN/us/archive/mapreduce-osdi04.pdf)                     |
| 資料處理 | **Spark** - Databricks 的分散式資料處理                  | [slideshare.net](http://www.slideshare.net/AGrishchenko/apache-spark-architecture)                                                             |
| 資料處理 | **Storm** - Twitter 的分散式資料處理                     | [slideshare.net](http://www.slideshare.net/previa/storm-16094009)                                                                              |
|          |                                                          |                                                                                                                                                |
| 資料儲存 | **Bigtable** - Google 的列式資料庫                       | [harvard.edu](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/chang06bigtable.pdf)                                                    |
| 資料儲存 | **HBase** - Bigtable 的開放原始碼解決方案                | [slideshare.net](http://www.slideshare.net/alexbaranau/intro-to-hbase)                                                                         |
| 資料儲存 | **Cassandra** - Facebook 的列式資料庫                    | [slideshare.net](http://www.slideshare.net/planetcassandra/cassandra-introduction-features-30103666)                                           |
| 資料儲存 | **DynamoDB** - Amazon 的文件式資料庫                     | [harvard.edu](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/decandia07dynamo.pdf)                                                   |
| 資料儲存 | **MongoDB** - 文件式資料庫                               | [slideshare.net](http://www.slideshare.net/mdirolf/introduction-to-mongodb)                                                                    |
| 資料儲存 | **Spanner** - Google 的全球分散式資料庫                  | [research.google.com](http://research.google.com/archive/spanner-osdi2012.pdf)                                                                 |
| 資料儲存 | **Memcached** - 分散式的記憶體快取系統                   | [slideshare.net](http://www.slideshare.net/oemebamo/introduction-to-memcached)                                                                 |
| 資料儲存 | **Redis** - 具有持久化及值型別的分散式快取系統           | [slideshare.net](http://www.slideshare.net/dvirsky/introduction-to-redis)                                                                      |
|          |                                                          |                                                                                                                                                |
| 檔案系統 | **Google File System (GFS)** - 分散式的檔案系統          | [research.google.com](http://static.googleusercontent.com/media/research.google.com/zh-CN/us/archive/gfs-sosp2003.pdf)                         |
| 檔案系統 | **Hadoop File System (HDFS)** - GFS 的開放原始碼解決方案 | [apache.org](https://hadoop.apache.org/docs/r1.2.1/hdfs_design.html)                                                                           |
|          |                                                          |                                                                                                                                                |
| 其他     | **Chubby** - Google 的分散式系統低耦合鎖服務             | [research.google.com](http://static.googleusercontent.com/external_content/untrusted_dlcp/research.google.com/en/us/archive/chubby-osdi06.pdf) |
| 其他     | **Dapper** - 分散式系統監控基礎設施                      | [research.google.com](http://static.googleusercontent.com/media/research.google.com/en//pubs/archive/36356.pdf)                                |
| 其他     | **Kafka** - LinkedIn 的 pub/sub 訊息佇列服務             | [slideshare.net](http://www.slideshare.net/mumrah/kafka-talk-tri-hug)                                                                          |
| 其他     | **Zookeeper** - 集中式的基礎架構和協調服務               | [slideshare.net](http://www.slideshare.net/sauravhaloi/introduction-to-apache-zookeeper)                                                       |
|          | 貢獻更多架構                                             | [Contribute](#如何貢獻)                                                                                                                        |

### 公司的系統架構

| 公司           | 參考                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Amazon         | [Amazon 的架構](http://highscalability.com/amazon-architecture)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Cinchcast      | [每天產生 1,500 小時的音樂](http://highscalability.com/blog/2012/7/16/cinchcast-architecture-producing-1500-hours-of-audio-every-d.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| DataSift       | [每秒探勘 120,000 則 tweet](http://highscalability.com/blog/2011/11/29/datasift-architecture-realtime-datamining-at-120000-tweets-p.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| DropBox        | [我們如何擴展 Dropbox](https://www.youtube.com/watch?v=PE4gwstWhmc)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ESPN           | [每秒操作 100,000 次 duh nuh nuhs](http://highscalability.com/blog/2013/11/4/espns-architecture-at-scale-operating-at-100000-duh-nuh-nuhs.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Google         | [Google 的架構](http://highscalability.com/google-architecture)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Instagram      | [一千四百萬個使用者，TB 等級的照片儲存](http://highscalability.com/blog/2011/12/6/instagram-architecture-14-million-users-terabytes-of-photos.html)<br/>[什麼驅動著 Instagram](http://instagram-engineering.tumblr.com/post/13649370142/what-powers-instagram-hundreds-of-instances)                                                                                                                                                                                                                                                                                                                                                                                                 |
| Justin.tv      | [Justin.Tv 的即時影片廣播架構](http://highscalability.com/blog/2010/3/16/justintvs-live-video-broadcasting-architecture.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Facebook       | [Facebook 可擴展的 memcached 架構](https://cs.uwaterloo.ca/~brecht/courses/854-Emerging-2014/readings/key-value/fb-memcached-nsdi-2013.pdf)<br/>[TAO: Facebook 為了社交網路架構的分散式資料儲存](https://cs.uwaterloo.ca/~brecht/courses/854-Emerging-2014/readings/data-store/tao-facebook-distributed-datastore-atc-2013.pdf)<br/>[Facebook 的圖片儲存架構](https://www.usenix.org/legacy/event/osdi10/tech/full_papers/Beaver.pdf)                                                                                                                                                                                                                                                     |
| Flickr         | [Flickr 的架構](http://highscalability.com/flickr-architecture)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Mailbox        | [在六週內從 0 到 100 萬個使用者](http://highscalability.com/blog/2013/6/18/scaling-mailbox-from-0-to-one-million-users-in-6-weeks-and-1.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Pinterest      | [從零到每個月數十億次的瀏覽量](http://highscalability.com/blog/2013/4/15/scaling-pinterest-from-0-to-10s-of-billions-of-page-views-a.html)<br/>[1800 萬個訪問人次、10 倍成長、12 名員工](http://highscalability.com/blog/2012/5/21/pinterest-architecture-update-18-million-visitors-10x-growth.html)                                                                                                                                                                                                                                                                                                                                                                                |
| Playfish       | [月使用者量 5000 萬人次在成長](http://highscalability.com/blog/2010/9/21/playfishs-social-gaming-architecture-50-million-monthly-user.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| PlentyOfFish   | [PlentyOfFish 的架構](http://highscalability.com/plentyoffish-architecture)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Salesforce     | [如何處理每天 13 億筆交易](http://highscalability.com/blog/2013/9/23/salesforce-architecture-how-they-handle-13-billion-transacti.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Stack Overflow | [Stack Overflow 的架構](http://highscalability.com/blog/2009/8/5/stack-overflow-architecture.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| TripAdvisor    | [4000 萬的訪問人次、2 億次頁面瀏覽量、30 TB 的資料](http://highscalability.com/blog/2011/6/27/tripadvisor-architecture-40m-visitors-200m-dynamic-page-view.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Tumblr         | [每月 150 億的瀏覽量](http://highscalability.com/blog/2012/2/13/tumblr-architecture-15-billion-page-views-a-month-and-harder.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Twitter        | [如何讓 Twitter 的速度成長 10000 倍](http://highscalability.com/scaling-twitter-making-twitter-10000-percent-faster)<br/>[使用 MySQL 儲存每天 2.5 億條 tweet](http://highscalability.com/blog/2011/12/19/how-twitter-stores-250-million-tweets-a-day-using-mysql.html)<br/>[1.5 億的活躍使用者、300K QPS、22 MB/S 的串流資料](http://highscalability.com/blog/2013/7/8/the-architecture-twitter-uses-to-deal-with-150m-active-users.html)<br/>[可擴展的 Timelines](https://www.infoq.com/presentations/Twitter-Timeline-Scalability)<br/>[Twitter 的大大小小的資料](https://www.youtube.com/watch?v=5cKTP36HVgI)<br/>[Twitter 的運營：擴展超過一億個使用者](https://www.youtube.com/watch?v=z8LU0Cj6BOU) |
| Uber           | [Uber 是如何擴展他們的及時行銷平台](http://highscalability.com/blog/2015/9/14/how-uber-scales-their-real-time-market-platform.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| WhatsApp       | [讓 Facebook 用 $190 億購買下來的 WhatsApp 的架構](http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| YouTube        | [YouTube 的可擴展性](https://www.youtube.com/watch?v=w5WVu624fY8)[YouTube 的架構](http://highscalability.com/youtube-architecture)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

### 公司的工程部落格

> 你即將面試的公司的架構
>
> 你被問到的問題可能就來自於相同領域的問題

* [Airbnb Engineering](http://nerds.airbnb.com/)
* [Atlassian Developers](https://developer.atlassian.com/blog/)
* [Autodesk Engineering](http://cloudengineering.autodesk.com/blog/)
* [AWS Blog](https://aws.amazon.com/blogs/aws/)
* [Bitly Engineering Blog](http://word.bitly.com/)
* [Box Blogs](https://www.box.com/blog/engineering/)
* [Cloudera Developer Blog](http://blog.cloudera.com/blog/)
* [Dropbox Tech Blog](https://tech.dropbox.com/)
* [Engineering at Quora](http://engineering.quora.com/)
* [Ebay Tech Blog](http://www.ebaytechblog.com/)
* [Evernote Tech Blog](https://blog.evernote.com/tech/)
* [Etsy Code as Craft](http://codeascraft.com/)
* [Facebook Engineering](https://www.facebook.com/Engineering)
* [Flickr Code](http://code.flickr.net/)
* [Foursquare Engineering Blog](http://engineering.foursquare.com/)
* [GitHub Engineering Blog](http://githubengineering.com/)
* [Google Research Blog](http://googleresearch.blogspot.com/)
* [Groupon Engineering Blog](https://engineering.groupon.com/)
* [Heroku Engineering Blog](https://engineering.heroku.com/)
* [Hubspot Engineering Blog](http://product.hubspot.com/blog/topic/engineering)
* [High Scalability](http://highscalability.com/)
* [Instagram Engineering](http://instagram-engineering.tumblr.com/)
* [Intel Software Blog](https://software.intel.com/en-us/blogs/)
* [Jane Street Tech Blog](https://blogs.janestreet.com/category/ocaml/)
* [LinkedIn Engineering](http://engineering.linkedin.com/blog)
* [Microsoft Engineering](https://engineering.microsoft.com/)
* [Microsoft Python Engineering](https://blogs.msdn.microsoft.com/pythonengineering/)
* [Netflix Tech Blog](http://techblog.netflix.com/)
* [Paypal Developer Blog](https://devblog.paypal.com/category/engineering/)
* [Pinterest Engineering Blog](http://engineering.pinterest.com/)
* [Quora Engineering](https://engineering.quora.com/)
* [Reddit Blog](http://www.redditblog.com/)
* [Salesforce Engineering Blog](https://developer.salesforce.com/blogs/engineering/)
* [Slack Engineering Blog](https://slack.engineering/)
* [Spotify Labs](https://labs.spotify.com/)
* [Twilio Engineering Blog](http://www.twilio.com/engineering)
* [Twitter Engineering](https://engineering.twitter.com/)
* [Uber Engineering Blog](http://eng.uber.com/)
* [Yahoo Engineering Blog](http://yahooeng.tumblr.com/)
* [Yelp Engineering Blog](http://engineeringblog.yelp.com/)
* [Zynga Engineering Blog](https://www.zynga.com/blogs/engineering)

#### 來源及延伸閱讀

* [kilimchoi/engineering-blogs](https://github.com/kilimchoi/engineering-blogs)

## 仍在進行中

有興趣增加一些內容，或幫忙完善某些部分嗎？ [來貢獻吧](#如何貢獻)!

* 使用 MapReduce 進行分散式運算
* 一致性的 hashing
* 直接記憶體存取
* [貢獻](#如何貢獻)

## 致謝

在這個 Repository 中提供的任何來源和開放原始碼庫

特別感謝：

* [Hired in tech](http://www.hiredintech.com/system-design/the-system-design-process/)
* [Cracking the coding interview](https://www.amazon.com/dp/0984782850/)
* [High scalability](http://highscalability.com/)
* [checkcheckzz/system-design-interview](https://github.com/checkcheckzz/system-design-interview)
* [shashank88/system_design](https://github.com/shashank88/system_design)
* [mmcgrana/services-engineering](https://github.com/mmcgrana/services-engineering)
* [System design cheat sheet](https://gist.github.com/vasanthk/485d1c25737e8e72759f)
* [A distributed systems reading list](http://dancres.github.io/Pages/)
* [Cracking the system design interview](http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview)

## 聯絡資訊

隨時歡迎與我討論相關的問題或意見。

我的聯絡資訊可以在我的 [GitHub 主頁](https://github.com/donnemartin) 中找到。

## 授權

*我已開放原始碼授權的方式提供你在此儲存庫中的程式碼和資源。因為這是我個人的儲存庫，所以你所以所收到的使用許可是來自於我，並非我的雇主(Facebook)*

    Copyright 2017 Donne Martin

    Creative Commons Attribution 4.0 International License (CC BY 4.0)

    http://creativecommons.org/licenses/by/4.0/
*[English](README.md) ∙ [日本語](README-ja.md) ∙ [简体中文](README-zh-Hans.md) ∙ [繁體中文](README-zh-TW.md) | [العَرَبِيَّة‎](https://github.com/donnemartin/system-design-primer/issues/170) ∙ [বাংলা](https://github.com/donnemartin/system-design-primer/issues/220) ∙ [Português do Brasil](https://github.com/donnemartin/system-design-primer/issues/40) ∙ [Deutsch](https://github.com/donnemartin/system-design-primer/issues/186) ∙ [ελληνικά](https://github.com/donnemartin/system-design-primer/issues/130) ∙ [עברית](https://github.com/donnemartin/system-design-primer/issues/272) ∙ [Italiano](https://github.com/donnemartin/system-design-primer/issues/104) ∙ [韓國語](https://github.com/donnemartin/system-design-primer/issues/102) ∙ [فارسی](https://github.com/donnemartin/system-design-primer/issues/110) ∙ [Polski](https://github.com/donnemartin/system-design-primer/issues/68) ∙ [русский язык](https://github.com/donnemartin/system-design-primer/issues/87) ∙ [Español](https://github.com/donnemartin/system-design-primer/issues/136) ∙ [ภาษาไทย](https://github.com/donnemartin/system-design-primer/issues/187) ∙ [Türkçe](https://github.com/donnemartin/system-design-primer/issues/39) ∙ [tiếng Việt](https://github.com/donnemartin/system-design-primer/issues/127) ∙ [Français](https://github.com/donnemartin/system-design-primer/issues/250) | [Add Translation](https://github.com/donnemartin/system-design-primer/issues/28)*

# The System Design Primer

<p align="center">
  <img src="http://i.imgur.com/jj3A5N8.png"/>
  <br/>
</p>

## Motivation

> Learn how to design large-scale systems.
>
> Prep for the system design interview.

### Learn how to design large-scale systems

Learning how to design scalable systems will help you become a better engineer.

System design is a broad topic.  There is a **vast amount of resources scattered throughout the web** on system design principles.

This repo is an **organized collection** of resources to help you learn how to build systems at scale.

### Learn from the open source community

This is a continually updated, open source project.

[Contributions](#contributing) are welcome!

### Prep for the system design interview

In addition to coding interviews, system design is a **required component** of the **technical interview process** at many tech companies.

**Practice common system design interview questions** and **compare** your results with **sample solutions**: discussions, code, and diagrams.

Additional topics for interview prep:

* [Study guide](#study-guide)
* [How to approach a system design interview question](#how-to-approach-a-system-design-interview-question)
* [System design interview questions, **with solutions**](#system-design-interview-questions-with-solutions)
* [Object-oriented design interview questions, **with solutions**](#object-oriented-design-interview-questions-with-solutions)
* [Additional system design interview questions](#additional-system-design-interview-questions)

## Anki flashcards

<p align="center">
  <img src="http://i.imgur.com/zdCAkB3.png"/>
  <br/>
</p>

The provided [Anki flashcard decks](https://apps.ankiweb.net/) use spaced repetition to help you retain key system design concepts.

* [System design deck](https://github.com/donnemartin/system-design-primer/tree/master/resources/flash_cards/System%20Design.apkg)
* [System design exercises deck](https://github.com/donnemartin/system-design-primer/tree/master/resources/flash_cards/System%20Design%20Exercises.apkg)
* [Object oriented design exercises deck](https://github.com/donnemartin/system-design-primer/tree/master/resources/flash_cards/OO%20Design.apkg)

Great for use while on-the-go.

### Coding Resource: Interactive Coding Challenges

Looking for resources to help you prep for the [**Coding Interview**](https://github.com/donnemartin/interactive-coding-challenges)?

<p align="center">
  <img src="http://i.imgur.com/b4YtAEN.png"/>
  <br/>
</p>

Check out the sister repo [**Interactive Coding Challenges**](https://github.com/donnemartin/interactive-coding-challenges), which contains an additional Anki deck:

* [Coding deck](https://github.com/donnemartin/interactive-coding-challenges/tree/master/anki_cards/Coding.apkg)

## Contributing

> Learn from the community.

Feel free to submit pull requests to help:

* Fix errors
* Improve sections
* Add new sections
* [Translate](https://github.com/donnemartin/system-design-primer/issues/28)

Content that needs some polishing is placed [under development](#under-development).

Review the [Contributing Guidelines](CONTRIBUTING.md).

## Index of system design topics

> Summaries of various system design topics, including pros and cons.  **Everything is a trade-off**.
>
> Each section contains links to more in-depth resources.

<p align="center">
  <img src="http://i.imgur.com/jrUBAF7.png"/>
  <br/>
</p>

* [System design topics: start here](#system-design-topics-start-here)
    * [Step 1: Review the scalability video lecture](#step-1-review-the-scalability-video-lecture)
    * [Step 2: Review the scalability article](#step-2-review-the-scalability-article)
    * [Next steps](#next-steps)
* [Performance vs scalability](#performance-vs-scalability)
* [Latency vs throughput](#latency-vs-throughput)
* [Availability vs consistency](#availability-vs-consistency)
    * [CAP theorem](#cap-theorem)
        * [CP - consistency and partition tolerance](#cp---consistency-and-partition-tolerance)
        * [AP - availability and partition tolerance](#ap---availability-and-partition-tolerance)
* [Consistency patterns](#consistency-patterns)
    * [Weak consistency](#weak-consistency)
    * [Eventual consistency](#eventual-consistency)
    * [Strong consistency](#strong-consistency)
* [Availability patterns](#availability-patterns)
    * [Fail-over](#fail-over)
    * [Replication](#replication)
    * [Availability in numbers](#availability-in-numbers)
* [Domain name system](#domain-name-system)
* [Content delivery network](#content-delivery-network)
    * [Push CDNs](#push-cdns)
    * [Pull CDNs](#pull-cdns)
* [Load balancer](#load-balancer)
    * [Active-passive](#active-passive)
    * [Active-active](#active-active)
    * [Layer 4 load balancing](#layer-4-load-balancing)
    * [Layer 7 load balancing](#layer-7-load-balancing)
    * [Horizontal scaling](#horizontal-scaling)
* [Reverse proxy (web server)](#reverse-proxy-web-server)
    * [Load balancer vs reverse proxy](#load-balancer-vs-reverse-proxy)
* [Application layer](#application-layer)
    * [Microservices](#microservices)
    * [Service discovery](#service-discovery)
* [Database](#database)
    * [Relational database management system (RDBMS)](#relational-database-management-system-rdbms)
        * [Master-slave replication](#master-slave-replication)
        * [Master-master replication](#master-master-replication)
        * [Federation](#federation)
        * [Sharding](#sharding)
        * [Denormalization](#denormalization)
        * [SQL tuning](#sql-tuning)
    * [NoSQL](#nosql)
        * [Key-value store](#key-value-store)
        * [Document store](#document-store)
        * [Wide column store](#wide-column-store)
        * [Graph Database](#graph-database)
    * [SQL or NoSQL](#sql-or-nosql)
* [Cache](#cache)
    * [Client caching](#client-caching)
    * [CDN caching](#cdn-caching)
    * [Web server caching](#web-server-caching)
    * [Database caching](#database-caching)
    * [Application caching](#application-caching)
    * [Caching at the database query level](#caching-at-the-database-query-level)
    * [Caching at the object level](#caching-at-the-object-level)
    * [When to update the cache](#when-to-update-the-cache)
        * [Cache-aside](#cache-aside)
        * [Write-through](#write-through)
        * [Write-behind (write-back)](#write-behind-write-back)
        * [Refresh-ahead](#refresh-ahead)
* [Asynchronism](#asynchronism)
    * [Message queues](#message-queues)
    * [Task queues](#task-queues)
    * [Back pressure](#back-pressure)
* [Communication](#communication)
    * [Transmission control protocol (TCP)](#transmission-control-protocol-tcp)
    * [User datagram protocol (UDP)](#user-datagram-protocol-udp)
    * [Remote procedure call (RPC)](#remote-procedure-call-rpc)
    * [Representational state transfer (REST)](#representational-state-transfer-rest)
* [Security](#security)
* [Appendix](#appendix)
    * [Powers of two table](#powers-of-two-table)
    * [Latency numbers every programmer should know](#latency-numbers-every-programmer-should-know)
    * [Additional system design interview questions](#additional-system-design-interview-questions)
    * [Real world architectures](#real-world-architectures)
    * [Company architectures](#company-architectures)
    * [Company engineering blogs](#company-engineering-blogs)
* [Under development](#under-development)
* [Credits](#credits)
* [Contact info](#contact-info)
* [License](#license)

## Study guide

> Suggested topics to review based on your interview timeline (short, medium, long).

![Imgur](http://i.imgur.com/OfVllex.png)

**Q: For interviews, do I need to know everything here?**

**A: No, you don't need to know everything here to prepare for the interview**.

What you are asked in an interview depends on variables such as:

* How much experience you have
* What your technical background is
* What positions you are interviewing for
* Which companies you are interviewing with
* Luck

More experienced candidates are generally expected to know more about system design.  Architects or team leads might be expected to know more than individual contributors.  Top tech companies are likely to have one or more design interview rounds.

Start broad and go deeper in a few areas.  It helps to know a little about various key system design topics.  Adjust the following guide based on your timeline, experience, what positions you are interviewing for, and which companies you are interviewing with.

* **Short timeline** - Aim for **breadth** with system design topics.  Practice by solving **some** interview questions.
* **Medium timeline** - Aim for **breadth** and **some depth** with system design topics.  Practice by solving **many** interview questions.
* **Long timeline** - Aim for **breadth** and **more depth** with system design topics.  Practice by solving **most** interview questions.

| | Short | Medium | Long |
|---|---|---|---|
| Read through the [System design topics](#index-of-system-design-topics) to get a broad understanding of how systems work | :+1: | :+1: | :+1: |
| Read through a few articles in the [Company engineering blogs](#company-engineering-blogs) for the companies you are interviewing with | :+1: | :+1: | :+1: |
| Read through a few [Real world architectures](#real-world-architectures) | :+1: | :+1: | :+1: |
| Review [How to approach a system design interview question](#how-to-approach-a-system-design-interview-question) | :+1: | :+1: | :+1: |
| Work through [System design interview questions with solutions](#system-design-interview-questions-with-solutions) | Some | Many | Most |
| Work through [Object-oriented design interview questions with solutions](#object-oriented-design-interview-questions-with-solutions) | Some | Many | Most |
| Review [Additional system design interview questions](#additional-system-design-interview-questions) | Some | Many | Most |

## How to approach a system design interview question

> How to tackle a system design interview question.

The system design interview is an **open-ended conversation**.  You are expected to lead it.

You can use the following steps to guide the discussion.  To help solidify this process, work through the [System design interview questions with solutions](#system-design-interview-questions-with-solutions) section using the following steps.

### Step 1: Outline use cases, constraints, and assumptions

Gather requirements and scope the problem.  Ask questions to clarify use cases and constraints.  Discuss assumptions.

* Who is going to use it?
* How are they going to use it?
* How many users are there?
* What does the system do?
* What are the inputs and outputs of the system?
* How much data do we expect to handle?
* How many requests per second do we expect?
* What is the expected read to write ratio?

### Step 2: Create a high level design

Outline a high level design with all important components.

* Sketch the main components and connections
* Justify your ideas

### Step 3: Design core components

Dive into details for each core component.  For example, if you were asked to [design a url shortening service](solutions/system_design/pastebin/README.md), discuss:

* Generating and storing a hash of the full url
    * [MD5](solutions/system_design/pastebin/README.md) and [Base62](solutions/system_design/pastebin/README.md)
    * Hash collisions
    * SQL or NoSQL
    * Database schema
* Translating a hashed url to the full url
    * Database lookup
* API and object-oriented design

### Step 4: Scale the design

Identify and address bottlenecks, given the constraints.  For example, do you need the following to address scalability issues?

* Load balancer
* Horizontal scaling
* Caching
* Database sharding

Discuss potential solutions and trade-offs.  Everything is a trade-off.  Address bottlenecks using [principles of scalable system design](#index-of-system-design-topics).

### Back-of-the-envelope calculations

You might be asked to do some estimates by hand.  Refer to the [Appendix](#appendix) for the following resources:

* [Use back of the envelope calculations](http://highscalability.com/blog/2011/1/26/google-pro-tip-use-back-of-the-envelope-calculations-to-choo.html)
* [Powers of two table](#powers-of-two-table)
* [Latency numbers every programmer should know](#latency-numbers-every-programmer-should-know)

### Source(s) and further reading

Check out the following links to get a better idea of what to expect:

* [How to ace a systems design interview](https://www.palantir.com/2011/10/how-to-rock-a-systems-design-interview/)
* [The system design interview](http://www.hiredintech.com/system-design)
* [Intro to Architecture and Systems Design Interviews](https://www.youtube.com/watch?v=ZgdS0EUmn70)

## System design interview questions with solutions

> Common system design interview questions with sample discussions, code, and diagrams.
>
> Solutions linked to content in the `solutions/` folder.

| Question | |
|---|---|
| Design Pastebin.com (or Bit.ly) | [Solution](solutions/system_design/pastebin/README.md) |
| Design the Twitter timeline and search (or Facebook feed and search) | [Solution](solutions/system_design/twitter/README.md) |
| Design a web crawler | [Solution](solutions/system_design/web_crawler/README.md) |
| Design Mint.com | [Solution](solutions/system_design/mint/README.md) |
| Design the data structures for a social network | [Solution](solutions/system_design/social_graph/README.md) |
| Design a key-value store for a search engine | [Solution](solutions/system_design/query_cache/README.md) |
| Design Amazon's sales ranking by category feature | [Solution](solutions/system_design/sales_rank/README.md) |
| Design a system that scales to millions of users on AWS | [Solution](solutions/system_design/scaling_aws/README.md) |
| Add a system design question | [Contribute](#contributing) |

### Design Pastebin.com (or Bit.ly)

[View exercise and solution](solutions/system_design/pastebin/README.md)

![Imgur](http://i.imgur.com/4edXG0T.png)

### Design the Twitter timeline and search (or Facebook feed and search)

[View exercise and solution](solutions/system_design/twitter/README.md)

![Imgur](http://i.imgur.com/jrUBAF7.png)

### Design a web crawler

[View exercise and solution](solutions/system_design/web_crawler/README.md)

![Imgur](http://i.imgur.com/bWxPtQA.png)

### Design Mint.com

[View exercise and solution](solutions/system_design/mint/README.md)

![Imgur](http://i.imgur.com/V5q57vU.png)

### Design the data structures for a social network

[View exercise and solution](solutions/system_design/social_graph/README.md)

![Imgur](http://i.imgur.com/cdCv5g7.png)

### Design a key-value store for a search engine

[View exercise and solution](solutions/system_design/query_cache/README.md)

![Imgur](http://i.imgur.com/4j99mhe.png)

### Design Amazon's sales ranking by category feature

[View exercise and solution](solutions/system_design/sales_rank/README.md)

![Imgur](http://i.imgur.com/MzExP06.png)

### Design a system that scales to millions of users on AWS

[View exercise and solution](solutions/system_design/scaling_aws/README.md)

![Imgur](http://i.imgur.com/jj3A5N8.png)

## Object-oriented design interview questions with solutions

> Common object-oriented design interview questions with sample discussions, code, and diagrams.
>
> Solutions linked to content in the `solutions/` folder.

>**Note: This section is under development**

| Question | |
|---|---|
| Design a hash map | [Solution](solutions/object_oriented_design/hash_table/hash_map.ipynb)  |
| Design a least recently used cache | [Solution](solutions/object_oriented_design/lru_cache/lru_cache.ipynb)  |
| Design a call center | [Solution](solutions/object_oriented_design/call_center/call_center.ipynb)  |
| Design a deck of cards | [Solution](solutions/object_oriented_design/deck_of_cards/deck_of_cards.ipynb)  |
| Design a parking lot | [Solution](solutions/object_oriented_design/parking_lot/parking_lot.ipynb)  |
| Design a chat server | [Solution](solutions/object_oriented_design/online_chat/online_chat.ipynb)  |
| Design a circular array | [Contribute](#contributing)  |
| Add an object-oriented design question | [Contribute](#contributing) |

## System design topics: start here

New to system design?

First, you'll need a basic understanding of common principles, learning about what they are, how they are used, and their pros and cons.

### Step 1: Review the scalability video lecture

[Scalability Lecture at Harvard](https://www.youtube.com/watch?v=-W9F__D3oY4)

* Topics covered:
    * Vertical scaling
    * Horizontal scaling
    * Caching
    * Load balancing
    * Database replication
    * Database partitioning

### Step 2: Review the scalability article

[Scalability](http://www.lecloud.net/tagged/scalability/chrono)

* Topics covered:
    * [Clones](http://www.lecloud.net/post/7295452622/scalability-for-dummies-part-1-clones)
    * [Databases](http://www.lecloud.net/post/7994751381/scalability-for-dummies-part-2-database)
    * [Caches](http://www.lecloud.net/post/9246290032/scalability-for-dummies-part-3-cache)
    * [Asynchronism](http://www.lecloud.net/post/9699762917/scalability-for-dummies-part-4-asynchronism)

### Next steps

Next, we'll look at high-level trade-offs:

* **Performance** vs **scalability**
* **Latency** vs **throughput**
* **Availability** vs **consistency**

Keep in mind that **everything is a trade-off**.

Then we'll dive into more specific topics such as DNS, CDNs, and load balancers.

## Performance vs scalability

A service is **scalable** if it results in increased **performance** in a manner proportional to resources added. Generally, increasing performance means serving more units of work, but it can also be to handle larger units of work, such as when datasets grow.<sup><a href=http://www.allthingsdistributed.com/2006/03/a_word_on_scalability.html>1</a></sup>

Another way to look at performance vs scalability:

* If you have a **performance** problem, your system is slow for a single user.
* If you have a **scalability** problem, your system is fast for a single user but slow under heavy load.

### Source(s) and further reading

* [A word on scalability](http://www.allthingsdistributed.com/2006/03/a_word_on_scalability.html)
* [Scalability, availability, stability, patterns](http://www.slideshare.net/jboner/scalability-availability-stability-patterns/)

## Latency vs throughput

**Latency** is the time to perform some action or to produce some result.

**Throughput** is the number of such actions or results per unit of time.

Generally, you should aim for **maximal throughput** with **acceptable latency**.

### Source(s) and further reading

* [Understanding latency vs throughput](https://community.cadence.com/cadence_blogs_8/b/sd/archive/2010/09/13/understanding-latency-vs-throughput)

## Availability vs consistency

### CAP theorem

<p align="center">
  <img src="http://i.imgur.com/bgLMI2u.png"/>
  <br/>
  <i><a href=http://robertgreiner.com/2014/08/cap-theorem-revisited>Source: CAP theorem revisited</a></i>
</p>

In a distributed computer system, you can only support two of the following guarantees:

* **Consistency** - Every read receives the most recent write or an error
* **Availability** - Every request receives a response, without guarantee that it contains the most recent version of the information
* **Partition Tolerance** - The system continues to operate despite arbitrary partitioning due to network failures

*Networks aren't reliable, so you'll need to support partition tolerance.  You'll need to make a software tradeoff between consistency and availability.*

#### CP - consistency and partition tolerance

Waiting for a response from the partitioned node might result in a timeout error.  CP is a good choice if your business needs require atomic reads and writes.

#### AP - availability and partition tolerance

Responses return the most recent version of the data available on a node, which might not be the latest.  Writes might take some time to propagate when the partition is resolved.

AP is a good choice if the business needs allow for [eventual consistency](#eventual-consistency) or when the system needs to continue working despite external errors.

### Source(s) and further reading

* [CAP theorem revisited](http://robertgreiner.com/2014/08/cap-theorem-revisited/)
* [A plain english introduction to CAP theorem](http://ksat.me/a-plain-english-introduction-to-cap-theorem/)
* [CAP FAQ](https://github.com/henryr/cap-faq)

## Consistency patterns

With multiple copies of the same data, we are faced with options on how to synchronize them so clients have a consistent view of the data.  Recall the definition of consistency from the [CAP theorem](#cap-theorem) - Every read receives the most recent write or an error.

### Weak consistency

After a write, reads may or may not see it.  A best effort approach is taken.

This approach is seen in systems such as memcached.  Weak consistency works well in real time use cases such as VoIP, video chat, and realtime multiplayer games.  For example, if you are on a phone call and lose reception for a few seconds, when you regain connection you do not hear what was spoken during connection loss.

### Eventual consistency

After a write, reads will eventually see it (typically within milliseconds).  Data is replicated asynchronously.

This approach is seen in systems such as DNS and email.  Eventual consistency works well in highly available systems.

### Strong consistency

After a write, reads will see it.  Data is replicated synchronously.

This approach is seen in file systems and RDBMSes.  Strong consistency works well in systems that need transactions.

### Source(s) and further reading

* [Transactions across data centers](http://snarfed.org/transactions_across_datacenters_io.html)

## Availability patterns

There are two main patterns to support high availability: **fail-over** and **replication**.

### Fail-over

#### Active-passive

With active-passive fail-over, heartbeats are sent between the active and the passive server on standby.  If the heartbeat is interrupted, the passive server takes over the active's IP address and resumes service.

The length of downtime is determined by whether the passive server is already running in 'hot' standby or whether it needs to start up from 'cold' standby.  Only the active server handles traffic.

Active-passive failover can also be referred to as master-slave failover.

#### Active-active

In active-active, both servers are managing traffic, spreading the load between them.

If the servers are public-facing, the DNS would need to know about the public IPs of both servers.  If the servers are internal-facing, application logic would need to know about both servers.

Active-active failover can also be referred to as master-master failover.

### Disadvantage(s): failover

* Fail-over adds more hardware and additional complexity.
* There is a potential for loss of data if the active system fails before any newly written data can be replicated to the passive.

### Replication

#### Master-slave and master-master

This topic is further discussed in the [Database](#database) section:

* [Master-slave replication](#master-slave-replication)
* [Master-master replication](#master-master-replication)

### Availability in numbers

Availability is often quantified by uptime (or downtime) as a percentage of time the service is available.  Availability is generally measured in number of 9s--a service with 99.99% availability is described as having four 9s.

#### 99.9% availability - three 9s

| Duration            | Acceptable downtime|
|---------------------|--------------------|
| Downtime per year   | 8h 45min 57s       |
| Downtime per month  | 43m 49.7s          |
| Downtime per week   | 10m 4.8s           |
| Downtime per day    | 1m 26.4s           |

#### 99.99% availability - four 9s

| Duration            | Acceptable downtime|
|---------------------|--------------------|
| Downtime per year   | 52min 35.7s        |
| Downtime per month  | 4m 23s             |
| Downtime per week   | 1m 5s              |
| Downtime per day    | 8.6s               |

#### Availability in parallel vs in sequence

If a service consists of multiple components prone to failure, the service's overall availability depends on whether the components are in sequence or in parallel.

###### In sequence

Overall availability decreases when two components with availability < 100% are in sequence:

```
Availability (Total) = Availability (Foo) * Availability (Bar)
```

If both `Foo` and `Bar` each had 99.9% availability, their total availability in sequence would be 99.8%.

###### In parallel

Overall availability increases when two components with availability < 100% are in parallel:

```
Availability (Total) = 1 - (1 - Availability (Foo)) * (1 - Availability (Bar))
```

If both `Foo` and `Bar` each had 99.9% availability, their total availability in parallel would be 99.9999%.

## Domain name system

<p align="center">
  <img src="http://i.imgur.com/IOyLj4i.jpg"/>
  <br/>
  <i><a href=http://www.slideshare.net/srikrupa5/dns-security-presentation-issa>Source: DNS security presentation</a></i>
</p>

A Domain Name System (DNS) translates a domain name such as www.example.com to an IP address.

DNS is hierarchical, with a few authoritative servers at the top level.  Your router or ISP provides information about which DNS server(s) to contact when doing a lookup.  Lower level DNS servers cache mappings, which could become stale due to DNS propagation delays.  DNS results can also be cached by your browser or OS for a certain period of time, determined by the [time to live (TTL)](https://en.wikipedia.org/wiki/Time_to_live).

* **NS record (name server)** - Specifies the DNS servers for your domain/subdomain.
* **MX record (mail exchange)** - Specifies the mail servers for accepting messages.
* **A record (address)** - Points a name to an IP address.
* **CNAME (canonical)** - Points a name to another name or `CNAME` (example.com to www.example.com) or to an `A` record.

Services such as [CloudFlare](https://www.cloudflare.com/dns/) and [Route 53](https://aws.amazon.com/route53/) provide managed DNS services.  Some DNS services can route traffic through various methods:

* [Weighted round robin](https://www.g33kinfo.com/info/round-robin-vs-weighted-round-robin-lb)
    * Prevent traffic from going to servers under maintenance
    * Balance between varying cluster sizes
    * A/B testing
* Latency-based
* Geolocation-based

### Disadvantage(s): DNS

* Accessing a DNS server introduces a slight delay, although mitigated by caching described above.
* DNS server management could be complex and is generally managed by [governments, ISPs, and large companies](http://superuser.com/questions/472695/who-controls-the-dns-servers/472729).
* DNS services have recently come under [DDoS attack](http://dyn.com/blog/dyn-analysis-summary-of-friday-october-21-attack/), preventing users from accessing websites such as Twitter without knowing Twitter's IP address(es).

### Source(s) and further reading

* [DNS architecture](https://technet.microsoft.com/en-us/library/dd197427(v=ws.10).aspx)
* [Wikipedia](https://en.wikipedia.org/wiki/Domain_Name_System)
* [DNS articles](https://support.dnsimple.com/categories/dns/)

## Content delivery network

<p align="center">
  <img src="http://i.imgur.com/h9TAuGI.jpg"/>
  <br/>
  <i><a href=https://www.creative-artworks.eu/why-use-a-content-delivery-network-cdn/>Source: Why use a CDN</a></i>
</p>

A content delivery network (CDN) is a globally distributed network of proxy servers, serving content from locations closer to the user.  Generally, static files such as HTML/CSS/JS, photos, and videos are served from CDN, although some CDNs such as Amazon's CloudFront support dynamic content.  The site's DNS resolution will tell clients which server to contact.

Serving content from CDNs can significantly improve performance in two ways:

* Users receive content at data centers close to them
* Your servers do not have to serve requests that the CDN fulfills

### Push CDNs

Push CDNs receive new content whenever changes occur on your server.  You take full responsibility for providing content, uploading directly to the CDN and rewriting URLs to point to the CDN.  You can configure when content expires and when it is updated.  Content is uploaded only when it is new or changed, minimizing traffic, but maximizing storage.

Sites with a small amount of traffic or sites with content that isn't often updated work well with push CDNs.  Content is placed on the CDNs once, instead of being re-pulled at regular intervals.

### Pull CDNs

Pull CDNs grab new content from your server when the first user requests the content.  You leave the content on your server and rewrite URLs to point to the CDN.  This results in a slower request until the content is cached on the CDN.

A [time-to-live (TTL)](https://en.wikipedia.org/wiki/Time_to_live) determines how long content is cached.  Pull CDNs minimize storage space on the CDN, but can create redundant traffic if files expire and are pulled before they have actually changed.

Sites with heavy traffic work well with pull CDNs, as traffic is spread out more evenly with only recently-requested content remaining on the CDN.

### Disadvantage(s): CDN

* CDN costs could be significant depending on traffic, although this should be weighed with additional costs you would incur not using a CDN.
* Content might be stale if it is updated before the TTL expires it.
* CDNs require changing URLs for static content to point to the CDN.

### Source(s) and further reading

* [Globally distributed content delivery](https://figshare.com/articles/Globally_distributed_content_delivery/6605972)
* [The differences between push and pull CDNs](http://www.travelblogadvice.com/technical/the-differences-between-push-and-pull-cdns/)
* [Wikipedia](https://en.wikipedia.org/wiki/Content_delivery_network)

## Load balancer

<p align="center">
  <img src="http://i.imgur.com/h81n9iK.png"/>
  <br/>
  <i><a href=http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html>Source: Scalable system design patterns</a></i>
</p>

Load balancers distribute incoming client requests to computing resources such as application servers and databases.  In each case, the load balancer returns the response from the computing resource to the appropriate client.  Load balancers are effective at:

* Preventing requests from going to unhealthy servers
* Preventing overloading resources
* Helping eliminate single points of failure

Load balancers can be implemented with hardware (expensive) or with software such as HAProxy.

Additional benefits include:

* **SSL termination** - Decrypt incoming requests and encrypt server responses so backend servers do not have to perform these potentially expensive operations
    * Removes the need to install [X.509 certificates](https://en.wikipedia.org/wiki/X.509) on each server
* **Session persistence** - Issue cookies and route a specific client's requests to same instance if the web apps do not keep track of sessions

To protect against failures, it's common to set up multiple load balancers, either in [active-passive](#active-passive) or [active-active](#active-active) mode.

Load balancers can route traffic based on various metrics, including:

* Random
* Least loaded
* Session/cookies
* [Round robin or weighted round robin](https://www.g33kinfo.com/info/round-robin-vs-weighted-round-robin-lb)
* [Layer 4](#layer-4-load-balancing)
* [Layer 7](#layer-7-load-balancing)

### Layer 4 load balancing

Layer 4 load balancers look at info at the [transport layer](#communication) to decide how to distribute requests.  Generally, this involves the source, destination IP addresses, and ports in the header, but not the contents of the packet.  Layer 4 load balancers forward network packets to and from the upstream server, performing [Network Address Translation (NAT)](https://www.nginx.com/resources/glossary/layer-4-load-balancing/).

### Layer 7 load balancing

Layer 7 load balancers look at the [application layer](#communication) to decide how to distribute requests.  This can involve contents of the header, message, and cookies.  Layer 7 load balancers terminates network traffic, reads the message, makes a load-balancing decision, then opens a connection to the selected server.  For example, a layer 7 load balancer can direct video traffic to servers that host videos while directing more sensitive user billing traffic to security-hardened servers.

At the cost of flexibility, layer 4 load balancing requires less time and computing resources than Layer 7, although the performance impact can be minimal on modern commodity hardware.

### Horizontal scaling

Load balancers can also help with horizontal scaling, improving performance and availability.  Scaling out using commodity machines is more cost efficient and results in higher availability than scaling up a single server on more expensive hardware, called **Vertical Scaling**.  It is also easier to hire for talent working on commodity hardware than it is for specialized enterprise systems.

#### Disadvantage(s): horizontal scaling

* Scaling horizontally introduces complexity and involves cloning servers
    * Servers should be stateless: they should not contain any user-related data like sessions or profile pictures
    * Sessions can be stored in a centralized data store such as a [database](#database) (SQL, NoSQL) or a persistent [cache](#cache) (Redis, Memcached)
* Downstream servers such as caches and databases need to handle more simultaneous connections as upstream servers scale out

### Disadvantage(s): load balancer

* The load balancer can become a performance bottleneck if it does not have enough resources or if it is not configured properly.
* Introducing a load balancer to help eliminate single points of failure results in increased complexity.
* A single load balancer is a single point of failure, configuring multiple load balancers further increases complexity.

### Source(s) and further reading

* [NGINX architecture](https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/)
* [HAProxy architecture guide](http://www.haproxy.org/download/1.2/doc/architecture.txt)
* [Scalability](http://www.lecloud.net/post/7295452622/scalability-for-dummies-part-1-clones)
* [Wikipedia](https://en.wikipedia.org/wiki/Load_balancing_(computing))
* [Layer 4 load balancing](https://www.nginx.com/resources/glossary/layer-4-load-balancing/)
* [Layer 7 load balancing](https://www.nginx.com/resources/glossary/layer-7-load-balancing/)
* [ELB listener config](http://docs.aws.amazon.com/elasticloadbalancing/latest/classic/elb-listener-config.html)

## Reverse proxy (web server)

<p align="center">
  <img src="http://i.imgur.com/n41Azff.png"/>
  <br/>
  <i><a href=https://upload.wikimedia.org/wikipedia/commons/6/67/Reverse_proxy_h2g2bob.svg>Source: Wikipedia</a></i>
  <br/>
</p>

A reverse proxy is a web server that centralizes internal services and provides unified interfaces to the public.  Requests from clients are forwarded to a server that can fulfill it before the reverse proxy returns the server's response to the client.

Additional benefits include:

* **Increased security** - Hide information about backend servers, blacklist IPs, limit number of connections per client
* **Increased scalability and flexibility** - Clients only see the reverse proxy's IP, allowing you to scale servers or change their configuration
* **SSL termination** - Decrypt incoming requests and encrypt server responses so backend servers do not have to perform these potentially expensive operations
    * Removes the need to install [X.509 certificates](https://en.wikipedia.org/wiki/X.509) on each server
* **Compression** - Compress server responses
* **Caching** - Return the response for cached requests
* **Static content** - Serve static content directly
    * HTML/CSS/JS
    * Photos
    * Videos
    * Etc

### Load balancer vs reverse proxy

* Deploying a load balancer is useful when you have multiple servers.  Often, load balancers  route traffic to a set of servers serving the same function.
* Reverse proxies can be useful even with just one web server or application server, opening up the benefits described in the previous section.
* Solutions such as NGINX and HAProxy can support both layer 7 reverse proxying and load balancing.

### Disadvantage(s): reverse proxy

* Introducing a reverse proxy results in increased complexity.
* A single reverse proxy is a single point of failure, configuring multiple reverse proxies (ie a [failover](https://en.wikipedia.org/wiki/Failover)) further increases complexity.

### Source(s) and further reading

* [Reverse proxy vs load balancer](https://www.nginx.com/resources/glossary/reverse-proxy-vs-load-balancer/)
* [NGINX architecture](https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/)
* [HAProxy architecture guide](http://www.haproxy.org/download/1.2/doc/architecture.txt)
* [Wikipedia](https://en.wikipedia.org/wiki/Reverse_proxy)

## Application layer

<p align="center">
  <img src="http://i.imgur.com/yB5SYwm.png"/>
  <br/>
  <i><a href=http://lethain.com/introduction-to-architecting-systems-for-scale/#platform_layer>Source: Intro to architecting systems for scale</a></i>
</p>

Separating out the web layer from the application layer (also known as platform layer) allows you to scale and configure both layers independently.  Adding a new API results in adding application servers without necessarily adding additional web servers.  The **single responsibility principle** advocates for small and autonomous services that work together.  Small teams with small services can plan more aggressively for rapid growth.

Workers in the application layer also help enable [asynchronism](#asynchronism).

### Microservices

Related to this discussion are [microservices](https://en.wikipedia.org/wiki/Microservices), which can be described as a suite of independently deployable, small, modular services.  Each service runs a unique process and communicates through a well-defined, lightweight mechanism to serve a business goal. <sup><a href=https://smartbear.com/learn/api-design/what-are-microservices>1</a></sup>

Pinterest, for example, could have the following microservices: user profile, follower, feed, search, photo upload, etc.

### Service Discovery

Systems such as [Consul](https://www.consul.io/docs/index.html), [Etcd](https://coreos.com/etcd/docs/latest), and [Zookeeper](http://www.slideshare.net/sauravhaloi/introduction-to-apache-zookeeper) can help services find each other by keeping track of registered names, addresses, and ports.  [Health checks](https://www.consul.io/intro/getting-started/checks.html) help verify service integrity and are often done using an [HTTP](#hypertext-transfer-protocol-http) endpoint.  Both Consul and Etcd have a built in [key-value store](#key-value-store) that can be useful for storing config values and other shared data.

### Disadvantage(s): application layer

* Adding an application layer with loosely coupled services requires a different approach from an architectural, operations, and process viewpoint (vs a monolithic system).
* Microservices can add complexity in terms of deployments and operations.

### Source(s) and further reading

* [Intro to architecting systems for scale](http://lethain.com/introduction-to-architecting-systems-for-scale)
* [Crack the system design interview](http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview)
* [Service oriented architecture](https://en.wikipedia.org/wiki/Service-oriented_architecture)
* [Introduction to Zookeeper](http://www.slideshare.net/sauravhaloi/introduction-to-apache-zookeeper)
* [Here's what you need to know about building microservices](https://cloudncode.wordpress.com/2016/07/22/msa-getting-started/)

## Database

<p align="center">
  <img src="http://i.imgur.com/Xkm5CXz.png"/>
  <br/>
  <i><a href=https://www.youtube.com/watch?v=w95murBkYmU>Source: Scaling up to your first 10 million users</a></i>
</p>

### Relational database management system (RDBMS)

A relational database like SQL is a collection of data items organized in tables.

**ACID** is a set of properties of relational database [transactions](https://en.wikipedia.org/wiki/Database_transaction).

* **Atomicity** - Each transaction is all or nothing
* **Consistency** - Any transaction will bring the database from one valid state to another
* **Isolation** - Executing transactions concurrently has the same results as if the transactions were executed serially
* **Durability** - Once a transaction has been committed, it will remain so

There are many techniques to scale a relational database: **master-slave replication**, **master-master replication**, **federation**, **sharding**, **denormalization**, and **SQL tuning**.

#### Master-slave replication

The master serves reads and writes, replicating writes to one or more slaves, which serve only reads.  Slaves can also replicate to additional slaves in a tree-like fashion.  If the master goes offline, the system can continue to operate in read-only mode until a slave is promoted to a master or a new master is provisioned.

<p align="center">
  <img src="http://i.imgur.com/C9ioGtn.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>Source: Scalability, availability, stability, patterns</a></i>
</p>

##### Disadvantage(s): master-slave replication

* Additional logic is needed to promote a slave to a master.
* See [Disadvantage(s): replication](#disadvantages-replication) for points related to **both** master-slave and master-master.

#### Master-master replication

Both masters serve reads and writes and coordinate with each other on writes.  If either master goes down, the system can continue to operate with both reads and writes.

<p align="center">
  <img src="http://i.imgur.com/krAHLGg.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>Source: Scalability, availability, stability, patterns</a></i>
</p>

##### Disadvantage(s): master-master replication

* You'll need a load balancer or you'll need to make changes to your application logic to determine where to write.
* Most master-master systems are either loosely consistent (violating ACID) or have increased write latency due to synchronization.
* Conflict resolution comes more into play as more write nodes are added and as latency increases.
* See [Disadvantage(s): replication](#disadvantages-replication) for points related to **both** master-slave and master-master.

##### Disadvantage(s): replication

* There is a potential for loss of data if the master fails before any newly written data can be replicated to other nodes.
* Writes are replayed to the read replicas.  If there are a lot of writes, the read replicas can get bogged down with replaying writes and can't do as many reads.
* The more read slaves, the more you have to replicate, which leads to greater replication lag.
* On some systems, writing to the master can spawn multiple threads to write in parallel, whereas read replicas only support writing sequentially with a single thread.
* Replication adds more hardware and additional complexity.

##### Source(s) and further reading: replication

* [Scalability, availability, stability, patterns](http://www.slideshare.net/jboner/scalability-availability-stability-patterns/)
* [Multi-master replication](https://en.wikipedia.org/wiki/Multi-master_replication)

#### Federation

<p align="center">
  <img src="http://i.imgur.com/U3qV33e.png"/>
  <br/>
  <i><a href=https://www.youtube.com/watch?v=w95murBkYmU>Source: Scaling up to your first 10 million users</a></i>
</p>

Federation (or functional partitioning) splits up databases by function.  For example, instead of a single, monolithic database, you could have three databases: **forums**, **users**, and **products**, resulting in less read and write traffic to each database and therefore less replication lag.  Smaller databases result in more data that can fit in memory, which in turn results in more cache hits due to improved cache locality.  With no single central master serializing writes you can write in parallel, increasing throughput.

##### Disadvantage(s): federation

* Federation is not effective if your schema requires huge functions or tables.
* You'll need to update your application logic to determine which database to read and write.
* Joining data from two databases is more complex with a [server link](http://stackoverflow.com/questions/5145637/querying-data-by-joining-two-tables-in-two-database-on-different-servers).
* Federation adds more hardware and additional complexity.

##### Source(s) and further reading: federation

* [Scaling up to your first 10 million users](https://www.youtube.com/watch?v=w95murBkYmU)

#### Sharding

<p align="center">
  <img src="http://i.imgur.com/wU8x5Id.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>Source: Scalability, availability, stability, patterns</a></i>
</p>

Sharding distributes data across different databases such that each database can only manage a subset of the data.  Taking a users database as an example, as the number of users increases, more shards are added to the cluster.

Similar to the advantages of [federation](#federation), sharding results in less read and write traffic, less replication, and more cache hits.  Index size is also reduced, which generally improves performance with faster queries.  If one shard goes down, the other shards are still operational, although you'll want to add some form of replication to avoid data loss.  Like federation, there is no single central master serializing writes, allowing you to write in parallel with increased throughput.

Common ways to shard a table of users is either through the user's last name initial or the user's geographic location.

##### Disadvantage(s): sharding

* You'll need to update your application logic to work with shards, which could result in complex SQL queries.
* Data distribution can become lopsided in a shard.  For example, a set of power users on a shard could result in increased load to that shard compared to others.
    * Rebalancing adds additional complexity.  A sharding function based on [consistent hashing](http://www.paperplanes.de/2011/12/9/the-magic-of-consistent-hashing.html) can reduce the amount of transferred data.
* Joining data from multiple shards is more complex.
* Sharding adds more hardware and additional complexity.

##### Source(s) and further reading: sharding

* [The coming of the shard](http://highscalability.com/blog/2009/8/6/an-unorthodox-approach-to-database-design-the-coming-of-the.html)
* [Shard database architecture](https://en.wikipedia.org/wiki/Shard_(database_architecture))
* [Consistent hashing](http://www.paperplanes.de/2011/12/9/the-magic-of-consistent-hashing.html)

#### Denormalization

Denormalization attempts to improve read performance at the expense of some write performance.  Redundant copies of the data are written in multiple tables to avoid expensive joins.  Some RDBMS such as [PostgreSQL](https://en.wikipedia.org/wiki/PostgreSQL) and Oracle support [materialized views](https://en.wikipedia.org/wiki/Materialized_view) which handle the work of storing redundant information and keeping redundant copies consistent.

Once data becomes distributed with techniques such as [federation](#federation) and [sharding](#sharding), managing joins across data centers further increases complexity.  Denormalization might circumvent the need for such complex joins.

In most systems, reads can heavily outnumber writes 100:1 or even 1000:1.  A read resulting in a complex database join can be very expensive, spending a significant amount of time on disk operations.

##### Disadvantage(s): denormalization

* Data is duplicated.
* Constraints can help redundant copies of information stay in sync, which increases complexity of the database design.
* A denormalized database under heavy write load might perform worse than its normalized counterpart.

###### Source(s) and further reading: denormalization

* [Denormalization](https://en.wikipedia.org/wiki/Denormalization)

#### SQL tuning

SQL tuning is a broad topic and many [books](https://www.amazon.com/s/ref=nb_sb_noss_2?url=search-alias%3Daps&field-keywords=sql+tuning) have been written as reference.

It's important to **benchmark** and **profile** to simulate and uncover bottlenecks.

* **Benchmark** - Simulate high-load situations with tools such as [ab](http://httpd.apache.org/docs/2.2/programs/ab.html).
* **Profile** - Enable tools such as the [slow query log](http://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html) to help track performance issues.

Benchmarking and profiling might point you to the following optimizations.

##### Tighten up the schema

* MySQL dumps to disk in contiguous blocks for fast access.
* Use `CHAR` instead of `VARCHAR` for fixed-length fields.
    * `CHAR` effectively allows for fast, random access, whereas with `VARCHAR`, you must find the end of a string before moving onto the next one.
* Use `TEXT` for large blocks of text such as blog posts.  `TEXT` also allows for boolean searches.  Using a `TEXT` field results in storing a pointer on disk that is used to locate the text block.
* Use `INT` for larger numbers up to 2^32 or 4 billion.
* Use `DECIMAL` for currency to avoid floating point representation errors.
* Avoid storing large `BLOBS`, store the location of where to get the object instead.
* `VARCHAR(255)` is the largest number of characters that can be counted in an 8 bit number, often maximizing the use of a byte in some RDBMS.
* Set the `NOT NULL` constraint where applicable to [improve search performance](http://stackoverflow.com/questions/1017239/how-do-null-values-affect-performance-in-a-database-search).

##### Use good indices

* Columns that you are querying (`SELECT`, `GROUP BY`, `ORDER BY`, `JOIN`) could be faster with indices.
* Indices are usually represented as self-balancing [B-tree](https://en.wikipedia.org/wiki/B-tree) that keeps data sorted and allows searches, sequential access, insertions, and deletions in logarithmic time.
* Placing an index can keep the data in memory, requiring more space.
* Writes could also be slower since the index also needs to be updated.
* When loading large amounts of data, it might be faster to disable indices, load the data, then rebuild the indices.

##### Avoid expensive joins

* [Denormalize](#denormalization) where performance demands it.

##### Partition tables

* Break up a table by putting hot spots in a separate table to help keep it in memory.

##### Tune the query cache

* In some cases, the [query cache](https://dev.mysql.com/doc/refman/5.7/en/query-cache.html) could lead to [performance issues](https://www.percona.com/blog/2016/10/12/mysql-5-7-performance-tuning-immediately-after-installation/).

##### Source(s) and further reading: SQL tuning

* [Tips for optimizing MySQL queries](http://aiddroid.com/10-tips-optimizing-mysql-queries-dont-suck/)
* [Is there a good reason i see VARCHAR(255) used so often?](http://stackoverflow.com/questions/1217466/is-there-a-good-reason-i-see-varchar255-used-so-often-as-opposed-to-another-l)
* [How do null values affect performance?](http://stackoverflow.com/questions/1017239/how-do-null-values-affect-performance-in-a-database-search)
* [Slow query log](http://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html)

### NoSQL

NoSQL is a collection of data items represented in a **key-value store**, **document store**, **wide column store**, or a **graph database**.  Data is denormalized, and joins are generally done in the application code.  Most NoSQL stores lack true ACID transactions and favor [eventual consistency](#eventual-consistency).

**BASE** is often used to describe the properties of NoSQL databases.  In comparison with the [CAP Theorem](#cap-theorem), BASE chooses availability over consistency.

* **Basically available** - the system guarantees availability.
* **Soft state** - the state of the system may change over time, even without input.
* **Eventual consistency** - the system will become consistent over a period of time, given that the system doesn't receive input during that period.

In addition to choosing between [SQL or NoSQL](#sql-or-nosql), it is helpful to understand which type of NoSQL database best fits your use case(s).  We'll review **key-value stores**, **document stores**, **wide column stores**, and **graph databases** in the next section.

#### Key-value store

> Abstraction: hash table

A key-value store generally allows for O(1) reads and writes and is often backed by memory or SSD.  Data stores can maintain keys in [lexicographic order](https://en.wikipedia.org/wiki/Lexicographical_order), allowing efficient retrieval of key ranges.  Key-value stores can allow for storing of metadata with a value.

Key-value stores provide high performance and are often used for simple data models or for rapidly-changing data, such as an in-memory cache layer.  Since they offer only a limited set of operations, complexity is shifted to the application layer if additional operations are needed.

A key-value store is the basis for more complex systems such as a document store, and in some cases, a graph database.

##### Source(s) and further reading: key-value store

* [Key-value database](https://en.wikipedia.org/wiki/Key-value_database)
* [Disadvantages of key-value stores](http://stackoverflow.com/questions/4056093/what-are-the-disadvantages-of-using-a-key-value-table-over-nullable-columns-or)
* [Redis architecture](http://qnimate.com/overview-of-redis-architecture/)
* [Memcached architecture](https://www.adayinthelifeof.nl/2011/02/06/memcache-internals/)

#### Document store

> Abstraction: key-value store with documents stored as values

A document store is centered around documents (XML, JSON, binary, etc), where a document stores all information for a given object.  Document stores provide APIs or a query language to query based on the internal structure of the document itself.  *Note, many key-value stores include features for working with a value's metadata, blurring the lines between these two storage types.*

Based on the underlying implementation, documents are organized by collections, tags, metadata, or directories.  Although documents can be organized or grouped together, documents may have fields that are completely different from each other.

Some document stores like [MongoDB](https://www.mongodb.com/mongodb-architecture) and [CouchDB](https://blog.couchdb.org/2016/08/01/couchdb-2-0-architecture/) also provide a SQL-like language to perform complex queries.  [DynamoDB](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/decandia07dynamo.pdf) supports both key-values and documents.

Document stores provide high flexibility and are often used for working with occasionally changing data.

##### Source(s) and further reading: document store

* [Document-oriented database](https://en.wikipedia.org/wiki/Document-oriented_database)
* [MongoDB architecture](https://www.mongodb.com/mongodb-architecture)
* [CouchDB architecture](https://blog.couchdb.org/2016/08/01/couchdb-2-0-architecture/)
* [Elasticsearch architecture](https://www.elastic.co/blog/found-elasticsearch-from-the-bottom-up)

#### Wide column store

<p align="center">
  <img src="http://i.imgur.com/n16iOGk.png"/>
  <br/>
  <i><a href=http://blog.grio.com/2015/11/sql-nosql-a-brief-history.html>Source: SQL & NoSQL, a brief history</a></i>
</p>

> Abstraction: nested map `ColumnFamily<RowKey, Columns<ColKey, Value, Timestamp>>`

A wide column store's basic unit of data is a column (name/value pair).  A column can be grouped in column families (analogous to a SQL table).  Super column families further group column families.  You can access each column independently with a row key, and columns with the same row key form a row.  Each value contains a timestamp for versioning and for conflict resolution.

Google introduced [Bigtable](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/chang06bigtable.pdf) as the first wide column store, which influenced the open-source [HBase](https://www.mapr.com/blog/in-depth-look-hbase-architecture) often-used in the Hadoop ecosystem, and [Cassandra](http://docs.datastax.com/en/cassandra/3.0/cassandra/architecture/archIntro.html) from Facebook.  Stores such as BigTable, HBase, and Cassandra maintain keys in lexicographic order, allowing efficient retrieval of selective key ranges.

Wide column stores offer high availability and high scalability.  They are often used for very large data sets.

##### Source(s) and further reading: wide column store

* [SQL & NoSQL, a brief history](http://blog.grio.com/2015/11/sql-nosql-a-brief-history.html)
* [Bigtable architecture](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/chang06bigtable.pdf)
* [HBase architecture](https://www.mapr.com/blog/in-depth-look-hbase-architecture)
* [Cassandra architecture](http://docs.datastax.com/en/cassandra/3.0/cassandra/architecture/archIntro.html)

#### Graph database

<p align="center">
  <img src="http://i.imgur.com/fNcl65g.png"/>
  <br/>
  <i><a href=https://en.wikipedia.org/wiki/File:GraphDatabase_PropertyGraph.png>Source: Graph database</a></i>
</p>

> Abstraction: graph

In a graph database, each node is a record and each arc is a relationship between two nodes.  Graph databases are optimized to represent complex relationships with many foreign keys or many-to-many relationships.

Graphs databases offer high performance for data models with complex relationships, such as a social network.  They are relatively new and are not yet widely-used; it might be more difficult to find development tools and resources.  Many graphs can only be accessed with [REST APIs](#representational-state-transfer-rest).

##### Source(s) and further reading: graph

* [Graph database](https://en.wikipedia.org/wiki/Graph_database)
* [Neo4j](https://neo4j.com/)
* [FlockDB](https://blog.twitter.com/2010/introducing-flockdb)

#### Source(s) and further reading: NoSQL

* [Explanation of base terminology](http://stackoverflow.com/questions/3342497/explanation-of-base-terminology)
* [NoSQL databases a survey and decision guidance](https://medium.com/baqend-blog/nosql-databases-a-survey-and-decision-guidance-ea7823a822d#.wskogqenq)
* [Scalability](http://www.lecloud.net/post/7994751381/scalability-for-dummies-part-2-database)
* [Introduction to NoSQL](https://www.youtube.com/watch?v=qI_g07C_Q5I)
* [NoSQL patterns](http://horicky.blogspot.com/2009/11/nosql-patterns.html)

### SQL or NoSQL

<p align="center">
  <img src="http://i.imgur.com/wXGqG5f.png"/>
  <br/>
  <i><a href=https://www.infoq.com/articles/Transition-RDBMS-NoSQL/>Source: Transitioning from RDBMS to NoSQL</a></i>
</p>

Reasons for **SQL**:

* Structured data
* Strict schema
* Relational data
* Need for complex joins
* Transactions
* Clear patterns for scaling
* More established: developers, community, code, tools, etc
* Lookups by index are very fast

Reasons for **NoSQL**:

* Semi-structured data
* Dynamic or flexible schema
* Non-relational data
* No need for complex joins
* Store many TB (or PB) of data
* Very data intensive workload
* Very high throughput for IOPS

Sample data well-suited for NoSQL:

* Rapid ingest of clickstream and log data
* Leaderboard or scoring data
* Temporary data, such as a shopping cart
* Frequently accessed ('hot') tables
* Metadata/lookup tables

##### Source(s) and further reading: SQL or NoSQL

* [Scaling up to your first 10 million users](https://www.youtube.com/watch?v=w95murBkYmU)
* [SQL vs NoSQL differences](https://www.sitepoint.com/sql-vs-nosql-differences/)

## Cache

<p align="center">
  <img src="http://i.imgur.com/Q6z24La.png"/>
  <br/>
  <i><a href=http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html>Source: Scalable system design patterns</a></i>
</p>

Caching improves page load times and can reduce the load on your servers and databases.  In this model, the dispatcher will first lookup if the request has been made before and try to find the previous result to return, in order to save the actual execution.

Databases often benefit from a uniform distribution of reads and writes across its partitions.  Popular items can skew the distribution, causing bottlenecks.  Putting a cache in front of a database can help absorb uneven loads and spikes in traffic.

### Client caching

Caches can be located on the client side (OS or browser), [server side](#reverse-proxy-web-server), or in a distinct cache layer.

### CDN caching

[CDNs](#content-delivery-network) are considered a type of cache.

### Web server caching

[Reverse proxies](#reverse-proxy-web-server) and caches such as [Varnish](https://www.varnish-cache.org/) can serve static and dynamic content directly.  Web servers can also cache requests, returning responses without having to contact application servers.

### Database caching

Your database usually includes some level of caching in a default configuration, optimized for a generic use case.  Tweaking these settings for specific usage patterns can further boost performance.

### Application caching

In-memory caches such as Memcached and Redis are key-value stores between your application and your data storage.  Since the data is held in RAM, it is much faster than typical databases where data is stored on disk.  RAM is more limited than disk, so [cache invalidation](https://en.wikipedia.org/wiki/Cache_algorithms) algorithms such as [least recently used (LRU)](https://en.wikipedia.org/wiki/Cache_algorithms#Least_Recently_Used) can help invalidate 'cold' entries and keep 'hot' data in RAM.

Redis has the following additional features:

* Persistence option
* Built-in data structures such as sorted sets and lists

There are multiple levels you can cache that fall into two general categories: **database queries** and **objects**:

* Row level
* Query-level
* Fully-formed serializable objects
* Fully-rendered HTML

Generally, you should try to avoid file-based caching, as it makes cloning and auto-scaling more difficult.

### Caching at the database query level

Whenever you query the database, hash the query as a key and store the result to the cache.  This approach suffers from expiration issues:

* Hard to delete a cached result with complex queries
* If one piece of data changes such as a table cell, you need to delete all cached queries that might include the changed cell

### Caching at the object level

See your data as an object, similar to what you do with your application code.  Have your application assemble the dataset from the database into a class instance or a data structure(s):

* Remove the object from cache if its underlying data has changed
* Allows for asynchronous processing: workers assemble objects by consuming the latest cached object

Suggestions of what to cache:

* User sessions
* Fully rendered web pages
* Activity streams
* User graph data

### When to update the cache

Since you can only store a limited amount of data in cache, you'll need to determine which cache update strategy works best for your use case.

#### Cache-aside

<p align="center">
  <img src="http://i.imgur.com/ONjORqk.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/tmatyashovsky/from-cache-to-in-memory-data-grid-introduction-to-hazelcast>Source: From cache to in-memory data grid</a></i>
</p>

The application is responsible for reading and writing from storage.  The cache does not interact with storage directly.  The application does the following:

* Look for entry in cache, resulting in a cache miss
* Load entry from the database
* Add entry to cache
* Return entry

```python
def get_user(self, user_id):
    user = cache.get("user.{0}", user_id)
    if user is None:
        user = db.query("SELECT * FROM users WHERE user_id = {0}", user_id)
        if user is not None:
            key = "user.{0}".format(user_id)
            cache.set(key, json.dumps(user))
    return user
```

[Memcached](https://memcached.org/) is generally used in this manner.

Subsequent reads of data added to cache are fast.  Cache-aside is also referred to as lazy loading.  Only requested data is cached, which avoids filling up the cache with data that isn't requested.

##### Disadvantage(s): cache-aside

* Each cache miss results in three trips, which can cause a noticeable delay.
* Data can become stale if it is updated in the database.  This issue is mitigated by setting a time-to-live (TTL) which forces an update of the cache entry, or by using write-through.
* When a node fails, it is replaced by a new, empty node, increasing latency.

#### Write-through

<p align="center">
  <img src="http://i.imgur.com/0vBc0hN.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>Source: Scalability, availability, stability, patterns</a></i>
</p>

The application uses the cache as the main data store, reading and writing data to it, while the cache is responsible for reading and writing to the database:

* Application adds/updates entry in cache
* Cache synchronously writes entry to data store
* Return

Application code:

```python
set_user(12345, {"foo":"bar"})
```

Cache code:

```python
def set_user(user_id, values):
    user = db.query("UPDATE Users WHERE id = {0}", user_id, values)
    cache.set(user_id, user)
```

Write-through is a slow overall operation due to the write operation, but subsequent reads of just written data are fast.  Users are generally more tolerant of latency when updating data than reading data.  Data in the cache is not stale.

##### Disadvantage(s): write through

* When a new node is created due to failure or scaling, the new node will not cache entries until the entry is updated in the database.  Cache-aside in conjunction with write through can mitigate this issue.
* Most data written might never be read, which can be minimized with a TTL.

#### Write-behind (write-back)

<p align="center">
  <img src="http://i.imgur.com/rgSrvjG.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/jboner/scalability-availability-stability-patterns/>Source: Scalability, availability, stability, patterns</a></i>
</p>

In write-behind, the application does the following:

* Add/update entry in cache
* Asynchronously write entry to the data store, improving write performance

##### Disadvantage(s): write-behind

* There could be data loss if the cache goes down prior to its contents hitting the data store.
* It is more complex to implement write-behind than it is to implement cache-aside or write-through.

#### Refresh-ahead

<p align="center">
  <img src="http://i.imgur.com/kxtjqgE.png"/>
  <br/>
  <i><a href=http://www.slideshare.net/tmatyashovsky/from-cache-to-in-memory-data-grid-introduction-to-hazelcast>Source: From cache to in-memory data grid</a></i>
</p>

You can configure the cache to automatically refresh any recently accessed cache entry prior to its expiration.

Refresh-ahead can result in reduced latency vs read-through if the cache can accurately predict which items are likely to be needed in the future.

##### Disadvantage(s): refresh-ahead

* Not accurately predicting which items are likely to be needed in the future can result in reduced performance than without refresh-ahead.

### Disadvantage(s): cache

* Need to maintain consistency between caches and the source of truth such as the database through [cache invalidation](https://en.wikipedia.org/wiki/Cache_algorithms).
* Cache invalidation is a difficult problem, there is additional complexity associated with when to update the cache.
* Need to make application changes such as adding Redis or memcached.

### Source(s) and further reading

* [From cache to in-memory data grid](http://www.slideshare.net/tmatyashovsky/from-cache-to-in-memory-data-grid-introduction-to-hazelcast)
* [Scalable system design patterns](http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html)
* [Introduction to architecting systems for scale](http://lethain.com/introduction-to-architecting-systems-for-scale/)
* [Scalability, availability, stability, patterns](http://www.slideshare.net/jboner/scalability-availability-stability-patterns/)
* [Scalability](http://www.lecloud.net/post/9246290032/scalability-for-dummies-part-3-cache)
* [AWS ElastiCache strategies](http://docs.aws.amazon.com/AmazonElastiCache/latest/UserGuide/Strategies.html)
* [Wikipedia](https://en.wikipedia.org/wiki/Cache_(computing))

## Asynchronism

<p align="center">
  <img src="http://i.imgur.com/54GYsSx.png"/>
  <br/>
  <i><a href=http://lethain.com/introduction-to-architecting-systems-for-scale/#platform_layer>Source: Intro to architecting systems for scale</a></i>
</p>

Asynchronous workflows help reduce request times for expensive operations that would otherwise be performed in-line.  They can also help by doing time-consuming work in advance, such as periodic aggregation of data.

### Message queues

Message queues receive, hold, and deliver messages.  If an operation is too slow to perform inline, you can use a message queue with the following workflow:

* An application publishes a job to the queue, then notifies the user of job status
* A worker picks up the job from the queue, processes it, then signals the job is complete

The user is not blocked and the job is processed in the background.  During this time, the client might optionally do a small amount of processing to make it seem like the task has completed.  For example, if posting a tweet, the tweet could be instantly posted to your timeline, but it could take some time before your tweet is actually delivered to all of your followers.

**[Redis](https://redis.io/)** is useful as a simple message broker but messages can be lost.

**[RabbitMQ](https://www.rabbitmq.com/)** is popular but requires you to adapt to the 'AMQP' protocol and manage your own nodes.

**[Amazon SQS](https://aws.amazon.com/sqs/)** is hosted but can have high latency and has the possibility of messages being delivered twice.

### Task queues

Tasks queues receive tasks and their related data, runs them, then delivers their results.  They can support scheduling and can be used to run computationally-intensive jobs in the background.

**Celery** has support for scheduling and primarily has python support.

### Back pressure

If queues start to grow significantly, the queue size can become larger than memory, resulting in cache misses, disk reads, and even slower performance.  [Back pressure](http://mechanical-sympathy.blogspot.com/2012/05/apply-back-pressure-when-overloaded.html) can help by limiting the queue size, thereby maintaining a high throughput rate and good response times for jobs already in the queue.  Once the queue fills up, clients get a server busy or HTTP 503 status code to try again later.  Clients can retry the request at a later time, perhaps with [exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff).

### Disadvantage(s): asynchronism

* Use cases such as inexpensive calculations and realtime workflows might be better suited for synchronous operations, as introducing queues can add delays and complexity.

### Source(s) and further reading

* [It's all a numbers game](https://www.youtube.com/watch?v=1KRYH75wgy4)
* [Applying back pressure when overloaded](http://mechanical-sympathy.blogspot.com/2012/05/apply-back-pressure-when-overloaded.html)
* [Little's law](https://en.wikipedia.org/wiki/Little%27s_law)
* [What is the difference between a message queue and a task queue?](https://www.quora.com/What-is-the-difference-between-a-message-queue-and-a-task-queue-Why-would-a-task-queue-require-a-message-broker-like-RabbitMQ-Redis-Celery-or-IronMQ-to-function)

## Communication

<p align="center">
  <img src="http://i.imgur.com/5KeocQs.jpg"/>
  <br/>
  <i><a href=http://www.escotal.com/osilayer.html>Source: OSI 7 layer model</a></i>
</p>

### Hypertext transfer protocol (HTTP)

HTTP is a method for encoding and transporting data between a client and a server.  It is a request/response protocol: clients issue requests and servers issue responses with relevant content and completion status info about the request.  HTTP is self-contained, allowing requests and responses to flow through many intermediate routers and servers that perform load balancing, caching, encryption, and compression.

A basic HTTP request consists of a verb (method) and a resource (endpoint).  Below are common HTTP verbs:

| Verb | Description | Idempotent* | Safe | Cacheable |
|---|---|---|---|---|
| GET | Reads a resource | Yes | Yes | Yes |
| POST | Creates a resource or trigger a process that handles data | No | No | Yes if response contains freshness info |
| PUT | Creates or replace a resource | Yes | No | No |
| PATCH | Partially updates a resource | No | No | Yes if response contains freshness info |
| DELETE | Deletes a resource | Yes | No | No |

*Can be called many times without different outcomes.

HTTP is an application layer protocol relying on lower-level protocols such as **TCP** and **UDP**.

#### Source(s) and further reading: HTTP

* [What is HTTP?](https://www.nginx.com/resources/glossary/http/)
* [Difference between HTTP and TCP](https://www.quora.com/What-is-the-difference-between-HTTP-protocol-and-TCP-protocol)
* [Difference between PUT and PATCH](https://laracasts.com/discuss/channels/general-discussion/whats-the-differences-between-put-and-patch?page=1)

### Transmission control protocol (TCP)

<p align="center">
  <img src="http://i.imgur.com/JdAsdvG.jpg"/>
  <br/>
  <i><a href=http://www.wildbunny.co.uk/blog/2012/10/09/how-to-make-a-multi-player-game-part-1/>Source: How to make a multiplayer game</a></i>
</p>

TCP is a connection-oriented protocol over an [IP network](https://en.wikipedia.org/wiki/Internet_Protocol).  Connection is established and terminated using a [handshake](https://en.wikipedia.org/wiki/Handshaking).  All packets sent are guaranteed to reach the destination in the original order and without corruption through:

* Sequence numbers and [checksum fields](https://en.wikipedia.org/wiki/Transmission_Control_Protocol#Checksum_computation) for each packet
* [Acknowledgement](https://en.wikipedia.org/wiki/Acknowledgement_(data_networks)) packets and automatic retransmission

If the sender does not receive a correct response, it will resend the packets.  If there are multiple timeouts, the connection is dropped.  TCP also implements [flow control](https://en.wikipedia.org/wiki/Flow_control_(data)) and [congestion control](https://en.wikipedia.org/wiki/Network_congestion#Congestion_control).  These guarantees cause delays and generally result in less efficient transmission than UDP.

To ensure high throughput, web servers can keep a large number of TCP connections open, resulting in high memory usage.  It can be expensive to have a large number of open connections between web server threads and say, a [memcached](https://memcached.org/) server.  [Connection pooling](https://en.wikipedia.org/wiki/Connection_pool) can help in addition to switching to UDP where applicable.

TCP is useful for applications that require high reliability but are less time critical.  Some examples include web servers, database info, SMTP, FTP, and SSH.

Use TCP over UDP when:

* You need all of the data to arrive intact
* You want to automatically make a best estimate use of the network throughput

### User datagram protocol (UDP)

<p align="center">
  <img src="http://i.imgur.com/yzDrJtA.jpg"/>
  <br/>
  <i><a href=http://www.wildbunny.co.uk/blog/2012/10/09/how-to-make-a-multi-player-game-part-1/>Source: How to make a multiplayer game</a></i>
</p>

UDP is connectionless.  Datagrams (analogous to packets) are guaranteed only at the datagram level.  Datagrams might reach their destination out of order or not at all.  UDP does not support congestion control.  Without the guarantees that TCP support, UDP is generally more efficient.

UDP can broadcast, sending datagrams to all devices on the subnet.  This is useful with [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol) because the client has not yet received an IP address, thus preventing a way for TCP to stream without the IP address.

UDP is less reliable but works well in real time use cases such as VoIP, video chat, streaming, and realtime multiplayer games.

Use UDP over TCP when:

* You need the lowest latency
* Late data is worse than loss of data
* You want to implement your own error correction

#### Source(s) and further reading: TCP and UDP

* [Networking for game programming](http://gafferongames.com/networking-for-game-programmers/udp-vs-tcp/)
* [Key differences between TCP and UDP protocols](http://www.cyberciti.biz/faq/key-differences-between-tcp-and-udp-protocols/)
* [Difference between TCP and UDP](http://stackoverflow.com/questions/5970383/difference-between-tcp-and-udp)
* [Transmission control protocol](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)
* [User datagram protocol](https://en.wikipedia.org/wiki/User_Datagram_Protocol)
* [Scaling memcache at Facebook](http://www.cs.bu.edu/~jappavoo/jappavoo.github.com/451/papers/memcache-fb.pdf)

### Remote procedure call (RPC)

<p align="center">
  <img src="http://i.imgur.com/iF4Mkb5.png"/>
  <br/>
  <i><a href=http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview>Source: Crack the system design interview</a></i>
</p>

In an RPC, a client causes a procedure to execute on a different address space, usually a remote server.  The procedure is coded as if it were a local procedure call, abstracting away the details of how to communicate with the server from the client program.  Remote calls are usually slower and less reliable than local calls so it is helpful to distinguish RPC calls from local calls.  Popular RPC frameworks include [Protobuf](https://developers.google.com/protocol-buffers/), [Thrift](https://thrift.apache.org/), and [Avro](https://avro.apache.org/docs/current/).

RPC is a request-response protocol:

* **Client program** - Calls the client stub procedure.  The parameters are pushed onto the stack like a local procedure call.
* **Client stub procedure** - Marshals (packs) procedure id and arguments into a request message.
* **Client communication module** - OS sends the message from the client to the server.
* **Server communication module** - OS passes the incoming packets to the server stub procedure.
* **Server stub procedure** -  Unmarshalls the results, calls the server procedure matching the procedure id and passes the given arguments.
* The server response repeats the steps above in reverse order.

Sample RPC calls:

```
GET /someoperation?data=anId

POST /anotheroperation
{
  "data":"anId";
  "anotherdata": "another value"
}
```

RPC is focused on exposing behaviors.  RPCs are often used for performance reasons with internal communications, as you can hand-craft native calls to better fit your use cases.

Choose a native library (aka SDK) when:

* You know your target platform.
* You want to control how your "logic" is accessed.
* You want to control how error control happens off your library.
* Performance and end user experience is your primary concern.

HTTP APIs following **REST** tend to be used more often for public APIs.

#### Disadvantage(s): RPC

* RPC clients become tightly coupled to the service implementation.
* A new API must be defined for every new operation or use case.
* It can be difficult to debug RPC.
* You might not be able to leverage existing technologies out of the box.  For example, it might require additional effort to ensure [RPC calls are properly cached](http://etherealbits.com/2012/12/debunking-the-myths-of-rpc-rest/) on caching servers such as [Squid](http://www.squid-cache.org/).

### Representational state transfer (REST)

REST is an architectural style enforcing a client/server model where the client acts on a set of resources managed by the server.  The server provides a representation of resources and actions that can either manipulate or get a new representation of resources.  All communication must be stateless and cacheable.

There are four qualities of a RESTful interface:

* **Identify resources (URI in HTTP)** - use the same URI regardless of any operation.
* **Change with representations (Verbs in HTTP)** - use verbs, headers, and body.
* **Self-descriptive error message (status response in HTTP)** - Use status codes, don't reinvent the wheel.
* **[HATEOAS](http://restcookbook.com/Basics/hateoas/) (HTML interface for HTTP)** - your web service should be fully accessible in a browser.

Sample REST calls:

```
GET /someresources/anId

PUT /someresources/anId
{"anotherdata": "another value"}
```

REST is focused on exposing data.  It minimizes the coupling between client/server and is often used for public HTTP APIs.  REST uses a more generic and uniform method of exposing resources through URIs, [representation through headers](https://github.com/for-GET/know-your-http-well/blob/master/headers.md), and actions through verbs such as GET, POST, PUT, DELETE, and PATCH.  Being stateless, REST is great for horizontal scaling and partitioning.

#### Disadvantage(s): REST

* With REST being focused on exposing data, it might not be a good fit if resources are not naturally organized or accessed in a simple hierarchy.  For example, returning all updated records from the past hour matching a particular set of events is not easily expressed as a path.  With REST, it is likely to be implemented with a combination of URI path, query parameters, and possibly the request body.
* REST typically relies on a few verbs (GET, POST, PUT, DELETE, and PATCH) which sometimes doesn't fit your use case.  For example, moving expired documents to the archive folder might not cleanly fit within these verbs.
* Fetching complicated resources with nested hierarchies requires multiple round trips between the client and server to render single views, e.g. fetching content of a blog entry and the comments on that entry. For mobile applications operating in variable network conditions, these multiple roundtrips are highly undesirable.
* Over time, more fields might be added to an API response and older clients will receive all new data fields, even those that they do not need, as a result, it bloats the payload size and leads to larger latencies.

### RPC and REST calls comparison

| Operation | RPC | REST |
|---|---|---|
| Signup    | **POST** /signup | **POST** /persons |
| Resign    | **POST** /resign<br/>{<br/>"personid": "1234"<br/>} | **DELETE** /persons/1234 |
| Read a person | **GET** /readPerson?personid=1234 | **GET** /persons/1234 |
| Read a person’s items list | **GET** /readUsersItemsList?personid=1234 | **GET** /persons/1234/items |
| Add an item to a person’s items | **POST** /addItemToUsersItemsList<br/>{<br/>"personid": "1234";<br/>"itemid": "456"<br/>} | **POST** /persons/1234/items<br/>{<br/>"itemid": "456"<br/>} |
| Update an item    | **POST** /modifyItem<br/>{<br/>"itemid": "456";<br/>"key": "value"<br/>} | **PUT** /items/456<br/>{<br/>"key": "value"<br/>} |
| Delete an item | **POST** /removeItem<br/>{<br/>"itemid": "456"<br/>} | **DELETE** /items/456 |

<p align="center">
  <i><a href=https://apihandyman.io/do-you-really-know-why-you-prefer-rest-over-rpc/>Source: Do you really know why you prefer REST over RPC</a></i>
</p>

#### Source(s) and further reading: REST and RPC

* [Do you really know why you prefer REST over RPC](https://apihandyman.io/do-you-really-know-why-you-prefer-rest-over-rpc/)
* [When are RPC-ish approaches more appropriate than REST?](http://programmers.stackexchange.com/a/181186)
* [REST vs JSON-RPC](http://stackoverflow.com/questions/15056878/rest-vs-json-rpc)
* [Debunking the myths of RPC and REST](http://etherealbits.com/2012/12/debunking-the-myths-of-rpc-rest/)
* [What are the drawbacks of using REST](https://www.quora.com/What-are-the-drawbacks-of-using-RESTful-APIs)
* [Crack the system design interview](http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview)
* [Thrift](https://code.facebook.com/posts/1468950976659943/)
* [Why REST for internal use and not RPC](http://arstechnica.com/civis/viewtopic.php?t=1190508)

## Security

This section could use some updates.  Consider [contributing](#contributing)!

Security is a broad topic.  Unless you have considerable experience, a security background, or are applying for a position that requires knowledge of security, you probably won't need to know more than the basics:

* Encrypt in transit and at rest.
* Sanitize all user inputs or any input parameters exposed to user to prevent [XSS](https://en.wikipedia.org/wiki/Cross-site_scripting) and [SQL injection](https://en.wikipedia.org/wiki/SQL_injection).
* Use parameterized queries to prevent SQL injection.
* Use the principle of [least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

### Source(s) and further reading

* [API security checklist](https://github.com/shieldfy/API-Security-Checklist)
* [Security guide for developers](https://github.com/FallibleInc/security-guide-for-developers)
* [OWASP top ten](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet)

## Appendix

You'll sometimes be asked to do 'back-of-the-envelope' estimates.  For example, you might need to determine how long it will take to generate 100 image thumbnails from disk or how much memory a data structure will take.  The **Powers of two table** and **Latency numbers every programmer should know** are handy references.

### Powers of two table

```
Power           Exact Value         Approx Value        Bytes
---------------------------------------------------------------
7                             128
8                             256
10                           1024   1 thousand           1 KB
16                         65,536                       64 KB
20                      1,048,576   1 million            1 MB
30                  1,073,741,824   1 billion            1 GB
32                  4,294,967,296                        4 GB
40              1,099,511,627,776   1 trillion           1 TB
```

#### Source(s) and further reading

* [Powers of two](https://en.wikipedia.org/wiki/Power_of_two)

### Latency numbers every programmer should know

```
Latency Comparison Numbers
--------------------------
L1 cache reference                           0.5 ns
Branch mispredict                            5   ns
L2 cache reference                           7   ns                      14x L1 cache
Mutex lock/unlock                           25   ns
Main memory reference                      100   ns                      20x L2 cache, 200x L1 cache
Compress 1K bytes with Zippy            10,000   ns       10 us
Send 1 KB bytes over 1 Gbps network     10,000   ns       10 us
Read 4 KB randomly from SSD*           150,000   ns      150 us          ~1GB/sec SSD
Read 1 MB sequentially from memory     250,000   ns      250 us
Round trip within same datacenter      500,000   ns      500 us
Read 1 MB sequentially from SSD*     1,000,000   ns    1,000 us    1 ms  ~1GB/sec SSD, 4X memory
Disk seek                           10,000,000   ns   10,000 us   10 ms  20x datacenter roundtrip
Read 1 MB sequentially from 1 Gbps  10,000,000   ns   10,000 us   10 ms  40x memory, 10X SSD
Read 1 MB sequentially from disk    30,000,000   ns   30,000 us   30 ms 120x memory, 30X SSD
Send packet CA->Netherlands->CA    150,000,000   ns  150,000 us  150 ms

Notes
-----
1 ns = 10^-9 seconds
1 us = 10^-6 seconds = 1,000 ns
1 ms = 10^-3 seconds = 1,000 us = 1,000,000 ns
```

Handy metrics based on numbers above:

* Read sequentially from disk at 30 MB/s
* Read sequentially from 1 Gbps Ethernet at 100 MB/s
* Read sequentially from SSD at 1 GB/s
* Read sequentially from main memory at 4 GB/s
* 6-7 world-wide round trips per second
* 2,000 round trips per second within a data center

#### Latency numbers visualized

![](https://camo.githubusercontent.com/77f72259e1eb58596b564d1ad823af1853bc60a3/687474703a2f2f692e696d6775722e636f6d2f6b307431652e706e67)

#### Source(s) and further reading

* [Latency numbers every programmer should know - 1](https://gist.github.com/jboner/2841832)
* [Latency numbers every programmer should know - 2](https://gist.github.com/hellerbarde/2843375)
* [Designs, lessons, and advice from building large distributed systems](http://www.cs.cornell.edu/projects/ladis2009/talks/dean-keynote-ladis2009.pdf)
* [Software Engineering Advice from Building Large-Scale Distributed Systems](https://static.googleusercontent.com/media/research.google.com/en//people/jeff/stanford-295-talk.pdf)

### Additional system design interview questions

> Common system design interview questions, with links to resources on how to solve each.

| Question | Reference(s) |
|---|---|
| Design a file sync service like Dropbox | [youtube.com](https://www.youtube.com/watch?v=PE4gwstWhmc) |
| Design a search engine like Google | [queue.acm.org](http://queue.acm.org/detail.cfm?id=988407)<br/>[stackexchange.com](http://programmers.stackexchange.com/questions/38324/interview-question-how-would-you-implement-google-search)<br/>[ardendertat.com](http://www.ardendertat.com/2012/01/11/implementing-search-engines/)<br/>[stanford.edu](http://infolab.stanford.edu/~backrub/google.html) |
| Design a scalable web crawler like Google | [quora.com](https://www.quora.com/How-can-I-build-a-web-crawler-from-scratch) |
| Design Google docs | [code.google.com](https://code.google.com/p/google-mobwrite/)<br/>[neil.fraser.name](https://neil.fraser.name/writing/sync/) |
| Design a key-value store like Redis | [slideshare.net](http://www.slideshare.net/dvirsky/introduction-to-redis) |
| Design a cache system like Memcached | [slideshare.net](http://www.slideshare.net/oemebamo/introduction-to-memcached) |
| Design a recommendation system like Amazon's | [hulu.com](https://web.archive.org/web/20170406065247/http://tech.hulu.com/blog/2011/09/19/recommendation-system.html)<br/>[ijcai13.org](http://ijcai13.org/files/tutorial_slides/td3.pdf) |
| Design a tinyurl system like Bitly | [n00tc0d3r.blogspot.com](http://n00tc0d3r.blogspot.com/) |
| Design a chat app like WhatsApp | [highscalability.com](http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html)
| Design a picture sharing system like Instagram | [highscalability.com](http://highscalability.com/flickr-architecture)<br/>[highscalability.com](http://highscalability.com/blog/2011/12/6/instagram-architecture-14-million-users-terabytes-of-photos.html) |
| Design the Facebook news feed function | [quora.com](http://www.quora.com/What-are-best-practices-for-building-something-like-a-News-Feed)<br/>[quora.com](http://www.quora.com/Activity-Streams/What-are-the-scaling-issues-to-keep-in-mind-while-developing-a-social-network-feed)<br/>[slideshare.net](http://www.slideshare.net/danmckinley/etsy-activity-feeds-architecture) |
| Design the Facebook timeline function | [facebook.com](https://www.facebook.com/note.php?note_id=10150468255628920)<br/>[highscalability.com](http://highscalability.com/blog/2012/1/23/facebook-timeline-brought-to-you-by-the-power-of-denormaliza.html) |
| Design the Facebook chat function | [erlang-factory.com](http://www.erlang-factory.com/upload/presentations/31/EugeneLetuchy-ErlangatFacebook.pdf)<br/>[facebook.com](https://www.facebook.com/note.php?note_id=14218138919&id=9445547199&index=0) |
| Design a graph search function like Facebook's | [facebook.com](https://www.facebook.com/notes/facebook-engineering/under-the-hood-building-out-the-infrastructure-for-graph-search/10151347573598920)<br/>[facebook.com](https://www.facebook.com/notes/facebook-engineering/under-the-hood-indexing-and-ranking-in-graph-search/10151361720763920)<br/>[facebook.com](https://www.facebook.com/notes/facebook-engineering/under-the-hood-the-natural-language-interface-of-graph-search/10151432733048920) |
| Design a content delivery network like CloudFlare | [figshare.com](https://figshare.com/articles/Globally_distributed_content_delivery/6605972) |
| Design a trending topic system like Twitter's | [michael-noll.com](http://www.michael-noll.com/blog/2013/01/18/implementing-real-time-trending-topics-in-storm/)<br/>[snikolov .wordpress.com](http://snikolov.wordpress.com/2012/11/14/early-detection-of-twitter-trends/) |
| Design a random ID generation system | [blog.twitter.com](https://blog.twitter.com/2010/announcing-snowflake)<br/>[github.com](https://github.com/twitter/snowflake/) |
| Return the top k requests during a time interval | [cs.ucsb.edu](https://www.cs.ucsb.edu/sites/cs.ucsb.edu/files/docs/reports/2005-23.pdf)<br/>[wpi.edu](http://davis.wpi.edu/xmdv/docs/EDBT11-diyang.pdf) |
| Design a system that serves data from multiple data centers | [highscalability.com](http://highscalability.com/blog/2009/8/24/how-google-serves-data-from-multiple-datacenters.html) |
| Design an online multiplayer card game | [indieflashblog.com](http://www.indieflashblog.com/how-to-create-an-asynchronous-multiplayer-game.html)<br/>[buildnewgames.com](http://buildnewgames.com/real-time-multiplayer/) |
| Design a garbage collection system | [stuffwithstuff.com](http://journal.stuffwithstuff.com/2013/12/08/babys-first-garbage-collector/)<br/>[washington.edu](http://courses.cs.washington.edu/courses/csep521/07wi/prj/rick.pdf) |
| Design an API rate limiter | [https://stripe.com/blog/](https://stripe.com/blog/rate-limiters) |
| Add a system design question | [Contribute](#contributing) |

### Real world architectures

> Articles on how real world systems are designed.

<p align="center">
  <img src="http://i.imgur.com/TcUo2fw.png"/>
  <br/>
  <i><a href=https://www.infoq.com/presentations/Twitter-Timeline-Scalability>Source: Twitter timelines at scale</a></i>
</p>

**Don't focus on nitty gritty details for the following articles, instead:**

* Identify shared principles, common technologies, and patterns within these articles
* Study what problems are solved by each component, where it works, where it doesn't
* Review the lessons learned

|Type | System | Reference(s) |
|---|---|---|
| Data processing | **MapReduce** - Distributed data processing from Google | [research.google.com](http://static.googleusercontent.com/media/research.google.com/zh-CN/us/archive/mapreduce-osdi04.pdf) |
| Data processing | **Spark** - Distributed data processing from Databricks | [slideshare.net](http://www.slideshare.net/AGrishchenko/apache-spark-architecture) |
| Data processing | **Storm** - Distributed data processing from Twitter | [slideshare.net](http://www.slideshare.net/previa/storm-16094009) |
| | | |
| Data store | **Bigtable** - Distributed column-oriented database from Google | [harvard.edu](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/chang06bigtable.pdf) |
| Data store | **HBase** - Open source implementation of Bigtable | [slideshare.net](http://www.slideshare.net/alexbaranau/intro-to-hbase) |
| Data store | **Cassandra** - Distributed column-oriented database from Facebook | [slideshare.net](http://www.slideshare.net/planetcassandra/cassandra-introduction-features-30103666)
| Data store | **DynamoDB** - Document-oriented database from Amazon | [harvard.edu](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/decandia07dynamo.pdf) |
| Data store | **MongoDB** - Document-oriented database | [slideshare.net](http://www.slideshare.net/mdirolf/introduction-to-mongodb) |
| Data store | **Spanner** - Globally-distributed database from Google | [research.google.com](http://research.google.com/archive/spanner-osdi2012.pdf) |
| Data store | **Memcached** - Distributed memory caching system | [slideshare.net](http://www.slideshare.net/oemebamo/introduction-to-memcached) |
| Data store | **Redis** - Distributed memory caching system with persistence and value types | [slideshare.net](http://www.slideshare.net/dvirsky/introduction-to-redis) |
| | | |
| File system | **Google File System (GFS)** - Distributed file system | [research.google.com](http://static.googleusercontent.com/media/research.google.com/zh-CN/us/archive/gfs-sosp2003.pdf) |
| File system | **Hadoop File System (HDFS)** - Open source implementation of GFS | [apache.org](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html) |
| | | |
| Misc | **Chubby** - Lock service for loosely-coupled distributed systems from Google | [research.google.com](http://static.googleusercontent.com/external_content/untrusted_dlcp/research.google.com/en/us/archive/chubby-osdi06.pdf) |
| Misc | **Dapper** - Distributed systems tracing infrastructure | [research.google.com](http://static.googleusercontent.com/media/research.google.com/en//pubs/archive/36356.pdf)
| Misc | **Kafka** - Pub/sub message queue from LinkedIn | [slideshare.net](http://www.slideshare.net/mumrah/kafka-talk-tri-hug) |
| Misc | **Zookeeper** - Centralized infrastructure and services enabling synchronization | [slideshare.net](http://www.slideshare.net/sauravhaloi/introduction-to-apache-zookeeper) |
| | Add an architecture | [Contribute](#contributing) |

### Company architectures

| Company | Reference(s) |
|---|---|
| Amazon | [Amazon architecture](http://highscalability.com/amazon-architecture) |
| Cinchcast | [Producing 1,500 hours of audio every day](http://highscalability.com/blog/2012/7/16/cinchcast-architecture-producing-1500-hours-of-audio-every-d.html) |
| DataSift | [Realtime datamining At 120,000 tweets per second](http://highscalability.com/blog/2011/11/29/datasift-architecture-realtime-datamining-at-120000-tweets-p.html) |
| DropBox | [How we've scaled Dropbox](https://www.youtube.com/watch?v=PE4gwstWhmc) |
| ESPN | [Operating At 100,000 duh nuh nuhs per second](http://highscalability.com/blog/2013/11/4/espns-architecture-at-scale-operating-at-100000-duh-nuh-nuhs.html) |
| Google | [Google architecture](http://highscalability.com/google-architecture) |
| Instagram | [14 million users, terabytes of photos](http://highscalability.com/blog/2011/12/6/instagram-architecture-14-million-users-terabytes-of-photos.html)<br/>[What powers Instagram](http://instagram-engineering.tumblr.com/post/13649370142/what-powers-instagram-hundreds-of-instances) |
| Justin.tv | [Justin.Tv's live video broadcasting architecture](http://highscalability.com/blog/2010/3/16/justintvs-live-video-broadcasting-architecture.html) |
| Facebook | [Scaling memcached at Facebook](https://cs.uwaterloo.ca/~brecht/courses/854-Emerging-2014/readings/key-value/fb-memcached-nsdi-2013.pdf)<br/>[TAO: Facebook’s distributed data store for the social graph](https://cs.uwaterloo.ca/~brecht/courses/854-Emerging-2014/readings/data-store/tao-facebook-distributed-datastore-atc-2013.pdf)<br/>[Facebook’s photo storage](https://www.usenix.org/legacy/event/osdi10/tech/full_papers/Beaver.pdf)<br/>[How Facebook Live Streams To 800,000 Simultaneous Viewers](http://highscalability.com/blog/2016/6/27/how-facebook-live-streams-to-800000-simultaneous-viewers.html) |
| Flickr | [Flickr architecture](http://highscalability.com/flickr-architecture) |
| Mailbox | [From 0 to one million users in 6 weeks](http://highscalability.com/blog/2013/6/18/scaling-mailbox-from-0-to-one-million-users-in-6-weeks-and-1.html) |
| Netflix | [A 360 Degree View Of The Entire Netflix Stack](http://highscalability.com/blog/2015/11/9/a-360-degree-view-of-the-entire-netflix-stack.html)<br/>[Netflix: What Happens When You Press Play?](http://highscalability.com/blog/2017/12/11/netflix-what-happens-when-you-press-play.html) |
| Pinterest | [From 0 To 10s of billions of page views a month](http://highscalability.com/blog/2013/4/15/scaling-pinterest-from-0-to-10s-of-billions-of-page-views-a.html)<br/>[18 million visitors, 10x growth, 12 employees](http://highscalability.com/blog/2012/5/21/pinterest-architecture-update-18-million-visitors-10x-growth.html) |
| Playfish | [50 million monthly users and growing](http://highscalability.com/blog/2010/9/21/playfishs-social-gaming-architecture-50-million-monthly-user.html) |
| PlentyOfFish | [PlentyOfFish architecture](http://highscalability.com/plentyoffish-architecture) |
| Salesforce | [How they handle 1.3 billion transactions a day](http://highscalability.com/blog/2013/9/23/salesforce-architecture-how-they-handle-13-billion-transacti.html) |
| Stack Overflow | [Stack Overflow architecture](http://highscalability.com/blog/2009/8/5/stack-overflow-architecture.html) |
| TripAdvisor | [40M visitors, 200M dynamic page views, 30TB data](http://highscalability.com/blog/2011/6/27/tripadvisor-architecture-40m-visitors-200m-dynamic-page-view.html) |
| Tumblr | [15 billion page views a month](http://highscalability.com/blog/2012/2/13/tumblr-architecture-15-billion-page-views-a-month-and-harder.html) |
| Twitter | [Making Twitter 10000 percent faster](http://highscalability.com/scaling-twitter-making-twitter-10000-percent-faster)<br/>[Storing 250 million tweets a day using MySQL](http://highscalability.com/blog/2011/12/19/how-twitter-stores-250-million-tweets-a-day-using-mysql.html)<br/>[150M active users, 300K QPS, a 22 MB/S firehose](http://highscalability.com/blog/2013/7/8/the-architecture-twitter-uses-to-deal-with-150m-active-users.html)<br/>[Timelines at scale](https://www.infoq.com/presentations/Twitter-Timeline-Scalability)<br/>[Big and small data at Twitter](https://www.youtube.com/watch?v=5cKTP36HVgI)<br/>[Operations at Twitter: scaling beyond 100 million users](https://www.youtube.com/watch?v=z8LU0Cj6BOU)<br/>[How Twitter Handles 3,000 Images Per Second](http://highscalability.com/blog/2016/4/20/how-twitter-handles-3000-images-per-second.html) |
| Uber | [How Uber scales their real-time market platform](http://highscalability.com/blog/2015/9/14/how-uber-scales-their-real-time-market-platform.html)<br/>[Lessons Learned From Scaling Uber To 2000 Engineers, 1000 Services, And 8000 Git Repositories](http://highscalability.com/blog/2016/10/12/lessons-learned-from-scaling-uber-to-2000-engineers-1000-ser.html) |
| WhatsApp | [The WhatsApp architecture Facebook bought for $19 billion](http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html) |
| YouTube | [YouTube scalability](https://www.youtube.com/watch?v=w5WVu624fY8)<br/>[YouTube architecture](http://highscalability.com/youtube-architecture) |

### Company engineering blogs

> Architectures for companies you are interviewing with.
>
> Questions you encounter might be from the same domain.

* [Airbnb Engineering](http://nerds.airbnb.com/)
* [Atlassian Developers](https://developer.atlassian.com/blog/)
* [AWS Blog](https://aws.amazon.com/blogs/aws/)
* [Bitly Engineering Blog](http://word.bitly.com/)
* [Box Blogs](https://blog.box.com/blog/category/engineering)
* [Cloudera Developer Blog](http://blog.cloudera.com/)
* [Dropbox Tech Blog](https://tech.dropbox.com/)
* [Engineering at Quora](http://engineering.quora.com/)
* [Ebay Tech Blog](http://www.ebaytechblog.com/)
* [Evernote Tech Blog](https://blog.evernote.com/tech/)
* [Etsy Code as Craft](http://codeascraft.com/)
* [Facebook Engineering](https://www.facebook.com/Engineering)
* [Flickr Code](http://code.flickr.net/)
* [Foursquare Engineering Blog](http://engineering.foursquare.com/)
* [GitHub Engineering Blog](http://githubengineering.com/)
* [Google Research Blog](http://googleresearch.blogspot.com/)
* [Groupon Engineering Blog](https://engineering.groupon.com/)
* [Heroku Engineering Blog](https://engineering.heroku.com/)
* [Hubspot Engineering Blog](http://product.hubspot.com/blog/topic/engineering)
* [High Scalability](http://highscalability.com/)
* [Instagram Engineering](http://instagram-engineering.tumblr.com/)
* [Intel Software Blog](https://software.intel.com/en-us/blogs/)
* [Jane Street Tech Blog](https://blogs.janestreet.com/category/ocaml/)
* [LinkedIn Engineering](http://engineering.linkedin.com/blog)
* [Microsoft Engineering](https://engineering.microsoft.com/)
* [Microsoft Python Engineering](https://blogs.msdn.microsoft.com/pythonengineering/)
* [Netflix Tech Blog](http://techblog.netflix.com/)
* [Paypal Developer Blog](https://devblog.paypal.com/category/engineering/)
* [Pinterest Engineering Blog](https://medium.com/@Pinterest_Engineering)
* [Quora Engineering](https://engineering.quora.com/)
* [Reddit Blog](http://www.redditblog.com/)
* [Salesforce Engineering Blog](https://developer.salesforce.com/blogs/engineering/)
* [Slack Engineering Blog](https://slack.engineering/)
* [Spotify Labs](https://labs.spotify.com/)
* [Twilio Engineering Blog](http://www.twilio.com/engineering)
* [Twitter Engineering](https://blog.twitter.com/engineering/)
* [Uber Engineering Blog](http://eng.uber.com/)
* [Yahoo Engineering Blog](http://yahooeng.tumblr.com/)
* [Yelp Engineering Blog](http://engineeringblog.yelp.com/)
* [Zynga Engineering Blog](https://www.zynga.com/blogs/engineering)

#### Source(s) and further reading

Looking to add a blog?  To avoid duplicating work, consider adding your company blog to the following repo:

* [kilimchoi/engineering-blogs](https://github.com/kilimchoi/engineering-blogs)

## Under development

Interested in adding a section or helping complete one in-progress?  [Contribute](#contributing)!

* Distributed computing with MapReduce
* Consistent hashing
* Scatter gather
* [Contribute](#contributing)

## Credits

Credits and sources are provided throughout this repo.

Special thanks to:

* [Hired in tech](http://www.hiredintech.com/system-design/the-system-design-process/)
* [Cracking the coding interview](https://www.amazon.com/dp/0984782850/)
* [High scalability](http://highscalability.com/)
* [checkcheckzz/system-design-interview](https://github.com/checkcheckzz/system-design-interview)
* [shashank88/system_design](https://github.com/shashank88/system_design)
* [mmcgrana/services-engineering](https://github.com/mmcgrana/services-engineering)
* [System design cheat sheet](https://gist.github.com/vasanthk/485d1c25737e8e72759f)
* [A distributed systems reading list](http://dancres.github.io/Pages/)
* [Cracking the system design interview](http://www.puncsky.com/blog/2016-02-13-crack-the-system-design-interview)

## Contact info

Feel free to contact me to discuss any issues, questions, or comments.

My contact info can be found on my [GitHub page](https://github.com/donnemartin).

## License

*I am providing code and resources in this repository to you under an open source license.  Because this is my personal repository, the license you receive to my code and resources is from me and not my employer (Facebook).*

    Copyright 2017 Donne Martin

    Creative Commons Attribution 4.0 International License (CC BY 4.0)

    http://creativecommons.org/licenses/by/4.0/
# Design Mint.com

*Note: This document links directly to relevant areas found in the [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) to avoid duplication.  Refer to the linked content for general talking points, tradeoffs, and alternatives.*

## Step 1: Outline use cases and constraints

> Gather requirements and scope the problem.
> Ask questions to clarify use cases and constraints.
> Discuss assumptions.

Without an interviewer to address clarifying questions, we'll define some use cases and constraints.

### Use cases

#### We'll scope the problem to handle only the following use cases

* **User** connects to a financial account
* **Service** extracts transactions from the account
    * Updates daily
    * Categorizes transactions
        * Allows manual category override by the user
        * No automatic re-categorization
    * Analyzes monthly spending, by category
* **Service** recommends a budget
    * Allows users to manually set a budget
    * Sends notifications when approaching or exceeding budget
* **Service** has high availability

#### Out of scope

* **Service** performs additional logging and analytics

### Constraints and assumptions

#### State assumptions

* Traffic is not evenly distributed
* Automatic daily update of accounts applies only to users active in the past 30 days
* Adding or removing financial accounts is relatively rare
* Budget notifications don't need to be instant
* 10 million users
    * 10 budget categories per user = 100 million budget items
    * Example categories:
        * Housing = $1,000
        * Food = $200
        * Gas = $100
    * Sellers are used to determine transaction category
        * 50,000 sellers
* 30 million financial accounts
* 5 billion transactions per month
* 500 million read requests per month
* 10:1 write to read ratio
    * Write-heavy, users make transactions daily, but few visit the site daily

#### Calculate usage

**Clarify with your interviewer if you should run back-of-the-envelope usage calculations.**

* Size per transaction:
    * `user_id` - 8 bytes
    * `created_at` - 5 bytes
    * `seller` - 32 bytes
    * `amount` - 5 bytes
    * Total: ~50 bytes
* 250 GB of new transaction content per month
    * 50 bytes per transaction * 5 billion transactions per month
    * 9 TB of new transaction content in 3 years
    * Assume most are new transactions instead of updates to existing ones
* 2,000 transactions per second on average
* 200 read requests per second on average

Handy conversion guide:

* 2.5 million seconds per month
* 1 request per second = 2.5 million requests per month
* 40 requests per second = 100 million requests per month
* 400 requests per second = 1 billion requests per month

## Step 2: Create a high level design

> Outline a high level design with all important components.

![Imgur](http://i.imgur.com/E8klrBh.png)

## Step 3: Design core components

> Dive into details for each core component.

### Use case: User connects to a financial account

We could store info on the 10 million users in a [relational database](https://github.com/donnemartin/system-design-primer#relational-database-management-system-rdbms).  We should discuss the [use cases and tradeoffs between choosing SQL or NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql).

* The **Client** sends a request to the **Web Server**, running as a [reverse proxy](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
* The **Web Server** forwards the request to the **Accounts API** server
* The **Accounts API** server updates the **SQL Database** `accounts` table with the newly entered account info

**Clarify with your interviewer how much code you are expected to write**.

The `accounts` table could have the following structure:

```
id int NOT NULL AUTO_INCREMENT
created_at datetime NOT NULL
last_update datetime NOT NULL
account_url varchar(255) NOT NULL
account_login varchar(32) NOT NULL
account_password_hash char(64) NOT NULL
user_id int NOT NULL
PRIMARY KEY(id)
FOREIGN KEY(user_id) REFERENCES users(id)
```

We'll create an [index](https://github.com/donnemartin/system-design-primer#use-good-indices) on `id`, `user_id `, and `created_at` to speed up lookups (log-time instead of scanning the entire table) and to keep the data in memory.  Reading 1 MB sequentially from memory takes about 250 microseconds, while reading from SSD takes 4x and from disk takes 80x longer.<sup><a href=https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know>1</a></sup>

We'll use a public [**REST API**](https://github.com/donnemartin/system-design-primer#representational-state-transfer-rest):

```
$ curl -X POST --data '{ "user_id": "foo", "account_url": "bar", \
    "account_login": "baz", "account_password": "qux" }' \
    https://mint.com/api/v1/account
```

For internal communications, we could use [Remote Procedure Calls](https://github.com/donnemartin/system-design-primer#remote-procedure-call-rpc).

Next, the service extracts transactions from the account.

### Use case: Service extracts transactions from the account

We'll want to extract information from an account in these cases:

* The user first links the account
* The user manually refreshes the account
* Automatically each day for users who have been active in the past 30 days

Data flow:

* The **Client** sends a request to the **Web Server**
* The **Web Server** forwards the request to the **Accounts API** server
* The **Accounts API** server places a job on a **Queue** such as [Amazon SQS](https://aws.amazon.com/sqs/) or [RabbitMQ](https://www.rabbitmq.com/)
    * Extracting transactions could take awhile, we'd probably want to do this [asynchronously with a queue](https://github.com/donnemartin/system-design-primer#asynchronism), although this introduces additional complexity
* The **Transaction Extraction Service** does the following:
    * Pulls from the **Queue** and extracts transactions for the given account from the financial institution, storing the results as raw log files in the **Object Store**
    * Uses the **Category Service** to categorize each transaction
    * Uses the **Budget Service** to calculate aggregate monthly spending by category
        * The **Budget Service** uses the **Notification Service** to let users know if they are nearing or have exceeded their budget
    * Updates the **SQL Database** `transactions` table with categorized transactions
    * Updates the **SQL Database** `monthly_spending` table with aggregate monthly spending by category
    * Notifies the user the transactions have completed through the **Notification Service**:
        * Uses a **Queue** (not pictured) to asynchronously send out notifications

The `transactions` table could have the following structure:

```
id int NOT NULL AUTO_INCREMENT
created_at datetime NOT NULL
seller varchar(32) NOT NULL
amount decimal NOT NULL
user_id int NOT NULL
PRIMARY KEY(id)
FOREIGN KEY(user_id) REFERENCES users(id)
```

We'll create an [index](https://github.com/donnemartin/system-design-primer#use-good-indices) on `id`, `user_id `, and `created_at`.

The `monthly_spending` table could have the following structure:

```
id int NOT NULL AUTO_INCREMENT
month_year date NOT NULL
category varchar(32)
amount decimal NOT NULL
user_id int NOT NULL
PRIMARY KEY(id)
FOREIGN KEY(user_id) REFERENCES users(id)
```

We'll create an [index](https://github.com/donnemartin/system-design-primer#use-good-indices) on `id` and `user_id `.

#### Category service

For the **Category Service**, we can seed a seller-to-category dictionary with the most popular sellers.  If we estimate 50,000 sellers and estimate each entry to take less than 255 bytes, the dictionary would only take about 12 MB of memory.

**Clarify with your interviewer how much code you are expected to write**.

```python
class DefaultCategories(Enum):

    HOUSING = 0
    FOOD = 1
    GAS = 2
    SHOPPING = 3
    ...

seller_category_map = {}
seller_category_map['Exxon'] = DefaultCategories.GAS
seller_category_map['Target'] = DefaultCategories.SHOPPING
...
```

For sellers not initially seeded in the map, we could use a crowdsourcing effort by evaluating the manual category overrides our users provide.  We could use a heap to quickly lookup the top manual override per seller in O(1) time.

```python
class Categorizer(object):

    def __init__(self, seller_category_map, self.seller_category_crowd_overrides_map):
        self.seller_category_map = seller_category_map
        self.seller_category_crowd_overrides_map = \
            seller_category_crowd_overrides_map

    def categorize(self, transaction):
        if transaction.seller in self.seller_category_map:
            return self.seller_category_map[transaction.seller]
        elif transaction.seller in self.seller_category_crowd_overrides_map:
            self.seller_category_map[transaction.seller] = \
                self.seller_category_crowd_overrides_map[transaction.seller].peek_min()
            return self.seller_category_map[transaction.seller]
        return None
```

Transaction implementation:

```python
class Transaction(object):

    def __init__(self, created_at, seller, amount):
        self.timestamp = timestamp
        self.seller = seller
        self.amount = amount
```

### Use case: Service recommends a budget

To start, we could use a generic budget template that allocates category amounts based on income tiers.  Using this approach, we would not have to store the 100 million budget items identified in the constraints, only those that the user overrides.  If a user overrides a budget category, which we could store the override in the `TABLE budget_overrides`.

```python
class Budget(object):

    def __init__(self, income):
        self.income = income
        self.categories_to_budget_map = self.create_budget_template()

    def create_budget_template(self):
        return {
            'DefaultCategories.HOUSING': income * .4,
            'DefaultCategories.FOOD': income * .2
            'DefaultCategories.GAS': income * .1,
            'DefaultCategories.SHOPPING': income * .2
            ...
        }

    def override_category_budget(self, category, amount):
        self.categories_to_budget_map[category] = amount
```

For the **Budget Service**, we can potentially run SQL queries on the `transactions` table to generate the `monthly_spending` aggregate table.  The `monthly_spending` table would likely have much fewer rows than the total 5 billion transactions, since users typically have many transactions per month.

As an alternative, we can run **MapReduce** jobs on the raw transaction files to:

* Categorize each transaction
* Generate aggregate monthly spending by category

Running analyses on the transaction files could significantly reduce the load on the database.

We could call the **Budget Service** to re-run the analysis if the user updates a category.

**Clarify with your interviewer how much code you are expected to write**.

Sample log file format, tab delimited:

```
user_id   timestamp   seller  amount
```

**MapReduce** implementation:

```python
class SpendingByCategory(MRJob):

    def __init__(self, categorizer):
        self.categorizer = categorizer
        self.current_year_month = calc_current_year_month()
        ...

    def calc_current_year_month(self):
        """Return the current year and month."""
        ...

    def extract_year_month(self, timestamp):
        """Return the year and month portions of the timestamp."""
        ...

    def handle_budget_notifications(self, key, total):
        """Call notification API if nearing or exceeded budget."""
        ...

    def mapper(self, _, line):
        """Parse each log line, extract and transform relevant lines.

        Argument line will be of the form:

        user_id   timestamp   seller  amount

        Using the categorizer to convert seller to category,
        emit key value pairs of the form:

        (user_id, 2016-01, shopping), 25
        (user_id, 2016-01, shopping), 100
        (user_id, 2016-01, gas), 50
        """
        user_id, timestamp, seller, amount = line.split('\t')
        category = self.categorizer.categorize(seller)
        period = self.extract_year_month(timestamp)
        if period == self.current_year_month:
            yield (user_id, period, category), amount

    def reducer(self, key, value):
        """Sum values for each key.

        (user_id, 2016-01, shopping), 125
        (user_id, 2016-01, gas), 50
        """
        total = sum(values)
        yield key, sum(values)
```

## Step 4: Scale the design

> Identify and address bottlenecks, given the constraints.

![Imgur](http://i.imgur.com/V5q57vU.png)

**Important: Do not simply jump right into the final design from the initial design!**

State you would 1) **Benchmark/Load Test**, 2) **Profile** for bottlenecks 3) address bottlenecks while evaluating alternatives and trade-offs, and 4) repeat.  See [Design a system that scales to millions of users on AWS](../scaling_aws/README.md) as a sample on how to iteratively scale the initial design.

It's important to discuss what bottlenecks you might encounter with the initial design and how you might address each of them.  For example, what issues are addressed by adding a **Load Balancer** with multiple **Web Servers**?  **CDN**?  **Master-Slave Replicas**?  What are the alternatives and **Trade-Offs** for each?

We'll introduce some components to complete the design and to address scalability issues.  Internal load balancers are not shown to reduce clutter.

*To avoid repeating discussions*, refer to the following [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) for main talking points, tradeoffs, and alternatives:

* [DNS](https://github.com/donnemartin/system-design-primer#domain-name-system)
* [CDN](https://github.com/donnemartin/system-design-primer#content-delivery-network)
* [Load balancer](https://github.com/donnemartin/system-design-primer#load-balancer)
* [Horizontal scaling](https://github.com/donnemartin/system-design-primer#horizontal-scaling)
* [Web server (reverse proxy)](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
* [API server (application layer)](https://github.com/donnemartin/system-design-primer#application-layer)
* [Cache](https://github.com/donnemartin/system-design-primer#cache)
* [Relational database management system (RDBMS)](https://github.com/donnemartin/system-design-primer#relational-database-management-system-rdbms)
* [SQL write master-slave failover](https://github.com/donnemartin/system-design-primer#fail-over)
* [Master-slave replication](https://github.com/donnemartin/system-design-primer#master-slave-replication)
* [Asynchronism](https://github.com/donnemartin/system-design-primer#asynchronism)
* [Consistency patterns](https://github.com/donnemartin/system-design-primer#consistency-patterns)
* [Availability patterns](https://github.com/donnemartin/system-design-primer#availability-patterns)

We'll add an additional use case: **User** accesses summaries and transactions.

User sessions, aggregate stats by category, and recent transactions could be placed in a **Memory Cache** such as Redis or Memcached.

* The **Client** sends a read request to the **Web Server**
* The **Web Server** forwards the request to the **Read API** server
    * Static content can be served from the **Object Store** such as S3, which is cached on the **CDN**
* The **Read API** server does the following:
    * Checks the **Memory Cache** for the content
        * If the url is in the **Memory Cache**, returns the cached contents
        * Else
            * If the url is in the **SQL Database**, fetches the contents
                * Updates the **Memory Cache** with the contents

Refer to [When to update the cache](https://github.com/donnemartin/system-design-primer#when-to-update-the-cache) for tradeoffs and alternatives.  The approach above describes [cache-aside](https://github.com/donnemartin/system-design-primer#cache-aside).

Instead of keeping the `monthly_spending` aggregate table in the **SQL Database**, we could create a separate **Analytics Database** using a data warehousing solution such as Amazon Redshift or Google BigQuery.

We might only want to store a month of `transactions` data in the database, while storing the rest in a data warehouse or in an **Object Store**.  An **Object Store** such as Amazon S3 can comfortably handle the constraint of 250 GB of new content per month.

To address the 2,000 *average* read requests per second (higher at peak), traffic for popular content should be handled by the **Memory Cache** instead of the database.  The **Memory Cache** is also useful for handling the unevenly distributed traffic and traffic spikes.  The **SQL Read Replicas** should be able to handle the cache misses, as long as the replicas are not bogged down with replicating writes.

200 *average* transaction writes per second (higher at peak) might be tough for a single **SQL Write Master-Slave**.  We might need to employ additional SQL scaling patterns:

* [Federation](https://github.com/donnemartin/system-design-primer#federation)
* [Sharding](https://github.com/donnemartin/system-design-primer#sharding)
* [Denormalization](https://github.com/donnemartin/system-design-primer#denormalization)
* [SQL Tuning](https://github.com/donnemartin/system-design-primer#sql-tuning)

We should also consider moving some data to a **NoSQL Database**.

## Additional talking points

> Additional topics to dive into, depending on the problem scope and time remaining.

#### NoSQL

* [Key-value store](https://github.com/donnemartin/system-design-primer#key-value-store)
* [Document store](https://github.com/donnemartin/system-design-primer#document-store)
* [Wide column store](https://github.com/donnemartin/system-design-primer#wide-column-store)
* [Graph database](https://github.com/donnemartin/system-design-primer#graph-database)
* [SQL vs NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql)

### Caching

* Where to cache
    * [Client caching](https://github.com/donnemartin/system-design-primer#client-caching)
    * [CDN caching](https://github.com/donnemartin/system-design-primer#cdn-caching)
    * [Web server caching](https://github.com/donnemartin/system-design-primer#web-server-caching)
    * [Database caching](https://github.com/donnemartin/system-design-primer#database-caching)
    * [Application caching](https://github.com/donnemartin/system-design-primer#application-caching)
* What to cache
    * [Caching at the database query level](https://github.com/donnemartin/system-design-primer#caching-at-the-database-query-level)
    * [Caching at the object level](https://github.com/donnemartin/system-design-primer#caching-at-the-object-level)
* When to update the cache
    * [Cache-aside](https://github.com/donnemartin/system-design-primer#cache-aside)
    * [Write-through](https://github.com/donnemartin/system-design-primer#write-through)
    * [Write-behind (write-back)](https://github.com/donnemartin/system-design-primer#write-behind-write-back)
    * [Refresh ahead](https://github.com/donnemartin/system-design-primer#refresh-ahead)

### Asynchronism and microservices

* [Message queues](https://github.com/donnemartin/system-design-primer#message-queues)
* [Task queues](https://github.com/donnemartin/system-design-primer#task-queues)
* [Back pressure](https://github.com/donnemartin/system-design-primer#back-pressure)
* [Microservices](https://github.com/donnemartin/system-design-primer#microservices)

### Communications

* Discuss tradeoffs:
    * External communication with clients - [HTTP APIs following REST](https://github.com/donnemartin/system-design-primer#representational-state-transfer-rest)
    * Internal communications - [RPC](https://github.com/donnemartin/system-design-primer#remote-procedure-call-rpc)
* [Service discovery](https://github.com/donnemartin/system-design-primer#service-discovery)

### Security

Refer to the [security section](https://github.com/donnemartin/system-design-primer#security).

### Latency numbers

See [Latency numbers every programmer should know](https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know).

### Ongoing

* Continue benchmarking and monitoring your system to address bottlenecks as they come up
* Scaling is an iterative process
# 设计 Pastebin.com (或者 Bit.ly)

**Note: 为了避免重复，当前文档直接链接到[系统设计主题](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#系统设计主题的索引)的相关区域，请参考链接内容以获得综合的讨论点、权衡和替代方案。**

**设计 Bit.ly** - 是一个类似的问题，区别是 pastebin 需要存储的是 paste 的内容，而不是原始的未短化的 url。

## 第一步：概述用例和约束

> 收集这个问题的需求和范畴。
> 问相关问题来明确用例和约束。
> 讨论一些假设。

因为没有面试官来明确这些问题，所以我们自己将定义一些用例和约束。

### 用例

#### 我们将问题的范畴限定在如下用例

* **用户** 输入一段文本，然后得到一个随机生成的链接
  * 过期设置
    * 默认的设置是不会过期的
    * 可以选择设置一个过期的时间
* **用户** 输入一个 paste 的 url 后，可以看到它存储的内容
* **用户** 是匿名的
* **Service** 跟踪页面分析
  * 一个月的访问统计
* **Service** 删除过期的 pastes
* **Service** 需要高可用

#### 超出范畴的用例

* **用户** 可以注册一个账户
  * **用户** 通过验证邮箱
* **用户** 可以用注册的账户登录
  * **用户** 可以编辑文档
* **用户** 可以设置可见性
* **用户** 可以设置短链接

### 约束和假设

#### 状态假设

* 访问流量不是均匀分布的
* 打开一个短链接应该是很快的
* pastes 只能是文本
* 页面访问分析数据可以不用实时
* 一千万的用户量
* 每个月一千万的 paste 写入量
* 每个月一亿的 paste 读取量
* 读写比例在 10:1

#### 计算使用

**向面试官说明你是否应该粗略计算一下使用情况。**

* 每个 paste 的大小
  * 每一个 paste 1 KB
  * `shortlink` - 7 bytes
  * `expiration_length_in_minutes` - 4 bytes
  * `created_at` - 5 bytes
  * `paste_path` - 255 bytes
  * 总共 = ~1.27 KB
* 每个月新的 paste 内容在 12.7GB
  * (1.27 * 10000000)KB / 月的 paste
  * 三年内将近 450GB 的新 paste 内容
  * 三年内 3.6 亿短链接
  * 假设大部分都是新的 paste，而不是需要更新已存在的 paste
* 平均 4paste/s 的写入速度
* 平均 40paste/s 的读取速度

简单的转换指南:

* 2.5 百万 req/s
* 1 req/s = 2.5 百万 req/m
* 40 req/s = 1 亿 req/m
* 400 req/s = 10 亿 req/m

## 第二步：创建一个高层次设计

> 概述一个包括所有重要的组件的高层次设计

![Imgur](http://i.imgur.com/BKsBnmG.png)

## 第三步：设计核心组件

> 深入每一个核心组件的细节

### 用例：用户输入一段文本，然后得到一个随机生成的链接

我们可以用一个 [关系型数据库](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#关系型数据库管理系统rdbms)作为一个大的哈希表，用来把生成的 url 映射到一个包含 paste 文件的文件服务器和路径上。

为了避免托管一个文件服务器，我们可以用一个托管的**对象存储**，比如 Amazon 的 S3 或者[NoSQL 文档类型存储](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#文档类型存储)。

作为一个大的哈希表的关系型数据库的替代方案，我们可以用[NoSQL 键值存储](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#键-值存储)。我们需要讨论[选择 SQL 或 NoSQL 之间的权衡](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#sql-还是-nosql)。下面的讨论是使用关系型数据库方法。

* **客户端** 发送一个创建 paste 的请求到作为一个[反向代理](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#反向代理web-服务器)启动的 **Web 服务器**。
* **Web 服务器** 转发请求给 **写接口** 服务器
* **写接口** 服务器执行如下操作：
  * 生成一个唯一的 url
    * 检查这个 url 在 **SQL 数据库** 里面是否是唯一的
    * 如果这个 url 不是唯一的，生成另外一个 url
    * 如果我们支持自定义 url，我们可以使用用户提供的 url（也需要检查是否重复）
  * 把生成的 url 存储到 **SQL 数据库** 的 `pastes` 表里面
  * 存储 paste 的内容数据到 **对象存储** 里面
  * 返回生成的 url

**向面试官阐明你需要写多少代码**

`pastes` 表可以有如下结构：

```sql
shortlink char(7) NOT NULL
expiration_length_in_minutes int NOT NULL
created_at datetime NOT NULL
paste_path varchar(255) NOT NULL
PRIMARY KEY(shortlink)
```

我们将在 `shortlink` 字段和 `created_at` 字段上创建一个[数据库索引](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#使用正确的索引)，用来提高查询的速度（避免因为扫描全表导致的长时间查询）并将数据保存在内存中，从内存里面顺序读取 1MB 的数据需要大概 250 微秒，而从 SSD 上读取则需要花费 4 倍的时间，从硬盘上则需要花费 80 倍的时间。<sup><a href=https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#每个程序员都应该知道的延迟数 > 1</a></sup>

为了生成唯一的 url，我们可以：

* 使用 [**MD5**](https://en.wikipedia.org/wiki/MD5) 来哈希用户的 IP 地址 + 时间戳
  * MD5 是一个普遍用来生成一个 128-bit 长度的哈希值的一种哈希方法
  * MD5 是一致分布的
  * 或者我们也可以用 MD5 哈希一个随机生成的数据
* 用 [**Base 62**](https://www.kerstner.at/2012/07/shortening-strings-using-base-62-encoding/) 编码 MD5 哈希值
  * 对于 urls，使用 Base 62 编码 `[a-zA-Z0-9]` 是比较合适的
  * 对于每一个原始输入只会有一个 hash 结果，Base 62 是确定的（不涉及随机性）
  * Base 64 是另外一个流行的编码方案，但是对于 urls，会因为额外的 `+` 和 `-` 字符串而产生一些问题
  * 以下 [Base 62 伪代码](http://stackoverflow.com/questions/742013/how-to-code-a-url-shortener) 执行的时间复杂度是 O(k)，k 是数字的数量 = 7：

```python
def base_encode(num, base=62):
    digits = []
    while num > 0
      remainder = modulo(num, base)
      digits.push(remainder)
      num = divide(num, base)
    digits = digits.reverse
```

* 取输出的前 7 个字符，结果会有 62^7 个可能的值，应该足以满足在 3 年内处理 3.6 亿个短链接的约束：

```python
url = base_encode(md5(ip_address+timestamp))[:URL_LENGTH]
```

我们将会用一个公开的 [**REST 风格接口**](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#表述性状态转移rest)：

```shell
$ curl -X POST --data '{"expiration_length_in_minutes":"60", \"paste_contents":"Hello World!"}' https://pastebin.com/api/v1/paste
```

Response:

```json
{
    "shortlink": "foobar"
}
```

用于内部通信，我们可以用 [RPC](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#远程过程调用协议rpc)。

### 用例：用户输入一个 paste 的 url 后可以看到它存储的内容

* **客户端** 发送一个获取 paste 请求到 **Web Server**
* **Web Server** 转发请求给 **读取接口** 服务器
* **读取接口** 服务器执行如下操作：
  * 在 **SQL 数据库** 检查这个生成的 url
    * 如果这个 url 在 **SQL 数据库** 里面，则从 **对象存储** 获取这个 paste 的内容
    * 否则，返回一个错误页面给用户

REST API：

```shell
curl https://pastebin.com/api/v1/paste?shortlink=foobar
```

Response:

```json
{
    "paste_contents": "Hello World",
    "created_at": "YYYY-MM-DD HH:MM:SS",
    "expiration_length_in_minutes": "60"
}
```

### 用例： 服务跟踪分析页面

因为实时分析不是必须的，所以我们可以简单的 **MapReduce** **Web Server** 的日志，用来生成点击次数。

```python
class HitCounts(MRJob):

    def extract_url(self, line):
        """Extract the generated url from the log line."""
        ...

    def extract_year_month(self, line):
        """Return the year and month portions of the timestamp."""
        ...

    def mapper(self, _, line):
        """Parse each log line, extract and transform relevant lines.

        Emit key value pairs of the form:

        (2016-01, url0), 1
        (2016-01, url0), 1
        (2016-01, url1), 1
        """
        url = self.extract_url(line)
        period = self.extract_year_month(line)
        yield (period, url), 1

    def reducer(self, key, values):
        """Sum values for each key.

        (2016-01, url0), 2
        (2016-01, url1), 1
        """
        yield key, sum(values)
```

### 用例： 服务删除过期的 pastes

为了删除过期的 pastes，我们可以直接搜索 **SQL 数据库** 中所有的过期时间比当前时间更早的记录，
所有过期的记录将从这张表里面删除（或者将其标记为过期）。

## 第四步：扩展这个设计

> 给定约束条件，识别和解决瓶颈。

![Imgur](http://i.imgur.com/4edXG0T.png)

**重要提示: 不要简单的从最初的设计直接跳到最终的设计**

说明您将迭代地执行这样的操作：1)**Benchmark/Load 测试**，2)**Profile** 出瓶颈，3)在评估替代方案和权衡时解决瓶颈，4)重复前面，可以参考[在 AWS 上设计一个可以支持百万用户的系统](../scaling_aws/README.md)这个用来解决如何迭代地扩展初始设计的例子。

重要的是讨论在初始设计中可能遇到的瓶颈，以及如何解决每个瓶颈。比如，在多个 **Web 服务器** 上添加 **负载平衡器** 可以解决哪些问题？ **CDN** 解决哪些问题？**Master-Slave Replicas** 解决哪些问题? 替代方案是什么和怎么对每一个替代方案进行权衡比较？

我们将介绍一些组件来完成设计，并解决可伸缩性问题。内部的负载平衡器并不能减少杂乱。

**为了避免重复的讨论**， 参考以下[系统设计主题](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#系统设计主题的索引)获取主要讨论要点、权衡和替代方案：

* [DNS](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#域名系统)
* [CDN](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#内容分发网络cdn)
* [负载均衡器](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#负载均衡器)
* [水平扩展](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#水平扩展)
* [反向代理（web 服务器）](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#反向代理web-服务器)
* [应用层](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#应用层)
* [缓存](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#缓存)
* [关系型数据库管理系统 (RDBMS)](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#关系型数据库管理系统rdbms)
* [SQL write master-slave failover](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#故障切换)
* [主从复制](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#主从复制)
* [一致性模式](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#一致性模式)
* [可用性模式](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#可用性模式)

**分析存储数据库** 可以用比如 Amazon Redshift 或者 Google BigQuery 这样的数据仓库解决方案。

一个像 Amazon S3 这样的 **对象存储**，可以轻松处理每月 12.7 GB 的新内容约束。

要处理 *平均* 每秒 40 读请求(峰值更高)，其中热点内容的流量应该由 **内存缓存** 处理，而不是数据库。**内存缓存** 对于处理分布不均匀的流量和流量峰值也很有用。只要副本没有陷入复制写的泥潭，**SQL Read Replicas** 应该能够处理缓存丢失。

对于单个 **SQL Write Master-Slave**，*平均* 每秒 4paste 写入 (峰值更高) 应该是可以做到的。否则，我们需要使用额外的 SQL 扩展模式:

* [联合](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#联合)
* [分片](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#分片)
* [非规范化](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#非规范化)
* [SQL 调优](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#SQL调优)

我们还应该考虑将一些数据移动到 **NoSQL 数据库**。

## 额外的话题

> 是否更深入探讨额外主题，取决于问题的范围和面试剩余的时间。

### NoSQL

* [键值存储](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#键-值存储)
* [文档存储](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#文档类型存储)
* [列型存储](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#列型存储)
* [图数据库](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#图数据库)
* [sql 还是 nosql](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#sql-还是-nosql)

### 缓存

* 在哪缓存
  * [客户端缓存](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#客户端缓存)
  * [CDN 缓存](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#cdn-缓存)
  * [Web 服务器缓存](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#web-服务器缓存)
  * [数据库缓存](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#数据库缓存)
  * [应用缓存](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#应用缓存)
* 缓存什么
  * [数据库查询级别的缓存](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#数据库查询级别的缓存)
  * [对象级别的缓存](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#对象级别的缓存)
* 何时更新缓存
  * [缓存模式](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#缓存模式)
  * [直写模式](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#直写模式)
  * [回写模式](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#回写模式)
  * [刷新](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#刷新)

### 异步和微服务

* [消息队列](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#消息队列)
* [任务队列](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#任务队列)
* [背压](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#背压)
* [微服务](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#微服务)

### 通信

* 讨论权衡:
  * 跟客户端之间的外部通信 - [HTTP APIs following REST](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#表述性状态转移rest)
  * 内部通信 - [RPC](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#远程过程调用协议rpc)
* [服务发现](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#服务发现)

### 安全

参考[安全](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#安全)。

### 延迟数字

见[每个程序员都应该知道的延迟数](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#每个程序员都应该知道的延迟数)。

### 持续进行

* 继续对系统进行基准测试和监控，以在瓶颈出现时解决它们
* 扩展是一个迭代的过程
# Design Pastebin.com (or Bit.ly)

*Note: This document links directly to relevant areas found in the [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) to avoid duplication.  Refer to the linked content for general talking points, tradeoffs, and alternatives.*

**Design Bit.ly** - is a similar question, except pastebin requires storing the paste contents instead of the original unshortened url.

## Step 1: Outline use cases and constraints

> Gather requirements and scope the problem.
> Ask questions to clarify use cases and constraints.
> Discuss assumptions.

Without an interviewer to address clarifying questions, we'll define some use cases and constraints.

### Use cases

#### We'll scope the problem to handle only the following use cases

* **User** enters a block of text and gets a randomly generated link
    * Expiration
        * Default setting does not expire
        * Can optionally set a timed expiration
* **User** enters a paste's url and views the contents
* **User** is anonymous
* **Service** tracks analytics of pages
    * Monthly visit stats
* **Service** deletes expired pastes
* **Service** has high availability

#### Out of scope

* **User** registers for an account
    * **User** verifies email
* **User** logs into a registered account
    * **User** edits the document
* **User** can set visibility
* **User** can set the shortlink

### Constraints and assumptions

#### State assumptions

* Traffic is not evenly distributed
* Following a short link should be fast
* Pastes are text only
* Page view analytics do not need to be realtime
* 10 million users
* 10 million paste writes per month
* 100 million paste reads per month
* 10:1 read to write ratio

#### Calculate usage

**Clarify with your interviewer if you should run back-of-the-envelope usage calculations.**

* Size per paste
    * 1 KB content per paste
    * `shortlink` - 7 bytes
    * `expiration_length_in_minutes` - 4 bytes
    * `created_at` - 5 bytes
    * `paste_path` - 255 bytes
    * total = ~1.27 KB
* 12.7 GB of new paste content per month
    * 1.27 KB per paste * 10 million pastes per month
    * ~450 GB of new paste content in 3 years
    * 360 million shortlinks in 3 years
    * Assume most are new pastes instead of updates to existing ones
* 4 paste writes per second on average
* 40 read requests per second on average

Handy conversion guide:

* 2.5 million seconds per month
* 1 request per second = 2.5 million requests per month
* 40 requests per second = 100 million requests per month
* 400 requests per second = 1 billion requests per month

## Step 2: Create a high level design

> Outline a high level design with all important components.

![Imgur](http://i.imgur.com/BKsBnmG.png)

## Step 3: Design core components

> Dive into details for each core component.

### Use case: User enters a block of text and gets a randomly generated link

We could use a [relational database](https://github.com/donnemartin/system-design-primer#relational-database-management-system-rdbms) as a large hash table, mapping the generated url to a file server and path containing the paste file.

Instead of managing a file server, we could use a managed **Object Store** such as Amazon S3 or a [NoSQL document store](https://github.com/donnemartin/system-design-primer#document-store).

An alternative to a relational database acting as a large hash table, we could use a [NoSQL key-value store](https://github.com/donnemartin/system-design-primer#key-value-store).  We should discuss the [tradeoffs between choosing SQL or NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql).  The following discussion uses the relational database approach.

* The **Client** sends a create paste request to the **Web Server**, running as a [reverse proxy](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
* The **Web Server** forwards the request to the **Write API** server
* The **Write API** server does the following:
    * Generates a unique url
        * Checks if the url is unique by looking at the **SQL Database** for a duplicate
        * If the url is not unique, it generates another url
        * If we supported a custom url, we could use the user-supplied (also check for a duplicate)
    * Saves to the **SQL Database** `pastes` table
    * Saves the paste data to the **Object Store**
    * Returns the url

**Clarify with your interviewer how much code you are expected to write**.

The `pastes` table could have the following structure:

```
shortlink char(7) NOT NULL
expiration_length_in_minutes int NOT NULL
created_at datetime NOT NULL
paste_path varchar(255) NOT NULL
PRIMARY KEY(shortlink)
```

We'll create an [index](https://github.com/donnemartin/system-design-primer#use-good-indices) on `shortlink ` and `created_at` to speed up lookups (log-time instead of scanning the entire table) and to keep the data in memory.  Reading 1 MB sequentially from memory takes about 250 microseconds, while reading from SSD takes 4x and from disk takes 80x longer.<sup><a href=https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know>1</a></sup>

To generate the unique url, we could:

* Take the [**MD5**](https://en.wikipedia.org/wiki/MD5) hash of the user's ip_address + timestamp
    * MD5 is a widely used hashing function that produces a 128-bit hash value
    * MD5 is uniformly distributed
    * Alternatively, we could also take the MD5 hash of randomly-generated data
* [**Base 62**](https://www.kerstner.at/2012/07/shortening-strings-using-base-62-encoding/) encode the MD5 hash
    * Base 62 encodes to `[a-zA-Z0-9]` which works well for urls, eliminating the need for escaping special characters
    * There is only one hash result for the original input and Base 62 is deterministic (no randomness involved)
    * Base 64 is another popular encoding but provides issues for urls because of the additional `+` and `/` characters
    * The following [Base 62 pseudocode](http://stackoverflow.com/questions/742013/how-to-code-a-url-shortener) runs in O(k) time where k is the number of digits = 7:

```python
def base_encode(num, base=62):
    digits = []
    while num > 0
      remainder = modulo(num, base)
      digits.push(remainder)
      num = divide(num, base)
    digits = digits.reverse
```

* Take the first 7 characters of the output, which results in 62^7 possible values and should be sufficient to handle our constraint of 360 million shortlinks in 3 years:

```python
url = base_encode(md5(ip_address+timestamp))[:URL_LENGTH]
```

We'll use a public [**REST API**](https://github.com/donnemartin/system-design-primer#representational-state-transfer-rest):

```
$ curl -X POST --data '{ "expiration_length_in_minutes": "60", \
    "paste_contents": "Hello World!" }' https://pastebin.com/api/v1/paste
```

Response:

```
{
    "shortlink": "foobar"
}
```

For internal communications, we could use [Remote Procedure Calls](https://github.com/donnemartin/system-design-primer#remote-procedure-call-rpc).

### Use case: User enters a paste's url and views the contents

* The **Client** sends a get paste request to the **Web Server**
* The **Web Server** forwards the request to the **Read API** server
* The **Read API** server does the following:
    * Checks the **SQL Database** for the generated url
        * If the url is in the **SQL Database**, fetch the paste contents from the **Object Store**
        * Else, return an error message for the user

REST API:

```
$ curl https://pastebin.com/api/v1/paste?shortlink=foobar
```

Response:

```
{
    "paste_contents": "Hello World"
    "created_at": "YYYY-MM-DD HH:MM:SS"
    "expiration_length_in_minutes": "60"
}
```

### Use case: Service tracks analytics of pages

Since realtime analytics are not a requirement, we could simply **MapReduce** the **Web Server** logs to generate hit counts.

**Clarify with your interviewer how much code you are expected to write**.

```python
class HitCounts(MRJob):

    def extract_url(self, line):
        """Extract the generated url from the log line."""
        ...

    def extract_year_month(self, line):
        """Return the year and month portions of the timestamp."""
        ...

    def mapper(self, _, line):
        """Parse each log line, extract and transform relevant lines.

        Emit key value pairs of the form:

        (2016-01, url0), 1
        (2016-01, url0), 1
        (2016-01, url1), 1
        """
        url = self.extract_url(line)
        period = self.extract_year_month(line)
        yield (period, url), 1

    def reducer(self, key, values):
        """Sum values for each key.

        (2016-01, url0), 2
        (2016-01, url1), 1
        """
        yield key, sum(values)
```

### Use case: Service deletes expired pastes

To delete expired pastes, we could just scan the **SQL Database** for all entries whose expiration timestamp are older than the current timestamp.  All expired entries would then be deleted (or  marked as expired) from the table.

## Step 4: Scale the design

> Identify and address bottlenecks, given the constraints.

![Imgur](http://i.imgur.com/4edXG0T.png)

**Important: Do not simply jump right into the final design from the initial design!**

State you would do this iteratively: 1) **Benchmark/Load Test**, 2) **Profile** for bottlenecks 3) address bottlenecks while evaluating alternatives and trade-offs, and 4) repeat.  See [Design a system that scales to millions of users on AWS](../scaling_aws/README.md) as a sample on how to iteratively scale the initial design.

It's important to discuss what bottlenecks you might encounter with the initial design and how you might address each of them.  For example, what issues are addressed by adding a **Load Balancer** with multiple **Web Servers**?  **CDN**?  **Master-Slave Replicas**?  What are the alternatives and **Trade-Offs** for each?

We'll introduce some components to complete the design and to address scalability issues.  Internal load balancers are not shown to reduce clutter.

*To avoid repeating discussions*, refer to the following [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) for main talking points, tradeoffs, and alternatives:

* [DNS](https://github.com/donnemartin/system-design-primer#domain-name-system)
* [CDN](https://github.com/donnemartin/system-design-primer#content-delivery-network)
* [Load balancer](https://github.com/donnemartin/system-design-primer#load-balancer)
* [Horizontal scaling](https://github.com/donnemartin/system-design-primer#horizontal-scaling)
* [Web server (reverse proxy)](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
* [API server (application layer)](https://github.com/donnemartin/system-design-primer#application-layer)
* [Cache](https://github.com/donnemartin/system-design-primer#cache)
* [Relational database management system (RDBMS)](https://github.com/donnemartin/system-design-primer#relational-database-management-system-rdbms)
* [SQL write master-slave failover](https://github.com/donnemartin/system-design-primer#fail-over)
* [Master-slave replication](https://github.com/donnemartin/system-design-primer#master-slave-replication)
* [Consistency patterns](https://github.com/donnemartin/system-design-primer#consistency-patterns)
* [Availability patterns](https://github.com/donnemartin/system-design-primer#availability-patterns)

The **Analytics Database** could use a data warehousing solution such as Amazon Redshift or Google BigQuery.

An **Object Store** such as Amazon S3 can comfortably handle the constraint of 12.7 GB of new content per month.

To address the 40 *average* read requests per second (higher at peak), traffic for popular content should be handled by the **Memory Cache** instead of the database.  The **Memory Cache** is also useful for handling the unevenly distributed traffic and traffic spikes.  The **SQL Read Replicas** should be able to handle the cache misses, as long as the replicas are not bogged down with replicating writes.

4 *average* paste writes per second (with higher at peak) should be do-able for a single **SQL Write Master-Slave**.  Otherwise, we'll need to employ additional SQL scaling patterns:

* [Federation](https://github.com/donnemartin/system-design-primer#federation)
* [Sharding](https://github.com/donnemartin/system-design-primer#sharding)
* [Denormalization](https://github.com/donnemartin/system-design-primer#denormalization)
* [SQL Tuning](https://github.com/donnemartin/system-design-primer#sql-tuning)

We should also consider moving some data to a **NoSQL Database**.

## Additional talking points

> Additional topics to dive into, depending on the problem scope and time remaining.

#### NoSQL

* [Key-value store](https://github.com/donnemartin/system-design-primer#key-value-store)
* [Document store](https://github.com/donnemartin/system-design-primer#document-store)
* [Wide column store](https://github.com/donnemartin/system-design-primer#wide-column-store)
* [Graph database](https://github.com/donnemartin/system-design-primer#graph-database)
* [SQL vs NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql)

### Caching

* Where to cache
    * [Client caching](https://github.com/donnemartin/system-design-primer#client-caching)
    * [CDN caching](https://github.com/donnemartin/system-design-primer#cdn-caching)
    * [Web server caching](https://github.com/donnemartin/system-design-primer#web-server-caching)
    * [Database caching](https://github.com/donnemartin/system-design-primer#database-caching)
    * [Application caching](https://github.com/donnemartin/system-design-primer#application-caching)
* What to cache
    * [Caching at the database query level](https://github.com/donnemartin/system-design-primer#caching-at-the-database-query-level)
    * [Caching at the object level](https://github.com/donnemartin/system-design-primer#caching-at-the-object-level)
* When to update the cache
    * [Cache-aside](https://github.com/donnemartin/system-design-primer#cache-aside)
    * [Write-through](https://github.com/donnemartin/system-design-primer#write-through)
    * [Write-behind (write-back)](https://github.com/donnemartin/system-design-primer#write-behind-write-back)
    * [Refresh ahead](https://github.com/donnemartin/system-design-primer#refresh-ahead)

### Asynchronism and microservices

* [Message queues](https://github.com/donnemartin/system-design-primer#message-queues)
* [Task queues](https://github.com/donnemartin/system-design-primer#task-queues)
* [Back pressure](https://github.com/donnemartin/system-design-primer#back-pressure)
* [Microservices](https://github.com/donnemartin/system-design-primer#microservices)

### Communications

* Discuss tradeoffs:
    * External communication with clients - [HTTP APIs following REST](https://github.com/donnemartin/system-design-primer#representational-state-transfer-rest)
    * Internal communications - [RPC](https://github.com/donnemartin/system-design-primer#remote-procedure-call-rpc)
* [Service discovery](https://github.com/donnemartin/system-design-primer#service-discovery)

### Security

Refer to the [security section](https://github.com/donnemartin/system-design-primer#security).

### Latency numbers

See [Latency numbers every programmer should know](https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know).

### Ongoing

* Continue benchmarking and monitoring your system to address bottlenecks as they come up
* Scaling is an iterative process
# Design a key-value cache to save the results of the most recent web server queries

*Note: This document links directly to relevant areas found in the [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) to avoid duplication.  Refer to the linked content for general talking points, tradeoffs, and alternatives.*

## Step 1: Outline use cases and constraints

> Gather requirements and scope the problem.
> Ask questions to clarify use cases and constraints.
> Discuss assumptions.

Without an interviewer to address clarifying questions, we'll define some use cases and constraints.

### Use cases

#### We'll scope the problem to handle only the following use cases

* **User** sends a search request resulting in a cache hit
* **User** sends a search request resulting in a cache miss
* **Service** has high availability

### Constraints and assumptions

#### State assumptions

* Traffic is not evenly distributed
    * Popular queries should almost always be in the cache
    * Need to determine how to expire/refresh
* Serving from cache requires fast lookups
* Low latency between machines
* Limited memory in cache
    * Need to determine what to keep/remove
    * Need to cache millions of queries
* 10 million users
* 10 billion queries per month

#### Calculate usage

**Clarify with your interviewer if you should run back-of-the-envelope usage calculations.**

* Cache stores ordered list of key: query, value: results
    * `query` - 50 bytes
    * `title` - 20 bytes
    * `snippet` - 200 bytes
    * Total: 270 bytes
* 2.7 TB of cache data per month if all 10 billion queries are unique and all are stored
    * 270 bytes per search * 10 billion searches per month
    * Assumptions state limited memory, need to determine how to expire contents
* 4,000 requests per second

Handy conversion guide:

* 2.5 million seconds per month
* 1 request per second = 2.5 million requests per month
* 40 requests per second = 100 million requests per month
* 400 requests per second = 1 billion requests per month

## Step 2: Create a high level design

> Outline a high level design with all important components.

![Imgur](http://i.imgur.com/KqZ3dSx.png)

## Step 3: Design core components

> Dive into details for each core component.

### Use case: User sends a request resulting in a cache hit

Popular queries can be served from a **Memory Cache** such as Redis or Memcached to reduce read latency and to avoid overloading the **Reverse Index Service** and **Document Service**.  Reading 1 MB sequentially from memory takes about 250 microseconds, while reading from SSD takes 4x and from disk takes 80x longer.<sup><a href=https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know>1</a></sup>

Since the cache has limited capacity, we'll use a least recently used (LRU) approach to expire older entries.

* The **Client** sends a request to the **Web Server**, running as a [reverse proxy](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
* The **Web Server** forwards the request to the **Query API** server
* The **Query API** server does the following:
    * Parses the query
        * Removes markup
        * Breaks up the text into terms
        * Fixes typos
        * Normalizes capitalization
        * Converts the query to use boolean operations
    * Checks the **Memory Cache** for the content matching the query
        * If there's a hit in the **Memory Cache**, the **Memory Cache** does the following:
            * Updates the cached entry's position to the front of the LRU list
            * Returns the cached contents
        * Else, the **Query API** does the following:
            * Uses the **Reverse Index Service** to find documents matching the query
                * The **Reverse Index Service** ranks the matching results and returns the top ones
            * Uses the **Document Service** to return titles and snippets
            * Updates the **Memory Cache** with the contents, placing the entry at the front of the LRU list

#### Cache implementation

The cache can use a doubly-linked list: new items will be added to the head while items to expire will be removed from the tail.  We'll use a hash table for fast lookups to each linked list node.

**Clarify with your interviewer how much code you are expected to write**.

**Query API Server** implementation:

```python
class QueryApi(object):

    def __init__(self, memory_cache, reverse_index_service):
        self.memory_cache = memory_cache
        self.reverse_index_service = reverse_index_service

    def parse_query(self, query):
        """Remove markup, break text into terms, deal with typos,
        normalize capitalization, convert to use boolean operations.
        """
        ...

    def process_query(self, query):
        query = self.parse_query(query)
        results = self.memory_cache.get(query)
        if results is None:
            results = self.reverse_index_service.process_search(query)
            self.memory_cache.set(query, results)
        return results
```

**Node** implementation:

```python
class Node(object):

    def __init__(self, query, results):
        self.query = query
        self.results = results
```

**LinkedList** implementation:

```python
class LinkedList(object):

    def __init__(self):
        self.head = None
        self.tail = None

    def move_to_front(self, node):
        ...

    def append_to_front(self, node):
        ...

    def remove_from_tail(self):
        ...
```

**Cache** implementation:

```python
class Cache(object):

    def __init__(self, MAX_SIZE):
        self.MAX_SIZE = MAX_SIZE
        self.size = 0
        self.lookup = {}  # key: query, value: node
        self.linked_list = LinkedList()

    def get(self, query)
        """Get the stored query result from the cache.

        Accessing a node updates its position to the front of the LRU list.
        """
        node = self.lookup[query]
        if node is None:
            return None
        self.linked_list.move_to_front(node)
        return node.results

    def set(self, results, query):
        """Set the result for the given query key in the cache.

        When updating an entry, updates its position to the front of the LRU list.
        If the entry is new and the cache is at capacity, removes the oldest entry
        before the new entry is added.
        """
        node = self.lookup[query]
        if node is not None:
            # Key exists in cache, update the value
            node.results = results
            self.linked_list.move_to_front(node)
        else:
            # Key does not exist in cache
            if self.size == self.MAX_SIZE:
                # Remove the oldest entry from the linked list and lookup
                self.lookup.pop(self.linked_list.tail.query, None)
                self.linked_list.remove_from_tail()
            else:
                self.size += 1
            # Add the new key and value
            new_node = Node(query, results)
            self.linked_list.append_to_front(new_node)
            self.lookup[query] = new_node
```

#### When to update the cache

The cache should be updated when:

* The page contents change
* The page is removed or a new page is added
* The page rank changes

The most straightforward way to handle these cases is to simply set a max time that a cached entry can stay in the cache before it is updated, usually referred to as time to live (TTL).

Refer to [When to update the cache](https://github.com/donnemartin/system-design-primer#when-to-update-the-cache) for tradeoffs and alternatives.  The approach above describes [cache-aside](https://github.com/donnemartin/system-design-primer#cache-aside).

## Step 4: Scale the design

> Identify and address bottlenecks, given the constraints.

![Imgur](http://i.imgur.com/4j99mhe.png)

**Important: Do not simply jump right into the final design from the initial design!**

State you would 1) **Benchmark/Load Test**, 2) **Profile** for bottlenecks 3) address bottlenecks while evaluating alternatives and trade-offs, and 4) repeat.  See [Design a system that scales to millions of users on AWS](../scaling_aws/README.md) as a sample on how to iteratively scale the initial design.

It's important to discuss what bottlenecks you might encounter with the initial design and how you might address each of them.  For example, what issues are addressed by adding a **Load Balancer** with multiple **Web Servers**?  **CDN**?  **Master-Slave Replicas**?  What are the alternatives and **Trade-Offs** for each?

We'll introduce some components to complete the design and to address scalability issues.  Internal load balancers are not shown to reduce clutter.

*To avoid repeating discussions*, refer to the following [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) for main talking points, tradeoffs, and alternatives:

* [DNS](https://github.com/donnemartin/system-design-primer#domain-name-system)
* [Load balancer](https://github.com/donnemartin/system-design-primer#load-balancer)
* [Horizontal scaling](https://github.com/donnemartin/system-design-primer#horizontal-scaling)
* [Web server (reverse proxy)](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
* [API server (application layer)](https://github.com/donnemartin/system-design-primer#application-layer)
* [Cache](https://github.com/donnemartin/system-design-primer#cache)
* [Consistency patterns](https://github.com/donnemartin/system-design-primer#consistency-patterns)
* [Availability patterns](https://github.com/donnemartin/system-design-primer#availability-patterns)

### Expanding the Memory Cache to many machines

To handle the heavy request load and the large amount of memory needed, we'll scale horizontally.  We have three main options on how to store the data on our **Memory Cache** cluster:

* **Each machine in the cache cluster has its own cache** - Simple, although it will likely result in a low cache hit rate.
* **Each machine in the cache cluster has a copy of the cache** - Simple, although it is an inefficient use of memory.
* **The cache is [sharded](https://github.com/donnemartin/system-design-primer#sharding) across all machines in the cache cluster** - More complex, although it is likely the best option.  We could use hashing to determine which machine could have the cached results of a query using `machine = hash(query)`.  We'll likely want to use [consistent hashing](https://github.com/donnemartin/system-design-primer#under-development).

## Additional talking points

> Additional topics to dive into, depending on the problem scope and time remaining.

### SQL scaling patterns

* [Read replicas](https://github.com/donnemartin/system-design-primer#master-slave-replication)
* [Federation](https://github.com/donnemartin/system-design-primer#federation)
* [Sharding](https://github.com/donnemartin/system-design-primer#sharding)
* [Denormalization](https://github.com/donnemartin/system-design-primer#denormalization)
* [SQL Tuning](https://github.com/donnemartin/system-design-primer#sql-tuning)

#### NoSQL

* [Key-value store](https://github.com/donnemartin/system-design-primer#key-value-store)
* [Document store](https://github.com/donnemartin/system-design-primer#document-store)
* [Wide column store](https://github.com/donnemartin/system-design-primer#wide-column-store)
* [Graph database](https://github.com/donnemartin/system-design-primer#graph-database)
* [SQL vs NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql)

### Caching

* Where to cache
    * [Client caching](https://github.com/donnemartin/system-design-primer#client-caching)
    * [CDN caching](https://github.com/donnemartin/system-design-primer#cdn-caching)
    * [Web server caching](https://github.com/donnemartin/system-design-primer#web-server-caching)
    * [Database caching](https://github.com/donnemartin/system-design-primer#database-caching)
    * [Application caching](https://github.com/donnemartin/system-design-primer#application-caching)
* What to cache
    * [Caching at the database query level](https://github.com/donnemartin/system-design-primer#caching-at-the-database-query-level)
    * [Caching at the object level](https://github.com/donnemartin/system-design-primer#caching-at-the-object-level)
* When to update the cache
    * [Cache-aside](https://github.com/donnemartin/system-design-primer#cache-aside)
    * [Write-through](https://github.com/donnemartin/system-design-primer#write-through)
    * [Write-behind (write-back)](https://github.com/donnemartin/system-design-primer#write-behind-write-back)
    * [Refresh ahead](https://github.com/donnemartin/system-design-primer#refresh-ahead)

### Asynchronism and microservices

* [Message queues](https://github.com/donnemartin/system-design-primer#message-queues)
* [Task queues](https://github.com/donnemartin/system-design-primer#task-queues)
* [Back pressure](https://github.com/donnemartin/system-design-primer#back-pressure)
* [Microservices](https://github.com/donnemartin/system-design-primer#microservices)

### Communications

* Discuss tradeoffs:
    * External communication with clients - [HTTP APIs following REST](https://github.com/donnemartin/system-design-primer#representational-state-transfer-rest)
    * Internal communications - [RPC](https://github.com/donnemartin/system-design-primer#remote-procedure-call-rpc)
* [Service discovery](https://github.com/donnemartin/system-design-primer#service-discovery)

### Security

Refer to the [security section](https://github.com/donnemartin/system-design-primer#security).

### Latency numbers

See [Latency numbers every programmer should know](https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know).

### Ongoing

* Continue benchmarking and monitoring your system to address bottlenecks as they come up
* Scaling is an iterative process
# Design Amazon's sales rank by category feature

*Note: This document links directly to relevant areas found in the [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) to avoid duplication.  Refer to the linked content for general talking points, tradeoffs, and alternatives.*

## Step 1: Outline use cases and constraints

> Gather requirements and scope the problem.
> Ask questions to clarify use cases and constraints.
> Discuss assumptions.

Without an interviewer to address clarifying questions, we'll define some use cases and constraints.

### Use cases

#### We'll scope the problem to handle only the following use case

* **Service** calculates the past week's most popular products by category
* **User** views the past week's most popular products by category
* **Service** has high availability

#### Out of scope

* The general e-commerce site
    * Design components only for calculating sales rank

### Constraints and assumptions

#### State assumptions

* Traffic is not evenly distributed
* Items can be in multiple categories
* Items cannot change categories
* There are no subcategories ie `foo/bar/baz`
* Results must be updated hourly
    * More popular products might need to be updated more frequently
* 10 million products
* 1000 categories
* 1 billion transactions per month
* 100 billion read requests per month
* 100:1 read to write ratio

#### Calculate usage

**Clarify with your interviewer if you should run back-of-the-envelope usage calculations.**

* Size per transaction:
    * `created_at` - 5 bytes
    * `product_id` - 8 bytes
    * `category_id` - 4 bytes
    * `seller_id` - 8 bytes
    * `buyer_id` - 8 bytes
    * `quantity` - 4 bytes
    * `total_price` - 5 bytes
    * Total: ~40 bytes
* 40 GB of new transaction content per month
    * 40 bytes per transaction * 1 billion transactions per month
    * 1.44 TB of new transaction content in 3 years
    * Assume most are new transactions instead of updates to existing ones
* 400 transactions per second on average
* 40,000 read requests per second on average

Handy conversion guide:

* 2.5 million seconds per month
* 1 request per second = 2.5 million requests per month
* 40 requests per second = 100 million requests per month
* 400 requests per second = 1 billion requests per month

## Step 2: Create a high level design

> Outline a high level design with all important components.

![Imgur](http://i.imgur.com/vwMa1Qu.png)

## Step 3: Design core components

> Dive into details for each core component.

### Use case: Service calculates the past week's most popular products by category

We could store the raw **Sales API** server log files on a managed **Object Store** such as Amazon S3, rather than managing our own distributed file system.

**Clarify with your interviewer how much code you are expected to write**.

We'll assume this is a sample log entry, tab delimited:

```
timestamp   product_id  category_id    qty     total_price   seller_id    buyer_id
t1          product1    category1      2       20.00         1            1
t2          product1    category2      2       20.00         2            2
t2          product1    category2      1       10.00         2            3
t3          product2    category1      3        7.00         3            4
t4          product3    category2      7        2.00         4            5
t5          product4    category1      1        5.00         5            6
...
```

The **Sales Rank Service** could use **MapReduce**, using the **Sales API** server log files as input and writing the results to an aggregate table `sales_rank` in a **SQL Database**.  We should discuss the [use cases and tradeoffs between choosing SQL or NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql).

We'll use a multi-step **MapReduce**:

* **Step 1** - Transform the data to `(category, product_id), sum(quantity)`
* **Step 2** - Perform a distributed sort

```python
class SalesRanker(MRJob):

    def within_past_week(self, timestamp):
        """Return True if timestamp is within past week, False otherwise."""
        ...

    def mapper(self, _ line):
        """Parse each log line, extract and transform relevant lines.

        Emit key value pairs of the form:

        (category1, product1), 2
        (category2, product1), 2
        (category2, product1), 1
        (category1, product2), 3
        (category2, product3), 7
        (category1, product4), 1
        """
        timestamp, product_id, category_id, quantity, total_price, seller_id, \
            buyer_id = line.split('\t')
        if self.within_past_week(timestamp):
            yield (category_id, product_id), quantity

    def reducer(self, key, value):
        """Sum values for each key.

        (category1, product1), 2
        (category2, product1), 3
        (category1, product2), 3
        (category2, product3), 7
        (category1, product4), 1
        """
        yield key, sum(values)

    def mapper_sort(self, key, value):
        """Construct key to ensure proper sorting.

        Transform key and value to the form:

        (category1, 2), product1
        (category2, 3), product1
        (category1, 3), product2
        (category2, 7), product3
        (category1, 1), product4

        The shuffle/sort step of MapReduce will then do a
        distributed sort on the keys, resulting in:

        (category1, 1), product4
        (category1, 2), product1
        (category1, 3), product2
        (category2, 3), product1
        (category2, 7), product3
        """
        category_id, product_id = key
        quantity = value
        yield (category_id, quantity), product_id

    def reducer_identity(self, key, value):
        yield key, value

    def steps(self):
        """Run the map and reduce steps."""
        return [
            self.mr(mapper=self.mapper,
                    reducer=self.reducer),
            self.mr(mapper=self.mapper_sort,
                    reducer=self.reducer_identity),
        ]
```

The result would be the following sorted list, which we could insert into the `sales_rank` table:

```
(category1, 1), product4
(category1, 2), product1
(category1, 3), product2
(category2, 3), product1
(category2, 7), product3
```

The `sales_rank` table could have the following structure:

```
id int NOT NULL AUTO_INCREMENT
category_id int NOT NULL
total_sold int NOT NULL
product_id int NOT NULL
PRIMARY KEY(id)
FOREIGN KEY(category_id) REFERENCES Categories(id)
FOREIGN KEY(product_id) REFERENCES Products(id)
```

We'll create an [index](https://github.com/donnemartin/system-design-primer#use-good-indices) on `id `, `category_id`, and `product_id` to speed up lookups (log-time instead of scanning the entire table) and to keep the data in memory.  Reading 1 MB sequentially from memory takes about 250 microseconds, while reading from SSD takes 4x and from disk takes 80x longer.<sup><a href=https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know>1</a></sup>

### Use case: User views the past week's most popular products by category

* The **Client** sends a request to the **Web Server**, running as a [reverse proxy](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
* The **Web Server** forwards the request to the **Read API** server
* The **Read API** server reads from the **SQL Database** `sales_rank` table

We'll use a public [**REST API**](https://github.com/donnemartin/system-design-primer#representational-state-transfer-rest):

```
$ curl https://amazon.com/api/v1/popular?category_id=1234
```

Response:

```
{
    "id": "100",
    "category_id": "1234",
    "total_sold": "100000",
    "product_id": "50",
},
{
    "id": "53",
    "category_id": "1234",
    "total_sold": "90000",
    "product_id": "200",
},
{
    "id": "75",
    "category_id": "1234",
    "total_sold": "80000",
    "product_id": "3",
},
```

For internal communications, we could use [Remote Procedure Calls](https://github.com/donnemartin/system-design-primer#remote-procedure-call-rpc).

## Step 4: Scale the design

> Identify and address bottlenecks, given the constraints.

![Imgur](http://i.imgur.com/MzExP06.png)

**Important: Do not simply jump right into the final design from the initial design!**

State you would 1) **Benchmark/Load Test**, 2) **Profile** for bottlenecks 3) address bottlenecks while evaluating alternatives and trade-offs, and 4) repeat.  See [Design a system that scales to millions of users on AWS](../scaling_aws/README.md) as a sample on how to iteratively scale the initial design.

It's important to discuss what bottlenecks you might encounter with the initial design and how you might address each of them.  For example, what issues are addressed by adding a **Load Balancer** with multiple **Web Servers**?  **CDN**?  **Master-Slave Replicas**?  What are the alternatives and **Trade-Offs** for each?

We'll introduce some components to complete the design and to address scalability issues.  Internal load balancers are not shown to reduce clutter.

*To avoid repeating discussions*, refer to the following [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) for main talking points, tradeoffs, and alternatives:

* [DNS](https://github.com/donnemartin/system-design-primer#domain-name-system)
* [CDN](https://github.com/donnemartin/system-design-primer#content-delivery-network)
* [Load balancer](https://github.com/donnemartin/system-design-primer#load-balancer)
* [Horizontal scaling](https://github.com/donnemartin/system-design-primer#horizontal-scaling)
* [Web server (reverse proxy)](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
* [API server (application layer)](https://github.com/donnemartin/system-design-primer#application-layer)
* [Cache](https://github.com/donnemartin/system-design-primer#cache)
* [Relational database management system (RDBMS)](https://github.com/donnemartin/system-design-primer#relational-database-management-system-rdbms)
* [SQL write master-slave failover](https://github.com/donnemartin/system-design-primer#fail-over)
* [Master-slave replication](https://github.com/donnemartin/system-design-primer#master-slave-replication)
* [Consistency patterns](https://github.com/donnemartin/system-design-primer#consistency-patterns)
* [Availability patterns](https://github.com/donnemartin/system-design-primer#availability-patterns)

The **Analytics Database** could use a data warehousing solution such as Amazon Redshift or Google BigQuery.

We might only want to store a limited time period of data in the database, while storing the rest in a data warehouse or in an **Object Store**.  An **Object Store** such as Amazon S3 can comfortably handle the constraint of 40 GB of new content per month.

To address the 40,000 *average* read requests per second (higher at peak), traffic for popular content (and their sales rank) should be handled by the **Memory Cache** instead of the database.  The **Memory Cache** is also useful for handling the unevenly distributed traffic and traffic spikes.  With the large volume of reads, the **SQL Read Replicas** might not be able to handle the cache misses.  We'll probably need to employ additional SQL scaling patterns.

400 *average* writes per second (higher at peak) might be tough for a single **SQL Write Master-Slave**, also pointing to a need for additional scaling techniques.

SQL scaling patterns include:

* [Federation](https://github.com/donnemartin/system-design-primer#federation)
* [Sharding](https://github.com/donnemartin/system-design-primer#sharding)
* [Denormalization](https://github.com/donnemartin/system-design-primer#denormalization)
* [SQL Tuning](https://github.com/donnemartin/system-design-primer#sql-tuning)

We should also consider moving some data to a **NoSQL Database**.

## Additional talking points

> Additional topics to dive into, depending on the problem scope and time remaining.

#### NoSQL

* [Key-value store](https://github.com/donnemartin/system-design-primer#key-value-store)
* [Document store](https://github.com/donnemartin/system-design-primer#document-store)
* [Wide column store](https://github.com/donnemartin/system-design-primer#wide-column-store)
* [Graph database](https://github.com/donnemartin/system-design-primer#graph-database)
* [SQL vs NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql)

### Caching

* Where to cache
    * [Client caching](https://github.com/donnemartin/system-design-primer#client-caching)
    * [CDN caching](https://github.com/donnemartin/system-design-primer#cdn-caching)
    * [Web server caching](https://github.com/donnemartin/system-design-primer#web-server-caching)
    * [Database caching](https://github.com/donnemartin/system-design-primer#database-caching)
    * [Application caching](https://github.com/donnemartin/system-design-primer#application-caching)
* What to cache
    * [Caching at the database query level](https://github.com/donnemartin/system-design-primer#caching-at-the-database-query-level)
    * [Caching at the object level](https://github.com/donnemartin/system-design-primer#caching-at-the-object-level)
* When to update the cache
    * [Cache-aside](https://github.com/donnemartin/system-design-primer#cache-aside)
    * [Write-through](https://github.com/donnemartin/system-design-primer#write-through)
    * [Write-behind (write-back)](https://github.com/donnemartin/system-design-primer#write-behind-write-back)
    * [Refresh ahead](https://github.com/donnemartin/system-design-primer#refresh-ahead)

### Asynchronism and microservices

* [Message queues](https://github.com/donnemartin/system-design-primer#message-queues)
* [Task queues](https://github.com/donnemartin/system-design-primer#task-queues)
* [Back pressure](https://github.com/donnemartin/system-design-primer#back-pressure)
* [Microservices](https://github.com/donnemartin/system-design-primer#microservices)

### Communications

* Discuss tradeoffs:
    * External communication with clients - [HTTP APIs following REST](https://github.com/donnemartin/system-design-primer#representational-state-transfer-rest)
    * Internal communications - [RPC](https://github.com/donnemartin/system-design-primer#remote-procedure-call-rpc)
* [Service discovery](https://github.com/donnemartin/system-design-primer#service-discovery)

### Security

Refer to the [security section](https://github.com/donnemartin/system-design-primer#security).

### Latency numbers

See [Latency numbers every programmer should know](https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know).

### Ongoing

* Continue benchmarking and monitoring your system to address bottlenecks as they come up
* Scaling is an iterative process
# Design a system that scales to millions of users on AWS

*Note: This document links directly to relevant areas found in the [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) to avoid duplication.  Refer to the linked content for general talking points, tradeoffs, and alternatives.*

## Step 1: Outline use cases and constraints

> Gather requirements and scope the problem.
> Ask questions to clarify use cases and constraints.
> Discuss assumptions.

Without an interviewer to address clarifying questions, we'll define some use cases and constraints.

### Use cases

Solving this problem takes an iterative approach of: 1) **Benchmark/Load Test**, 2) **Profile** for bottlenecks 3) address bottlenecks while evaluating alternatives and trade-offs, and 4) repeat, which is good pattern for evolving basic designs to scalable designs.

Unless you have a background in AWS or are applying for a position that requires AWS knowledge, AWS-specific details are not a requirement.  However, **much of the principles discussed in this exercise can apply more generally outside of the AWS ecosystem.**

#### We'll scope the problem to handle only the following use cases

* **User** makes a read or write request
    * **Service** does processing, stores user data, then returns the results
* **Service** needs to evolve from serving a small amount of users to millions of users
    * Discuss general scaling patterns as we evolve an architecture to handle a large number of users and requests
* **Service** has high availability

### Constraints and assumptions

#### State assumptions

* Traffic is not evenly distributed
* Need for relational data
* Scale from 1 user to tens of millions of users
    * Denote increase of users as:
        * Users+
        * Users++
        * Users+++
        * ...
    * 10 million users
    * 1 billion writes per month
    * 100 billion reads per month
    * 100:1 read to write ratio
    * 1 KB content per write

#### Calculate usage

**Clarify with your interviewer if you should run back-of-the-envelope usage calculations.**

* 1 TB of new content per month
    * 1 KB per write * 1 billion writes per month
    * 36 TB of new content in 3 years
    * Assume most writes are from new content instead of updates to existing ones
* 400 writes per second on average
* 40,000 reads per second on average

Handy conversion guide:

* 2.5 million seconds per month
* 1 request per second = 2.5 million requests per month
* 40 requests per second = 100 million requests per month
* 400 requests per second = 1 billion requests per month

## Step 2: Create a high level design

> Outline a high level design with all important components.

![Imgur](http://i.imgur.com/B8LDKD7.png)

## Step 3: Design core components

> Dive into details for each core component.

### Use case: User makes a read or write request

#### Goals

* With only 1-2 users, you only need a basic setup
    * Single box for simplicity
    * Vertical scaling when needed
    * Monitor to determine bottlenecks

#### Start with a single box

* **Web server** on EC2
    * Storage for user data
    * [**MySQL Database**](https://github.com/donnemartin/system-design-primer#relational-database-management-system-rdbms)

Use **Vertical Scaling**:

* Simply choose a bigger box
* Keep an eye on metrics to determine how to scale up
    * Use basic monitoring to determine bottlenecks: CPU, memory, IO, network, etc
    * CloudWatch, top, nagios, statsd, graphite, etc
* Scaling vertically can get very expensive
* No redundancy/failover

*Trade-offs, alternatives, and additional details:*

* The alternative to **Vertical Scaling** is [**Horizontal scaling**](https://github.com/donnemartin/system-design-primer#horizontal-scaling)

#### Start with SQL, consider NoSQL

The constraints assume there is a need for relational data.  We can start off using a **MySQL Database** on the single box.

*Trade-offs, alternatives, and additional details:*

* See the [Relational database management system (RDBMS)](https://github.com/donnemartin/system-design-primer#relational-database-management-system-rdbms) section
* Discuss reasons to use [SQL or NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql)

#### Assign a public static IP

* Elastic IPs provide a public endpoint whose IP doesn't change on reboot
* Helps with failover, just point the domain to a new IP

#### Use a DNS

Add a **DNS** such as Route 53 to map the domain to the instance's public IP.

*Trade-offs, alternatives, and additional details:*

* See the [Domain name system](https://github.com/donnemartin/system-design-primer#domain-name-system) section

#### Secure the web server

* Open up only necessary ports
    * Allow the web server to respond to incoming requests from:
        * 80 for HTTP
        * 443 for HTTPS
        * 22 for SSH to only whitelisted IPs
    * Prevent the web server from initiating outbound connections

*Trade-offs, alternatives, and additional details:*

* See the [Security](https://github.com/donnemartin/system-design-primer#security) section

## Step 4: Scale the design

> Identify and address bottlenecks, given the constraints.

### Users+

![Imgur](http://i.imgur.com/rrfjMXB.png)

#### Assumptions

Our user count is starting to pick up and the load is increasing on our single box.  Our **Benchmarks/Load Tests** and **Profiling** are pointing to the **MySQL Database** taking up more and more memory and CPU resources, while the user content is filling up disk space.

We've been able to address these issues with **Vertical Scaling** so far.  Unfortunately, this has become quite expensive and it doesn't allow for independent scaling of the **MySQL Database** and **Web Server**.

#### Goals

* Lighten load on the single box and allow for independent scaling
    * Store static content separately in an **Object Store**
    * Move the **MySQL Database** to a separate box
* Disadvantages
    * These changes would increase complexity and would require changes to the **Web Server** to point to the **Object Store** and the **MySQL Database**
    * Additional security measures must be taken to secure the new components
    * AWS costs could also increase, but should be weighed with the costs of managing similar systems on your own

#### Store static content separately

* Consider using a managed **Object Store** like S3 to store static content
    * Highly scalable and reliable
    * Server side encryption
* Move static content to S3
    * User files
    * JS
    * CSS
    * Images
    * Videos

#### Move the MySQL database to a separate box

* Consider using a service like RDS to manage the **MySQL Database**
    * Simple to administer, scale
    * Multiple availability zones
    * Encryption at rest

#### Secure the system

* Encrypt data in transit and at rest
* Use a Virtual Private Cloud
    * Create a public subnet for the single **Web Server** so it can send and receive traffic from the internet
    * Create a private subnet for everything else, preventing outside access
    * Only open ports from whitelisted IPs for each component
* These same patterns should be implemented for new components in the remainder of the exercise

*Trade-offs, alternatives, and additional details:*

* See the [Security](https://github.com/donnemartin/system-design-primer#security) section

### Users++

![Imgur](http://i.imgur.com/raoFTXM.png)

#### Assumptions

Our **Benchmarks/Load Tests** and **Profiling** show that our single **Web Server** bottlenecks during peak hours, resulting in slow responses and in some cases, downtime.  As the service matures, we'd also like to move towards higher availability and redundancy.

#### Goals

* The following goals attempt to address the scaling issues with the **Web Server**
    * Based on the **Benchmarks/Load Tests** and **Profiling**, you might only need to implement one or two of these techniques
* Use [**Horizontal Scaling**](https://github.com/donnemartin/system-design-primer#horizontal-scaling) to handle increasing loads and to address single points of failure
    * Add a [**Load Balancer**](https://github.com/donnemartin/system-design-primer#load-balancer) such as Amazon's ELB or HAProxy
        * ELB is highly available
        * If you are configuring your own **Load Balancer**, setting up multiple servers in [active-active](https://github.com/donnemartin/system-design-primer#active-active) or [active-passive](https://github.com/donnemartin/system-design-primer#active-passive) in multiple availability zones will improve availability
        * Terminate SSL on the **Load Balancer** to reduce computational load on backend servers and to simplify certificate administration
    * Use multiple **Web Servers** spread out over multiple availability zones
    * Use multiple **MySQL** instances in [**Master-Slave Failover**](https://github.com/donnemartin/system-design-primer#master-slave-replication) mode across multiple availability zones to improve redundancy
* Separate out the **Web Servers** from the [**Application Servers**](https://github.com/donnemartin/system-design-primer#application-layer)
    * Scale and configure both layers independently
    * **Web Servers** can run as a [**Reverse Proxy**](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
    * For example, you can add **Application Servers** handling **Read APIs** while others handle **Write APIs**
* Move static (and some dynamic) content to a [**Content Delivery Network (CDN)**](https://github.com/donnemartin/system-design-primer#content-delivery-network) such as CloudFront to reduce load and latency

*Trade-offs, alternatives, and additional details:*

* See the linked content above for details

### Users+++

![Imgur](http://i.imgur.com/OZCxJr0.png)

**Note:** **Internal Load Balancers** not shown to reduce clutter

#### Assumptions

Our **Benchmarks/Load Tests** and **Profiling** show that we are read-heavy (100:1 with writes) and our database is suffering from poor performance from the high read requests.

#### Goals

* The following goals attempt to address the scaling issues with the **MySQL Database**
    * Based on the **Benchmarks/Load Tests** and **Profiling**, you might only need to implement one or two of these techniques
* Move the following data to a [**Memory Cache**](https://github.com/donnemartin/system-design-primer#cache) such as Elasticache to reduce load and latency:
    * Frequently accessed content from **MySQL**
        * First, try to configure the **MySQL Database** cache to see if that is sufficient to relieve the bottleneck before implementing a **Memory Cache**
    * Session data from the **Web Servers**
        * The **Web Servers** become stateless, allowing for **Autoscaling**
    * Reading 1 MB sequentially from memory takes about 250 microseconds, while reading from SSD takes 4x and from disk takes 80x longer.<sup><a href=https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know>1</a></sup>
* Add [**MySQL Read Replicas**](https://github.com/donnemartin/system-design-primer#master-slave-replication) to reduce load on the write master
* Add more **Web Servers** and **Application Servers** to improve responsiveness

*Trade-offs, alternatives, and additional details:*

* See the linked content above for details

#### Add MySQL read replicas

* In addition to adding and scaling a **Memory Cache**, **MySQL Read Replicas** can also help relieve load on the **MySQL Write Master**
* Add logic to **Web Server** to separate out writes and reads
* Add **Load Balancers** in front of **MySQL Read Replicas** (not pictured to reduce clutter)
* Most services are read-heavy vs write-heavy

*Trade-offs, alternatives, and additional details:*

* See the [Relational database management system (RDBMS)](https://github.com/donnemartin/system-design-primer#relational-database-management-system-rdbms) section

### Users++++

![Imgur](http://i.imgur.com/3X8nmdL.png)

#### Assumptions

Our **Benchmarks/Load Tests** and **Profiling** show that our traffic spikes during regular business hours in the U.S. and drop significantly when users leave the office.  We think we can cut costs by automatically spinning up and down servers based on actual load.  We're a small shop so we'd like to automate as much of the DevOps as possible for **Autoscaling** and for the general operations.

#### Goals

* Add **Autoscaling** to provision capacity as needed
    * Keep up with traffic spikes
    * Reduce costs by powering down unused instances
* Automate DevOps
    * Chef, Puppet, Ansible, etc
* Continue monitoring metrics to address bottlenecks
    * **Host level** - Review a single EC2 instance
    * **Aggregate level** - Review load balancer stats
    * **Log analysis** - CloudWatch, CloudTrail, Loggly, Splunk, Sumo
    * **External site performance** - Pingdom or New Relic
    * **Handle notifications and incidents** - PagerDuty
    * **Error Reporting** - Sentry

#### Add autoscaling

* Consider a managed service such as AWS **Autoscaling**
    * Create one group for each **Web Server** and one for each **Application Server** type, place each group in multiple availability zones
    * Set a min and max number of instances
    * Trigger to scale up and down through CloudWatch
        * Simple time of day metric for predictable loads or
        * Metrics over a time period:
            * CPU load
            * Latency
            * Network traffic
            * Custom metric
    * Disadvantages
        * Autoscaling can introduce complexity
        * It could take some time before a system appropriately scales up to meet increased demand, or to scale down when demand drops

### Users+++++

![Imgur](http://i.imgur.com/jj3A5N8.png)

**Note:** **Autoscaling** groups not shown to reduce clutter

#### Assumptions

As the service continues to grow towards the figures outlined in the constraints, we iteratively run **Benchmarks/Load Tests** and **Profiling** to uncover and address new bottlenecks.

#### Goals

We'll continue to address scaling issues due to the problem's constraints:

* If our **MySQL Database** starts to grow too large, we might consider only storing a limited time period of data in the database, while storing the rest in a data warehouse such as Redshift
    * A data warehouse such as Redshift can comfortably handle the constraint of 1 TB of new content per month
* With 40,000 average read requests per second, read traffic for popular content can be addressed by scaling the **Memory Cache**, which is also useful for handling the unevenly distributed traffic and traffic spikes
    * The **SQL Read Replicas** might have trouble handling the cache misses, we'll probably need to employ additional SQL scaling patterns
* 400 average writes per second (with presumably significantly higher peaks) might be tough for a single **SQL Write Master-Slave**, also pointing to a need for additional scaling techniques

SQL scaling patterns include:

* [Federation](https://github.com/donnemartin/system-design-primer#federation)
* [Sharding](https://github.com/donnemartin/system-design-primer#sharding)
* [Denormalization](https://github.com/donnemartin/system-design-primer#denormalization)
* [SQL Tuning](https://github.com/donnemartin/system-design-primer#sql-tuning)

To further address the high read and write requests, we should also consider moving appropriate data to a [**NoSQL Database**](https://github.com/donnemartin/system-design-primer#nosql) such as DynamoDB.

We can further separate out our [**Application Servers**](https://github.com/donnemartin/system-design-primer#application-layer) to allow for independent scaling.  Batch processes or computations that do not need to be done in real-time can be done [**Asynchronously**](https://github.com/donnemartin/system-design-primer#asynchronism) with **Queues** and **Workers**:

* For example, in a photo service, the photo upload and the thumbnail creation can be separated:
    * **Client** uploads photo
    * **Application Server** puts a job in a **Queue** such as SQS
    * The **Worker Service** on EC2 or Lambda pulls work off the **Queue** then:
        * Creates a thumbnail
        * Updates a **Database**
        * Stores the thumbnail in the **Object Store**

*Trade-offs, alternatives, and additional details:*

* See the linked content above for details

## Additional talking points

> Additional topics to dive into, depending on the problem scope and time remaining.

### SQL scaling patterns

* [Read replicas](https://github.com/donnemartin/system-design-primer#master-slave-replication)
* [Federation](https://github.com/donnemartin/system-design-primer#federation)
* [Sharding](https://github.com/donnemartin/system-design-primer#sharding)
* [Denormalization](https://github.com/donnemartin/system-design-primer#denormalization)
* [SQL Tuning](https://github.com/donnemartin/system-design-primer#sql-tuning)

#### NoSQL

* [Key-value store](https://github.com/donnemartin/system-design-primer#key-value-store)
* [Document store](https://github.com/donnemartin/system-design-primer#document-store)
* [Wide column store](https://github.com/donnemartin/system-design-primer#wide-column-store)
* [Graph database](https://github.com/donnemartin/system-design-primer#graph-database)
* [SQL vs NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql)

### Caching

* Where to cache
    * [Client caching](https://github.com/donnemartin/system-design-primer#client-caching)
    * [CDN caching](https://github.com/donnemartin/system-design-primer#cdn-caching)
    * [Web server caching](https://github.com/donnemartin/system-design-primer#web-server-caching)
    * [Database caching](https://github.com/donnemartin/system-design-primer#database-caching)
    * [Application caching](https://github.com/donnemartin/system-design-primer#application-caching)
* What to cache
    * [Caching at the database query level](https://github.com/donnemartin/system-design-primer#caching-at-the-database-query-level)
    * [Caching at the object level](https://github.com/donnemartin/system-design-primer#caching-at-the-object-level)
* When to update the cache
    * [Cache-aside](https://github.com/donnemartin/system-design-primer#cache-aside)
    * [Write-through](https://github.com/donnemartin/system-design-primer#write-through)
    * [Write-behind (write-back)](https://github.com/donnemartin/system-design-primer#write-behind-write-back)
    * [Refresh ahead](https://github.com/donnemartin/system-design-primer#refresh-ahead)

### Asynchronism and microservices

* [Message queues](https://github.com/donnemartin/system-design-primer#message-queues)
* [Task queues](https://github.com/donnemartin/system-design-primer#task-queues)
* [Back pressure](https://github.com/donnemartin/system-design-primer#back-pressure)
* [Microservices](https://github.com/donnemartin/system-design-primer#microservices)

### Communications

* Discuss tradeoffs:
    * External communication with clients - [HTTP APIs following REST](https://github.com/donnemartin/system-design-primer#representational-state-transfer-rest)
    * Internal communications - [RPC](https://github.com/donnemartin/system-design-primer#remote-procedure-call-rpc)
* [Service discovery](https://github.com/donnemartin/system-design-primer#service-discovery)

### Security

Refer to the [security section](https://github.com/donnemartin/system-design-primer#security).

### Latency numbers

See [Latency numbers every programmer should know](https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know).

### Ongoing

* Continue benchmarking and monitoring your system to address bottlenecks as they come up
* Scaling is an iterative process
# Design the data structures for a social network

*Note: This document links directly to relevant areas found in the [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) to avoid duplication.  Refer to the linked content for general talking points, tradeoffs, and alternatives.*

## Step 1: Outline use cases and constraints

> Gather requirements and scope the problem.
> Ask questions to clarify use cases and constraints.
> Discuss assumptions.

Without an interviewer to address clarifying questions, we'll define some use cases and constraints.

### Use cases

#### We'll scope the problem to handle only the following use cases

* **User** searches for someone and sees the shortest path to the searched person
* **Service** has high availability

### Constraints and assumptions

#### State assumptions

* Traffic is not evenly distributed
    * Some searches are more popular than others, while others are only executed once
* Graph data won't fit on a single machine
* Graph edges are unweighted
* 100 million users
* 50 friends per user average
* 1 billion friend searches per month

Exercise the use of more traditional systems - don't use graph-specific solutions such as [GraphQL](http://graphql.org/) or a graph database like [Neo4j](https://neo4j.com/)

#### Calculate usage

**Clarify with your interviewer if you should run back-of-the-envelope usage calculations.**

* 5 billion friend relationships
    * 100 million users * 50 friends per user average
* 400 search requests per second

Handy conversion guide:

* 2.5 million seconds per month
* 1 request per second = 2.5 million requests per month
* 40 requests per second = 100 million requests per month
* 400 requests per second = 1 billion requests per month

## Step 2: Create a high level design

> Outline a high level design with all important components.

![Imgur](http://i.imgur.com/wxXyq2J.png)

## Step 3: Design core components

> Dive into details for each core component.

### Use case: User searches for someone and sees the shortest path to the searched person

**Clarify with your interviewer how much code you are expected to write**.

Without the constraint of millions of users (vertices) and billions of friend relationships (edges), we could solve this unweighted shortest path task with a general BFS approach:

```python
class Graph(Graph):

    def shortest_path(self, source, dest):
        if source is None or dest is None:
            return None
        if source is dest:
            return [source.key]
        prev_node_keys = self._shortest_path(source, dest)
        if prev_node_keys is None:
            return None
        else:
            path_ids = [dest.key]
            prev_node_key = prev_node_keys[dest.key]
            while prev_node_key is not None:
                path_ids.append(prev_node_key)
                prev_node_key = prev_node_keys[prev_node_key]
            return path_ids[::-1]

    def _shortest_path(self, source, dest):
        queue = deque()
        queue.append(source)
        prev_node_keys = {source.key: None}
        source.visit_state = State.visited
        while queue:
            node = queue.popleft()
            if node is dest:
                return prev_node_keys
            prev_node = node
            for adj_node in node.adj_nodes.values():
                if adj_node.visit_state == State.unvisited:
                    queue.append(adj_node)
                    prev_node_keys[adj_node.key] = prev_node.key
                    adj_node.visit_state = State.visited
        return None
```

We won't be able to fit all users on the same machine, we'll need to [shard](https://github.com/donnemartin/system-design-primer#sharding) users across **Person Servers** and access them with a **Lookup Service**.

* The **Client** sends a request to the **Web Server**, running as a [reverse proxy](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
* The **Web Server** forwards the request to the **Search API** server
* The **Search API** server forwards the request to the **User Graph Service**
* The **User Graph Service** does the following:
    * Uses the **Lookup Service** to find the **Person Server** where the current user's info is stored
    * Finds the appropriate **Person Server** to retrieve the current user's list of `friend_ids`
    * Runs a BFS search using the current user as the `source` and the current user's `friend_ids` as the ids for each `adjacent_node`
    * To get the `adjacent_node` from a given id:
        * The **User Graph Service** will *again* need to communicate with the **Lookup Service** to determine which **Person Server** stores the`adjacent_node` matching the given id (potential for optimization)

**Clarify with your interviewer how much code you should be writing**.

**Note**: Error handling is excluded below for simplicity.  Ask if you should code proper error handing.

**Lookup Service** implementation:

```python
class LookupService(object):

    def __init__(self):
        self.lookup = self._init_lookup()  # key: person_id, value: person_server

    def _init_lookup(self):
        ...

    def lookup_person_server(self, person_id):
        return self.lookup[person_id]
```

**Person Server** implementation:

```python
class PersonServer(object):

    def __init__(self):
        self.people = {}  # key: person_id, value: person

    def add_person(self, person):
        ...

    def people(self, ids):
        results = []
        for id in ids:
            if id in self.people:
                results.append(self.people[id])
        return results
```

**Person** implementation:

```python
class Person(object):

    def __init__(self, id, name, friend_ids):
        self.id = id
        self.name = name
        self.friend_ids = friend_ids
```

**User Graph Service** implementation:

```python
class UserGraphService(object):

    def __init__(self, lookup_service):
        self.lookup_service = lookup_service

    def person(self, person_id):
        person_server = self.lookup_service.lookup_person_server(person_id)
        return person_server.people([person_id])

    def shortest_path(self, source_key, dest_key):
        if source_key is None or dest_key is None:
            return None
        if source_key is dest_key:
            return [source_key]
        prev_node_keys = self._shortest_path(source_key, dest_key)
        if prev_node_keys is None:
            return None
        else:
            # Iterate through the path_ids backwards, starting at dest_key
            path_ids = [dest_key]
            prev_node_key = prev_node_keys[dest_key]
            while prev_node_key is not None:
                path_ids.append(prev_node_key)
                prev_node_key = prev_node_keys[prev_node_key]
            # Reverse the list since we iterated backwards
            return path_ids[::-1]

    def _shortest_path(self, source_key, dest_key, path):
        # Use the id to get the Person
        source = self.person(source_key)
        # Update our bfs queue
        queue = deque()
        queue.append(source)
        # prev_node_keys keeps track of each hop from
        # the source_key to the dest_key
        prev_node_keys = {source_key: None}
        # We'll use visited_ids to keep track of which nodes we've
        # visited, which can be different from a typical bfs where
        # this can be stored in the node itself
        visited_ids = set()
        visited_ids.add(source.id)
        while queue:
            node = queue.popleft()
            if node.key is dest_key:
                return prev_node_keys
            prev_node = node
            for friend_id in node.friend_ids:
                if friend_id not in visited_ids:
                    friend_node = self.person(friend_id)
                    queue.append(friend_node)
                    prev_node_keys[friend_id] = prev_node.key
                    visited_ids.add(friend_id)
        return None
```

We'll use a public [**REST API**](https://github.com/donnemartin/system-design-primer#representational-state-transfer-rest):

```
$ curl https://social.com/api/v1/friend_search?person_id=1234
```

Response:

```
{
    "person_id": "100",
    "name": "foo",
    "link": "https://social.com/foo",
},
{
    "person_id": "53",
    "name": "bar",
    "link": "https://social.com/bar",
},
{
    "person_id": "1234",
    "name": "baz",
    "link": "https://social.com/baz",
},
```

For internal communications, we could use [Remote Procedure Calls](https://github.com/donnemartin/system-design-primer#remote-procedure-call-rpc).

## Step 4: Scale the design

> Identify and address bottlenecks, given the constraints.

![Imgur](http://i.imgur.com/cdCv5g7.png)

**Important: Do not simply jump right into the final design from the initial design!**

State you would 1) **Benchmark/Load Test**, 2) **Profile** for bottlenecks 3) address bottlenecks while evaluating alternatives and trade-offs, and 4) repeat.  See [Design a system that scales to millions of users on AWS](../scaling_aws/README.md) as a sample on how to iteratively scale the initial design.

It's important to discuss what bottlenecks you might encounter with the initial design and how you might address each of them.  For example, what issues are addressed by adding a **Load Balancer** with multiple **Web Servers**?  **CDN**?  **Master-Slave Replicas**?  What are the alternatives and **Trade-Offs** for each?

We'll introduce some components to complete the design and to address scalability issues.  Internal load balancers are not shown to reduce clutter.

*To avoid repeating discussions*, refer to the following [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) for main talking points, tradeoffs, and alternatives:

* [DNS](https://github.com/donnemartin/system-design-primer#domain-name-system)
* [Load balancer](https://github.com/donnemartin/system-design-primer#load-balancer)
* [Horizontal scaling](https://github.com/donnemartin/system-design-primer#horizontal-scaling)
* [Web server (reverse proxy)](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
* [API server (application layer)](https://github.com/donnemartin/system-design-primer#application-layer)
* [Cache](https://github.com/donnemartin/system-design-primer#cache)
* [Consistency patterns](https://github.com/donnemartin/system-design-primer#consistency-patterns)
* [Availability patterns](https://github.com/donnemartin/system-design-primer#availability-patterns)

To address the constraint of 400 *average* read requests per second (higher at peak), person data can be served from a **Memory Cache** such as Redis or Memcached to reduce response times and to reduce traffic to downstream services.  This could be especially useful for people who do multiple searches in succession and for people who are well-connected.  Reading 1 MB sequentially from memory takes about 250 microseconds, while reading from SSD takes 4x and from disk takes 80x longer.<sup><a href=https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know>1</a></sup>

Below are further optimizations:

* Store complete or partial BFS traversals to speed up subsequent lookups in the **Memory Cache**
* Batch compute offline then store complete or partial BFS traversals to speed up subsequent lookups in a **NoSQL Database**
* Reduce machine jumps by batching together friend lookups hosted on the same **Person Server**
    * [Shard](https://github.com/donnemartin/system-design-primer#sharding) **Person Servers** by location to further improve this, as friends generally live closer to each other
* Do two BFS searches at the same time, one starting from the source, and one from the destination, then merge the two paths
* Start the BFS search from people with large numbers of friends, as they are more likely to reduce the number of [degrees of separation](https://en.wikipedia.org/wiki/Six_degrees_of_separation) between the current user and the search target
* Set a limit based on time or number of hops before asking the user if they want to continue searching, as searching could take a considerable amount of time in some cases
* Use a **Graph Database** such as [Neo4j](https://neo4j.com/) or a graph-specific query language such as [GraphQL](http://graphql.org/) (if there were no constraint preventing the use of **Graph Databases**)

## Additional talking points

> Additional topics to dive into, depending on the problem scope and time remaining.

### SQL scaling patterns

* [Read replicas](https://github.com/donnemartin/system-design-primer#master-slave-replication)
* [Federation](https://github.com/donnemartin/system-design-primer#federation)
* [Sharding](https://github.com/donnemartin/system-design-primer#sharding)
* [Denormalization](https://github.com/donnemartin/system-design-primer#denormalization)
* [SQL Tuning](https://github.com/donnemartin/system-design-primer#sql-tuning)

#### NoSQL

* [Key-value store](https://github.com/donnemartin/system-design-primer#key-value-store)
* [Document store](https://github.com/donnemartin/system-design-primer#document-store)
* [Wide column store](https://github.com/donnemartin/system-design-primer#wide-column-store)
* [Graph database](https://github.com/donnemartin/system-design-primer#graph-database)
* [SQL vs NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql)

### Caching

* Where to cache
    * [Client caching](https://github.com/donnemartin/system-design-primer#client-caching)
    * [CDN caching](https://github.com/donnemartin/system-design-primer#cdn-caching)
    * [Web server caching](https://github.com/donnemartin/system-design-primer#web-server-caching)
    * [Database caching](https://github.com/donnemartin/system-design-primer#database-caching)
    * [Application caching](https://github.com/donnemartin/system-design-primer#application-caching)
* What to cache
    * [Caching at the database query level](https://github.com/donnemartin/system-design-primer#caching-at-the-database-query-level)
    * [Caching at the object level](https://github.com/donnemartin/system-design-primer#caching-at-the-object-level)
* When to update the cache
    * [Cache-aside](https://github.com/donnemartin/system-design-primer#cache-aside)
    * [Write-through](https://github.com/donnemartin/system-design-primer#write-through)
    * [Write-behind (write-back)](https://github.com/donnemartin/system-design-primer#write-behind-write-back)
    * [Refresh ahead](https://github.com/donnemartin/system-design-primer#refresh-ahead)

### Asynchronism and microservices

* [Message queues](https://github.com/donnemartin/system-design-primer#message-queues)
* [Task queues](https://github.com/donnemartin/system-design-primer#task-queues)
* [Back pressure](https://github.com/donnemartin/system-design-primer#back-pressure)
* [Microservices](https://github.com/donnemartin/system-design-primer#microservices)

### Communications

* Discuss tradeoffs:
    * External communication with clients - [HTTP APIs following REST](https://github.com/donnemartin/system-design-primer#representational-state-transfer-rest)
    * Internal communications - [RPC](https://github.com/donnemartin/system-design-primer#remote-procedure-call-rpc)
* [Service discovery](https://github.com/donnemartin/system-design-primer#service-discovery)

### Security

Refer to the [security section](https://github.com/donnemartin/system-design-primer#security).

### Latency numbers

See [Latency numbers every programmer should know](https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know).

### Ongoing

* Continue benchmarking and monitoring your system to address bottlenecks as they come up
* Scaling is an iterative process
# Design the Twitter timeline and search

*Note: This document links directly to relevant areas found in the [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) to avoid duplication.  Refer to the linked content for general talking points, tradeoffs, and alternatives.*

**Design the Facebook feed** and **Design Facebook search** are similar questions.

## Step 1: Outline use cases and constraints

> Gather requirements and scope the problem.
> Ask questions to clarify use cases and constraints.
> Discuss assumptions.

Without an interviewer to address clarifying questions, we'll define some use cases and constraints.

### Use cases

#### We'll scope the problem to handle only the following use cases

* **User** posts a tweet
    * **Service** pushes tweets to followers, sending push notifications and emails
* **User** views the user timeline (activity from the user)
* **User** views the home timeline (activity from people the user is following)
* **User** searches keywords
* **Service** has high availability

#### Out of scope

* **Service** pushes tweets to the Twitter Firehose and other streams
* **Service** strips out tweets based on user's visibility settings
    * Hide @reply if the user is not also following the person being replied to
    * Respect 'hide retweets' setting
* Analytics

### Constraints and assumptions

#### State assumptions

General

* Traffic is not evenly distributed
* Posting a tweet should be fast
    * Fanning out a tweet to all of your followers should be fast, unless you have millions of followers
* 100 million active users
* 500 million tweets per day or 15 billion tweets per month
    * Each tweet averages a fanout of 10 deliveries
    * 5 billion total tweets delivered on fanout per day
    * 150 billion tweets delivered on fanout per month
* 250 billion read requests per month
* 10 billion searches per month

Timeline

* Viewing the timeline should be fast
* Twitter is more read heavy than write heavy
    * Optimize for fast reads of tweets
* Ingesting tweets is write heavy

Search

* Searching should be fast
* Search is read-heavy

#### Calculate usage

**Clarify with your interviewer if you should run back-of-the-envelope usage calculations.**

* Size per tweet:
    * `tweet_id` - 8 bytes
    * `user_id` - 32 bytes
    * `text` - 140 bytes
    * `media` - 10 KB average
    * Total: ~10 KB
* 150 TB of new tweet content per month
    * 10 KB per tweet * 500 million tweets per day * 30 days per month
    * 5.4 PB of new tweet content in 3 years
* 100 thousand read requests per second
    * 250 billion read requests per month * (400 requests per second / 1 billion requests per month)
* 6,000 tweets per second
    * 15 billion tweets per month * (400 requests per second / 1 billion requests per month)
* 60 thousand tweets delivered on fanout per second
    * 150 billion tweets delivered on fanout per month * (400 requests per second / 1 billion requests per month)
* 4,000 search requests per second

Handy conversion guide:

* 2.5 million seconds per month
* 1 request per second = 2.5 million requests per month
* 40 requests per second = 100 million requests per month
* 400 requests per second = 1 billion requests per month

## Step 2: Create a high level design

> Outline a high level design with all important components.

![Imgur](http://i.imgur.com/48tEA2j.png)

## Step 3: Design core components

> Dive into details for each core component.

### Use case: User posts a tweet

We could store the user's own tweets to populate the user timeline (activity from the user) in a [relational database](https://github.com/donnemartin/system-design-primer#relational-database-management-system-rdbms).  We should discuss the [use cases and tradeoffs between choosing SQL or NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql).

Delivering tweets and building the home timeline (activity from people the user is following) is trickier.  Fanning out tweets to all followers (60 thousand tweets delivered on fanout per second) will overload a traditional [relational database](https://github.com/donnemartin/system-design-primer#relational-database-management-system-rdbms).  We'll probably want to choose a data store with fast writes such as a **NoSQL database** or **Memory Cache**.  Reading 1 MB sequentially from memory takes about 250 microseconds, while reading from SSD takes 4x and from disk takes 80x longer.<sup><a href=https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know>1</a></sup>

We could store media such as photos or videos on an **Object Store**.

* The **Client** posts a tweet to the **Web Server**, running as a [reverse proxy](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
* The **Web Server** forwards the request to the **Write API** server
* The **Write API** stores the tweet in the user's timeline on a **SQL database**
* The **Write API** contacts the **Fan Out Service**, which does the following:
    * Queries the **User Graph Service** to find the user's followers stored in the **Memory Cache**
    * Stores the tweet in the *home timeline of the user's followers* in a **Memory Cache**
        * O(n) operation:  1,000 followers = 1,000 lookups and inserts
    * Stores the tweet in the **Search Index Service** to enable fast searching
    * Stores media in the **Object Store**
    * Uses the **Notification Service** to send out push notifications to followers:
        * Uses a **Queue** (not pictured) to asynchronously send out notifications

**Clarify with your interviewer how much code you are expected to write**.

If our **Memory Cache** is Redis, we could use a native Redis list with the following structure:

```
           tweet n+2                   tweet n+1                   tweet n
| 8 bytes   8 bytes  1 byte | 8 bytes   8 bytes  1 byte | 8 bytes   8 bytes  1 byte |
| tweet_id  user_id  meta   | tweet_id  user_id  meta   | tweet_id  user_id  meta   |
```

The new tweet would be placed in the **Memory Cache**, which populates user's home timeline (activity from people the user is following).

We'll use a public [**REST API**](https://github.com/donnemartin/system-design-primer#representational-state-transfer-rest):

```
$ curl -X POST --data '{ "user_id": "123", "auth_token": "ABC123", \
    "status": "hello world!", "media_ids": "ABC987" }' \
    https://twitter.com/api/v1/tweet
```

Response:

```
{
    "created_at": "Wed Sep 05 00:37:15 +0000 2012",
    "status": "hello world!",
    "tweet_id": "987",
    "user_id": "123",
    ...
}
```

For internal communications, we could use [Remote Procedure Calls](https://github.com/donnemartin/system-design-primer#remote-procedure-call-rpc).

### Use case: User views the home timeline

* The **Client** posts a home timeline request to the **Web Server**
* The **Web Server** forwards the request to the **Read API** server
* The **Read API** server contacts the **Timeline Service**, which does the following:
    * Gets the timeline data stored in the **Memory Cache**, containing tweet ids and user ids - O(1)
    * Queries the **Tweet Info Service** with a [multiget](http://redis.io/commands/mget) to obtain additional info about the tweet ids - O(n)
    * Queries the **User Info Service** with a multiget to obtain additional info about the user ids - O(n)

REST API:

```
$ curl https://twitter.com/api/v1/home_timeline?user_id=123
```

Response:

```
{
    "user_id": "456",
    "tweet_id": "123",
    "status": "foo"
},
{
    "user_id": "789",
    "tweet_id": "456",
    "status": "bar"
},
{
    "user_id": "789",
    "tweet_id": "579",
    "status": "baz"
},
```

### Use case: User views the user timeline

* The **Client** posts a user timeline request to the **Web Server**
* The **Web Server** forwards the request to the **Read API** server
* The **Read API** retrieves the user timeline from the **SQL Database**

The REST API would be similar to the home timeline, except all tweets would come from the user as opposed to the people the user is following.

### Use case: User searches keywords

* The **Client** sends a search request to the **Web Server**
* The **Web Server** forwards the request to the **Search API** server
* The **Search API** contacts the **Search Service**, which does the following:
    * Parses/tokenizes the input query, determining what needs to be searched
        * Removes markup
        * Breaks up the text into terms
        * Fixes typos
        * Normalizes capitalization
        * Converts the query to use boolean operations
    * Queries the **Search Cluster** (ie [Lucene](https://lucene.apache.org/)) for the results:
        * [Scatter gathers](https://github.com/donnemartin/system-design-primer#under-development) each server in the cluster to determine if there are any results for the query
        * Merges, ranks, sorts, and returns the results

REST API:

```
$ curl https://twitter.com/api/v1/search?query=hello+world
```

The response would be similar to that of the home timeline, except for tweets matching the given query.

## Step 4: Scale the design

> Identify and address bottlenecks, given the constraints.

![Imgur](http://i.imgur.com/jrUBAF7.png)

**Important: Do not simply jump right into the final design from the initial design!**

State you would 1) **Benchmark/Load Test**, 2) **Profile** for bottlenecks 3) address bottlenecks while evaluating alternatives and trade-offs, and 4) repeat.  See [Design a system that scales to millions of users on AWS](../scaling_aws/README.md) as a sample on how to iteratively scale the initial design.

It's important to discuss what bottlenecks you might encounter with the initial design and how you might address each of them.  For example, what issues are addressed by adding a **Load Balancer** with multiple **Web Servers**?  **CDN**?  **Master-Slave Replicas**?  What are the alternatives and **Trade-Offs** for each?

We'll introduce some components to complete the design and to address scalability issues.  Internal load balancers are not shown to reduce clutter.

*To avoid repeating discussions*, refer to the following [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) for main talking points, tradeoffs, and alternatives:

* [DNS](https://github.com/donnemartin/system-design-primer#domain-name-system)
* [CDN](https://github.com/donnemartin/system-design-primer#content-delivery-network)
* [Load balancer](https://github.com/donnemartin/system-design-primer#load-balancer)
* [Horizontal scaling](https://github.com/donnemartin/system-design-primer#horizontal-scaling)
* [Web server (reverse proxy)](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
* [API server (application layer)](https://github.com/donnemartin/system-design-primer#application-layer)
* [Cache](https://github.com/donnemartin/system-design-primer#cache)
* [Relational database management system (RDBMS)](https://github.com/donnemartin/system-design-primer#relational-database-management-system-rdbms)
* [SQL write master-slave failover](https://github.com/donnemartin/system-design-primer#fail-over)
* [Master-slave replication](https://github.com/donnemartin/system-design-primer#master-slave-replication)
* [Consistency patterns](https://github.com/donnemartin/system-design-primer#consistency-patterns)
* [Availability patterns](https://github.com/donnemartin/system-design-primer#availability-patterns)

The **Fanout Service** is a potential bottleneck.  Twitter users with millions of followers could take several minutes to have their tweets go through the fanout process.  This could lead to race conditions with @replies to the tweet, which we could mitigate by re-ordering the tweets at serve time.

We could also avoid fanning out tweets from highly-followed users.  Instead, we could search to find tweets for highly-followed users, merge the search results with the user's home timeline results, then re-order the tweets at serve time.

Additional optimizations include:

* Keep only several hundred tweets for each home timeline in the **Memory Cache**
* Keep only active users' home timeline info in the **Memory Cache**
    * If a user was not previously active in the past 30 days, we could rebuild the timeline from the **SQL Database**
        * Query the **User Graph Service** to determine who the user is following
        * Get the tweets from the **SQL Database** and add them to the **Memory Cache**
* Store only a month of tweets in the **Tweet Info Service**
* Store only active users in the **User Info Service**
* The **Search Cluster** would likely need to keep the tweets in memory to keep latency low

We'll also want to address the bottleneck with the **SQL Database**.

Although the **Memory Cache** should reduce the load on the database, it is unlikely the **SQL Read Replicas** alone would be enough to handle the cache misses.  We'll probably need to employ additional SQL scaling patterns.

The high volume of writes would overwhelm a single **SQL Write Master-Slave**, also pointing to a need for additional scaling techniques.

* [Federation](https://github.com/donnemartin/system-design-primer#federation)
* [Sharding](https://github.com/donnemartin/system-design-primer#sharding)
* [Denormalization](https://github.com/donnemartin/system-design-primer#denormalization)
* [SQL Tuning](https://github.com/donnemartin/system-design-primer#sql-tuning)

We should also consider moving some data to a **NoSQL Database**.

## Additional talking points

> Additional topics to dive into, depending on the problem scope and time remaining.

#### NoSQL

* [Key-value store](https://github.com/donnemartin/system-design-primer#key-value-store)
* [Document store](https://github.com/donnemartin/system-design-primer#document-store)
* [Wide column store](https://github.com/donnemartin/system-design-primer#wide-column-store)
* [Graph database](https://github.com/donnemartin/system-design-primer#graph-database)
* [SQL vs NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql)

### Caching

* Where to cache
    * [Client caching](https://github.com/donnemartin/system-design-primer#client-caching)
    * [CDN caching](https://github.com/donnemartin/system-design-primer#cdn-caching)
    * [Web server caching](https://github.com/donnemartin/system-design-primer#web-server-caching)
    * [Database caching](https://github.com/donnemartin/system-design-primer#database-caching)
    * [Application caching](https://github.com/donnemartin/system-design-primer#application-caching)
* What to cache
    * [Caching at the database query level](https://github.com/donnemartin/system-design-primer#caching-at-the-database-query-level)
    * [Caching at the object level](https://github.com/donnemartin/system-design-primer#caching-at-the-object-level)
* When to update the cache
    * [Cache-aside](https://github.com/donnemartin/system-design-primer#cache-aside)
    * [Write-through](https://github.com/donnemartin/system-design-primer#write-through)
    * [Write-behind (write-back)](https://github.com/donnemartin/system-design-primer#write-behind-write-back)
    * [Refresh ahead](https://github.com/donnemartin/system-design-primer#refresh-ahead)

### Asynchronism and microservices

* [Message queues](https://github.com/donnemartin/system-design-primer#message-queues)
* [Task queues](https://github.com/donnemartin/system-design-primer#task-queues)
* [Back pressure](https://github.com/donnemartin/system-design-primer#back-pressure)
* [Microservices](https://github.com/donnemartin/system-design-primer#microservices)

### Communications

* Discuss tradeoffs:
    * External communication with clients - [HTTP APIs following REST](https://github.com/donnemartin/system-design-primer#representational-state-transfer-rest)
    * Internal communications - [RPC](https://github.com/donnemartin/system-design-primer#remote-procedure-call-rpc)
* [Service discovery](https://github.com/donnemartin/system-design-primer#service-discovery)

### Security

Refer to the [security section](https://github.com/donnemartin/system-design-primer#security).

### Latency numbers

See [Latency numbers every programmer should know](https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know).

### Ongoing

* Continue benchmarking and monitoring your system to address bottlenecks as they come up
* Scaling is an iterative process
# Design a web crawler

*Note: This document links directly to relevant areas found in the [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) to avoid duplication.  Refer to the linked content for general talking points, tradeoffs, and alternatives.*

## Step 1: Outline use cases and constraints

> Gather requirements and scope the problem.
> Ask questions to clarify use cases and constraints.
> Discuss assumptions.

Without an interviewer to address clarifying questions, we'll define some use cases and constraints.

### Use cases

#### We'll scope the problem to handle only the following use cases

* **Service** crawls a list of urls:
    * Generates reverse index of words to pages containing the search terms
    * Generates titles and snippets for pages
        * Title and snippets are static, they do not change based on search query
* **User** inputs a search term and sees a list of relevant pages with titles and snippets  the crawler generated
    * Only sketch high level components and interactions for this use case, no need to go into depth
* **Service** has high availability

#### Out of scope

* Search analytics
* Personalized search results
* Page rank

### Constraints and assumptions

#### State assumptions

* Traffic is not evenly distributed
    * Some searches are very popular, while others are only executed once
* Support only anonymous users
* Generating search results should be fast
* The web crawler should not get stuck in an infinite loop
    * We get stuck in an infinite loop if the graph contains a cycle
* 1 billion links to crawl
    * Pages need to be crawled regularly to ensure freshness
    * Average refresh rate of about once per week, more frequent for popular sites
        * 4 billion links crawled each month
    * Average stored size per web page: 500 KB
        * For simplicity, count changes the same as new pages
* 100 billion searches per month

Exercise the use of more traditional systems - don't use existing systems such as [solr](http://lucene.apache.org/solr/) or [nutch](http://nutch.apache.org/).

#### Calculate usage

**Clarify with your interviewer if you should run back-of-the-envelope usage calculations.**

* 2 PB of stored page content per month
    * 500 KB per page * 4 billion links crawled per month
    * 72 PB of stored page content in 3 years
* 1,600 write requests per second
* 40,000 search requests per second

Handy conversion guide:

* 2.5 million seconds per month
* 1 request per second = 2.5 million requests per month
* 40 requests per second = 100 million requests per month
* 400 requests per second = 1 billion requests per month

## Step 2: Create a high level design

> Outline a high level design with all important components.

![Imgur](http://i.imgur.com/xjdAAUv.png)

## Step 3: Design core components

> Dive into details for each core component.

### Use case: Service crawls a list of urls

We'll assume we have an initial list of `links_to_crawl` ranked initially based on overall site popularity.  If this is not a reasonable assumption, we can seed the crawler with popular sites that link to outside content such as [Yahoo](https://www.yahoo.com/), [DMOZ](http://www.dmoz.org/), etc

We'll use a table `crawled_links` to store processed links and their page signatures.

We could store `links_to_crawl` and `crawled_links` in a key-value **NoSQL Database**.  For the ranked links in `links_to_crawl`, we could use [Redis](https://redis.io/) with sorted sets to maintain a ranking of page links.  We should discuss the [use cases and tradeoffs between choosing SQL or NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql).

* The **Crawler Service** processes each page link by doing the following in a loop:
    * Takes the top ranked page link to crawl
        * Checks `crawled_links` in the **NoSQL Database** for an entry with a similar page signature
            * If we have a similar page, reduces the priority of the page link
                * This prevents us from getting into a cycle
                * Continue
            * Else, crawls the link
                * Adds a job to the **Reverse Index Service** queue to generate a [reverse index](https://en.wikipedia.org/wiki/Search_engine_indexing)
                * Adds a job to the **Document Service** queue to generate a static title and snippet
                * Generates the page signature
                * Removes the link from `links_to_crawl` in the **NoSQL Database**
                * Inserts the page link and signature to `crawled_links` in the **NoSQL Database**

**Clarify with your interviewer how much code you are expected to write**.

`PagesDataStore` is an abstraction within the **Crawler Service** that uses the **NoSQL Database**:

```python
class PagesDataStore(object):

    def __init__(self, db);
        self.db = db
        ...

    def add_link_to_crawl(self, url):
        """Add the given link to `links_to_crawl`."""
        ...

    def remove_link_to_crawl(self, url):
        """Remove the given link from `links_to_crawl`."""
        ...

    def reduce_priority_link_to_crawl(self, url)
        """Reduce the priority of a link in `links_to_crawl` to avoid cycles."""
        ...

    def extract_max_priority_page(self):
        """Return the highest priority link in `links_to_crawl`."""
        ...

    def insert_crawled_link(self, url, signature):
        """Add the given link to `crawled_links`."""
        ...

    def crawled_similar(self, signature):
        """Determine if we've already crawled a page matching the given signature"""
        ...
```

`Page` is an abstraction within the **Crawler Service** that encapsulates a page, its contents, child urls, and signature:

```python
class Page(object):

    def __init__(self, url, contents, child_urls, signature):
        self.url = url
        self.contents = contents
        self.child_urls = child_urls
        self.signature = signature
```

`Crawler` is the main class within **Crawler Service**, composed of `Page` and `PagesDataStore`.

```python
class Crawler(object):

    def __init__(self, data_store, reverse_index_queue, doc_index_queue):
        self.data_store = data_store
        self.reverse_index_queue = reverse_index_queue
        self.doc_index_queue = doc_index_queue

    def create_signature(self, page):
        """Create signature based on url and contents."""
        ...

    def crawl_page(self, page):
        for url in page.child_urls:
            self.data_store.add_link_to_crawl(url)
        page.signature = self.create_signature(page)
        self.data_store.remove_link_to_crawl(page.url)
        self.data_store.insert_crawled_link(page.url, page.signature)

    def crawl(self):
        while True:
            page = self.data_store.extract_max_priority_page()
            if page is None:
                break
            if self.data_store.crawled_similar(page.signature):
                self.data_store.reduce_priority_link_to_crawl(page.url)
            else:
                self.crawl_page(page)
```

### Handling duplicates

We need to be careful the web crawler doesn't get stuck in an infinite loop, which happens when the graph contains a cycle.

**Clarify with your interviewer how much code you are expected to write**.

We'll want to remove duplicate urls:

* For smaller lists we could use something like `sort | unique`
* With 1 billion links to crawl, we could use **MapReduce** to output only entries that have a frequency of 1

```python
class RemoveDuplicateUrls(MRJob):

    def mapper(self, _, line):
        yield line, 1

    def reducer(self, key, values):
        total = sum(values)
        if total == 1:
            yield key, total
```

Detecting duplicate content is more complex.  We could generate a signature based on the contents of the page and compare those two signatures for similarity.  Some potential algorithms are [Jaccard index](https://en.wikipedia.org/wiki/Jaccard_index) and [cosine similarity](https://en.wikipedia.org/wiki/Cosine_similarity).

### Determining when to update the crawl results

Pages need to be crawled regularly to ensure freshness.  Crawl results could have a `timestamp` field that indicates the last time a page was crawled.  After a default time period, say one week, all pages should be refreshed.  Frequently updated or more popular sites could be refreshed in shorter intervals.

Although we won't dive into details on analytics, we could do some data mining to determine the mean time before a particular page is updated, and use that statistic to determine how often to re-crawl the page.

We might also choose to support a `Robots.txt` file that gives webmasters control of crawl frequency.

### Use case: User inputs a search term and sees a list of relevant pages with titles and snippets

* The **Client** sends a request to the **Web Server**, running as a [reverse proxy](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
* The **Web Server** forwards the request to the **Query API** server
* The **Query API** server does the following:
    * Parses the query
        * Removes markup
        * Breaks up the text into terms
        * Fixes typos
        * Normalizes capitalization
        * Converts the query to use boolean operations
    * Uses the **Reverse Index Service** to find documents matching the query
        * The **Reverse Index Service** ranks the matching results and returns the top ones
    * Uses the **Document Service** to return titles and snippets

We'll use a public [**REST API**](https://github.com/donnemartin/system-design-primer#representational-state-transfer-rest):

```
$ curl https://search.com/api/v1/search?query=hello+world
```

Response:

```
{
    "title": "foo's title",
    "snippet": "foo's snippet",
    "link": "https://foo.com",
},
{
    "title": "bar's title",
    "snippet": "bar's snippet",
    "link": "https://bar.com",
},
{
    "title": "baz's title",
    "snippet": "baz's snippet",
    "link": "https://baz.com",
},
```

For internal communications, we could use [Remote Procedure Calls](https://github.com/donnemartin/system-design-primer#remote-procedure-call-rpc).

## Step 4: Scale the design

> Identify and address bottlenecks, given the constraints.

![Imgur](http://i.imgur.com/bWxPtQA.png)

**Important: Do not simply jump right into the final design from the initial design!**

State you would 1) **Benchmark/Load Test**, 2) **Profile** for bottlenecks 3) address bottlenecks while evaluating alternatives and trade-offs, and 4) repeat.  See [Design a system that scales to millions of users on AWS](../scaling_aws/README.md) as a sample on how to iteratively scale the initial design.

It's important to discuss what bottlenecks you might encounter with the initial design and how you might address each of them.  For example, what issues are addressed by adding a **Load Balancer** with multiple **Web Servers**?  **CDN**?  **Master-Slave Replicas**?  What are the alternatives and **Trade-Offs** for each?

We'll introduce some components to complete the design and to address scalability issues.  Internal load balancers are not shown to reduce clutter.

*To avoid repeating discussions*, refer to the following [system design topics](https://github.com/donnemartin/system-design-primer#index-of-system-design-topics) for main talking points, tradeoffs, and alternatives:

* [DNS](https://github.com/donnemartin/system-design-primer#domain-name-system)
* [Load balancer](https://github.com/donnemartin/system-design-primer#load-balancer)
* [Horizontal scaling](https://github.com/donnemartin/system-design-primer#horizontal-scaling)
* [Web server (reverse proxy)](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server)
* [API server (application layer)](https://github.com/donnemartin/system-design-primer#application-layer)
* [Cache](https://github.com/donnemartin/system-design-primer#cache)
* [NoSQL](https://github.com/donnemartin/system-design-primer#nosql)
* [Consistency patterns](https://github.com/donnemartin/system-design-primer#consistency-patterns)
* [Availability patterns](https://github.com/donnemartin/system-design-primer#availability-patterns)

Some searches are very popular, while others are only executed once.  Popular queries can be served from a **Memory Cache** such as Redis or Memcached to reduce response times and to avoid overloading the **Reverse Index Service** and **Document Service**.  The **Memory Cache** is also useful for handling the unevenly distributed traffic and traffic spikes.  Reading 1 MB sequentially from memory takes about 250 microseconds, while reading from SSD takes 4x and from disk takes 80x longer.<sup><a href=https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know>1</a></sup>

Below are a few other optimizations to the **Crawling Service**:

* To handle the data size and request load, the **Reverse Index Service** and **Document Service** will likely need to make heavy use sharding and replication.
* DNS lookup can be a bottleneck, the **Crawler Service** can keep its own DNS lookup that is refreshed periodically
* The **Crawler Service** can improve performance and reduce memory usage by keeping many open connections at a time, referred to as [connection pooling](https://en.wikipedia.org/wiki/Connection_pool)
    * Switching to [UDP](https://github.com/donnemartin/system-design-primer#user-datagram-protocol-udp) could also boost performance
* Web crawling is bandwidth intensive, ensure there is enough bandwidth to sustain high throughput

## Additional talking points

> Additional topics to dive into, depending on the problem scope and time remaining.

### SQL scaling patterns

* [Read replicas](https://github.com/donnemartin/system-design-primer#master-slave-replication)
* [Federation](https://github.com/donnemartin/system-design-primer#federation)
* [Sharding](https://github.com/donnemartin/system-design-primer#sharding)
* [Denormalization](https://github.com/donnemartin/system-design-primer#denormalization)
* [SQL Tuning](https://github.com/donnemartin/system-design-primer#sql-tuning)

#### NoSQL

* [Key-value store](https://github.com/donnemartin/system-design-primer#key-value-store)
* [Document store](https://github.com/donnemartin/system-design-primer#document-store)
* [Wide column store](https://github.com/donnemartin/system-design-primer#wide-column-store)
* [Graph database](https://github.com/donnemartin/system-design-primer#graph-database)
* [SQL vs NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql)

### Caching

* Where to cache
    * [Client caching](https://github.com/donnemartin/system-design-primer#client-caching)
    * [CDN caching](https://github.com/donnemartin/system-design-primer#cdn-caching)
    * [Web server caching](https://github.com/donnemartin/system-design-primer#web-server-caching)
    * [Database caching](https://github.com/donnemartin/system-design-primer#database-caching)
    * [Application caching](https://github.com/donnemartin/system-design-primer#application-caching)
* What to cache
    * [Caching at the database query level](https://github.com/donnemartin/system-design-primer#caching-at-the-database-query-level)
    * [Caching at the object level](https://github.com/donnemartin/system-design-primer#caching-at-the-object-level)
* When to update the cache
    * [Cache-aside](https://github.com/donnemartin/system-design-primer#cache-aside)
    * [Write-through](https://github.com/donnemartin/system-design-primer#write-through)
    * [Write-behind (write-back)](https://github.com/donnemartin/system-design-primer#write-behind-write-back)
    * [Refresh ahead](https://github.com/donnemartin/system-design-primer#refresh-ahead)

### Asynchronism and microservices

* [Message queues](https://github.com/donnemartin/system-design-primer#message-queues)
* [Task queues](https://github.com/donnemartin/system-design-primer#task-queues)
* [Back pressure](https://github.com/donnemartin/system-design-primer#back-pressure)
* [Microservices](https://github.com/donnemartin/system-design-primer#microservices)

### Communications

* Discuss tradeoffs:
    * External communication with clients - [HTTP APIs following REST](https://github.com/donnemartin/system-design-primer#representational-state-transfer-rest)
    * Internal communications - [RPC](https://github.com/donnemartin/system-design-primer#remote-procedure-call-rpc)
* [Service discovery](https://github.com/donnemartin/system-design-primer#service-discovery)

### Security

Refer to the [security section](https://github.com/donnemartin/system-design-primer#security).

### Latency numbers

See [Latency numbers every programmer should know](https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know).

### Ongoing

* Continue benchmarking and monitoring your system to address bottlenecks as they come up
* Scaling is an iterative process
