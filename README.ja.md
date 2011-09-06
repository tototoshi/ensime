# ENSIME
the ENhanced Scala Interaction Mode for Emacs

# リンク
- [ Downloads ](https://github.com/aemoncannon/ensime/downloads)
- [ Manual ](http://aemon.com/file_dump/ensime_manual.html)
- [ Discussion Group ](http://groups.google.com/group/ensime?hl=en)


## Features

- エラーや警告をバッファにハイライト表示
- 任意の式の型の調査
- パッケージの閲覧
- 変数、メソッド、コンストラクタなどの補完
- クラスパスにあるシンボルのインクリメンタルサーチ
- あるシンボルに関するリファレンスを引く
- シンボルの定義元へのジャンプ
- 自動リファクタリング (名前の変更, インポート分の整理, メソッドの抽出)
- ソースの整形
- ASTに基づいた選択
- sbt, Maven, Ivyプロジェクトのサポート
- 組み込みのsbtシェル
- REPL
- デバッガ


## デモ

- [Overview (a bit out of date)](http://www.youtube.com/watch?v=A2Lai8IjLoY)
- [Searching](http://www.youtube.com/watch?v=fcgnAJz98QE)
- [Debugger Support](http://www.youtube.com/watch?v=v7-G6vD42z8)
- [Import Suggestions](http://www.youtube.com/watch?v=Ynp8Df7-paw&hd=1)



## システム要件

- Emacs 22 以上
- UnixライクなOSもしくはWindows
- Java 実行環境
- Scala 2.8.1 互換のプロジェクト


## ドキュメント
- [The ENSIME User Manual](http://aemon.com/file_dump/ensime_manual.html)


## クイックスタート

__1) scala-modeのインストール__

ENSIMEはscala-mode(及びその他のscala用モード)に敬意を表しつつ作られています・scala-modeはScalaの配布パッケージの./misc/scala-tool-support/emacs/以下にあります。以下の手順はscala-modeがすでにインストールされ、正常に動作しているものとしています。


__2) ensime-modeのインストール__

github([downloads page](http://github.com/aemoncannon/ensime/downloads)からENSIMEの配布パッケージをダウンロードします。適当なディレクトリを選んでENSIMEのパッケージを解凍してください。

以下を.emacsに追記してください。

    ;; ensimeのlispコードをロードする...
    (add-to-list 'load-path "ENSIME_ROOT/elisp/")
    (require 'ensime)

    ;; バッファがscala-modeになると必ずensime-modeになるように設定します。
    ;; 標準のscala-modeを使用していない場合、この部分には手を加える必要があるかもしれません。
    (add-hook 'scala-mode-hook 'ensime-scala-mode-hook)

    ;; MINI HOWTO:
    ;; .scala ファイルを開いて M-x ensime としてみましょう。(1つのプロジェクトにつき1回です。)


__3) パーミッションの確認__

起動スクリプト(大抵はbin/server.sh)に実行権限が付与されていることを確認してください。

__4) プロジェクトの作成__

Emacs上で M-x ensime-config-genを実行し、ミニバッファの指示に従ってあなたのプロジェクト用に.ensimeファイルを作成してください。

__5) ENSIMEの起動__

M-x ensime を実行してください。
1つのプロジェクトにつき1回だけ必要です。


## クイックスタート(開発者用)
注: この節はENSIMEそのものをハックしたい人用です。

cloneしたあとensimeを起動させるためにまず、配布されてるようなディレクトリ構造を作らなければなりません。sbtのタスク'task'を実行するとcloneしたディレクトリのルート下に'dist'というディレクトリができます。次に、上にある2.2節のインストール手順に従って、CLONE_DIR/distをENSIMEの配布パッケージのルートと取り替えてください。

私がENSIMEをハックするときのワークフローは、

- ソースファイルの編集
- 'sbt update'
- 'sbt dist'
- Stop existing ENSIME server by killing *inferior-ensime-server* buffer
- *inferior-ensime-server* バッファをkillして、起動しているENSIMEサーバを止める
- M-x ensime で ENSIMEを再起動する

