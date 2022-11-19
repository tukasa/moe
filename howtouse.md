---
title: 基本的な使い方
layout: page
date: 2022-03-30
last_modified_at: 
permalink: /howtouse/
---

## メモの作成

[Ctrl+N]でPPE(エディタ)が開く。

![PPE]({{ "/assets/images/howtouse01.png" | relative_url }})

PPEでの操作は以下。

- [Ctrl+N] 新しいメモを書く
- [Ctrl+S] 保存
- [Ctrl+W] 保存して終了

作成したメモは、[E]で編集することができる。

## タイトル表示

[;]で表示形式メニューを表示し、「このパス以降」「howmtitle」を選択する。
フォルダで[H]を押し、出てきたウィンドウに`*diroption -thisbranch cmd:"*script %0Script\title2comment.js %%: *setcust XC_cwrt= 2"`を入力して実行する。自動更新を解除したい場合は`*diroption -thisbranch cmd:""`とする。

![タイトル表示]({{ "/assets/images/howtouse02.png" | relative_url }})

## メモの閲覧

[Enter]でビューアが開く。もう一度[Enter]を押すと閉じる。
[↑][↓] で表示ファイルを切り替える。

![PPv]({{ "/assets/images/howtouse03.png" | relative_url }})

## メモの移動

反対窓で移動先フォルダを開いたあと、現在窓で移動させたいファイルを[SPACE]でマークし、[M]で移動する。

![move]({{ "/assets/images/howtouse04.png" | relative_url }})

## フォルダ名を変更

Categoryフォルダ内に作ったフォルダ名を[Ctrl+R]で変更する。コメント機能を利用して表示名を変更しているので、同一フォルダ内のフォルダ名とかぶっても問題ない。

![rename]({{ "/assets/images/howtouse05.png" | relative_url }})

