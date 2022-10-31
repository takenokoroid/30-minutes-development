# Pick up, Pick up（ピカピカ）

## Contents

- [Pick up, Pick up（ピカピカ）](#pick-up-pick-upピカピカ)
  - [Contents](#contents)
    - [Why?](#why)
    - [Installation](#installation)
    - [Usage](#usage)

### Why?

私のチームでは Notion を使ってチケット管理を行っています。Notion は Github との連携を提供していますがセキュリティの関係上私のチームでは使用できません。

以上の条件で PBI と issue を紐づけるために Notion ページの URL が必要でした。紐づけられた URL は String になりフィルターとして機能します。

Notion ページの URL は基本的には以下の形式をとります。

```
https://www.notion.so/{TEAM_NAME}/aaaabbbbcccc1234567890
```

通常であれば URL はユニークであるため、そのままコピー＆ペーストをするだけです。ただタイトルに半角文字が入ると URL はユニークではなくなります。

```
https://www.notion.so/{TEAM_NAME}/why-did-you-ask-EVA-aaaabbbbcccc1234567890
```

これはタイトルが変更されるたびに書き変わります。URL としてはリダイレクトされるため問題ありませんが、URL は紐づけ時には String になります。つまりタイトルが変更されると PBI と issue の連携が面倒になります。

私たちにはユニークな URL を得るためにタイトル箇所を切り取るツールが必要でした。

### Installation

1. npm -i

```bash
$ npm install
```

2. building...

```bash
$ npm run relative-build
```

3. deploy

以下の手順 2 に従いインストールしてください。（テストであることを十分に理解すること）

https://support.google.com/chrome/a/answer/2714278?hl=ja

### Usage

対象となる Notion を開いた状態で拡張機能を動作させましょう。

Notion ページを開いている状態。テーブルビューで Notion ページをポップアップしている状態で使用できます。
