# Maven

Date: 2016-09-12 13:23
Tags: []
Categories: []

---

## General

- Javadocスキップ

        -Dmaven.javadoc.skip=true

- テストスキップ:
    - テストの実行のみをスキップする

            mvn hoge -DskipTests=true

            // pomに書く場合
            <properties>
              <skipTests>true</skipTests>
            </properties>

    - テストコードのコンパイル、およびテストの実行をスキップする

            mvn hoge mvn install -Dmaven.test.skip=true

            // pomに書く場合
            <properties>
              <maven.test.skip>true</maven.test.skip>
            </properties>

    > 後者の場合、jar:test-jar(org.apache.maven.plugins:maven-jar-plugin:test-jar) もスキップされるようになるため、意図的に *-tests.jar を作成している場合は注意が必要です。

- 依存するライブラリのソースをダウンロード

        mvn clean eclipse:eclipse -DdownloadSources=true -DdownloadJavadocs=true

- 大きなメモリ領域を割り当てる
    - consoleで実施

            set MAVEN_OPTS=-Xmx2048M

        Refs: [Maven2で大きなメモリ領域を割り当てる - wutseのダイアリー](http://d.hatena.ne.jp/wutse/20071102/1193975925)
    - Eclipseで実施
            "Run As" - "Maven Build", click on the "JRE" tab, enter VM args e.g. : -Xms128M -Xmx512M
        Refs: [memory - Increase heap size in m2e Eclipse plugin - Stack Overflow](http://stackoverflow.com/questions/7899221/increase-heap-size-in-m2e-eclipse-plugin)

- プロファイルを指定

        mvn -P dev
        mvn -P dev,test

- pomファイルで使用できる変数

        ${project.groupId}
        ${project.version}
        ${project.build.sourceDirectory}

        project.basedir: The directory that the current project resides in.
        project.baseUri: The directory that the current project resides in, represented as an URI. Since Maven 2.1.0
        maven.build.timestamp: The timestamp that denotes the start of the build. Since Maven 2.1.0-M1

    Refs: [Maven – Introduction to the POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)

## Archetype

- クイックスタート

        mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false -DgroupId=sandbox -DartifactId=hoge

- ルートプロジェクト

        mvn archetype:generate -DarchetypeGroupId=org.codehaus.mojo.archetypes -DarchetypeArtifactId=pom-root -DinteractiveMode=false -DgroupId=sandbox -DartifactId=hoge

- Java 8

        mvn archetype:generate -DarchetypeGroupId=pl.org.miki -DarchetypeArtifactId=java8-quickstart-archetype -DinteractiveMode=false -DgroupId=com.sandbox -DartifactId=hello

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

### Maven Dependency Plugin

    mvn dependency:tree

- コマンドラインで指定したartifactを取得

        mvn dependency:get -DgroupId=javax -DartifactId=javaee-api -Dversion=7.0

    - ソースコード取得

            mvn dependency:get -DgroupId=javax -DartifactId=javaee-api -Dversion=7.0 -Dclassifier=sources

    - 取得ディレクトリ指定

            mvn dependency:get -DgroupId=javax -DartifactId=javaee-api -Dversion=7.0 -Ddest=.

- dependency の conflict を表示

        mvn dependency:tree -Dverbose -Dincludes=commons-collections

    Refs: [ApacheMavenDependencyPlugin&#x2013;Resolvingconflictsusingthedependencytree](https://maven.apache.org/plugins/maven-dependency-plugin/examples/resolving-conflicts-using-the-dependency-tree.html)

- 依存関係を分析

        dependency:analyze : analyzes the dependencies of this project and determines which are: used and declared; used and undeclared; unused and declared.
        dependency:analyze-dep-mgt : analyzes your projects dependencies and lists mismatches between resolved dependencies and those listed in your dependencyManagement section.
        dependency:analyze-only : is the same as analyze, but is meant to be bound in a pom. It does not fork the build and execute test-compile.
        dependency:analyze-report : analyzes the dependencies of this project and produces a report that summarises which are: used and declared; used and undeclared; unused and declared.
        dependency:analyze-duplicate : analyzes the <dependencies/> and <dependencyManagement/> tags in the pom.xml and determines the duplicate declared dependencies.

### Maven Eclipse Plugin

    mvn eclipse:eclipse

### Maven Graph Plugin

- サブモジュール間の依存関係グラフ表示

        mvn org.fusesource.mvnplugins:maven-graph-plugin:reactor -Dhide-external=true

### Maven Help Plugin

- 有効なpomを表示

        mvn help:effective-pom

- 有効なsettingsを表示

        mvn help:effective-settings

### Maven Javadoc Plugin

    mvn javadoc:javadoc

### Maven Surefire Plugin

- 特定のクラス、メソッドのみ実行

        mvn test -Dtest=fooClass#barMethod

