# coding-principles

Date: 2017-05-14 21:06
Tags: []
Categories: []

---

## Template

```markdown
## ${Principle ID} : ${Summary}

Description.

## Problematic code - 問題のあるコード:

## Correct code - 正しいコード:

## Rationale - 理論的根拠:

## Exceptions - 例外事項:
```

## Examples

```markdown
## P001 : コンストラクタインジェクションのみを使用する

インジェクと方式はコンストラクタインジェクションを使用する。

## Problematic code - 問題のあるコード:

```java
class Hoge {
    @Inject
    Target t;
}
```

## Correct code - 正しいコード:

```java
class Hoge {

    prviate final Target t;
}
```
## Exceptions - 例外事項:
```

## CP0001

## Want to escape a single quote? echo 'This is how it'\''s done'.

(Note: in v0.4.6, the error message was accidentally missing the backslash)

## Problematic code:

echo 'This is not how it\'s done'.
Correct code:

echo 'This is how it'\''s done'.
Rationale

In POSIX shell, the shell cares about nothing but another single quote to terminate the quoted segment. Not even backslashes are interpreted.

POSIX.1 Shell Command Language § 2.2.2 Single Quotes:

Enclosing characters in single-quotes ( '' ) shall preserve the literal value of each character within the single-quotes. A single-quote cannot occur within single-quotes.

## Exceptions

If you want your single quoted string to end in a backslash, you can rewrite as 'string'\\ or ignore this warning.
