# RNA-Seqデータ解析　WETラボのための鉄板レシピ Chapter1 AnnualUpdate  2021/11/28

## M1 Macについて
M1 Macではbiocondaを用いたツールインストールなどが現状できない。dockerを用いるか、ワークステーションなどを別途用意することが必要。また、[遺伝研スパコン](https://sc.ddbj.nig.ac.jp/)は基本無償使用可能。

# RNA-Seqデータ解析　WETラボのための鉄板レシピ Chapter1 AnnualUpdate  2020/11/05 

## Anaconda

ダウンロードリンクが[https://www.anaconda.com/products/individual](https://www.anaconda.com/products/individual)へ変更されている。バージョンも3.8へ。

## Anaconda installのzshへの対応

condaはインストール時に、`~/.bash_profile`というbashの設定ファイルにconda自動立ち上げに関する処理を追記する。一方、2019年にデフォルトとなったzshではこの設定が反映されていないため、手動で対応しなければならない。以下に2つの解決方法をあげる。また、この手順は今後のanacondaのアップデートで不要になる可能性があるので常にインストール前に確認してほしい。

1. `~/.bash_profile`の内容を`~/.zshrc`に追記する。`~/.zshrc`を編集するには`% open -e ~/.zshrc`をターミナルから実行する。追記後はターミナルを再起動。なお、`.zshrc`は重要なzshの設定ファイルで破損すると容易にターミナルが立ち上がらなくなる。よく吟味しながら編集すること。

```
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/opt/anaconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
   eval "$__conda_setup"
else
   if [ -f "/opt/anaconda3/etc/profile.d/conda.sh" ]; then
       . "/opt/anaconda3/etc/profile.d/conda.sh"
   else
       export PATH="/opt/anaconda3/bin:$PATH"
   fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

2. `source ~/.bash_profile` という一文を`~/.zshrc`に追加する。

## brew install

推奨インストール方法が以下へと変更されていた。

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

## Rの最新版が4.0.3へとバージョンアップされている。

## samtoolsがインストールできない場合 2020/04/29

書籍の方法でもsamtoolsが適切にインストールできない場合、以下のようにソースからビルドする。なお、パスの通し方に関してはネット上の文献等を参照のこと。

```
% cd ~
% mkdir Programs
% cd Programs
% curl -L https://github.com/samtools/samtools/releases/download/1.10/samtools-1.10.tar.bz2 > samtools-1.10.tar.bz2\ntar -jxvf % samtools-1.10.tar.bz2
% cd samtools-1.10
% ./configure --prefix=/usr/local/
% make -j 8
% make install
% ./samtools
% open -e ~/.zshrc  # PATHに$HOME/Programs/samtools-1.10を追加。
% source ~/.zshrc
```

詳細は公式サイト（http://www.htslib.org/download/）を参照。
