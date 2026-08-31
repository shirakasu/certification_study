# SQLの基本構文まとめ


## データ定義言語（DDL）

- CREATE TABLE: 新しいテーブルの作成

```sql
CREATE TABLE テーブル名 (
  カラム名1 データ型,
  カラム名2 データ型,
  カラム名3 データ型
);

```

- ALTER TABLE: 既存テーブルの構造変更

```sql
ALTER TABLE テーブル名
ADD COLUMN カラム名4 データ型;
```

- DROP TABLE: テーブルの削除

```sql
DROP TABLE テーブル名;
```

## データ操作言語（DML）

- SELECT: データの照会

```sql
SELECT カラム名1, カラム名2
FROM テーブル名
WHERE 条件;

```

- ORDER BY: 結果の並べ替え
- ORDER BY句は，クエリ結果を指定したカラムの値で並べ替える際に使用する



```sql
SELECT * FROM employees ORDER BY salary DESC;

```

- HAVING: グループ化後の条件指定
- HAVING句は，GROUP BYでグループ化した後に，そのグループに対する条件を指定する際に使用する



```sql
SELECT department_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 5000;

```

- INSERT: データの挿入

```sql
INSERT INTO テーブル名 (カラム名1, カラム名2)
VALUES (値1, 値2);

```

- UPDATE: データの更新

```sql
UPDATE テーブル名
SET カラム名1 = 新しい値
WHERE 条件;

```

- DELETE: データの削除

```sql
DELETE FROM テーブル名
WHERE 条件;

```

## データ制御言語（DCL）

- GRANT: ユーザーへの権限付与

```sql
GRANT 権限 TO ユーザー名;

```

- REVOKE: ユーザーからの権限剥奪

```sql
REVOKE 権限 FROM ユーザー名;

```

## その他

- CASE式: 条件式の使用

```sql
SELECT CASE 
  WHEN 条件 THEN 結果1 
  ELSE 結果2 
END AS エイリアス
FROM テーブル名;

```

- COALESCE関数: NULL値の処理

```sql
SELECT COALESCE(カラム名, デフォルト値) AS エイリアス
FROM テーブル名;

```

- NULLIF関数: NULL値の比較

```sql
SELECT NULLIF(カラム名1, カラム名2) AS エイリアス
FROM テーブル名;

```

- CASCADE: 参照データの同時削除を行う


## JOIN: テーブルの結合

- 内部結合（INNER JOIN）: 両方のテーブルに一致するデータのみを取得します。

```sql
SELECT employees.first_name, departments.department_name
FROM employees
INNER JOIN departments ON employees.department_id = departments.id;

```

- 外部結合（OUTER JOIN）: 片方のテーブルにのみ存在するデータも含めて取得します。

```sql
SELECT employees.first_name, departments.department_name
FROM employees
LEFT OUTER JOIN departments ON employees.department_id = departments.id;

```

- 自己結合（SELF JOIN）: 同じテーブルを2回使用して、関連するデータを結合します。

```sql
SELECT e1.first_name AS Employee, e2.first_name AS Manager
FROM employees e1
LEFT JOIN employees e2 ON e1.manager_id = e2.id;

```

## 副問い合わせ（サブクエリ）: クエリ内のクエリ

```sql
SELECT first_name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);

```
