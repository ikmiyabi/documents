# INNER JOINとOUTER JOINの違い
## INNER JOIN
- 指定した条件に合致するテーブルを結びつけるレコード同士を結合させる（内部結合）
- 指定した条件に合うレコードがない場合は取得しない
- 一番よく使うJOIN

例）
id,name,company_idのカラムをもつuserテーブルと
id,nameを持つcompanyテーブルを結合する

```SQL
SELECT u.id,
    u.name,
    u.company_id,
    c.id,
    c.name
FROM user u
INNER JOIN company c
    ON u.company_id = c.id
```

## OUTER JOIN
- 指定した条件に合うレコードがない場合も取得する
- LEFT JOINは結合される側（右側）のレコードがベース
- RIGHT JOINは結合する側（左側）のレコードがベース
- ベースのレコードは条件に合致するものがなくても残る

## INNER JOINとOUTER JOINの違い
- INNER JOINは条件に合致するレコードだけ取得する
- OUTER JOINは条件に合致しないレコードも取得する

## 省略について
- ただの JOIN は INNER JOIN の省略形
- LEFT JOIN は LEFT OUTER JOIN の省略形
- RIGHT JOIN は RIGHT OUTER JOIN の省略形
