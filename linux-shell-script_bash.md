# Linux / Shell script / Bash

Date: 2014-09-09 13:34
Tags:[]
Categories:[]

---

## Bash

### Grammar - 文法

- Shebang - シバン（グ）

        #!/bin/sh
        #!/bin/bash

#### Array - 配列

- 宣言

        fooArray=()
        fooArray=("hoge" "fuga")

- データ追加

        fooArray+=("piyo")
        fooArray+=("hogera")

#### 比較演算子

- 文字列1と文字列2は等しいか？

        test 文字列1 = 文字列2
        $ test "abc" = "abc" ; echo $?
        0
        $ test "abc" = "def" ; echo $?
        1
        比較する 2つの文字列が同一である場合のみ真 (終了ステータスが 0) となっている。

- 文字列1と文字列2は等しくないか？

        test 文字列1 != 文字列2
        $ test "abc" != "abc" ; echo $?
        1
        $ test "abc" != "def" ; echo $?
        0

### Idiom, Notes

- 標準[エラー]出力
    - 標準エラー出力をリダイレクト

            command 2> /dev/null

    Refs: [UNIXの部屋 コマンド検索:リダイレクト (*BSD/Linux)](http://x68000.q-e-d.net/~68user/unix/pickup?%A5%EA%A5%C0%A5%A4%A5%EC%A5%AF%A5%C8)

    - 標準出力とエラー出力両方をリダイレクト :

            command >& /dev/null
            command > /dev/null 2>&1 # legacy

    - 標準出力とエラー出力両方を別コマンドに渡す :

            command |& less
            command 2>&1 | less

    - 標準エラー出力のみを別コマンドに渡す :

            command 2>&1 1>/dev/null | less

    - 標準出力と標準エラー出力を別ファイルにリダイレクト :

            command 1> file1 2> file2

    - echoの出力を標準エラーに出力 :

            echo "msg" >&2

- エイリアスを一時的に無効にする
    コマンドの先頭にバックスラッシュをつける

        \cd

- ビルトインコマンドリスト表示

        help

- bashのプロセス置換機能 - [bashのプロセス置換機能を活用して、シェル作業やスクリプト書きを効率化する - 双六工場日誌](http://sechiro.hatenablog.com/entry/2013/08/15/bash%E3%81%AE%E3%83%97%E3%83%AD%E3%82%BB%E3%82%B9%E7%BD%AE%E6%8F%9B%E6%A9%9F%E8%83%BD%E3%82%92%E6%B4%BB%E7%94%A8%E3%81%97%E3%81%A6%E3%80%81%E3%82%B7%E3%82%A7%E3%83%AB%E4%BD%9C%E6%A5%AD%E3%82%84%E3%82%B9)
    - 出力対象としてプロセス置換を使う
        - スクリプト出力のすべてをログに取る

                exec 1> >(tee -a stdout.log)

    - 入力対象としてプロセス置換を使う
        - コマンド結果をdiff [一時ファイルを作成せずに、コマンドの実行結果のdiffを取る (bashのProcess Substitutionで) - うまいぼうぶろぐ](http://hogem.hatenablog.com/entry/20090530/1243612485)

                diff <(grep -v "exclude" inputfile) <(sed -e 's/a/b/' inputfile)

- 連番作成

        for i in {1..10} ; do echo $i ; done

- &&と|| - コマンドの実行結果によって別コマンドを実行する。Refs: [bashの&&と: みズとおかズ](http://okazu.air-nifty.com/blog/2010/04/bash-f628.html)
    - コマンド成功したら別コマンドを実行

            make && make install

    - コマンド失敗したら別コマンドを実行

            [ -f /usr/sbin/sendmail ] || exit 0

- 三項演算子（条件演算子）

        [ -f $file ]  && success $file || failure $file

    Refs: [シェルスクリプトで三項演算子ぽいやつ - harry’s memorandum](http://dharry.hatenablog.com/entry/2014/05/20/023644)
    - -> shellcheckで警告出る。厳密にはダメみたい。Refs: [SC2015 · koalaman/shellcheck Wiki · GitHub](https://github.com/koalaman/shellcheck/wiki/SC2015)

- グルーピングとサブシェル
    - サブシェル

            (CMD1; CMD2; CMDn) > hoge.out

    - グルーピング

            { CMD1; CMD2; CMDn; } > hoge.out
    - 違い
        - {}はコマンドの前後に空白が必要
        - {}は最終コマンドの後にも;が必要
        - ()はサブシェルで実行される
            - つまり別プロセスで実行される
            - { cd /tmp; ls } > hoge.outしたら実行後のpwdは/tmpになるが、(cd /tmp; ls) > hoge.out実行後のpwdは変わらない
    - Refs. [割りと便利だけど微妙に忘れがちなbashのコマンド・チートシート - Qiita](http://qiita.com/jpshadowapps/items/d6f9b55026637519347f)

### 特殊変数

- reference : [bash - 特殊変数 - あんみのの備忘録](http://d.hatena.ne.jp/anmino/20090802/1249206149)
- list :

        $0    スクリプトの名前
        $1-9  スクリプトに指定された引数の値(数値は引数の位置)
        $#    スクリプトに指定された引数の数
        $*    スクリプトに指定された引数全部 "$*"の場合は "$1 $2..."
        $@    スクリプトに指定された引数全部 "$@"の場合は "$1" "$2" ...
        $?    直前のコマンドの終了ステータス
        $$    カレントシェルのプロセスID
        $!    直前のバックグランドジョブのプロセスID
        $-    カレントシェルの動作オプション

### パラメータ展開

- 代入
    - 変数varに値がない場合wordを返す : `${var:-word}`
    - 変数varに値がない場合wordを代入 : `${var:=word}`
    - 変数varに値がない場合wordを出力 : `${var:?word}`
    - 変数varに値がある場合wordを代入 : `${var:+word}`
- 削除
    - 最短後置パターンの削除 : `${var%word}`
        - e.g. ディレクトリ部を取得 : `${var%/*}`
    - 最長後置パターンの削除 : `${var%%word}`
    - 最短前置パターンの削除 : `${var#word}`
    - 最長前置パターンの削除 : `${var##word}`
        - e.g. ファイル名を取得 : `${var##*/}`
- 置換
    - 一致パターンの置換（最初のマッチのみ） : `${var/pattern/str}`
    - 一致パターンの置換（すべてのマッチ）   : `${var//pattern/str}`
- 切り出す
    - 文字列の切り出し           : `${var:offset}`
    - 文字列の切り出し（長さ指定） : `${var:offset:length}`
- その他
    - 文字列長の取得 : `${#var}`
    - 変数名を表示   : `${!prefix*}`
    - 値の検査とエラー : `${var:?[word]}`
    - 間接参照

            foo=hoge
            bar=foo
            echo ${!bar}
            # -> hoge

Refs:

- [shell - シェルの変数展開 - Qiita](http://qiita.com/bsdhack/items/597eb7daee4a8b3276ba)
- [Bashの変数パラメータ展開のまとめ - harry’s memorandum](http://dharry.hatenablog.com/entry/20090211/1234290856)
- [03 特殊な変数展開 \[fl8 Wiki\]](http://dokuwiki.fl8.jp/doku.php/bash/03_special_variable)

パラメータ展開をネストすることはできない

Refs: [Can ${var} parameter expansion expressions be nested in bash? - Stack Overflow](http://stackoverflow.com/questions/917260/can-var-parameter-expansion-expressions-be-nested-in-bash)

### ブレース展開

- カンマ指定

        echo {a,b,c}
        mkdir dir{1,2,3}

- 範囲指定
    - 昇順

            echo {1..10}
            mkdir test{1..10}

    - 降順

            echo {5..1}
    - 文字

            echo {A..Z}
            echo {a..z}
            echo {z..a}

    - インクリメント数指定

            echo {1..10..2}
            # -> 1 3 5 7 9

### ヒアドキュメント

- 基本文法

        cat << EOS
        hoge
        fuga
        piyo
        EOS

- ヒアドキュメント結果をリダイレクト

        cat << EOS >> /tmp/hoge 2>&1
        hoge
        piyo
        EOS

- 簡易ヒアドキュメント？　(ぐぐっても出てこない。`tldr bc`でみつけた）

        cat <<< abc
        bc <<< "1 + 2"

### Tips / Notes

- ステップ実行

        trap 'read -p "$BASH_COMMAND"' DEBUG

    Refs: [shellのデバッグ方法(1279) teratail](https://teratail.com/questions/1279)

### Style Guide - スタイルガイド（コーディング基準）

Refs: [Shell Style Guide](https://google.github.io/styleguide/shell.xml)

Rules

- Naming Conventions - 命名規則
    - Function Names : `function`キーワードはつける(vimでindentされるように)
    - Source Filenames - ファイル名： Lowercase


### Refs.

- [コマンドラインプログラムにおける引数、オプションなどの標準仕様 プログラマーズ雑記帳](http://yohshiy.blog.fc2.com/blog-entry-260.html)
- [コマンドラインツールを書くなら知っておきたい Bash の 予約済み Exit Code - Qiita](http://qiita.com/Linda_pp/items/1104d2d9a263b60e104b)

## Regex - Regular Expression

### Kind - 種類

- BRE (基本正規表現） メタ文字セット
- ERE (拡張正規表現） メタ文字セット
    - サブセット
        - AWKのサブセット
    - スーパーセット
        - GNU拡張正規表現メタ文字セット
        - Perl拡張正規表現メタ文字セット

### META Character set - 各コマンドの対応しているメタ文字セット

| コマンド        | 対応しているメタ文字セット |
|-----------------|----------------------------|
| AWK             | EREのAWKサブセット         |
| ed              | BREメタ文字セット          |
| egrep           | EREメタ文字セット          |
| ex              | BREメタ文字セット          |
| grep('-E'なし） | BREメタ文字セット          |
| grep('-E'あり） | EREメタ文字セット          |
| more            | BREメタ文字セット          |
| sed             | BREメタ文字セット          |
| vi              | BREメタ文字セット          |

Important:

> 参考までに述べておくと、GNU拡張やPerl拡張、JavaScript拡張は、いずれもEREのスーパーセットである。ということはすなわち、EREメタ文字セットを覚えておけばそれらの上でも動くということだ。
> Refs: [どのUNIXコマンドでも使える正規表現 - Qiita](http://qiita.com/richmikan@github/items/b6fb641e5b2b9af3522e)

### Perl拡張正規表現

- 改行を含む検索

        grep -P 'bbb[\s\S]*?ddd' test.txt

    - 改行を含む検索でマッチした部分のみ表示

            grep -oP 'bbb[\s\S]*?ddd' test.txt

- 肯定否定先読み戻り読みRefs: [正規表現(肯定先読み、否定先読み、肯定戻り読み、否定戻り読み) - satosystemsの日記](http://d.hatena.ne.jp/satosystems/20100519/1274237784)
    - 肯定先読み - (?=regex)

            # "Windows 2000" の "Windows" には一致するが、"Windows 3.1" の "Windows" には一致しない。
            Windows (?=95|98|NT|2000)
            # static ネストクラスを保持するJUnitテストクラスを検索
            grep -lroP "public class .+Test[\s\S]*?(?=static class)" . --include="*Test.java"
            grep -lroP "public\s(final\s)?class\s.+Test[\s\S]*?(?=static\s(final\s)?class)" . --include="*Test. java" | v -

    - 否定先読み - (?! regex)

            "Windows (?!95|98|NT|2000)" は、"Windows 3.1" の "Windows" には一致するが、"Windows 2000" の "Windows" には一致しない。

    - 肯定戻り読み - `(?<=regex)`

            "(?<=Ubuntu|Debian GNU) Linux" は、"Ubuntu Linux" の "Linux" には一致するが、"Vine Linux" の "Linux" には一致しない。

    - 否定戻り読み - `(?<!regex)`

            "(?<!Ubuntu|Debian GNU) Linux" は、"Vine Linux" の "Linux" には一致するが、"Ubuntu Linux" の "Linux" には一致しない。

## Commands

- grep
- sed

### (De)Compression commands

- 7z - 7-zip操作

        7z x filename.7z

- zip/unzip - zip圧縮・解凍 :
    - 圧縮

            zip -r foo.zip bar

        - 特定フォルダ、ファイルを除外

                zip -r hoge.zip hoge -x \*txt\*

    - 解凍

            unzip archive.zip
            unzip -d 解凍先 archive.zip

        - 内容確認

                unzip -l file

        - 特定のファイルのみ解凍

                unzip file.zip [files ...]
                unzip file.zip */*.log

        - 複数解凍

                # Note: *のエスケープが必要
                unzip \*.zip

- pigz - マルチコアで圧縮
    - 圧縮

            pigz hoge

    - 解凍

            pigz -d hoge

- tar.gz (tar + gzip) :
    - 解凍 :

            tar zxvf filename

    - 圧縮 :

            tar zcvf archive.tar.gz filename

    - 中身確認

            tar tvfz foo.tar.gz

- tar.bz2 (tar + bzip2) :
    - 解凍 :

            tar jxf filename

    - 圧縮 :

            tar jcf package.tar.bz2 package-dir

    - 中身確認

            tar tvfj foo.tar.bz2

- tar.xz (tar + xz) :
    - 解凍（Note: Required tar 1.22)

            tar Jxvf foo.tar.xz

- tar
    - 展開

            tar xvf foo.tar

    - 中身確認

            tar tvf foo.tar

#### 圧縮率、速度比較

結論からいうととりあえずbzip2がオールマイティに良い。

以下を比較

- gzip
- bzip2
- xz
- zip
- 7zip
- lzh

対象は以下

- text
- binary

Refs: [DigiLoog » Linuxの各圧縮コマンド実行速度と圧縮率を測定してみた gzip/bzip2/xz/zip/7zip/lzh](http://www.ns-lab.org/digiloog/2014/06/article_2384/)

### Built-in commands

- read - ユーザ入力を受け取る

### Performance

- free - TODO
- sar - TODO
- top - TODO
- vmstat - TODO

### Network (iproute2)

- ss - ソケットの調査

### Network (deprecated - net-tools)

- TODO
    - dig
    - ifconfig
    - netstat
    - ping
    - route
    - traceroute

### Useful commands

- chown - 再帰的に所有者変更 :
- cut - 文字列を切り出す :
- diff - 差分をとる
- du - ディレクトリサイズ表示 :
- find - 検索：
- gpasswd - グループ操作
- groups - ユーザの所属グループを表示
- less, tail - ファイル内容を監視
- ln - (シンボリック）リンクを貼る
- ls - ファイルリスト表示
- lsof - プロセスが使用しているファイルを調べるRefs: [lsofの使い方 - プロセスが使用中のファイルを調べる - うまいぼうぶろぐ](http://hogem.hatenablog.com/entry/20070223/1172221315)
- man - マニュアル閲覧
- nkf - 文字コード変換Refs: [文字コード変換コマンドの nkfの使い方と実例をまとめました。 - それマグで！](http://takuya-1st.hatenablog.jp/entry/20100511/1273585953)
- nohup - ログアウトしてもバックグラウンドジョブを継続する
- paste - 各ファイルの行を結合する
- pgrep - プロセスをgrep
- pkill - プロセスをkill
- rsync - ファイル・ディレクトリを同期する
- sort - ソートする
- ulimit - コマンドに割り当てる資源を制限する :
- usermod - ユーザ情報変更
- xargs - 引数を標準入力から与える :

### Seldom used commands

- bc - 複雑な計算する（電卓として使う） :
- cal - カレンダを表示する :
- install - ファイルをコピーし、その属性を設定する :
- nl - 行番号を付けてファイルを出力する :
- rename - ファイル名の一括変更（リネーム・一括置換） :
- tee - 標準出力に加えファイルにも出力する
- time - コマンドの時間計測やリソース使用量を表示する :
- tr - 文字の置換・変換をする
- w - ログインしている人とその人がやっていることを表示する :
- yes - killされるまで文字列を繰り返して出力する :

### Complex commands

- 複数jarの中から特定クラスを探す :

        unzip -l '*.zip' | grep foo.class

- 複数ファイルから文字列を一括置換

        find ./path/to/file -type f | xargs sed -i "s/hoge/hage/g"
        find -name "config.xml" | xargs sed -i -e 's?<dispatch>?\0\n\t\t<limit>10</limit>?g'

- grep結果件数を表示

        grep foo bar | wc -l

- grep結果を一括置換

        grep -l 'hoge' ./foo* | xargs sed -i -e 's/hoge/hage/g'

    Refs: [複数のファイル内の文字列をまとめて置換するLinuxコマンド - Qiita](http://qiita.com/kkyouhei/items/b4ff839a2f36ba194df3)

- grep結果表示を置換

        grep 'hoge' ./foo* | sed -e 's/hoge/hage/g'

    Refs: [シェル・スクリプト・リファレンス - 【 文字列を置換する「sed」 】：ITpro](http://itpro.nikkeibp.co.jp/article/COLUMN/20060228/231161/)

- grep結果の大文字小文字を変換

        egrep "# [a-z]" *.md | sed -e 's/\(#\+ \)\(.\)/\1\U\2/'
        egrep -l "# [a-z]" *.md | xargs sed -i -e 's/\(#\+ \)\(.\)/\1\U\2/'

- mvした先にcd (前のコマンドの引数を指定）

        mv foo.file barDir/
        cd $_
        # ↓も
        cd !$

- lsでディレクトリのみ表示

        find . -maxdepth 1 -type d
        ls -l | grep ^d
        ls -F | grep .*/$

- find結果などのファイル名のみ取得する

        find . -name '*.deb' | xargs -n1 basename
        find . -name '*.deb' -printf "%f\n" # gnu findのみ

- find結果などのディレクトリ名のみ取得する

        find . -name '*.deb' | xargs -n1 dirname

- 複数ファイルの拡張子を一括変更（renameコマンド使わない場合）

        for filename in *.dmp; do mv $fliename ${filename%.dmp}.sql; done

- find結果のファイル一括リネーム

        find -name hogefuga | xargs rename hoge piyo

- プロセスの起動時間を確認する

        ps -eo lstart,pid,args | grep hoge

- スクリプトファイルの場所を取得する
        - 実行されたシェルの場所(sourceコマンドなどで呼ばれた場合、呼び元が取得される)

                script_dir=$(cd "$(dirname "$0")" || exit 1; pwd)

        - 常に実行シェルの場所(sourceコマンドなどで呼ばれた場合、呼び先が取得される)

                here="$(cd "$(dirname "${BASH_SOURCE:-$0}")"; pwd)"

- 4ファイル以上間のdiffを取る（3ファイルはdiff3コマンドが使えそう） TODO: もっといいやり方ないか

        for i in `find -name operation.sh` ; do echo $i; diff $(find -name operation.sh | head -1) $i ; done

- プロセスが存在しているかどうかで処理を分ける

        if kill -0 $PID; then
            echo "exists"
        else
            echo "not exists"
        fi

- カレントディレクトリ内のディレクトリをすべてzipする（\* Caution: これだけだとディレクトリ以外も対象となる）

        for t in `ls`; do zip -r ${t}{. zip,} ; done
        # サブディレクトリをすべて
        for t in `ls`; do (cd ${t}; for tt in `ls` ; do zip -r ${tt}{. zip,} ; done) ; done

## Key-shortcuts

Refs: [shell のショートカットキー適当にまとめてみた。 Lonely Mobiler](http://loumo.jp/wp/archive/20120305090532/)

- 行頭へ移動：

        ctrl+a

- 行末へ移動：

        ctrl+e

- 一文字後に移動：

        ctrl+f

- 一文字前に移動：

        ctrl+b

- 一単語後に移動：

        Alt(Meta)+f

- 一単語前に移動：

        Alt(Meta)+b

- ヒストリー(戻る） :

        ctrl+p

- ヒストリー(進む） :

        ctrl+n

- 一文字削除（Backspace) :

        ctrl+h

- 一文字削除（Delete) :

        ctrl+d

- 一単語削除（Backspace)(パス区切り文字を単語扱いする） :

        alt+backspace (alt+ctrl+h)

- 一単語削除（Backspace)(パス区切り文字は単語扱いしない） :

        ctrl+w

- 一単語削除（Delete) :

        Alt(Meta) + d

- 行頭まで削除：

        ctrl+u

- 行末まで削除：

        ctrl+k

- 貼り付け

        ctrl+y

- クリア：

        ctrl+l

- Enter:

        ctrl+j
        ctrl+m
        ctrl+o -> これは使わない。 vim で history back 。

- Tab(補完）:

        ctrl+i

## Tips

- ssh鍵認証を設定する <http://www.tooyama.org/ssh-key.html>
    - client

            cd ~/.ssh
            ssh-keygen -t ecdsa
            Enter passphrase: <Enter>
            ls ~/.ssh
            -> id_ecdsa:秘密鍵, id_ecdsa.pub:公開鍵

    - server

            mkdir .ssh
            chmod 700 .ssh
            cd ~/.ssh
            ssh client "cat ~/.ssh/id_ecdsa.pub" >> authorized_keys
            chmod 600 authorized_keys

- lessで色付き表示をする

        ls --color="always" | less -R

- 複数ファイルの改行コードを置換する
    - LF -> CRLF

            nkf --windows --overwrite *.txt
            nkf --window  --overwrite `find -name "*.log"`
            unix2dos *.txt

    - CRLF -> LF

            nkf --unix --overwrite *.txt
            nkf --unix --overwrite `find -name "*.log"`
            dos2unix *.txt

- sshログインして指定のディレクトリに移動

        ssh -t user@host "cd hoge; bash"

- 先頭に-（ハイフン）があるファイルを操作する

        mv -- -c foo
        mv ./-c foo

- 複数行の置換はPerl使うのがいちばん楽そうRefs: [languages](languages)

- ミリ秒単位で時刻を表示するRefs: [dateコマンドでミリ秒まで出す２ - 揮発性のメモ](http://d.hatena.ne.jp/iww/20131214/dash)

        date +'%Y-%m-%d %H:%M:%S.%3N'
        echo  $(date +%c) $(printf '%03d' $(expr `date +%N` / 1000000))

- `Ctrl + s`でキー入力受け付けられなくなる。(操作できなくなる）
    Ctrl + qで解除
    Refs: [「Ctrl」＋「S」でキー入力が受け付けられなくなる - ITmedia エンタープライズ](http://www.itmedia.co.jp/help/tips/linux/l0612.html)

- [6万ミリ秒でできるLinuxパフォーマンス分析 | Yakst](https://yakst.com/ja/posts/3601?platform=hootsuite)

### スペシャルファイル

- nullデバイス

        /dev/null

- 標準（エラー)出力デバイス

        /dev/stdout
        /dev/stderr

## Tools

### Systemd

- システムブート時のサービスの起動設定

        systemctl enable/disable [Unit名(e.g. docker)]

- 起動

        systemctl start [Unit名(e.g. docker)]

