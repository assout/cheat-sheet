# Maven

Date: 2016-09-12 13:23
Tags: []
Categories: []

---

## General

- テストスキップ:
    - テストの実行のみをスキップする

            <properties>
              <skipTests>true</skipTests>
            </properties>

    - テストコードのコンパイル、およびテストの実行をスキップする

            <properties>
              <maven.test.skip>true</maven.test.skip>
            </properties>

    > 後者の場合、jar:test-jar(org.apache.maven.plugins:maven-jar-plugin:test-jar) もスキップされるようになるため、意図的に *-tests.jar を作成している場合は注意が必要です。

- 大きなメモリ領域を割り当てる
    - consoleで実施

            set MAVEN_OPTS=-Xmx2048M

        Refs: [Maven2で大きなメモリ領域を割り当てる - wutseのダイアリー](http://d.hatena.ne.jp/wutse/20071102/1193975925)
    - Eclipseで実施
            "Run As" - "Maven Build", click on the "JRE" tab, enter VM args e.g. : -Xms128M -Xmx512M
        Refs: [memory - Increase heap size in m2e Eclipse plugin - Stack Overflow](http://stackoverflow.com/questions/7899221/increase-heap-size-in-m2e-eclipse-plugin)

- pomファイルで使用できる変数

        ${project.groupId}
        ${project.version}
        ${project.build.sourceDirectory}

        project.basedir: The directory that the current project resides in.
        project.baseUri: The directory that the current project resides in, represented as an URI. Since Maven 2.1.0
        maven.build.timestamp: The timestamp that denotes the start of the build. Since Maven 2.1.0-M1

    Refs: [Maven – Introduction to the POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)

## Phase

mvnコマンドの引数に渡す、行いたいことを"Phase"という。(e.g. clean, validate, compile)

Refs: [Mavenの使い方 Maven3のはじめかた](https://kengotoda.gitbooks.io/what-is-maven/content/primer/abstract.html)

## Build Lifecycle

複数のPhaseのつながりをビルドライフサイクルという。(e.g. default, clean)

Refs:

- [ビルド・ライフサイクル Maven3のはじめかた](https://kengotoda.gitbooks.io/what-is-maven/content/primer/build-lifecycle.html)
- [Undertree's Lab: Mavenのビルドライフサイクル](http://undertrees-lab.blogspot.jp/2011/11/maven.html)

## Plugin Development

> WikiによるとMojoExecutionExceptionは設定に問題がありMojoの実行ができなかったときに、MojoFailureExceptionは依存関係やプロジェクトが持つソースコードに問題がありMojoの実行が失敗したときに投げる必要があります。
>
> Refs: [単体テストを作成する · Maven3のはじめかた](https://kengotoda.gitbooks.io/what-is-maven/content/implement-plugin/unit-test.html)

## Plugins

### Maven Compiler Plugin

- mavenのコンパイルjavaバージョンを指定する

        <properties>
            <java.version>1.8</java.version>
            <maven.compiler.target>${java.version}</maven.compiler.target>
            <maven.compiler.source>${java.version}</maven.compiler.source>
        </properties>

