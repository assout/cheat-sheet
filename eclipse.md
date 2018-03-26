# Eclipse

Date: 2014-09-09 13:45
Tags: []
Categories: []

---

## Prelude

- Version: Eclipse Mars
    - office: `eclipse-java-mars-2-win32-x86_64.zip`

## Settings

### General

- Tool bar - Next Annotation ▼ - Error以外 : unchecked.(エラーのみを修正していくことが多いので) : TODO: Error/Warningを両方区別して飛びたい
- Perspective
    - Outlineを右にする
    - Progress, {Other}を中央下部にする

#### Working sets

- Configure Working Sets
    - {Project Group} : 任意のプロジェクトグループごと.
    - Sandbox         : 実験用.
    - Third           : 3rd party用
    - Old             : 基本見ない古いやつ.
    - Other Projects  : デフォルトである、それ以外.

### INI files (eclipse.ini)

- メモリ割当て

        -Xms1g
        -Xmx2g

- コンソールの文字化け対応のためUTF-8にする

        -Dfile.encoding=utf-8

- プラグインの英語化(特にFindBugs)

        -Duser.language=en
        -Duser.country=US

### Tool Bar

- Launch
    - External Tools
        - External Tools Configurations..
            - Add mintty
                - Main
                    - Location: tool path (mingw64.exe)
                    - Working Directory: ${resource_loc}
                    \* 設定時、Eclipse上で「ディレクトリ」を選択していないとエラー表示されるが問題なし!
                - Build
                    - Build before launch : unchecked
                - Common
                    - Display in favorites menu : checked
                    - Launch in background : checked

### Window

- Perspective - Customize Perspective - Command Groups Availability - Window Working Set | Working Set Manipulation : checked. <http://mcuoneclipse.com/2012/05/17/eclipse-working-sets-explained/>

### Views

#### Project Explorer

- View Menu
    - Customize View - Content - Nested Projects: Checked.

#### Package Explorer

- View Menu
    - Top Level Elements   : Working Sets

#### Tasks

TasksにPackage Explorerで選択した範囲のみ表示する

- View Menu
    - Show - TODOs : checked
        - Configure Contents - Description - Text : do empty!(FIXMEとかも表示するため)

#### Problems

- View Menu
    - Show : Errors/Warnings on Project

### Preferences

- なるべくデフォルト厨
- できるものは設定のexport,importで移行する。
    \* 設定ファイル(epf)はdotfiles管理するが視認性が悪いので↓もメンテすること。

- General
    - Appearance
        - Colors and Font theme: Classsic Theme
    - Editors
        - AnyEdit Tools
            - Auto - Convert
                - Remove trailing whitespace: off
            - Convert...
                - Save modified editor buffer before executing actions: off
        - File Associations
            - ftl TODO: ?
        - Structured Text Editors
            - Task Tags
                - Enable searching for Task Tags : checked
        - Text Editors
            - Displayed tab width: 2
            - Show print margin - print margin column: specify same with Java Maximum line width value(e.g. 100).
            - Show whitespace characters : checked
            - Spelling
                - Enable spell checking : check
                - User defined dictionary : specify(hoge.add)
                - Encoding : UTF-8
    - Keys
        - Scheme: `Vim's key bindings`(pluginインストール後じゃないとできない)
        - Command : Vrapper用のキーを無効(Refs: `.vrapperrc`)
- Java
    - Appearance
        - Members Sort Order
            - case 1 - staticか否かが設計で頻繁に変わる場合 : Types -> Static Fields -> Fields -> Static Initializers -> Initializers -> Constructors -> Static Methods -> Methods
            - case 2 - keep default                         : Types -> Static Fields -> Static Initializers -> Static Methods -> Fields -> Initializers -> Constructors -> Methods
            \* ただしTypesは場合によって最下部がよさそう
            - Sort members in same category by visibility : checked
                - Public -> Protected -> Default -> Private
        - Type Filters : add [java.awt.List]
    - Code Style
        - Formatter
            - New...
                - Profile name: Eclipse [custom]
                - Initialize settings with the following profile: Eclipse [built-in]
            - Edit...
                - Indentation
                    - General settings
                        - Tab size: 2
                - Comments
                    - Enable line comment formatting : uncheck
    - Editor
        - Content Assist
            - Auto Activation - Auto activation delay (ms): 80
            - Advanced
                - Default Proposal Kinds
                    - Java Non-Type Proposals : checked!(候補が重複して表示されるように見えるので、代わりに Intelligent Java Proposals をunchecked! - > 今度はほしい時にだめになった..
        - Templates
            - testc  : Setup,Exercise,Verifyコメントを入れる
            - log    : logger定義
            - lstack : log stacktrace
    - Installed JREs
        - Add... : add system jre(in jdk).
- Team
    - Git
        - 直下
            - Cloning repositories
                - Default repository folder: D:¥admin¥Development \* @office
        - Projects
            - Automatically ignore derived resources by adding them to .gitignore : uncheck
    - Ignored Resources
        - Add Pattern... : target, Settings, .settings, .classpath, .project, *.swo, *.swp, tags, .tags
    - SVN
        - Performance
            - Comute deep outgoing state ... : uncheck

#### About Data Management

- Preferences > Data Management
- Window > Show View > Data Management > Data Source Explorer

## Plug-ins

- `AnyEdit tools plugin` : From Marketplace
- `Codic Eclipse Plugin` : <http://kenji-namba.github.io/codic-eclipse-plugin/updates> <https://github.com/kenji-namba/codic-eclipse-plugin>
- `DBViewer` : From Marketplace
- `EasyShell` : From Marketplace
- `EclEmma Java Code Coverage(jacoco)` : From Marketplace
- `Eclipse Checkstyle Plug-in` : From Marketplace
- `Eclipse Class Decompiler` : From Marketplace
- `Eclipse Explorer for Java` : From Marketplace : `EasyShell`でもできるがキーストロークが長いので。 : TODO: 1回しか実行できない
- `Eclipse Metrics Plugin(frank sauer)` : <http://metrics.sourceforge.net/update>
- `FindBugs Eclipse Plugin` : From Marketplace
- `HTML Editor (WTP) Mars` : From Marketplace
- `JBoss Tools` : From Marketplace
    - `Contexts and Dependency Injection Tools`
    - `FreeMaker IDE`
    - `JBoss JAX-RS Tools`
    - `JBoss OpenShift Tools`
- `Java Decompiler Eclipse Plug-in` : <http://jd.benow.ca/jd-eclipse/update> : required Microsoft Visual C++ 2008 SP1 Redistributable Package
- `JUnitLoop`
- `M2Eclipse(m2e)` : built-in
- `Marketplace Client` : built-in
- `Plant UML` : <http://plantuml.sourceforge.net/updatesitejuno/>
- `Properties Editor` : From Marketplace
- `Quick JUnit` : From Marketplace : デフォルトだとなぜかCtrl+0で全テスト実行されてしまう。再インストールすると直った。
- `ShellEd` : <http://sourceforge.net/projects/shelled/files/shelled/update/>
- `StepCounter` : <https://github.com/takezoe/stepcounter>
- `TM Terminal` : From Marketplace
- `UCDetector` : <http://ucdetector.sourceforge.net/update>
- `Vrapper` : <http://vrapper.sourceforge.net/update-site/stable> : MarketplaceにもあるがpluginをどうせURLから入れる。unstableのほうが機能豊富
- `eclipse-pmd` : From Marketplace TODO 不要？
- `pmd-eclipse-plugin` : From Marketplace

### Useless

- `Eclipse Color Theme`  : いらない
- `Eclipse Postfix Code Completion Plugin` : <https://raw.githubusercontent.com/trylimits/Eclipse-Postfix-Code-Completion/master/org.eclipse.jdt.postfixcompletion.updateSite/target/site/> : 結局使わない
- `File Bookmark Plugin` : <http://sourceforge.jp/projects/filebookmark/> : Eclipse Luna だと使えないっぽい。。
- `Lombok` : 不要にライブラリ使わない
- `SimplePropertyEditor` : 軽いらしいがフォントが見づらい。`Ctrl + /`でのコメントアウトトグルが効かない。
- `Subversive`           : Subversionもう使わない。
- `m2e-subversive`       : Subversionもう使わない。: Check out as Maven Project が出るようになる: File - import - Maven - Check out Maven Projects from SCM - m2e Marketplace - m2e-subversive

### CheckStyle

Sun Checks (Eclipse) を元に以下変更 TODO: 今だったらGoogle Checksのほうがよさそう
設定ファイルをファイルで保存。(External Configuration File)
TODO: デフォルトとの差分だけを管理できないか

- Miscellaneous
    - Final Parameters : ignore
- Javadoc Comments
    - Style Javadoc
        - end of sentenceFormat : ([(.|。)?!][ ¥t¥n¥r¥f<])|([(.|。)?!]$)
    - package private以下のスコープはチェックしない

### Eclipse Metrics Plugin

- Total Lines of Code          : 600
- Method Lines of Code         : 50
- Nested Block Depth           : 5
- McCabe Cyclomatic Complexity : 10
- Number of Parameters         : 5

### FindBugs

最も厳しくする。

- analysis effort: Maximal
- Reporter Configuration
    - Minimum rank to report: 20 (Of Concern)
    - Minimum confidence to report: Low
    - Reported (visible) bug categories: all check.
- Detector configuration: all check.

### M2Eclipse(m2e)

- General
    - Editors
        - File Associations
            - *.uml : Text Editor (Plant UML Viewで見たいため外部エディタで開かない)
            - pom.xml : XML Editor to default.(Maven POM EditorだとVrapperが変な動きになるので)

### PMD

- Preferences
    - PMD
        - Log file name: D:¥admin¥Tmp¥pmd-eclipse¥pmd-eclipse.log

### Subversive

- Notes
    [Eclipse subversion ディレクトリがSwitchになってしまった時 -でじうぃき](http://onlineconsultant.jp/pukiwiki/?Eclipse%20subversion%20%E3%83%87%E3%82%A3%E3%83%AC%E3%82%AF%E3%83%88%E3%83%AA%E3%81%8CSwitch%E3%81%AB%E3%81%AA%E3%81%A3%E3%81%A6%E3%81%97%E3%81%BE%E3%81%A3%E3%81%9F%E6%99%82)

### Vrapper

Plug-ins

- Java Extensions
- Split Editor Plugin
- Surround.vim
- argtextobj.vim        : 引数を対象とするtextobj.     : {motion}(i|a)a
- methodtextobj.vim     : methodを対象とするtextobj.   : {motion}(i|a)f
- textobj-line.vim      : 引数を対象とするtextobj.     : {motion}(i|a)l
- vim-indent-object.vim : 同一インデントを対象とする？ : {motion}(i|a)i?

Notes

- /¥Cで大文字小文字考慮した検索
- /¥cで大文字小文字考慮しない検索

### codic eclipse plugin

Ctrl+Shift+Dでクイック辞書検索
\* もともと割り当てられたものをALT+Ctrl+Shift+Dに退避

## Debug

実はいろいろ多機能。

- 値の変更
- 任意のコードの実行
- 任意の場所で任意の例外発生
- 条件を指定してブレークポイント
- デバッグ中にソース変更(Hotswap Bug Fixing)

Refs: [EclipseによるJavaアプリケーションのデバッグ](http://www.oki-osk.jp/esc/eclipse3/eclipse-debug.html)

### Breakpoint

- 条件を指定してブレークポイント:
    `Breakpoints` - `Conditional` に停止する条件を書く(`Ctrl + Space`で補完もできる)

## Technique, Caution

- 既存プロジェクトのインポート、既存ソースをもとにプロジェクトを作成 (意外とめんどい Refs: [java - How to create a project from existing source in Eclipse and then find it? - Stack Overflow](http://stackoverflow.com/questions/2636201/how-to-create-a-project-from-existing-source-in-eclipse-and-then-find-it))
    - Mavenプロジェクトの場合)
        - File - Import - Maven - Existing Maven Projects
    - Mavenプロジェクト以外の場合)
        - `.project`ファイルが存在する場合)
            - File - Import - General - Existing Project into workspace
        - `.project`ファイルが存在しない場合)
            - ProjectNameの名前のディレクトリをworkspace内に作成し、ソースを全て格納
            - [File] - [New] - [JavaProject] : [Project name]と[Location]を↑と同じに指定
            - 警告が出るので[Next >]押下で作成できるはず

- JUnit構成のプロジェクト作成
        File - New - Maven - Maven Project
- システムプロパティを設定してrun
        Run - Run configurations, select project, second tab: “Arguments”. Top box is for your program, bottom box is for VM arguments, e.g. -Dkey=value.
- 特定のリビジョンに戻したい
        ナビゲータービューで、元に戻したいファイルを右クリック→置換→HEAD改訂（またはローカルヒストリー）。
        置換機能で書き換えられる箇所を知りたい場合には、
        ナビゲータービューで、元に戻したいファイルを右クリック→比較→HEAD改訂（またはローカルヒストリー）
    Refs: [Eclipseでローカルのファイルを元に戻す方法 Hack](http://hack.aipo.com/archives/1447/)
- 補完アクション(Save Actions)が無効にならない
    Any Edit プラグインが悪さしている可能性がある。[アウトプットメモ: eclipseでソースコードを保存したときに&#12289;空の行のインデントが自動で削除されないようにする方法](http://y188ra.blogspot.jp/2011/01/eclipse.html)
- ローカルヒストリーから復元: `Package Explorer`で右クリック -> `Restore from Local History...`を選択


