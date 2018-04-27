# Chrome

Date: 2014-11-13 11:54
Tags: []
Categories: []

---

## Extensions

### List

- `Add to Wunderlist`
- `AutoPagerize`
- `Clutter Free - Prevent duplicate tabs` : 重複タブを自動クローズ。ショートカットキーはすべて無効にする。
- `Disable Extensions Temporarily`
- `FireShot` : 1ページ内スクロールしてきゃぷれる。1回毎に保存先聞かれるけど他にいいのも無さそうなので。
- `Github Toc`
- `IE Tab` : 印刷プレビューを見るためにも使用
- `JSONView`
- `LastPass`
- `LivePage` : インストールにログインが必要っぽい
- `Markdown Linker` : markdownでの[title]<url>形式を作成してくれる。`cmd(Windowsキー)+ctrl+c`でも行ける。
- `Mate Translate`
- `Moqups`
- `Octotree`
- `PlantUML Viewer`
- `Postman`
- `Save to Pocket`
- `Session Buddy`
- `Stylish`
- `Text Blaze`
- `Wiki Search for GitHub`
- `ZenHub` : 試験運用中
- `ato-ichinen`
- `cVim(chromium-vim)`
- `japanese-search` : 自作。。なぜか審査通らず
- `textlint`
- `μBlock Origin`
- `カラフル英語品詞分類`
- `ローカルファイルリンク有効化`

### Unused

- `Disconnect` : @office での基本認証ダイアログ問題対策。-> ソーシャルウィジェットが原因ぽかったので入れたら一切でなくなったので最高っぽい。TODO: 外しても出なくなったっぽい？
- `Google Translate`
- `IE Tab Multi (Enhance)` : 最新のchromeでは使えないためIE Tabに移行
- `Screencastify` : 画面キャプチャ(一部無料) : gif化が有料っぽいので
- `Scrum for Trello` : 一旦Trello使わないので
- `Shortcut Manager` : Vichrome でのマッピングキーを無効にするため(誤爆防止) : Vichrome 使わなくなったので不要
- `Sourcegraph for GitHub` : 特に理由はないけど使いこなせていないので使わない
- `Vichrome` : cVim に乗り換え
- `Web Cliper for Trello`
- `Weblioポップアップ英和辞典` : Chromeのtask manager見ると常に通信が発生してそう。。。 : 重い
- `firenavi-addon`
- `jsshell` : https://chrome.google.com/webstore/detail/jsshell/kmgmkbicahmbceidoidjbkbpkfogaldh

### Details

#### cVim(chromium-vim)

Keys

- Normal Mode - Miscellaneous
    - copy the URL of the current page to the clipboard

            yy

    - open the clipboard selection in a new tab

            P

    - open multiple links

            mf

- Visual/Caret Mode
    - copys the current selection

            y

    - open highlighted text in new tab

            P

- Sync : [cvim settings · GitHub](https://gist.github.com/assout/e4172ddf70f52f05abe2)
- chrome://extensions/ : Keyboard shortcuts
    - Let Chrome use <C-w> for the deleteBackWord insert mapping      : `Ctrl + W`
    - Let Chrome use <C-n> for cncpcompletion setting (see Help file) : `Ctrl + N`
    - Go to the next tab                                              : `Alt + L`
    - Go to the preview tab                                           : `Alt + H`

#### Fire Shot

- Hot key - ページ全体をキャプチャ - Ctrl + Alt + P と 保存
- Options - Capturing - Default file name - Specify template :

        %y%m%d_%H%M%S_FireShot_%t

#### Mate Translate

- Settings
    - `Shift + z` : Automatic detection -> Japanese
- Caution: TODO: chromeの認証ダイアログが閉じられちゃう？ @office
- TODO: Shiftなしのキー割り当てにしたい

#### Octotree

- Settings
    - GitHub
        - Site access token: {GitHub Personal Access Token}
    - GitLab
        - GitLab Enterprise URLs: {Local GitLab URL}
        - Remember sidebar visibility : unchecked

#### PlantUML Viewer

- SVGにする(PNGよりちょっと早い気がする)
- (遅かったら)localにplantuml-server立ててseverに指定する -> ちょっと早くなった気がする。
    - Refs: <https://github.com/plantuml/plantuml-server>
    - Server: <http://localhost:8080/plantuml> (default: <http://plantuml.com/plantuml>)

Caution: 外に出したくないファイルはローカルにサーバ立てること!

## Apps

### List

- Postman
- Simple Docker UI

## Configuration

### Settings - 設定

- Web Contents - ウェブ コンテンツ
    - Customize fonts... - フォントをカスタマイズ
        - Font : メイリオ
        - Encode - エンコード : Unicode (UTF-8)
- Languages - 言語 : English(US)
- System - システム
    - Google Chrome を閉じた際に... : Unchecked (TODO: もしかしたらしなくてもパフォーマンス改善されてるかも)

### Tool bar

- Show apps shortcuts : unchecked.

