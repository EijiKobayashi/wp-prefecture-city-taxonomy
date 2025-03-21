# WordPress 都道府県・市区町村 タクソノミーインポートデータ

WordPress でウェブサイトを構築する際、都道府県や市区町村をタクソノミー（カテゴリ）として登録したい場合がありますよね？
このリポジトリでは、**47 の都道府県と 1,741 の市区町村を一括登録できるデータ** を提供します。

## 特徴

- **[デジタル庁のデータ](https://catalog.registries.digital.go.jp/rc/dataset/ba-o1-000000_g2-000002)** と **[総務省の全国地方公共団体コード](https://www.soumu.go.jp/denshijiti/code.html)** を基にデータを生成
- **WP Taxonomy Import** 形式に対応
- <del>**BulkPress** 形式に対応</del>（仕様が面倒なので止めました）
- どちらのプラグインもインポート時に A-Z に並び替えられてしまいます。  
  順番を維持するため名称の前に `000 - 999 の連番＋半角空白` を付与しています。  
  この連番は SQL コマンドで削除可能です。
- どちらのプラグインもすでにアップデートされていないため要注意！

## デモサイト

以下の WordPress でデモを確認できます。

### フロントエンド

[都道府県・市区町村一覧](https://dev.d24c.com/prefecture-city/)

### 管理画面

[管理画面](https://dev.d24c.com/prefecture-city/admin/)

<!-- **ベーシック認証**

- prefecture / city -->

**ログイン情報**

- **ID**: `admin`
- **PW**: `s8Tmc(EFuZHzBDsAue`

## インポート方法

### WP Taxonomy Import を使用する場合

1. プラグイン `WP Taxonomy Import` をインストール
2. このリポジトリのデータをダウンロード
3. プラグインのインポート機能を使用して登録
   1. 都道府県 prefecture.md を登録
   2. 市区町村 city.md を登録  
      ※ 以下 3 つ同じ地名がある場合、登録されない可能性あり  
      `024 三重県mie -> 018 朝日町$asahi-cho`  
      `045 宮崎県$miyazaki -> 023 美郷町$misato-cho`  
      その際は WordPress のタクソノミー管理画面から登録してください
4. 順番を維持するための連番を SQL コマンド <del>`クイック編集` で数字を</del> で削除

```
UPDATE wp_terms
SET name = TRIM(SUBSTRING(name, 5))
WHERE name REGEXP '^[0-9]{3} ';
```

<!--

### BulkPress を使用する場合

1. プラグイン `BulkPress` をインストール
2. このリポジトリのデータをダウンロード
3. BulkPress の `Taxonomy` インポート機能を使用して登録
   -->

## 注意点

- **プラグインのアップデート**: `WP Taxonomy Import` や `BulkPress` は現在アップデートが停止している可能性があります。
- **データ更新**: 最新の都道府県・市区町村情報を元に適宜データを更新予定です。

## コントリビューション

バグ報告や機能改善の提案は **Pull Request** または **Issue** にて受け付けています！

---

**WordPress のタクソノミーを活用して、より便利な地域データ管理を実現しましょう！** 🚀
