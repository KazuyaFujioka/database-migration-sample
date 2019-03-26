## アプリケーション用途
- データベースに何らかのマイグレーションを実行する

### 構成
- datasource/${env}/configuration.gradle
    - flywayで接続するデータベースのアクセス情報をここに配置
    - 環境変数(${env})を読み込むことで、マイグレーション実行先が切り替える  
      database-migration-partner直下に用意してあるgradle.propertiesにenv=localと指定しているので何も設定せずにマイグレーションを実行した場合は、ローカルの設定情報を使用する

- src/main/resources/db/migration
    - **マイグレーションファイル**をここに配置

#### マイグレーションファイルの配置ルール
**release_${リリース日付}/V{リリース日付}_${管理番号}_${枝番}__${マイグレーションファイル名}.sql**のような形で配置
```
例)
release_20190326/V20190326_01_01__create_schema.sql
```

#### マイグレーション実行方法
- IntelliJから実行する
    1. IntelliJの右のメニューからGradleタブを選択
    1. 表示された一覧から:partner-cmsを選択
    1. Tasks → flywayと選択
    1. flywayMigrateを選択  
    するとマイグレーションが実行される

- コマンドから実行する  
database-migration-sample直下で以下のコマンドを実行するとデータベースマイグレーションが実行される
```
./gradlew migration-sample:flywayMigrate
```