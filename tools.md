# Tools

Date: 2015-10-01 11:05
Tags: []
Categories: []

---

## Prelude

- Linux限定のものは、Refs: [linux-shell-script](linux-shell-script)
- Windows限定のものは、Refs: [windows-command-prompt](windows-command-prompt)
- 重要なものは別ファイル化
    - Git : [git](git)
    - Docker : [docker](docker)
    - And other

## Lint tools

### List

- Ansible
    - Ansible-lint
- Dockerfile
    - dockerfile-lint
    - dockerlint : Deprecated (結構ゆるそう)
- Markdown(text)
    - Markdown lint tool (mdl)
    - Redpen : Deprecated ("textlint"のほうがモダンっぽい)
    - eslint-md
    - textlint
    - textstat : TODO: 実行時Error出る
- JavaScript
    - ESLint
- JSON
    - JSON Lint
- ShellScript
    - bashate
    - checkbashisms
    - shellcheck
- SQL
    - SQLint : TODO: Error出て入れれてない
- VimScript
    - vint
- YAML
    - JS-YAML
    - yaml-lint: Deprecated ("JS-YAML"に比べドキュメントがあんまなさそう)

### Redpen

- Spelling機能は半角スペースで区切られた単語にたいしてのみ動作する点に注意してください

### ShellCheck

- Directive

        # shellcheck disable=SC2059

- SC2034
    - -> for文とかではdummyとして`_`を使う

            for _ in ${1..10} ; do foo; done

### bashate

    bashate -i E002,E003

- E002: ensure that indents are only spaces, and not hard tabs
- E003: Not an indent with multiple of 4

## Pomodoro

方針

- msys2, linux両方で動く(office/home)
- tmux統合がある

候補

- Bash
    - pomosh
    - p
    - pomodoro_sh
- Chrome Extension
    - Strict Workflow
    - Simple Pomodoro
- Ruby
    - Thyme: Refs: [Thyme - Console Pomodoro Timer](http://hughbien.com/thyme/) デーモン実行がエラー、tmuxステータス領域がみづらい(時間経過後消えちゃうだけ)
    - pomo: 動かないっぽい@msys2
    - pomodoro_timer: 動かないっぽい@msys2
- Node.js
    - pomo(pomojs): tmux連携、動かない、ログが出力されない @msys2
    - pomodoro: tmux連携なし。動かないっポイ@msys2
    - pomodoro-timer: tmux連携なし
    - turnip: 動かない@msys2
    - tomato-timer: 動いた。tmux連携無し
    - pommy: 動かない@msys2

決定

- Bash
    - p: Linux, msys2で同じように使える。tmux連携できる。chromeはだるい。

## Other tools

### Ctags

- langmap確認

        ctags --list-maps

### GitBook

- 初期化

        gitbook init

    \* SUMMARY.mdに従ってディレクトリ、ファイルを作成できる

- ビルド

        gitbook build

- サーブ

        gitbook serve

### Pacman

- リスト表示

        pacman -Sl

- 検索(パッケージ名と説明の両方)

        pacman -Ss grep

- インストール済みパッケージのリストアップ

        pacman -Qqe

- インストール

        pacman -S grep

- アンインストール

        pacman -R grep

- 更新

        update-core
        pacman -Su

- ダウングレード
    > : /var/cache/pacman/pkg ディレクトリの中にもし古いバージョンのパッケージが保存されていた場合、簡単にダウングレードすることができます。
    > （つい最近に pacman -Scc をしたりしていない限り存在しているはずです）。
    > pacman -U /var/cache/pacman/pkg/pkgname-olderpkgver.pkg.tar.gz でその指定したバージョンのパッケージをインストールできます。

Refs:

- [pacman - ArchWiki](https://wiki.archlinuxjp.org/index.php/Pacman)
- [Pacman ヒント - ArchWiki](https://wiki.archlinuxjp.org/index.php/Pacman_%E3%83%92%E3%83%B3%E3%83%88)

### Pandoc

- markdownからtextileに変換

        pandoc -s hogehohe.md -o hogehohe.textile

### jid

    jid < foo.json
    echo '{"aa":"2AA2","bb":{"aaa":[123,"cccc",[1,2]],"c":321}}'| jid

### socat

Refs: [socat を使うと各種ソケットの操作が捗りまくる件 | CUBE SUGAR STORAGE](http://momijiame.tumblr.com/post/48934531325/socat-%E3%82%92%E4%BD%BF%E3%81%86%E3%81%A8%E5%90%84%E7%A8%AE%E3%82%BD%E3%82%B1%E3%83%83%E3%83%88%E3%81%AE%E6%93%8D%E4%BD%9C%E3%81%8C%E6%8D%97%E3%82%8A%E3%81%BE%E3%81%8F%E3%82%8B%E4%BB%B6)

- Echoサーバを立てる

        # サーバ
        socat -v tcp-listen:8080,fork system:cat
        # アクセス
        telnet localhost 8080

- TCPクライアントとして使う

        socat -v tcp-listen:8080,fork system:cat
        socat STDIN tcp-connect:localhost:8080
        HELLO

### tmux

#### Commands

- すべてのセッションを終了させる

        tmux kill-server

- ログ取得開始

        <C-s><C-p>

- ログ取得終了

        <C-s>P

#### Plug-ins

- tpm (Tmux Plugin Manager)
    - インストール

            Prefix + I

## Tools key unity

### Before (Default)

| Commands      | Vim                   | Vrapper (Eclipse) | tmux (Gnome Terminal, Mintty) | cVim (Crhome)            |
|---------------|-----------------------|-------------------|-------------------------------|--------------------------|
| Cut           | `x`                   | `<C-x>`           | n/a                           | n/a                      |
| Copy          | `y`                   | `<C-c>`           | `<C-s>[`, `<C-S-c>`           | n/a                      |
| Paste         | `p`                   | `<C-v>`           | `<C-s>]`, `<C-S-v>`           | n/a                      |
| Tab open      | `:tabe[dit]`          | `:tabe[dit]`      | `<M-t>`                       | `<C-t>`                  |
| Tab move      | `<M-{h, l}>`          | `<M-{h, l}>`      | `<M-{h, l}`                   | `<M-{h, l}`,`<C-{h, l}>` |
| Pane split    | `<C-w>s`, `:s[plit]`  | -                 | `<C-s>p`                      | n/a                      |
| Pane vsplit   | `<C-w>v`, `:v[split]` | -                 | `<C-s>v`                      | n/a                      |
| Pane move     | `<C-w>{h, j, k, l>`   | -                 | `<C-s><AllowKey>`             | n/a                      |
| Pane close    | `<C-w>c`, `:clo[se]`  | `<C-F4>`          | -                             | `x`                      |
| Pane maximize | `sm`                  | `sm`              | `<C-s>m`                      | `F11`                    |
| Shutdown      | `:qa[ll]`             | `<Alt-F4>`        | -                             | `<Alt-F4>`               |

### After

| Commands      | Vim                 | Vrapper (Eclipse)   | tmux (Gnome Terminal, Mintty) | cVim (Chrome)              |
|---------------|---------------------|---------------------|-------------------------------|----------------------------|
| Cut           | `x`                 | As with Vim         | -                             | -                          |
| Copy          | `y`                 | As with Vim         | `<C-s>[`, `<C-S-c>`           | `y`                        |
| Paste         | `p`                 | As with Vim         | `<C-s>]`, `<C-S-v>`           | `p`                        |
| Tab open      | `:tabe[dit]`        | -                   | `<M-t>`                       | `<C-t>`                    |
| Tab move      | `gt, gT`            | `<C-{h, l}>`        | `<M-{h, l}>`                  | `<M-{h, l}>`, `<C-{h, l}>` |
| Tab close     | `:tabc[lose]`       | `<C-q>`             | `<M-c>`                       | `x`                        |
| Pane split    | `<C-w>s`            | As with Vim         | `<C-s>s`                      | -                          |
| Pane vsplit   | `<C-w>v`            | As with Vim         | `<C-s>v`                      | -                          |
| Pane move     | `<C-w>{h, j, k, l}` | As with Vim         | `<C-s>{h, l, j, k}`           | n/a                        |
| Pane close    | `<C-w>c`            | As with Vim,`<C-q>` | `<C-s>c`                      | `x`                        |
| Pane exit     | `<C-w>q`            | As with Vim,`<C-q>` | `<C-s>q`                      | `x`                        |
| Pane maximize | `sm`                | As with Vim         | `<C-s>m`                      | `F11`                      |
| Pane size     | `<C-w>{<, >, -, +}` | -                   | `<C-s>{<, >, -, +}`           | n/a                        |
| Buffer delete | `:bd[elete]`        | As with Vim         | `<C-s>q`                      | `x`                        |
| Shutdown      | `:qa[ll]`           | `<Alt-F4>`          | `<C-s>Q`(kill session)        | `:qa[ll]`, `<Alt-F4>`      |

Hint/TODOs

- 上記"Pane"はtmuxでいうPaneで、Vimでいうウィンドウにあたるもの
- `<C-S-hoge>`のような3キー同時押しは、cVim のみで可能
- `<C-S>hoge`のようなprefix -> キーという定義は、Vim, Vrapper, tmuxのみで可能

## Tools color unity

| Tools   | dark/light | color          |
|---------|------------|----------------|
| Vim     | dark       | hybrid         |
| GVim    | dark       | hybrid         |
| Mintty  | dark       | hybrid         |
| Eclipse | light      | default(light) |

Hint

- TODO: Linux GVimでTomorrow-Nightだと無駄にboldになるキーワードがある(無駄ではない?)

