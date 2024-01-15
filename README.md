# SQL基礎学習

## 問題
### 1-1
- userという名前のデータベースの作成
```sql
CREATE DATABASE user;
```
### 2-1
- 1で作成したデータベース上でテーブル作成
```sql
 CREATE TABLE user (
    id INT(20) UNSIGNED not NULL AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    age INT(3) UNSIGNED DEFAULT NULL,
    gender INT(3) UNSIGNED NOT NULL,
    updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```
### 2-2 
- user_infoテーブル作成
```sql
CREATE TABLE user_info (
    user_id INT(20) UNSIGNED NOT NULL PRIMARY KEY,
    email VARCHAR(255) NOT NULL UNIQUE,
    phone VARCHAR(16) NOT NULL,
    updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
)  ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

### 3-1 
- userテーブルにレコード作成
```sql
INSERT INTO user(name, age, gender, updated_at, created_at) VALUES ("seiji", 15, 1, CURRENT_TIMESTAMP, CURRENT_TIMESTAMP); 
```
- idは自動的に1になった
```sql
SELECT * from user;
```
```sql
mysql> select * from user;
+----+-------+------+--------+---------------------+---------------------+
| id | name  | age  | gender | updated_at          | created_at          |
+----+-------+------+--------+---------------------+---------------------+
|  1 | seiji |   15 |      1 | 2024-01-15 18:28:28 | 2024-01-15 18:28:28 |
+----+-------+------+--------+---------------------+---------------------+
1 row in set (0.00 sec)
```

### 3-2
- user_infoテーブルにレコード作成
```sql
INSERT INTO user_info(user_id, email, phone) VALUES (1, "seiji@nextbeat.net", "09011111111");
```
- updated_at,created_atはdefaultでCURRENT_TIMESTAMPを設定しているので指定する必要なかった
```sql
mysql> select * from user_info;
+---------+--------------------+-------------+---------------------+---------------------+
| user_id | email              | phone       | updated_at          | created_at          |
+---------+--------------------+-------------+---------------------+---------------------+
|       1 | seiji@nextbeat.net | 09011111111 | 2024-01-15 18:32:18 | 2024-01-15 18:32:18 |
+---------+--------------------+-------------+---------------------+---------------------+
1 row in set (0.00 sec)
```
### 4-1
- userテーブルにレコード一括追加
```sql
INSERT INTO user(name, age, gender) VALUES ("emiko", NULL, 2), ("yoshinobu", 22, 1), ("yoichi", 30, 1), ("kazuya", 18, 1), ("kaoru", 18, 3);
```
```sql
mysql> select * from user;
+----+-----------+------+--------+---------------------+---------------------+
| id | name      | age  | gender | updated_at          | created_at          |
+----+-----------+------+--------+---------------------+---------------------+
|  1 | seiji     |   15 |      1 | 2024-01-15 18:28:28 | 2024-01-15 18:28:28 |
|  2 | emiko     | NULL |      2 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
|  3 | yoshinobu |   22 |      1 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
|  4 | yoichi    |   30 |      1 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
|  5 | kazuya    |   18 |      1 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
|  6 | kaoru     |   18 |      3 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
+----+-----------+------+--------+---------------------+---------------------+
6 rows in set (0.00 sec)
```


### 4-2
- user_infoテーブルにレコード一括追加
```sql
INSERT INTO user_info(user_id, email, phone) VALUES (2, "emiko@nextbeat.net", "09022222222"), (3, "yoshinobu@nextbeat.net", "09033333333"), (4, "yoichi@nextbeat.net", "09044444444"), (5, "kazuya@gmail.com", "08055555555"), (6, "kaoru@gmail.com", "08066666666");
```
```sql
mysql> select * from user_info;
+---------+------------------------+-------------+---------------------+---------------------+
| user_id | email                  | phone       | updated_at          | created_at          |
+---------+------------------------+-------------+---------------------+---------------------+
|       1 | seiji@nextbeat.net     | 09011111111 | 2024-01-15 18:32:18 | 2024-01-15 18:32:18 |
|       2 | emiko@nextbeat.net     | 09022222222 | 2024-01-15 18:40:54 | 2024-01-15 18:40:54 |
|       3 | yoshinobu@nextbeat.net | 09033333333 | 2024-01-15 18:40:54 | 2024-01-15 18:40:54 |
|       4 | yoichi@nextbeat.net    | 09044444444 | 2024-01-15 18:40:54 | 2024-01-15 18:40:54 |
|       5 | kazuya@gmail.com       | 08055555555 | 2024-01-15 18:40:54 | 2024-01-15 18:40:54 |
|       6 | kaoru@gmail.com        | 08066666666 | 2024-01-15 18:40:54 | 2024-01-15 18:40:54 |
+---------+------------------------+-------------+---------------------+---------------------+
6 rows in set (0.00 sec)
```

### 5-1
```sql
SELECT * from user;
```

### 5-2
```sql
SELECT  from user_info;
```
### 6-1
- userテーブルに対してidとnameのみ全権取得するクエリ
```sql
SELECT id, name FROM user;
```
```sql
mysql> select id, name from user;
+----+-----------+
| id | name      |
+----+-----------+
|  1 | seiji     |
|  2 | emiko     |
|  3 | yoshinobu |
|  4 | yoichi    |
|  5 | kazuya    |
|  6 | kaoru     |
+----+-----------+
6 rows in set (0.00 sec)
```
### 6-2
- user_infoテーブルに対してuser_id,emailのみ全権取得するクエリ
```sql
SELECT user_id, email FROM user_info;
```
```sql
mysql> select user_id, email from user_info;
+---------+------------------------+
| user_id | email                  |
+---------+------------------------+
|       2 | emiko@nextbeat.net     |
|       6 | kaoru@gmail.com        |
|       5 | kazuya@gmail.com       |
|       1 | seiji@nextbeat.net     |
|       4 | yoichi@nextbeat.net    |
|       3 | yoshinobu@nextbeat.net |
+---------+------------------------+
6 rows in set (0.00 sec)
```

### 6-3
- userテーブルに対してageで降順をかけ全権取得するクエリ
```sql
SELECT * FROM user ORDER BY age DESC;
```
```sql
+----+-----------+------+--------+---------------------+---------------------+
| id | name      | age  | gender | updated_at          | created_at          |
+----+-----------+------+--------+---------------------+---------------------+
|  4 | yoichi    |   30 |      1 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
|  3 | yoshinobu |   22 |      1 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
|  5 | kazuya    |   18 |      1 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
|  6 | kaoru     |   18 |      3 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
|  1 | seiji     |   15 |      1 | 2024-01-15 18:28:28 | 2024-01-15 18:28:28 |
|  2 | emiko     | NULL |      2 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
+----+-----------+------+--------+---------------------+---------------------+
6 rows in set (0.00 sec)
```
### 6-4
- user_infoテーブルに対してcreated_atで昇順をかけ全件取得するクエリ
```sql
SELECT * FROM user_info ORDER BY created_at ASC;
```
```sql
+---------+------------------------+-------------+---------------------+---------------------+
| user_id | email                  | phone       | updated_at          | created_at          |
+---------+------------------------+-------------+---------------------+---------------------+
|       1 | seiji@nextbeat.net     | 09011111111 | 2024-01-15 18:32:18 | 2024-01-15 18:32:18 |
|       2 | emiko@nextbeat.net     | 09022222222 | 2024-01-15 18:40:54 | 2024-01-15 18:40:54 |
|       3 | yoshinobu@nextbeat.net | 09033333333 | 2024-01-15 18:40:54 | 2024-01-15 18:40:54 |
|       4 | yoichi@nextbeat.net    | 09044444444 | 2024-01-15 18:40:54 | 2024-01-15 18:40:54 |
|       5 | kazuya@gmail.com       | 08055555555 | 2024-01-15 18:40:54 | 2024-01-15 18:40:54 |
|       6 | kaoru@gmail.com        | 08066666666 | 2024-01-15 18:40:54 | 2024-01-15 18:40:54 |
+---------+------------------------+-------------+---------------------+---------------------+
6 rows in set (0.00 sec)
```

### 6-5
- userテーブルに対してidが2のレコードのみ取得するクエリ
```sql
SELECT * FROM user WHERE id = 2;
```
```sql
+----+-------+------+--------+---------------------+---------------------+
| id | name  | age  | gender | updated_at          | created_at          |
+----+-------+------+--------+---------------------+---------------------+
|  2 | emiko | NULL |      2 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
+----+-------+------+--------+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> SELECT * FROM user WHERE age <= 20;
+----+--------+------+--------+---------------------+---------------------+
| id | name   | age  | gender | updated_at          | created_at          |
+----+--------+------+--------+---------------------+---------------------+
|  1 | seiji  |   15 |      1 | 2024-01-15 18:28:28 | 2024-01-15 18:28:28 |
|  5 | kazuya |   18 |      1 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
|  6 | kaoru  |   18 |      3 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
+----+--------+------+--------+---------------------+---------------------+
3 rows in set (0.00 sec)
```

### 6-6
- userテーブルに対してageが20以下のレコードのみ取得するクエリ
```sql
SELECT * FROM user WHERE age <= 20;
```
```sql
mysql> SELECT * FROM user WHERE age <= 20;
+----+--------+------+--------+---------------------+---------------------+
| id | name   | age  | gender | updated_at          | created_at          |
+----+--------+------+--------+---------------------+---------------------+
|  1 | seiji  |   15 |      1 | 2024-01-15 18:28:28 | 2024-01-15 18:28:28 |
|  5 | kazuya |   18 |      1 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
|  6 | kaoru  |   18 |      3 | 2024-01-15 18:37:12 | 2024-01-15 18:37:12 |
+----+--------+------+--------+---------------------+---------------------+
3 rows in set (0.00 sec)
```

## 自分用メモ
### AUTO_INCREMENT
- テーブルを作成するときにカラムにAUTO_INCREMENTをつけると、データを追加したときにカラムに対して現在格納されている最大の数値に1を追加した数値を自動で格納することができる
- idで使うと自動で昇順にできて便利ということ？

### DATETIMEとTIMESTAMPの違い
- TIMESTAMP : 保存時にはタイムゾーンからUTCへ、読み出し時にはUTCからタイムゾーンへと変換される
- DATETIME : タイムゾーンの影響を受けることなく文字列として認識され保存される

### ON UPDATE CURRENT_TIMESTAMP 
 - CREATE TABLEでカラムにON UPDATE CURRENT_TIMESTAMP句をつけると、自動的に更新される

### ENGINE
- CREATE TABLEでENGINE句を使うとストレートエンジンを指定できる
- デフォルトはInnoDB

### InnoDB
- 高い信頼性と高いパフォーマンスとのバランスをとる汎用のストレージエンジン

### mysql起動方法
- `mysql.server start`
- ` mysql -u root`

### データベース選択
- `USE データベース名;`

### カレントデータベース確認
- `select database();`

### table削除
- `DROP TABLE テーブル名`


### テーブル定義確認
- `SHOW FULL COLUMNS FROM テーブル名;`