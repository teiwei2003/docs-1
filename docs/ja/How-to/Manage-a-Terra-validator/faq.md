# バリデーターFAQ

:::警告の提案
検証者になる前に、このドキュメントを注意深くお読みください。
:::

## 一般的な概念

### バリデーターとは何ですか？

Terra Coreは、Tendermintコンセンサスによってサポートされています。検証者はフルノードを実行し、ブロードキャスト投票を通じてコン​​センサスに参加し、新しいブロックをブロックチェーンに送信し、ブロックチェーンのガバナンスに参加します。検証者は、委任者に代わって投票できます。バリデーターの議決権は、総株式数に基づいて加重されます。

### フルノードとは何ですか？

フルノードは、ブロックチェーントランザクションとブロックを検証するプログラムです。ベリファイアはフルノードを実行する必要があります。フルノードは、ブロックヘッダーとトランザクションのごく一部のみを処理するライトノードよりも多くのリソースを必要とします。フルノードを実行するということは、妥協のない最新バージョンのTerra Coreソフトウェアを、ネットワーク遅延が少なく、ダウンタイムなしで実行していることを意味します。

すべてのユーザーは、バリデーターになるつもりがない場合でも、完全なノードを実行するように勧めることができます。

### 質権とは何ですか？

ルナ保有者がルナをバリデーターに委任するとき、彼らは***賭けをします。 ***ステーキングはバリデーターの重みを増し、それは彼らに役立ち、その見返りに、委任者は報われるでしょう。

Columbus-5 Mainnetは、パブリックプルーフオブステーク(PoS)ブロックチェーンです。つまり、バリデーターの重み(総エクイティ)は、バリデーターに委託するエクイティトークン(ルナ)の数と、外部の委任者によってバインドされたルナの数によって決まります。バリデーターの重みは、それらがアクティブなバリデーターであるかどうか、およびブロックを提案する頻度を決定します。より高い重みを持つ検証者は、より多くのブロックを提案し、したがってより多くの収入を得るでしょう。

アクティブなバリデーターセットは130のバリデーターで構成されており、最も多くのルナを保持しています。基盤となるバリデーターの権利と利益は、常にネットワークへの参入障壁を構成します。一番下のバリデーターよりも多くのエクイティを持つバリデーターを作成することが、アクティブセットに入る唯一の方法です。検証者が二重署名するか、多くの場合オフラインである場合、過失と違法行為を罰するという合意によって、誓約されたルナ(ユーザーから委託されたルナを含む)が減少するリスクがあります。

### クライアントとは何ですか？

委任者はルナの所有者であり、バリデーターの実行に責任を負うことなく、誓約報酬を受け取りたいと考えています。 Terra Stationを介して、ユーザーはLunaを検証者に委任し、検証者の収入の一部を引き換えに取得できます。収入の分配方法の詳細については、[エクイティインセンティブとは何ですか？]を参照してください。 ](#what-are-the-incentives-to-stake)および[バリデーターのコミッションは何ですか？ ](#what-is-a-VerifierCommittee)。

委任者は、誓約のメリットと報酬を検証者と共有します。検証者が成功した場合、その委任者は常に報酬構造を共有します。バリデーターが削減されると、プリンシパルのシェアも削減されます。これが、委任者が委任する前に検証者に対してデューデリジェンスを実施する必要がある理由です。委任者は、共有を複数のバリデーターに分散させることによって分散することもできます。

デリゲーターは、バリデーターの選択を担当するため、システムで重要な役割を果たします。クライアントであることは受動的な役割ではありません。委任者は、警戒を怠らず、検証者の動作を積極的に監視し、現在の検証者がそのニーズを満たすことができないと感じたときに再委任する必要があります。

## バリデーターになる

### バリデーターになる方法は？

ネットワークの参加者は誰でも、バリデーターを作成してそのバリデータープロファイルを登録することにより、バリデーターになる意思を表明できます。次に、候補者は次のデータを含む `create-validator`トランザクションをブロードキャストします。

-**公開鍵:**検証オペレーターは、流動性のある資金を検証および保持するためにさまざまなアカウントを持つことができます。送信されたPubKeyは、バリデーターが_prevotes_および_precommits_に署名するために使用する秘密鍵に関連付けられている必要があります。

-**アドレス:** `terravaloper-`アドレス。これは、検証者を公に識別するために使用されるアドレスです。このアドレスに関連付けられた秘密鍵は、報酬のバインド、バインド解除、および請求に使用されます。

-**名前**(**ニックネーム**とも呼ばれます)

-**ウェブサイト** _(オプションですが推奨)_

-**説明** _(オプションですが推奨)_

-**初期手数料率:**ブロック規制、ブロック報酬、および元本に請求される手数料の手数料率。

-**最大コミッション:**バリデーターが許可する最高のコミッション率。 (これは変更できません)

-**コミッションの変更率**:バリデーターのコミッションの1日あたりの最大増加額。 (変えられない)

-**セルフバインディングの最小数**:バリデーターが常に必要とするバインディングLunaの最小数。検証者の自己拘束力のある誓約がこの制限よりも低い場合、その誓約プール全体が解放されます。

-**初期自己結合量**:バリデーターが自己結合するLunaの初期量。

**例:** 
```bash
terrad tx staking create-validator
    --pubkey terravalconspub1zcjduepqs5s0vddx5m65h5ntjzwd0x8g3245rgrytpds4ds7vdtlwx06mcesmnkzly
    --amount "2uluna"
    --from tmp
    --commission-rate="0.20"
    --commission-max-rate="1.00"
    --commission-max-change-rate="0.01"
    --min-self-delegation "1"
    --moniker "gazua"
    --chain-id "test-chain-uEe0bV"
    --gas auto
    --node tcp://127.0.0.1:26647
```

バリデーターを作成して登録した後、Luna保有者は、Lunaを委任して、プールに共有を効果的に追加できます。バリデーターの総資本は、それ自体が拘束するルナと外部のプリンシパルが拘束するルナの合計です。

**最初の130個のバリデーターのみがアクティブまたは*バインドされたバリデーター***と見なされます。バリデーターの総エクイティが上位130未満の場合、バリデーターはそのバリデーター特権を失い、アクティブセットの一部ではなくなり、**バインド解除モード**に入り、最終的に**ブロック解除**または非アクティブになります。 。

## バリデーターキーとステータス

### キーの種類は何ですか？

キーには2つのタイプがあります。

-**テンダーミントキー:**公開キー「terravalconspub」に関連付けられたブロックハッシュに署名するために使用される一意のキー。

  -このキーは、 `terradinit`を使用してノードを作成するときに生成されます。
  -「terradtendenmintshow-validator」を使用してキーを表示します

    **例:** `terravalconspub1zcjduc3qcyj09qc03elte23zwshdx92jm6ce88fgc90rtqhjx8v0608qh5ssp0w94c`

-**アプリキー:**これらのキーはアプリから作成され、トランザクションに署名するために使用されます。バリデーターとして、1つのキーを使用してステーキングに関連するトランザクションに署名し、別のキーを使用してoracleに関連するトランザクションに署名することができます。アプリケーションキーは、公開キー「terrapub-」とアドレス「terra-」に関連付けられています。どちらも「terradkeysadd」によって生成されたアカウントキーから派生しています。

:::警告警告
バリデーターのオペレーターキーはアプリケーションキーに直接関連付けられていますが、予約済みのプレフィックスはこの目的でのみ使用されます: `terravaloper`と` terravaloperpub`
:::

### バリデーターはどのような状態になりますか？

`create-validator`トランザクションを使用してバリデーターを作成した後、次の3つの状態になります。

-`bonded`:アクティブでコンセンサスに参加しているバリデーター。バリデーターは報酬を受け取っており、不正行為のためにカットされる可能性があります。

-`unbonding`:アクティブな濃度になく、コンセンサスに参加してはならないバリデーター。検証者には報酬はありませんが、不正行為により罰せられる可能性があります。これは、「結合」から「非結合」への遷移状態です。ベリファイアが「バインド解除」モードで「再バインド」トランザクションを送信しない場合、状態遷移が完了するまでに3週間かかります。

-`unbonded`:アクティブセットになく、ブロックに署名しないバリデーター。バインドされていないバリデーターを減らすことはできません。また、操作から報酬を受け取ることもできません。 Lunaをバインドされていないバリデーターに委任することは引き続き可能です。 「バインドされていない」バリデーターからの委任のキャンセルは即座に行われます。

すべての委任者は、検証者と同じステータスになります。

委任は必ずしも拘束されていません。ルナは、委託および結合、委託および非結合、委託および非結合、またはモバイルにすることができます。

### 「自己拘束」とは何ですか？ 「自己拘束力」を高めるにはどうすればよいですか？

バリデーター演算子の「自己拘束」とは、それ自体に委託されたルナの量を指します。より多くのLunaをバリデーターアカウントに委任することで、自己拘束力を高めることができます。

### アクティビティセット外のバリデーターに委任できますか？

Terra Stationに表示されない場合でも、ベリファイアに委任できます。次のURLの最後に、目的のバリデーターのterravaloperアドレスを追加するだけです。

`https://station.terra.money/validator/<terravaloper-address>`

バリデーターにテラバロパーアドレスを尋ねます。

アクティブセット外のバリデーターに委任する場合は注意してください。一部の非アクティブなバリデーターは、投獄されているか、サポートされていない可能性があります。 Stationは、コンセンサスに参加できるアクティブまたは最近アクティブなバリデーターのみを表示します。

### タップはありますか？

[Terra蛇口](https://faucet.terra.money/)を使用してテストネットコインを入手します。

### アクティブな(バインドされた)バリデーターになるために誓約しなければならないルナの最小量はありますか？

最小値はありません。合計エクイティが最も高い上位130のバリデーター(そのうち、合計エクイティ=自己拘束力のあるエクイティ+委任されたエクイティ)は、アクティブなバリデーターのセットを構成します。下部にある130番目のバリデーターは、アクティブセットの参入障壁を設定します。

### 委任者はどのようにバリデーターを選択しますか？

プリンシパルは、独自の基準に従ってバリデーターを自由に選択できます。これには次のものが含まれます。

-**自己バインドされたルナの数:**バリデーターが住宅ローンプールにバインドしたルナの数。より多くの自己拘束力のあるLunaバリデーターを使用すると、ゲーム内のスキンが増え、アクションに対する責任が高まります。

-**委託されたルナの量:**バリデーターに委託されたルナの合計量。ハイステークスは、コミュニティが検証者を信頼していることを示しますが、それはまた、検証者がハッカーのより大きな標的であることを意味します。大きな株式は大きな議決権を提供します。これはネットワークを弱めます。いつでも、誓約されたルナの33％以上がアクセスできなくなると、ネットワークは機能しなくなります。インセンティブと教育を通じて、過剰な議決権を持つバリデーターを委任することで、これを防ぐことができます。ベリファイアが委任するルナの数が増えると、ベリファイアの魅力が低下することがあります。

-**コミッション率:**バリデーターが委任者に分配する前に報酬に適用するコミッション。

-**追跡レコード:**委任者は、委任する予定のバリデーターの追跡レコードを表示できます。これには、優先順位、提案に対する過去の投票、過去の平均稼働時間、およびノー​​ドが侵害される頻度が含まれます。

検証者は、履歴書を完成させるためのWebサイトアドレスを提供することもできます。検証者は、委任者を引き付けるために良い評判を確立する必要があります。検証者の設定をサードパーティが確認することをお勧めします。 Terraチームはレビューを承認または実施しないことに注意してください。

## 責任

### バリデーターは公に認められる必要がありますか？

いいえ、しませんでした。各委任者は、独自の基準に従って検証者を評価します。一般的に、検証者は自分を指名するときにWebサイトのアドレスを登録して、適切と思われるときに自分の行動を促進できるようにすることをお勧めします。

### 検証者の責任は何ですか？

検証者は次のことを行う必要があります。

-**正しいソフトウェアバージョンの実行:**検証者は、サーバーが常にオンラインであり、秘密鍵が危険にさらされていないことを確認する必要があります。

-**価格発見と安定性に積極的に参加します:**バリデーターがルナの実際の市場価格に対して正直で正しい投票を提出するように非常に動機付けます。バリデーターは、Terraステーブルコインの価格を安定させるためにアービトラージスワップを実施することも推奨されます。

-**コミュニティプール資金の正しい展開に関する監督とフィードバックを提供します。** Terraプロトコルには、その通貨の採用を促進するための提案ガバナンスシステムが含まれています。検証者は、透明性を提供し、資金を効果的に使用するために、予算執行者を保持する必要があります。

-**コミュニティの積極的なメンバーになる:**検証者は、変化に簡単に適応できるように、エコシステムの現在の状態を常に認識している必要があります。

### 質権とはどういう意味ですか？

抵当に入れられたルナを検証者の活動のための保証金として扱います。検証者または委任者が預金の一部またはすべてを取り戻したい場合、バンドル解除トランザクションを送信します。誓約されたルナは、その後、_ 3週間の拘束力のない期間_を経ます。この期間中、拘束力のないプロセスが始まる前に、バリデーターによって行われた潜在的な不正行為により、大幅に削減されるリスクがあります。

検証者は、ブロック供給、ブロック報酬、および料金報酬を受け取り、これらを委任者と共有します。検証者が誤動作した場合、その総資本の一部が減少します(罰の厳しさは不正行為の種類によって異なります)。これは、Lunaを削減されたバリデーターにバインドするすべてのユーザーが、賭け金に比例して罰せられることを意味します。安全な操作のために、プリンシパルにバリデーターに委任するように促します。

###ベリファイアは、クライアントのルナを脱出させることができますか？

**できません。 **ベリファイアに委任することにより、ユーザーは権利と利益を委任します。検証者の公平性が高いほど、コンセンサスとプロセスにおけるその重要性は大きくなります。これは、検証者がそのプリンシパルのルナを管理していることを意味するものではありません。

:::警告警告
検証者は本人の資金で逃げることはできません。
:::

委任された資金を検証者が盗むことはできませんが、検証者が誤動作した場合でも、本人が責任を負う必要があります。これが発生すると、元本の株式は、相対的な株式に比例して部分的に減少します。

### バリデーターが次のブロックを提案するのにどのくらい時間がかかりますか？ルナの誓約の数とともに増えるのでしょうか？

次のブロックをマイニングするために選択されたバリデーターは、**プロポーザー**、またはコンセンサスラウンドの「リーダー」と呼ばれます。各提案者は決定論的に選択され、選択される頻度は、バリデーターの相対的な合計エクイティに等しくなります(合計エクイティ=自己拘束力のあるエクイティ+元本エクイティ)。たとえば、すべてのバリデーターの住宅ローンのエクイティの合計が100ルナで、1つのバリデーターのエクイティの合計が10ルナの場合、バリデーターは10％の確率で提案者として選択されます。

Tendermint BFTコンセンサスでの提案者の選択プロセスの詳細については、[公式ドキュメント](https://docs.tendermint.com/master/spec/consensus/proposer-selection.html)を参照してください。

## インセンティブ

### 誓約の動機は何ですか？

バリデーターエクイティプールの各メンバーは、さまざまな種類の収入を受け取ります。

-**計算料金(ガス)**:スパムを防ぐために、バリデーターは、メモリプールに含まれるトランザクションの最小ガス料金を設定できます。各ブロックの終わりに、計算料金は参加しているバリデーターに比例して分配されます。

-**安定料金**:Lunaの価値を安定させるために、契約では、Terraトランザクションごとに0.1％から1％の小額の料金が請求され、上限は1TerraSDRです。これは任意のTerra通貨で支払われ、TerraSDRの各ブロックの最後にある各バリデーターのシェアに比例して支払われます。

総収入は、各バリデーターの重みに応じて、バリデーターのエクイティプールに分配されます。次に、各プリンシパルの株式の割合に応じて、プリンシパル間で収入が分配されます。元本の収入の手数料は、分配前にバリデーターによって収集されることに注意してください。

-**スワップ料金**:LunaとTerra通貨間の市場スワップ取引では、少量のスプレッドが請求されます。これは、オラクルの為替レートを忠実に報告するバリデーターに報酬を与えるために使用されます。異なるTerraステーブルコイン間のスワップ手数料はトービン税と呼ばれます。

### バリデーターを実行する動機は何ですか？

検証者は、委任者よりも手数料を通じてより多くの収入を得ることができます。また、[`Oracle`](../dev/spec-oracle.md)を通じてオンチェーンの為替レートを決定する際にも重要な役割を果たし、為替レートとスワップ手数料を忠実に報告することで報酬が得られます。

### バリデーターコミッションとは何ですか？

バリデータープールが受け取る収益は、バリデーターとその委任者の間で分配されます。検証者は、元本の収入の一部に基づいてコミッションを集めることができます。手数料はパーセンテージで設定されます。各検証者は、初期コミッション、1日の最大コミッション変更率、および最大コミッションを自由に設定できます。メインネットは、各バリデーターによって設定されたパラメーターを適用します。これらのパラメータは、候補が最初に発表されたときにのみ定義でき、発表後にさらに制限することができます。

### ブロック用語はどのように配布されますか？

ブロック供給は、各検証者の総資本に比例して分配されます。これは、各ベリファイアが各句を介してTerraSDR \(SDT \)を取得した場合でも、すべてのベリファイアが同じ重みを維持することを意味します。

 **例:**同じステーキングウェイトと1％の手数料率で10人のバリデーターを取ります。ブロックは1000SDTとして指定され、各バリデーターには自己結合Lunaの20％が含まれます。これらのトークンは、提案者に直接与えられることはありません。代わりに、それらはバリデーターに均等に分散されます。したがって、各バリデーターのマイニングプールには100個のSDTがあり、各参加者の公平性に応じて分散されます。

-コミッション:100 SDT〜 * 〜80 \％〜* 〜1 \％$ = 0.8 SDT

-各バリデーターは次のようになります:100 SDT〜 * 〜20 \％〜+ 〜Commission $ = 20.8 SDT

-すべてのクライアントが取得:100 SDT〜 * 〜80 \％〜-〜コミッション$ = 79.2 SDT

各プリンシパルは、プール内のシェアに応じて79.2SDTの一部を要求できます。検証者の手数料はブロック条件には適用されないことに注意してください。ブロック報酬(SDTで支払われる)は同じメカニズムに従って分配されます。

### コストはどのように割り当てられますか？

手数料はコミッションと同じ方法でバリデーターに分配されます。各バリデーターはその総シェアに比例して分配されます。提案者が最小要件を超える事前コミットを含む場合、ブロック提案者はボーナスを受け取ることもできます。

#### 賞

次のブロックを提案するために検証者を選択する場合、検証者の署名の形式で、前のブロックの事前コミットの少なくとも3分の2を含める必要があります。 3分の2以上を含む提案者は、追加の事前提出の数に比例したボーナスを受け取ります。提案者が事前コミットの3分の2を含む場合、報酬範囲は1％であり、提案者が事前コミットを100％含む場合、報酬範囲は5％です。ただし、提案者の待機時間が長すぎると、他のバリデーターがタイムアウトして次の提案者に進む可能性があります。これが、検証者が最も多くの署名を取得するための待機時間と、提案された次のブロックを失うリスクとの間のバランスを見つけなければならない理由です。この機能は、空でないブロックの提案、バリデーター間のより良いネットワークを奨励し、検閲を容易にするように設計されています。

**例:**同等の公平性を持つ10のバリデーターがあります。それぞれに1％の手数料と20％の自己保険ルナがあります。ブロックが成功すると1005SDTの料金が請求され、提案者がブロックに署名の100％を含めると、5％の完全なボーナスを受け取ります。

簡単な方程式を使用して、各バリデーターの報酬$ R $を計算できます。
$$ 9R〜 + 〜R〜 + 〜5 \％(R)〜= 〜1005〜 \ Leftrightarrow〜R〜 = 〜1005〜/〜10.05〜 = 〜100 $$

-ブロックを提案したバリデーターの場合:
  -マイニングプールは$ R〜 + 〜5 \％(R)$を取得します:105 SDT
  -コミッション:105 SDT〜 * 〜80 \％〜* 〜1 \％$ = 0.84 SDT
  -検証者の報酬:105 SDT〜 * 〜20 \％〜+ 〜Commission $ = 21.84 SDT
  -委任者の報酬:105 SDT〜 * 〜80 \％〜-〜手数料$ = 83.16 SDT \(各委任者は、シェアに比例してこれらの報酬の一部を受け取ることができます\)

-他のすべてのバリデーターの場合:
  -マイニングプールは$ R $を取得します:100 SDT
  -コミッション:100 SDT〜 * 〜80 \％〜* 〜1 \％$ = 0.8 SDT
  -検証者の報酬:100 SDT〜 * 〜20 \％〜+ 〜Commission $ = 20.8 SDT
  -委任者の報酬:100 SDT〜 * 〜80 \％〜-〜手数料$ = 79.2 SDT \(各委任者は、シェアに比例してこれらの報酬の一部を受け取ることができます\)

### ルナの供給は時間とともにどのように変化しますか？

Lunaは、Terra Proof ofStakeチェーンのネイティブステーキングトークンです。ルナは鉱業力を代表し、テラステーブルコインの担保として機能します。 Terraステーブルコインの価格が低い場合、関連するTerraステーブルコインが燃やされ、ルナが鋳造されます。これにより、Terraステーブルコインの価格が上昇します。ルナのインフレを制限するために、協定はすべてのシニョリッジと配当スワップ手数料を為替レートのオラクル投票の勝者に燃やし、次にルナの供給を目標に戻します。テラ協定は本質的にデフレです。

### 注文をカットするための条件は何ですか？

検証者が誤動作した場合、彼らの住宅ローンの株式と受託者の株式は減少します。罰の厳しさは、過失の種類によって異なります。資金の大幅な削減につながる可能性のある3つの主な間違いがあります。

-**二重署名:**誰かがチェーンAについて、バリデーターがチェーンAとチェーンBで同じ高さの2つのブロックに署名したことを報告し、チェーンAとチェーンBが共通の祖先を共有している場合、このバリデーターは次のようになります。チェーンA。

-**使用不可:**検証者の署名が最後のXブロックに含まれていない場合、検証者はXに比例するわずかな量だけ削減されます。 Xが特定の制限よりも高い場合、ベリファイアはバインド解除されます。

-**非投票:**検証者が提案に投票しない場合、その株式は小さなスラッシュを受け取ります。

:::警告警告
 ベリファイアが意図的に誤動作しなかった場合でも、ノードがクラッシュしたり、接続が失われたり、DDoSに攻撃されたり、秘密鍵が漏洩したりすると、ベリファイアが切断される可能性があります。
:::

### ベリファイアはLunaをそれ自体にバインドする必要がありますか？

いいえ。ただし、自己関連付けには利点があります。検証者の総資本は、自己拘束力のある資本と委託された資本で構成されます。これは、バリデーターがより多くの委任者を引き付けることによって、少量の自己拘束力のあるルナを補うことができることを意味します。これが、検証者にとって評判が非常に重要である理由です。

バリデーターはLunaを自分自身にバインドする必要はありませんが、すべてのバリデーターが「ゲーム内のスキン」を持つことをお勧めします。これにより、バリデーターの信頼性が高まります。

委任者がバリデーターが持つ「ゲームスキン」の数について一定の保証を得るために、バリデーターは最小数の自己拘束型Lunaシグナルを送信できます。ベリファイアのセルフバインディングが事前定義された制限よりも低い場合、ベリファイアとそのすべてのプリンシパルはバインド解除されます。

## スキル要件

### ハードウェア要件は何ですか？

テラコアをすること、次の方法をおむします。

-4コアコンピューティングに最適化されたCPU
-16GB RAM(ジェネシスをエクスポートするための32GB)
-1TBのストレージスペース(SSD以上)
-少なくとも100mbpsのネットワーク帯域幅

### ソフトウェア要件は何ですか？

Terra Coreノードの実行に加えて、バリデーターは監視、アラート、および管理ソリューションも開発する必要があります。

検証者は、アップグレードとバグ修正に対応するために定期的なソフトウェア更新を実行することを期待する必要があります。ネットワークの問題は必然的に発生し、警戒が必要です。

### 人員要件は何ですか？

バリデーターの操作を成功させるには、複数の高度なスキルを持つ担当者の努力と継続的な注意が必要です。バリデーターの実行は、ビットコインのマイニングよりもはるかに複雑です。

偶発的な緩みや切断を防ぐためには、効果的な操作が不可欠です。これには、攻撃や停止に対応し、データセンターのセキュリティと分離を維持できることが含まれます。

### ベリファイアは、サービス拒否攻撃から自分自身をどのように保護できますか？

攻撃者が大量のインターネットトラフィックをオーセンティケータのIPアドレスに送信すると、サービス拒否攻撃が発生します。これにより、検証者のサーバーがインターネットに接続できなくなります。

これを行うために、攻撃者はネットワークをスキャンし、さまざまなバリデータノードのIPアドレスを学習しようとし、それらにトラフィックを注入することによってそれらを切断します。

これらのリスクを軽減する1つの方法は、センチネルノードアーキテクチャを使用してバリデーターネットワークを慎重に構築することです。

バリデーターノードは、信頼できる完全なノードにのみ接続する必要があります。それらは、同じバリデーターまたはそれらが知っている他のバリデーターによって実行できます。バリデーターノードは通常、データセンターで実行されます。ほとんどのデータセンターは、主要なクラウドプロバイダーへの直接リンクを提供します。検証者はこれらのリンクを使用して、クラウド内のセンチネルノードに接続できます。これにより、サービス拒否の負担が検証者のノードからセンチネルノードに直接転送されます。これには、既存のセンチネルノードへの攻撃を軽減するために、新しいセンチネルノードを開始またはアクティブ化する必要がある場合があります。

セントリーノードは、すぐに起動したり、IPアドレスを変更するために使用したりできます。センチネルノードへのリンクはプライベートIPスペースにあるため、インターネットベースの攻撃が直接干渉することはありません。これにより、バリデーターブロックの提案と投票が常にネットワークの残りの部分に届くようになります。

セントリーノードアーキテクチャの詳細については、[this](https://forum.cosmos.network/t/sentry-node-architecture-overview/454)を参照してください。