# P-Tech Restia

FiveM向け飲食・店舗運営システム群。

## 方針

- 機能ごとに独立したFiveMリソースとして提供する。
- 共通Coreは必要になった場合のみ導入し、各モジュールの依存関係を明示する。
- 他のモジュールとの連携は原則オプションとする。
- UI・命名・設定形式はP-Tech製品群で整合させる。
- 機能仕様や対応フレームワークは設計・実装の進捗に応じて確定する。

## 命名規則

リソース名は `ptech_restia_<module>` とする。

候補モジュール（**未実装**）：
- `ptech_restia_cooking` — 調理
- `ptech_restia_order` — 注文
- `ptech_restia_inventory` — 在庫
- `ptech_restia_register` — 会計

## ドキュメント

- [基本方針](docs/architecture.md)
- [開発計画](docs/roadmap.md)

> 現在は初期設計段階です。ゲーム内で利用できる機能はまだありません。
