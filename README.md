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