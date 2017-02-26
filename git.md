# Git

Date: 2015-02-02 22:13
Tags: []
Categories: []

---

## Basic usage

## Technique

- 初回push - Refs: [githubのレポジトリに初回pushするとき - MEMOcho-](http://jsapachehtml.hatenablog.com/entry/2014/03/14/205721)

        touch README.md
        git init
        git add README.md
        git commit -m "first commit"
        git remote add origin git@github.com:username/hoge.git
        git push -u origin master

- git addを取り消す

        git reset HEAD foo.txt

- originの再登録方法

        git remote rm origin
        git remote add origin git@github.com:(githubのid)/(リポジトリ).git
        git push -u origin master

- GitのリモートリポジトリoriginのURLを変更する

        git remote set-url origin git@git.example.com:foo/bar.git

- remote設定
    - HTTPS

            https://github.com/USERNAME/OTHERREPOSITORY.git
    - SSH

            git@github.com:USERNAME/OTHERREPOSITORY.git

- ある特定のファイルを前のバージョンに戻す

        git checkout HEAD^ path/to/file.java

- 相対でリビジョンを指定する
    - ヘッドの1つ前のコミットを見る

            git show HEAD^

    - ヘッドの3つ前のコミットを見る

            git show HEAD~3
            git show HEAD^^^
            git show HEAD~~~

- リモートのGitブランチをローカルにチェックアウトする

        git branch -a
        git fetch
        git checkout -b other_branch origin/other_branch

- Gitの歴史に残っているユーザー名やメールアドレスを書き換える

        git filter-branch -f --commit-filter '
        GIT_AUTHOR_NAME="assout"
        GIT_AUTHOR_EMAIL="assout@users.noreply.github.com"
        GIT_COMMITTER_NAME="assout"
        GIT_COMMITTER_EMAIL="assout@users.noreply.github.com"
        git commit-tree "$@"
        ' HEAD
        git push -f

    Refs: [gitの歴史に残っているユーザー名やメールアドレスを書き換える deadwood](http://www.d-wood.com/blog/2013/10/22_4900.html)

- Forkしたリポジトリを本家リポジトリに追従、追跡する
    - 追従するFork元を追加

            git remote add upstream git://github.com/foo/bar.git

    - Fork元の変更を取得

            git fetch upstream

    - 自分のリポジトリに反映

            git merge upstream/master

- Conflict を解消する

        git mergetool

- Git diffで新規追加したファイルをdiff結果に含める

        git add -N foo.txt
        git diff HEAD

    Refs: [git diffで新規追加したファイルをdiff結果に含める RainbowDevilsLand](http://rainbowdevil.jp/?p=1247)

- Gitでリモート(remote)のブランチにローカルを強制一致させたい時

        git fetch origin
        git reset --hard origin/${branch}
        # masterブランチの場合
        # git reset --hard origin/master

    Refs: [gitでリモートのブランチにローカルを強制一致させたい時 - Qiita](http://qiita.com/ms2sato/items/72b48c1b1923beb1e186)

- detached HEAD状態から元に戻すコマンド

        git checkout master

    Refs: [detached HEAD状態から元に戻すコマンド (git, checkout, fix a detached HEAD, .git/HEAD, refs/heads/master) - いろいろ備忘録日記](http://devlights.hatenablog.com/entry/20130417/p1)

- 1ファイルだけ別のブランチから持ってくる

        git checkout <ブランチ名> -- <ファイル名>

    Refs: [Git 1ファイルだけ別のブランチから持ってくる - Qiita](http://qiita.com/oret/items/b646fcada9d89ed308c4)

- 派生元ブランチの変更

        git rebase --onto master(正しい派生元) develop(誤った派生元) topic(適用先ブランチ)

    Refs: [git rebase \-\-onto で派生元ブランチの変更 - northaven](http://yamayo.github.io/blog/2013/12/01/git-rebase-onto/)

- git の履歴とワークツリーの両方から削除

        git filter-branch -f --index-filter 'git rm --ignore-unmatch filename' HEAD

- git の履歴を削除してワークツリーには残す

        git filter-branch -f --index-filter 'git rm --cached --ignore-unmatch filename' HEAD

## Configuration

- 日本語のファイル名を表示できるようにする

        git config --global core.quotepath false

## Git hook management

- Overcommit            : Star 1164: : [GitHub - brigade/overcommit: A fully configurable and extendable Git hook manager](https://github.com/brigade/overcommit/)
- pre-commit by Yelp    : Star 774 : だめ。pipでhomeにbin入るし : [pre-commit by Yelp](http://pre-commit.com/)
- pre-commit(jish)      : Star 607 : [GitHub - jish/pre-commit: A slightly improved pre-commit hook for git](https://github.com/jish/pre-commit)
    - -> これにする(シンプル)
- Git-hooks (Meyer)     : Star 661 : メンテされてないっぽい: [Meta Magic: Managing project, user, and global git hooks](http://benjamin-meyer.blogspot.jp/2010/06/managing-project-user-and-global-git.html)
- Git-hooks (git-hooks) : Star 121 : : [Git-hooks by git-hooks](http://git-hooks.github.io/git-hooks/)

## Github

### Search

- ファイル名(パス)を検索

        .travis.yml in:path

- 特定ファイル名(パス)を対象にファイル内検索

        filename:.travis.yml checkbashisms

Refs:. [Searching code - User Documentation](https://help.github.com/articles/searching-code/)

### Other

- メールアドレスを非公開にする
    - <https://github.com/settings/emails> - Keep my email address private : checked
- プロキシを超える
    - [各種コマンド類でプロキシサーバを越えるための設定 - iwasakimsの日記](http://d.hatena.ne.jp/iwasakims/touch/20120726/1343322297)
    - [Git - プロキシの指定方法 - Qiita](http://qiita.com/tunepolo/items/296c2639e0b750de41c6)
- Pull Request送信後に修正があった場合の作法について
    Refs: [Pull Request送信後に修正があった場合の作法について - QA@IT](http://qa.atmarkit.co.jp/q/2894)
- wikiからファイルへリンク

        [I'm a relative reference to a repository file](../blob/master/LICENSE)

    Refs: [Markdown Cheatsheet · adam-p/markdown-here Wiki · GitHub](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#links)

## GitLab

Refs: [docker#GitLab](docker#GitLab)

リポジトリ取得

    git clone ssh://git@localhost:10022/root/sandbox.git

### Special GitLab References

| input                | references                 |
|----------------------|----------------------------|
| @user_name           | specific user              |
| @group_name          | specific group             |
| @all                 | entire team                |
| #123                 | issue                      |
| !123                 | merge request              |
| $123                 | snippet                    |
| ~123                 | label by ID                |
| ~bug                 | one-word label by name     |
| ~"feature request"   | multi-word label by name   |
| 9ba12248             | specific commit            |
| 9ba12248...b19a04f5  | commit range comparison    |
| [README](doc/README) | repository file references |

Refs: [GitLab Documentation](http://doc.gitlab.com/ce/markdown/markdown.html)

### Notes

merge requestとpull request の違い

-> 結論から言うと全く同じ(位置づけが違うためあえて変えてるっぽい)

- Refs: [GitLab flowから学ぶワークフローの実践 開発手法・プロジェクト管理 POSTD](http://postd.cc/gitlab-flow/)
- Refs: [git - Pull request vs Merge request - Stack Overflow](http://stackoverflow.com/questions/22199432/pull-request-vs-merge-request)

