---
title: 準備
layout: page
date: 2022-03-30
last_modified_at: 2022-11-13
permalink: /ppx/
---

[TORO's Library](http://toro.d.dooo.jp/)から

- PPx本体(UNICODE版か64bit版)
- PPx Script Module
- PPx Text Module
- PPx WIndow Module
- PPx Key Module

をダウンロードする。

![TORO's Library]({{ "/assets/images/ppx01.png" | relative_url }})

まずは、PPX本体を解凍する。

![ppxフォルダ]({{ "/assets/images/ppx02.png" | relative_url }})

各PPx Moduleを解凍し、PPXフォルダに

- PPXSCR.DLL / PPXSCR64.DLL
- PPXTEXT.DLL / PPXTEXT64.DLL
- PPXWIN.DLL / PPXWIN64.DLL
- PPXKEY.DLL / PPXKEY64.DLL

を入れる。PPX○○64.DLLが64bit版だ。また、Scriptという名前で空フォルダを作成する。

![ppxフォルダその2]({{ "/assets/images/ppx03.png" | relative_url }})

Scriptフォルダに以下のファイルを入れる。

_title2comment_all.js_

```text
//!*script

// コメントのないhowmファイルの一行目をコメントに

for (var a = PPx.Entry.AllEntry; !a.atEnd(); a.moveNext() ){
  // フォルダを除外
  if (a.Attributes & 16){
    continue;
  // .howmかつコメントのないファイルへの処理
  } else if (a.Name.match(/.howm$/i) && a.Comment.match(/^$/i)){
    var dir = PPx.Extract('%1');
    var entryName = a.Name;
    var f = dir + "\\" + entryName;
    // 一行目を読み込む。文字化けする場合は"sjis"を"utf-8"に
    var s = readFile(f, "sjis");
    // 2~40字を切り取ったものをコメントに
    a.Comment = s.slice( 2,40 );
  }
}

// ファイルの一行目を読み込む関数
function readFile(fname, charset) {
  if (charset == undefined) {
    charset = "_autodetect_all";
  }
  var adTypeBinary = 1, adTypeText = 2;
  var adReadAll = -1,   adReadLine = -2;
  var s = new ActiveXObject("ADODB.Stream");
  s.Type = adTypeText;
  s.charset = charset;
  s.Open();
  s.LoadFromFile(fname);
  var text = s.ReadText(adReadLine);
  s.Close();
  return text;
}
```

以下をクリップボードにコピーする。

```text
{% raw %}
KC_main    = {	; PPcメイン窓
E ,%ME_editor
F6    ,*script %0\title2Comment_all.js
^R ,*comment "%ee%"コメントの編集"%{%*comment%|%}"
^N ,*ppememo
}

KV_main    = {	; PPvメイン窓
UP    ,%K-C"@UP@N"
DOWN    ,%K-C"@DOWN@N"
LEFT ,%K-C"@LEFT@N"
RIGHT ,%K-C"@RIGHT@N"
SPACE    ,%K-C"@SPACE@N"
\SPACE    ,%K-C"@\SPACE@N"
ENTER    = @Q
}

MC_celS    = {    ; エントリ表示 書式([;]メニュー)
howmtitle    = M cF25,6 w35C z7 S1 tC"y-N-D" s1
}

E_cr    = {	; [Enter]用判別
HOWM    ,*ppv %*name(CD,"%R","%1")
}

_Command = {	; ユーザコマンド・関数
saveppepos = *setcust S_ppe:l=%*windowrect(%N.,l)
 *setcust S_ppe:t=%*windowrect(%N.,t)
 *setcust S_ppe:w=%*windowrect(%N.,w)
 *setcust S_ppe:h=%*windowrect(%N.,h)
loadppepos = *ifmatch !0,0%*getcust(S_ppe:l) %: *windowposition %N.,%*getcust(S_ppe:l),%*getcust(S_ppe:t),%*getcust(S_ppe:w),%*getcust(S_ppe:h)
ppememo = *edit %*nowdatetime(Y-N-D-HMS).howm -new -k *mapkey use,K_ppememo %%: *howmformat %%: *editmode -modify:clear %%: *editmode -modify:silent %%: *loadppepos
howmformat = *insert "= %bn%bn%bn[%*nowdatetime(Y-N-D-HMS)]" %: *cursor -3,2,0
}

E_editor	= {	; エディタ用の拡張子判別
*	,%"Text edit"%Orib,editor %FDC
HOWM	,*linecust howmpos,K_ppe:FIRSTEVENT,*loadppepos %%: *linecust howmpos,K_ppe:FIRSTEVENT= %: *edit %FDC -k *mapkey use,K_ppememo
}

K_ppememo = {	; moe用のppeキーバインド
^W ,*saveppepos %: %k"&F4"
^N ,*if %*editprop(modify) %: %K"^S"
 *replacefile %*nowdatetime(Y-N-D-HMS).howm -new -k *howmformat %%: *editmode -modify:clear
}

_others	= {	; その他設定
NewDir	= %*nowdatetime(Y-N-D-HMS)
}

XC_cwrt	= 2	; コメントファイル作成は	0:手動 1:確認有 2:自動
{% endraw %}
```

PPxフォルダにあるPPCW.exeを実行して、PPCを起動する。
PPCで[H]を押すと出るウィンドウに、`%OB *PPCUST /edit`を入力して実行する。

![一行編集]({{ "/assets/images/ppx04.png" | relative_url }})

「編集した内容の取込」ウィンドウが、クリップボードの内容をペーストした状態で表示されるので、OKボタンを押す。

![編集して取込]({{ "/assets/images/ppx05.png" | relative_url }})

