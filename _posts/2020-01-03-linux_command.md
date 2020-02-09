---
layout: post
title: "linuxで、よく忘れるコマンド"
excerpt: ""
categories: 技術
tags: [linux, tar, zip, find, screen, df, top, free, systemctl, service]
comments: false
---
<img src="{{ site.baseurl}}/images/linux_command/linux.jpg"  width="100%" height="200"><br>
<br>
## 1. はじめに
MacやWindowsなどのGUIメインのOSに慣れ、急にLinuxのターミナルに戻ると、なかなか頭の中に出てこないコマンドやパラメータがあります。  
筆者がよく使うのに忘れる（？）コマンドを、必要かつ忘れる順に紹介していきます。  
<br>

## 2. 環境
本記事は、以下の環境で動作は確認しています。

>・Amazon Linux  
・Ubuntu  

<br>

## 3. いつも忘れてしまうLinuxコマンド
大事なのに、なんでいつも出てこないんでしょう(笑)  
忘れたときに、さっと思い出すことを目的としているので、各コマンド・パラメータの説明は割愛しています。  
また、よく使われるパターンと思うもののみを載せています。  
<br>

### 圧縮・解凍
tar.gz形式で圧縮します。

```
tar cvzf {圧縮ファイル名}.tar.gz {圧縮したいフォルダ}  
```

tar.gz形式で解凍します。

```
tar xvzf {圧縮ファイル名}.tar.gz
```

zip形式で圧縮します。

```
zip -r {圧縮ファイル名} {圧縮したいフォルダ}  
```

zip形式で解凍します。

```
unzip {圧縮ファイル名}.zip
```
<br>

### ファイル・ディレクトリの検索
ファイル・ディレクトリを曖昧検索します。  
検索名に、*(ワイルドカード)を使います。

```
find {検索対象PATH} -name "{検索名}"
```

>例：ルートディレクトリ以下から、「abc」の文字列を含むファイル・ディレクトリを検索する。

```
find / -name "*abc*"
```

ファイルのみを曖昧検索します。  
検索名に、*(ワイルドカード)を使います。

```
find {検索対象PATH} -name "{検索名}" -type f
```

>例：ルートディレクトリ以下から、拡張子が「txt」のファイルを検索する。

```
find / -name "*.txt" -type f
```

ディレクトリのみを曖昧検索します。  
検索名に、*(ワイルドカード)を使います。

```
find {検索対象PATH} -name "{検索名}" -type d
```

>例：ルートディレクトリ以下から、「123」の文字列を含むディレクトリを検索する。

```
find / -name "*123*" -type -d
```
<br>

### デーモンの起動
バックグラウンドで起動するプログラムを実行します。  
操作は、ディストリビューションによって違います。  
動いたほうが正解です(笑)

デーモンを起動します。

```
systemctl start {デーモン名}
```
<center>or</center>
```
service {デーモン名} start
```

デーモンを止めます。

```
systemctl stop {デーモン名}
```
<center>or</center>
```
service {デーモン名} stop
```

デーモンを再起動します。

```
systemctl restart {デーモン名}
```
<center>or</center>
```
service {デーモン名} restart
```

自動起動の設定です。

```
systemctl enable {デーモン名}
```
<center>or</center>
```
chkconfig {デーモン名} on
```
<br>

### screen（仮想端末）
screenを使うと、SSHクライアントを中断しても、操作が再開できます。

screenを開始します。

```
screen
```

開始したscreenを中断（デタッチ）します。

```
Ctrl + a → d
※ Ctrlキーを押したまま、aキー → dキーの順番で押下する。
```

デタッチしたscreenの一覧を表示します。

```
screen -ls
```

デタッチしたscreenを再開（アタッチ）します。

```
screen -r [{ID}]
```

screenを終了します。

```
exit
```
<br>

### CPUの使用状況
CPUの使用状況を確認できます。  
Ctrl + c を押すまでトレースします。

```
top
```
<br>

### メモリーの使用状況
スワップ領域を含めた、メモリーの使用状況を確認できます。

```
free -wht
```

メモリー状況をトレースしたい場合は下記を使います。

```
free -wht -s {何秒おきに表示} -c {繰り返し数}
```

>例：3秒おきに10回表示する

```
free -wht -s 3 -c 10
```
<br>

### ディスクの使用状況
ディスクの使用を状況できます。

```
df -h
```
<br>

## 4. 終わりに
筆者がよく忘れるのは、tar.gzの圧縮・解凍パラメータです。  
ちょっと、圧縮したいだけなのに、おろおろします。  

{% include page_footer_2.md %}
