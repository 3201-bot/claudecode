# シッピングポリシー決定表 — FREE-DDP-1KG(送料無料DDP・標準セット)

作成日: 2026-10-05
正典: `.claude/skills/ebay-listing-maker/references/business-policies.md`(3本目: Shipping)
用途: eBay `https://www.ebay.com/bp/manage` → Create policy → Shipping で入力する全項目の決定値。
lessons L9(触らなかった項目も決定事項)に従い、「デフォルトのまま」も明示的に決定として書く。

## 0. 作業前の確認(必須)

- [ ] `ebay.com/bp/manage` を開き、既存のShippingポリシーの有無を確認する
  - **既存のFREE-DDP系ポリシーがある場合は、この表で新規作成しない。** 既存を Copy して名前だけ変える(国際サービス・Rate Table・除外113ヶ所が引き継がれる)
  - 本表と既存の稼働中ポリシーが食い違ったら、**稼働中の実物が勝つ**。差分はユーザーに確認
- [ ] 出品に紐付いたポリシー(Listings列 > 0)を編集する場合は、全出品に即反映されるため実行前にユーザー確認

## 1. 決定表(全項目)

| # | 項目 | 決定値 | 備考 |
|---|---|---|---|
| 1 | Policy name | `FREE-DDP-1KG` | 名前だけで送料/関税/重量帯が分かる命名 |
| 2 | Policy description | 空欄 | デフォルトのまま(任意項目) |
| 3 | Shipping method | `Standard shipping: Small to medium items` | デフォルトのまま |
| 4 | Domestic shipping — Cost type | `Flat: Same cost to all buyers` | デフォルトのまま |
| 5 | Domestic — Primary service | `Expedited Shipping from outside US (1-4 business days)` | 「+ Add primary service」→ 検索欄に `outside US` → 該当にチェック → Save。Economy(11-23日)は不採用 |
| 6 | Domestic — Offer free shipping | **ON(チェック)** | 金額欄が `$0.00` グレーアウトになれば送料無料化の合図。手入力不要 |
| 7 | Domestic — Buyer pays (first item) | `$0.00`(自動) | 上記6の結果 |
| 8 | Domestic — Each identical item | `$0.00`(自動) | 上記6の結果 |
| 9 | Domestic — Additional service | 追加しない | デフォルトのまま |
| 10 | International shipping | **ON** | 本番ポリシーは国際設定まで組んで完成とする |
| 11 | International — Cost type | `Flat: Same cost to all buyers` | FREE-DDP系は全サービス無料 |
| 12 | International — Service 1 | `SpeedPAK Standard` / Ships to: Worldwide(除外は§13で制御) / Free shipping ON | 標準構成 |
| 13 | International — Service 2 | `SpeedPAK Expedited` / Free shipping ON | Expeditedオプション付き |
| 14 | International — Rate Table | EU向け **+$8** の Rate Table を適用。**UKは外す** | 既存アカウントにRate Tableがあればそれを選択。無ければ Seller Hub → Shipping preferences → Rate tables で先に作る |
| 15 | Local pickup | **OFF** | デフォルトのまま |
| 16 | Handling time | **`7 business days`** | デフォルト `2 business days` のまま保存しない(旧版事故) |
| 17 | Excluded locations | **下記§2のとおり合計113ヶ所** | `None` のまま保存しない(旧版事故) |
| 18 | Set as default shipping policy | 任意(初回なら ON 推奨) | 一覧で後から変更可 |

## 2. 除外地域(Excluded locations)— 合計113ヶ所

ポリシー内で設定する(アカウント全体設定ではない)。

### 地域ごと(全域除外)
- Africa — All countries
- South America — All countries
- Central America and Caribbean — All countries

### 国別(11ヶ国)
Russian Federation / Ukraine / Belarus / China / India / Turkey / Iraq / Lebanon / Yemen / Afghanistan / **Japan**(転送業者・国内転売対策)

### 国内(Additional locations)
- PO Box
- APO/FPO(軍事郵便。USPS限定でクーリエ不可)
- US Protectorates(グアム等。固定送料だと赤字)

### 除外しないもの
- Alaska/Hawaii(FedEx配達可)
- Iran / Syria / North Korea(eBayのリスト自体に無いため設定不要)

### 除外モーダルの操作順(誤爆防止・実測)
1. リージョンを1つチェック → スクリーンショットで確認 → 次へ(連続クリック禁止。「All countries」行が挿入され下がズレる)
2. 国別は検索ボックスに国名 → 単一結果をクリック → クリア → 次の国(一覧の連続クリック禁止)
3. 国が複数リージョンに重複所属していても、選択は国単位で共有されるため二重登録の心配なし
4. Done で閉じたあと、欄の件数表示が「APO/FPO (+112)」形式=合計113になっていることを確認

## 3. 保存後の検品ゲート(完了報告の前に必ず実施)

- [ ] 緑のバナー "Your shipping policy was successfully created." を確認
- [ ] 一覧 `ebay.com/bp/manage` を再読込し、Shipping行が1行増えたことを数える
- [ ] **ポリシーを開き直して**以下を実値確認
  - [ ] Handling time = 7 business days
  - [ ] Excluded locations = 113ヶ所(開き直して件数が残っていること。表示と内部状態がズレる事故あり)
  - [ ] Domestic = Expedited Shipping from outside US / Free shipping
  - [ ] International = SpeedPAK Standard + SpeedPAK Expedited / Free / EU Rate Table +$8・UK除外
- [ ] 本表の§1・§2と diff して差分ゼロ → 完了報告
- [ ] 事故があれば対処より先に `lessons.md` に記録

## 4. 補足

- Payment(`eBay Managed Payments`)と Return(`Returns 30D Buyer Pays` 推奨)が未作成なら、同じ正典の1本目・2本目の手順で先に作ると出品フォームのポリシー欄が全部埋まる
- 2025-10-17以降、eBayは日本発・米国宛にDDPを必須化済み。米国向けは Section 301 の12.5%が送料見積に含まれる(`gate-and-profit.md`)
- `bizpolicy.ebay.com` 系の直リンクは全滅。必ず `ebay.com/bp/manage` から入る
