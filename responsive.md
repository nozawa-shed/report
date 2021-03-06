文字コードについて　　　　　　　　　　　　　　　　　　　　　2015/01/23 担当：野澤                                                                                                                                                                                                                                                                                  
#### 文字コードとは             
-------------------------
文字コードとは、コンピュータ上で文字を扱うために、文字に対して割り当てられた数値のことであり、  
文字と数値の対応付け。  
この対応付けの種類は沢山あり、shift-JISやUTF-8などがある。

#### 文字コードの構成要素
-------------------------
文字コードの世界は２つの要素で構成されている。  

1. 文字集合 - 表現したい文字の範囲 (文字の集合体)  
 > 世界中には日本語、英語、フランス語、ドイツ語、中国語・・・など大量の文字が存在するが、   
 > これらの文字から表現したい文字の範囲（集合体）を定義すること。  
  
2. 符号化方式(エンコード) – 文字集合を構成する個々の文字の表現方法（数値の振り方）  
  
  > 文字集合の個々の文字をコンピュータ上でどういった数値で表現するかを定義する。  
  > この数値の振り方。  
  > コンピュータはこの符号化方式で割り当てられた数値を用いて文字を表現する。

#### 文字コードセットとは
-------------------------
どんな文字をどれくらい扱うかを取り決めたもの  
  
例えば・・・  
日本語なら「ひらがな」と「カタカナ」「漢字」で構成されている。  
ひらがなは50個で済むが、漢字だと一杯ありすぎてどの範囲まで扱えば良いかわからない  
  
なので、常用漢字を漢字とするといったルールがが必要になり    
このルールを元に揃えた文字に対応させた数値を  
表のように表したものが文字コードセット。

#### 文字コードの種類
-------------------------
##### ASCIIコード
 最も基本的な文字コードとして世界的に普及している。  
 アルファベットと数字、記号だけが定義された代表的な文字コード。最初の文字コード 
 ラテンアルファベット(ローマ字)、数字、記号、空白文字、制御文字など128文字を収録している。
 
##### Unicode
 世界で使われる全ての文字を共通の文字集合にて利用できるようにしようという考えで定義された文字コード
###### Unicodeの符号化方式(エンコード)
* UTF-8  
  ASCIIの文字をそのままUnicodeで使用可能にするために制定された。  
  LinuxやMac OS Xで標準文字符号化方式として採用され、  
  また、インターネット上でもっともよく使われるUnicode系の符号化方式。  

* UTF-16
 
##### 日本語の文字コード
---------------------------

##### ISO-2020-JP 
 JISコードとも呼ばれることもあり主に電子メールで使われる文字コード  
 Webページではほとんど利用されていない
 
##### Shift_JIS  
 Windowsをはじめ、日本語の文字コードとして最も一般的に用いられている文字コードの一つとなっている。    
 Microsoft社が日本にパソコンを普及させるときに策定された文字コード  
 現在では世界各国の言語が扱えないなどのことから利用は減ってきている

##### EUC-JP 
 主にUNIX系で使われている文字コード  
 UNIXで日本語を扱うために策定された  
 
#### 機種依存文字
-------------------------
WindowsやMacintoshなどその機種でのみ表示することができる文字のことを機種依存文字と呼ぶ。  

Windowsの機種依存文字である○の中に数字が書かれたものなどを使用した場合、  
Macintoshではうまく表示されずWEBサイト制作者の意図が伝わらないことがあるため、    
機種依存文字は使用しないようにする。

#### 文字化けが発生する理由
-------------------------
HTMLファイル自体の文字コードとブラウザが解釈した文字コードが異なるときに文字化けが発生する    

例えば・・・  
Shift_JISで保存したHTMLファイルをブラウザがUTF-8と勘違いして表示してしまうと文字化けが発生する・・

#### 制作時に文字化けを防ぐポイント
-------------------------
##### サイト制作時に文字コードを決める
サイトを企画する段階で何の文字コードを使うか決めておく事で文字化けを防ぐ。  
また、既存のサイトで使われている文字コードと合わせる。

##### ファイルの文字コード
元々のHTMLファイルがどの文字コードで保存されているか確認する。  
エディタによりデフォルトの文字コード異なるため、どの文字コードで保存されているかチェックする。  

##### HTMLファイルで指定する文字コード
HTML内で指定する文字コードを宣言する。
HTMLファイル内で、Webブラウザに対してのHTMLファイルの文字コードを助言するためのタグがある。

````html
 <meta http-equiv="Content-Type" content="text/html; charset=Shift_JIS" />
`````
このタグの文字コード部分がHTMLファイル自体の文字コードと同じかをチェックする。  
これによりWebブラウザが正しくHTMLの文字コードを解釈してくれる。  

■ 注意点  
文字コード宣言より手前に日本語を書かない  
文字コード宣言は1回だけ

##### CSSファイルで指定する文字コード  
日本語のプロパティ値を使う場合は、文字コード宣言を行わないとプロパティ値を誤って解釈され  
思い通りの表示にならないことがある。  

CSSファイルでの宣言の仕方  
````css
  @charset "shift_jis";
```````
````css
  @charset "UTF-8";
```````

■ 注意点  
文字コードの宣言の場所は必ずファイルの先頭で行う必要があり、  
以下のように、宣言の前に文字の記述をしないようにする。  

````css
  /* charset */
 @charset "iso-2022-jp";
```````
