# business-policies.md — ビジネスポリシー3点セットの構築手順(実測版)

フォーム操作は2026-07-21にポリシー0件の白紙アカウントで全手順を実測。設定値は稼働中の実アカウント(返品60日・除外113ヶ所・ハンドリング7営業日)と設計正典に準拠。eBayのUI変更で画面が変わっていたら、この文書を実測し直して更新する。

## ★最優先ルール(これを飛ばした事故が実際に起きた)

このファイルは**フォームの操作手順**を教えるものであって、**設定値を決める権限**を与えるものではない。設定値の正典は別にある。

1. **白紙から自分で設定値を考えない。** 設定値の正典は次の2つ:
   - **本ファイルに書かれた設計値**(除外国リスト・ハンドリング7営業日・国際サービス構成。以下の手順内にすべて明記してある)
   - **ユーザーの実アカウントの既存ポリシー**(`ebay.com/bp/manage`)。既存ポリシーがあるなら**新規作成ではなくコピーして名前と金額だけ変える**のが正
2. 本ファイルと実アカウントの既存設定が食い違ったら、**稼働中の実物が勝つ**(実物はユーザーが運用で検証済みのため)。判断に迷う差分はユーザーに確認する。
3. 事故事例(2026-07-21): 本ファイルの旧版だけを読んだAIが「返品不可・除外国ゼロ・ハンドリング2日」という劣化版を白紙から作り、「成功」と報告した。操作の成功と設定値の正しさは別物(lessons L6・L15)。**設定作業にも検品ゲートを効かせる: 作った後、正典・実物既存ポリシーとdiffして差分ゼロを確認してから完了報告。**

## 前提と権限

- ビジネスポリシーの作成・変更は**アカウント設定の変更**にあたる。スキルの絶対安全ルール3の対象なので、AIが勝手にやらない。**ユーザーが明示的に依頼した初期セットアップ作業としてのみ実行する。**
- 稼働中アカウント(出品に紐付いたポリシーがある)での変更は、非破壊に見えても全出品に即反映される。**実行前にユーザー確認必須。**
- 出品に最低限必要なのは Payment / Return / Shipping の3本。この3本があれば出品フォームのポリシー欄が全部埋まる。
- 一度作れば全出品で使い回す。出品ごとに作るものではない。

## 管理画面への行き方(重要: 直リンクは死んでいる)

- **正しいURL: `https://www.ebay.com/bp/manage`**
- ネット記事によく載っている `bizpolicy.ebay.com/businesspolicy/manage` と `.../policyoptin` は、ログイン済みでも「SORRY Something went wrong」エラーページになる(実測)。使わない。
- UIから辿る場合: My eBay → Account タブ → 左メニュー Selling → **Business Policies**。
- 各作成フォームの直URL(遷移確認済み): Payment `/bp/payment/create`、Return `/bp/rtn/create`、Shipping `/bp/ship/create`。
- 白紙アカウントでも opt-in 画面は出ず、いきなり「Manage your business policies」(0件の一覧)が表示された。opt-in 操作は不要。

作成はすべて一覧右上の **「Create policy」ボタン → ドロップダウンから Payment / Return / Shipping を選択**。保存に成功すると一覧に戻り、緑のバナー(例: "Your payment policy was successfully created.")が出て一覧に1行増える。**各保存後に一覧の行数が増えたことを目視確認してから次に進む。**

## 1本目: Payment「eBay Managed Payments」

やることは名前を入れて保存するだけ。決済方法自体はeBay管理(Managed Payments)で固定されており、フォームに決済手段の選択肢は無い。

1. Create policy → Payment
2. Policy name: `eBay Managed Payments`
3. デフォルト値をそのまま使う(実測):
   - 「Require immediate payment when buyer uses Buy It Now」= **ON**(チェック済みで出てくる。そのままにする。即時支払い必須は無在庫・有在庫どちらでも事故防止になる)
   - Allow offline payment(Cash On Pickup / Check / Money Order)= **すべてOFF**(そのまま。オンにしない)
4. Save

## 2本目: Return — 2択から選ぶ(教材推奨は「返品受付」)

**先に大前提: 「返品不可」にしても返品リスクは消えない。** INAD(Item Not As Described=説明と違う)クレームは、返品設定に**関係なく**eBayが返品・返金を強制する。返品設定が効くのは「買い手都合(remorse)の返品」だけ。つまりNo Returnで防げるのは気変わり返品のみで、事故の本丸(INAD)は防げない。

その上で判断材料:

- 返品受付30日以上は**Top Rated Seller資格の条件**のひとつで、検索露出・バイヤーの購入転換率でも有利に働く
- **教材のデフォルトは30日・返送料買い手負担。** 30日はTop Rated要件を満たす最短で、フォームのデフォルト値でもあるので操作も最少
- 稼働中の実アカウントは**60日・返送料セラー負担(国内・国際とも)**で運用している。60日はより太っ腹な上級設定、国際返品の返送料セラー負担はコスト露出が大きい。真似るのは実績が付いてからでよい

### 選択肢A(推奨・教材デフォルト): 返品受付30日・買い手負担

1. Create policy → Return
2. Policy name: `Returns 30D Buyer Pays`(期間と負担が名前で分かるように)
3. Domestic returns「Accept returns」トグル = **ON** → 表示される詳細はデフォルトのまま(実測):
   - Allowed within: `30 Days`(デフォルト。選択肢は14/30/60の3つ)
   - Return shipping paid by: `Buyer`(デフォルト)
   - Refund method: `Money back`(デフォルト)
4. International returns「Accept returns」トグル = **ON** → こちらも同じデフォルト(30 Days・Buyer・Money back)のまま
5. Save

つまり選択肢Aは「トグル2つをONにして名前を入れて保存」だけ。期間を60日にしたい場合のみAllowed withinを両セクションで変更する。2026-07-21に白紙アカウントで実測済み(30日版・60日版とも作成成功)。

### 選択肢B: 「No Return Accepted」(意味を理解した上で選ぶ)

買い手都合の返品だけを断る設定。INADは防げず、Top Rated資格は満たさなくなる。それでも初期の様子見として選ぶ場合:

1. Create policy → Return
2. Policy name: `No Return Accepted`
3. Domestic / International returns の「Accept returns」トグル = **両方OFF**(デフォルトのままで両方OFF・実測)
4. Save

## 3本目: Shipping「FREE-DDP-1KG」

送料込み(Free)・DDPクーリエ・1kg級の基本ポリシー。手順が一番長い。**除外国とハンドリングはデフォルトのまま保存してはいけない**(旧版の事故ポイント)。

既存の稼働中アカウントで作る場合は、この手順ではなく**既存のFREE-DDP系ポリシーをCopyして名前だけ変える**こと(国際サービス・Rate Table・除外113ヶ所がそのまま引き継がれる)。以下は白紙アカウントで1本目を作るときの手順。

1. Create policy → Shipping
2. Policy name: `FREE-DDP-1KG`
3. Shipping method: `Standard shipping: Small to medium items`(デフォルトのまま)
4. Domestic shipping の Cost type: `Flat: Same cost to all buyers`(デフォルトのまま)
5. **「+ Add primary service」をクリック** → 「Add services」モーダルが開く
   - 検索欄に `outside US` と入れる(日本発送のセラーはここが肝。素のリストはUPS/USPS/FedExなど米国内サービスしか見えない)
   - 検索結果3件(実測): Economy Shipping from outside US (11-23営業日) / Standard Shipping from outside US (5-10営業日) / **Expedited Shipping from outside US (1-4営業日)**
   - DDPクーリエ(FedEx/DHL)設計なので **Expedited Shipping from outside US** にチェック → モーダルの **Save**
   - ※ SpeedPAK Economy相当(11-23営業日)は不採用。クレーム源になり、$750超の署名要件にも対応しない(正典準拠)
6. **「Offer free shipping」にチェック**を入れる → Buyer pays (first item) / Each identical item の金額欄が `$0.00` でグレーアウトされる(これが送料無料になった合図)
7. International shipping: 標準構成は **SpeedPAK Standard + SpeedPAK Expedited + EUのRate Table(+$8・UKは外す)**。FREE-DDP系は全サービス無料+Expeditedオプション付き。この構成のとおり組む(ユーザーの実アカウントに稼働中の構成があればそちらをコピーするのが正)。白紙アカウントでの操作練習だけならOFFのままでも保存はできるが、**本番ポリシーとしては国際設定まで組んで完成**とする
8. Local pickup: **OFF**(デフォルトのまま)
9. Handling time: **`7 business days` に変更する。** デフォルトは `2 business days` で出てくるが、そのまま保存しない。無在庫運用の仕入れ→取り寄せ→検品→発送のリードタイムで、正典・稼働中実アカウントとも7営業日
10. Excluded locations: **必須ステップ。`None` のまま保存しない。**
    - 除外は**このシッピングポリシーの中で**設定する(「アカウント全体の設定で管理する」は旧版の事実誤認。稼働中実アカウントはポリシー内除外113ヶ所で運用している)
    - 「Edit」等から除外モーダルを開き、以下を除外(正典準拠):
      - 地域ごと: **アフリカ全域 / 南アメリカ全域 / 中央アメリカ&カリブ全域**
      - 国別: **ロシア・ウクライナ・ベラルーシ・中国・インド・トルコ・イラク・レバノン・イエメン・アフガニスタン・日本**(日本除外は転送業者・国内転売対策)
      - 国内(Additional locations): **PO Box(私書箱)・APO/FPO(軍事郵便=USPS限定でクーリエ配達不可)・US Protectorates(グアム等=別料金ゾーンで固定送料だと赤字)**
      - Alaska/Hawaii は開けておく(FedEx配達可・料金差は許容範囲)
      - イラン・シリア・北朝鮮はeBayのリスト自体に無いので設定不要
    - ※ 除外モーダルは**表示と内部状態がズレる事故**が過去にあった。保存後にもう一度開いて、除外件数(実アカウント実測で113ヶ所)が残っていることを確認する
11. Save

## 完成確認

一覧(`ebay.com/bp/manage`)に3行あればOK:

| Type | Name | Listings |
|------|------|----------|
| Payment | eBay Managed Payments | 0 |
| Return | Returns 30D Buyer Pays(またはNo Return Accepted) | 0 |
| Shipping | FREE-DDP-1KG | 0 |

行数確認だけで終わらせない。**Shippingポリシーを開き直して、ハンドリング7営業日と除外国リスト(113ヶ所)が保存されていることまで確認**し、本ファイルの設計値とdiffして差分ゼロを確認してから完了報告(lessons L15)。

Listings列は使用中の出品数。0のポリシーは後から自由に編集・削除できるが、出品に紐付いた後の編集はその全出品に即反映されるので、紐付き後は編集前にユーザー確認を取る。

## 除外モーダルのUIの罠(2026-07-21の再実測で踏んだもの)

除外国の設定は本手順で一番誤爆しやすい。以下は白紙アカウントでの実測:

- **リージョンのチェックボックスは、チェックすると直下に「All countries」リンク行が挿入され、それより下の行が全部ズレる。** 複数のリージョンを連続クリックすると2つ目以降が別の行に誤爆する(実測でOceaniaを誤チェックした)。**1クリックごとにスクリーンショットで確認**してから次を押す。
- リージョン内の国別ピッカーも同じ罠: **チェックした国は上部の「Selected」グループに移動して一覧全体が並び替わる**。一覧を上から連続クリックすると誤爆する(実測でBahrain/Bhutan/Brunei/Cambodiaを誤チェックした)。**検索ボックスに国名を入れて単一結果をクリック→クリア→次の国**、の1国ずつ方式が安全。
- 国別に絞る手順: リージョンをチェック(全域選択になる)→「All countries」リンクをクリック→ピッカー内の「Clear」で全解除→検索で対象国だけチェック→Done。
- **国は複数リージョンに重複所属している**(例: Iraq・Turkey・Lebanon・YemenはAsiaとMiddle East両方のリストに出る)。選択は国単位のセットとして共有され、リージョン行の表示は「Iraq only」「5 countries」のように連動して変わる。片方で選べばもう片方にも反映されるので二重登録の心配は不要。
- リージョン一覧に覚えのない部分選択(「Russian Federation only」等)が一瞬表示されることがあった=**表示と内部状態のズレを実測で確認**(正典の警告どおり)。Doneで閉じたあと、Excluded locations欄の件数表示(「APO/FPO (+112)」形式=合計113)と、保存後にポリシーを開き直しての再確認を必ずやる。
- 完成形の確認値: 正典どおりに設定すると除外は**合計113ヶ所**(Africa全域/South America全域/Central America and Caribbean全域+露宇白・中印・土・イラク・レバノン・イエメン・アフガン・日本+APO/FPO+US Protectorates+PO Box)。

## ハマりどころ(実測で踏んだもの)

- **旧版最大の事故: デフォルト値を「決定」として保存した。** ハンドリング2日・除外None・返品不可は、フォームのデフォルトであって設計値ではない。触らなかった項目も決定事項(lessons L9)
- **テスト用アカウントのポリシーは永続を当てにしない。** 2026-07-21朝に作った3本が同日午後には0件に消えていた(原因不明)。テスト垢での実測はその場で記録を取り切る。
- **既存ポリシーの編集保存は非同期。** 保存すると「Your return policy is being updated. Check back later.」のバナーが出て、一覧のStatusにしばらく「Update in progress」と表示される(新規作成は即時)。反映確認は少し待ってから開き直す。
- **bizpolicy.ebay.com 直リンクは全滅**。エラーページが出ても壊れているのはリンクだけ。`ebay.com/bp/manage` に行き直す。
- Shippingのサービス選択で検索を使わずスクロールで探すと、米国内サービスの海に沈む。**必ず `outside US` で検索**。
- 「Offer free shipping」にチェックを入れる前に金額欄に$0を手入力する必要はない。チェックだけで$0.00固定になる。
- 保存ボタンは名前が空だとグレーアウトのまま。名前を入れると青くなる。
