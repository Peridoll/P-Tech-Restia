# FiveM飲食システム調査 — 2026-10-13

## 目的
Restiaの設計に先立ち、公開FiveM飲食関連リソースの機能、公開形態、連携方式を初期調査する。調査内容は各公開製品ページ・リポジトリ・Cfx.reの説明から抽出したもので、実機導入・コード監査・購入検証は未実施。

## 主要リソース
| 名称 | 配布 | 公開説明で確認できた機能 | Restiaで参考にする点 | ソース |
|---|---|---|---|---|
| Quasar Restaurant Creator | 商用 | ゲーム内店舗作成、注文画面、厨房注文、料理ミニゲーム、レシピ、冷蔵庫、配送、Boss Menu | 店舗設定・注文と調理フロー | https://www.quasar-store.com/docs/restaurant-creator |
| g-order-system | 商用、別途unlocked版案内あり | 多店舗、POS、レシート決済、セルフ注文、スタッフ通知、任意の調理機能、QBox対応 | POSとセルフ注文、外部連携 | https://forum.cfx.re/t/realistic-advanced-pos-order-restaurant-system-billing-cooking-qb-esx-qbox/5352904 |
| Restaurant Management Suite | 商用 | WYSIWYGメニュー、DUI壁面スクリーン、厨房注文、レビュー、告知 | メニュー表示・厨房UI | https://forum.cfx.re/t/restaurant-management-suite-menu-editor-dui-screens-kitchen-orders-esx-qbcore-qbox/5400531 |
| v-supplychain-restaurants | ソース公開 | レストランと倉庫、配送、料理場所、レジ、トレイ、座席、メニュー | 物流・店舗コンフィグ | https://github.com/Virgildev/v-supplychain-restaurants |
| Pops Diner Job | 無料・ソース公開と説明 | 調理、店舗インタラクション、MLO変更、jim-consumables連携 | 既存の調理ジョブ実装 | https://forum.cfx.re/t/free-qb-pops-diner-job/5176708 |
| Jim-Consumables | 無料・ソース公開 | 食事・飲み物の消費、アニメーション維持、進捗バー設定。QBCore/ESX/QBox/OX | 着席時のアニメーション競合回避 | https://github.com/jimathy/jim-consumables |
| JamzRestaurantJob | 商用 | NPC来店、受付・面接、シフト、テーブル接客、注文、請求、清掃 | 店員・NPCテーブルサービスの設計 | https://forum.cfx.re/t/jamzrestaurantjob-full-restaurant-waiter-experience-qbcore-esx-qbox/5409571 |
| UWU Cafe Job V2 | 商用 | 店舗エリアの出退勤、セルフ注文キオスク、レシート | 店舗業務・注文導線 | https://forum.cfx.re/t/qb-qbox-esx-uwu-cafe-job-v2-script/5376576 |
| jim-shops | 無料・ソース公開 | 店舗設定、ジョブ制限、Ped、Stash、商品販売 | 既存店舗管理と連携 | https://github.com/jimathy/jim-shops |

## 現時点の知見
- 店舗・注文・厨房・食材・店舗経営を統合した既存製品は複数存在する。
- 多くのリソースは既存インベントリ、ターゲット、ジョブ・請求機能と連携する。
- 「料理をインベントリに入れず、指定席でのみ食べて高回復」「店舗ごとの有人/自動提供の切替」を**同時に満たす**かどうかは、今回確認した公開説明からは判定できない。不存在と断定しない。
- 有人/自動提供の切替と食事体験の独立モジュール化はRestiaで検証する主要な設計ポイント。

## Restiaの方針案
1. `ptech_restia_dining`: 店内専用料理、座席、提供ステート、食事時間、回復効果を最初の対象にする。
2. 決済・注文・調理とは疎結合にし、独立導入できるようにする。
3. `serviceMode = 'staff' | 'auto'` を店舗ごとに設定する（既定の設計方針）。
4. クライアント表示と別に、サーバー側で距離・座席・状態遷移・二重支払い/回復を検証する。
5. QBox/QBCore/ESX等の対応範囲と具体的なステータス連携APIは現行サーバー構成を確認してから確定する。

## 次段階の追加調査
- 各リソースの正確なライセンス・再利用条件・更新状況・ソース公開範囲
- 実際の座席・食事アニメーション、食べかけキャンセル処理
- インベントリなしで料理を提供する公開実装
- QBox・ox_inventory等への依存、他リソースとの競合
- 既存導入済みのサーバーリソースの実物調査

この資料は初期の公開情報調査であり、製品の性能・安全性・実装可能性を保証しない。
