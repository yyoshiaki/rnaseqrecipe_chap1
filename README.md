# RNA-Seqデータ解析　WETラボのための鉄板レシピ Chapter1 AnnualUpdate

## Anaconda installのzshへの対応 2020/04/29

zshを使用する場合、`~/.zshrc`に以下のanacondaを読み込む処理を追記する必要がある。将来的にanacondaが対応してくれることが予想される。`~/.zshrc`を編集するには`% open -e ~/.zshrc`をターミナルから実行する。追記後はターミナルを再起動。

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

## samtoolsがインストールできない場合 2020/04/29

書籍の方法でもsamtoolsが適切にインストールできない場合、以下のようにソースからビルドする。なお、パスの通し方に関してはネット上の文献等を参照してください。

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
