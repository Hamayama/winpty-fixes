# winpty-fixes

## 概要
- MSYS2 用の winpty ( https://github.com/rprichard/winpty ) について、  
  一部修正を行ったものです。

- オリジナルのコミット 7e59fe2 (2018-12-19) をベースに変更を行いました。

- 変更の差分は、以下のページで確認できます。  
  https://github.com/Hamayama/winpty-fixes/compare/winpty-orig-7e59fe2...main


## 変更点
- オリジナルからの変更点を、以下に示します。

1. カーソルを、1 行目の 2 ～ 8 桁目に置いて Esc キーを押すと、  
   以後、Esc キーと他のキーの組み合わせ ( Esc-< 等) が入力できなくなる件の修正  
   ( `src/agent/ConsoleInput.cc` )  
   本件は、オリジナルの方にも報告した(マージ未)。  
   https://github.com/rprichard/winpty/pull/175

2. Windows 10 で、カーソルが隠れるように画面をリサイズ(縮小)すると、  
   異常終了する件の修正  
   ( `src/agent/Scraper.cc` )  
   これは、Windows Console の以下の問題に関係があると思われる。  
   https://github.com/microsoft/terminal/issues/1976  
   ただ、発生するプログラムと発生しないプログラムがあり、  
   再現条件がまだよく分からない。  
   (PDCurses ライブラリを使ったプログラムでは発生した)  
   (Windows 8.1 では発生しない)


## インストール方法
- MSYS2/MinGW-w64 (64bit) 環境でのインストール手順を、以下に示します。  
  A または B のどちらかの方法で、インストールを実施ください。

＜A：パッケージファイルでインストールする場合＞

1. MSYS2 用のパッケージファイルを用意しています。  
   以下のページを参照して、インストールを実施ください。  
   https://github.com/Hamayama/winpty-fixes-package

＜B：ソースコードからビルドしてインストールする場合＞

1. MSYS2/MinGW-w64 (64bit) のインストール  
   事前に MSYS2/MinGW-w64 (64bit) がインストールされている必要があります。  
   以下のページを参考に、開発環境のインストールを実施ください。  
   https://gist.github.com/Hamayama/eb4b4824ada3ac71beee0c9bb5fa546d  
   (すでにインストール済みであれば本手順は不要です)

2. 標準版の winpty のインストール  
   プログラムメニューから MSYS2 の MinGW 64bit Shell を起動して、以下のコマンドを実行してください。
   ```
     pacman -S winpty
   ```
   (すでにインストール済みであれば本手順は不要です)

3. msys/gcc と make のインストール  
   プログラムメニューから MSYS2 の MinGW 64bit Shell を起動して、以下のコマンドを実行してください。
   ```
     pacman -S msys/gcc
     pacman -S make
   ```
   (すでにインストール済みであれば本手順は不要です)

4. winpty のソースの展開  
   本サイト ( https://github.com/Hamayama/winpty-fixes ) のソースを、  
   (Download Zip ボタン等で) ダウンロードして、作業用のフォルダに展開してください。  
   例えば、作業用のフォルダを c:\work とすると、  
   c:\work\winpty の下にファイル一式が配置されるように展開してください。  
   (注意) 作業用フォルダのパスには、空白を入れないようにしてください。

5. winpty のコンパイル  
   プログラムメニューから MSYS2 の MinGW 64bit Shell を起動して、以下のコマンドを実行してください。  
   ( c:\work にソースを展開した場合)
   ```
     cd /c/work/winpty
     ./configure
     make
   ```

6. winpty のインストール  
   プログラムメニューから MSYS2 の MinGW 64bit Shell を起動して、以下のコマンドを実行してください。  
   ( c:\work にソースを展開した場合)
   ```
     cd /c/work/winpty
     make PREFIX=/usr UNIX_ADAPTER_EXE=winpty.exe install
   ```

- 以上です。


## 環境等
- OS
  - Windows 10 (version 1909) (64bit)
  - Windows 8.1 (64bit)
- 環境
  - MSYS2/MinGW-w64 (64bit) (gcc version 10.2.0 (Rev1, Built by MSYS2 project)) (Windows 10)
  - MSYS2/MinGW-w64 (64bit) (gcc version 9.2.0 (Rev2, Built by MSYS2 project)) (Windows 8.1)
- 端末
  - mintty 3.3.0 (Windows 10)
  - mintty 3.1.4 (Windows 8.1)
- ライセンス
  - オリジナルと同様とします

## 履歴
- 2020-10-17 v0.4.4-dev-fix0001 Escキーの問題を修正
- 2020-10-17 v0.4.4-dev-fix0002 画面リサイズの問題を修正


(2020-10-18)
