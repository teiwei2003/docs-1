# Terraプロトコル

Terraプロトコルは、[algorithm stablecoin](/ja/Concepts/glossary.md#algorithmic-stablecoin)向けの主要な分散型オープンソースパブリックブロックチェーンプロトコルです。公開市場の[アービトラージ](/ja/Concepts/glossary.md#arbitrage)インセンティブと分散型オラクル投票を組み合わせることで、Terraプロトコルは、あらゆる法定通貨の価格を一貫して追跡できる安定した通貨を作成します。ユーザーは、TerraブロックチェーンでTerraステーブルコインを即座に消費、保存、交換、または交換できます。ルナは、その保有者に誓約報酬とガバナンス権を提供します。 Terraエコシステムは、急速に拡大する分散型アプリケーションのネットワークであり、Terraの安定した需要を生み出し、Lunaの価格を上昇させます。

## TerraとLUNA

プロトコルは、TerraとLunaの2つの主要なトークンで構成されています。

-** Terra **:法定通貨の価格を追跡する安定した通貨。ユーザーはルナを燃やして新しいテラをキャストします。ステーブルコインは、法定通貨にちなんで名付けられています。たとえば、基本的なTerraステーブルコインは、TerraSDRまたはSDTと呼ばれるIMFのSDRの価格を追跡します。その他の安定した通貨単位には、TerraUSDまたはUST、およびTerraKRWまたはKRTが含まれます。すべてのテラの宗派は同じプールに存在します。

-** Luna **:Terraプロトコルのネイティブの誓約トークンであり、Terraの価格変動を吸収するために使用されます。ルナは統治と採掘に使用されます。ユーザーは、取引手数料の見返りと引き換えに、ブロックチェーンでの取引を記録および検証する検証者にルナを誓約します。 Terraを多く使用するほど、Lunaの値は高くなります。

## Terraプロトコルのしくみ

### ステーブルコイン

安定した通貨はTerraプロトコルの主な機能です。基本通貨の価格を追跡する暗号化された資産です。通貨のデジタル形式として、Terraステーブルコインは法定通貨のように使用でき、ブロックチェーンの追加の利点があります。不変の公開元帳、即時取引、決済時間の短縮、手数料の削減です。

Stablecoinは、価格に固定されたままである場合にのみ、ユーザーにとって価値があります。 Terra契約は、Terraの価格を維持するために、需要と供給の基本的な市場の力を使用します。テラの需要が強く、供給が限られている場合、テラの価格は上昇します。 Terraの需要が少なく、供給が多すぎると、Terraの価格は下がります。この合意により、Terraの需要と供給のバランスが常に保たれ、価格が安定します。

### 拡張と縮小

テラ経済全体を2つのプールと考えてください。1つはテラ用、もう1つはルナ用です。 Terraの価格を維持するために、Lunaの供給プールはTerraの供給を増減します。ユーザーはLunaを燃やしてTerraをキャストし、Terraを燃やしてLunaをキャストします。これらはすべて、プロトコルアルゴリズム[マーケットモジュール](/ja/Reference/Terra-core/Module-specifications/spec-market.html)によって動機付けられています。

-**拡張**:Terraの価格がペグに比べて高い場合、供給が少なすぎて需要が多すぎます。この契約は、ユーザーがルナを燃やしてテラをキャストすることを奨励しています。 Terraの新しい供給により、プールが大きくなり、需要と供給のバランスがとれます。ユーザーは、テラが目標価格に達するまで、燃えているルナからより多くのテラをキャストします。その過程でルナプールが小さくなり、ルナの価格が上昇します。

-**縮小**:Terraの価格がペグに比べて低すぎる場合、供給が多すぎて需要が低すぎます。この契約は、ユーザーがテラを燃やしてルナをキャストすることを奨励しています。テラの供給の減少は希少性につながり、テラの価格は上昇します。テラが目標価格に達するまで、燃やされたテラからより多くのルナがキャストされます。ルナマイニングプールの価格は上下しました。

ルナは安定した資産テラの可変の対応物です。供給を調整することにより、ステーブルコインの需要が増加するにつれてルナの価格が上昇します。

### マーケットモジュールと裁定取引

Terraの価格の安定性は、契約のアルゴリズム[market module](/ja/reference/terra-core/module-specifications/spec-market.md)によって達成されます。これは、裁定取引の機会を通じてTerraのキャストまたは書き込みを奨励します。裁定取引は、ユーザーが市場間の価格差から利益を得るときに発生します。

Terra契約のマーケットモジュールを使用すると、ユーザーは常に1 USTを1米ドル相当のLunaと交換でき、その逆も可能であり、ユーザーはTerraの価格を維持することができます。同じ原則がすべてのTerraステーブルコインの金種に適用されます。

- **例**
  1USTの取引価格が1.01USドルの場合、ユーザーはTerra Stationのマーケットスワップ機能を使用して、1USドルのLunaを1USTと交換できます。市場は1ドルのルナを燃やし、1USTをミントします。次に、ユーザーは1つのUSTを1.01米ドルの価格で販売し、裁定取引を通じて0.01米ドルを獲得し、それをUSTプールに追加できます。この裁定取引は、USTの価格が米ドルの価格と一致するように下落するまで続き、それによってTerraのペグが維持されます。

同じ裁定取引メカニズムは、収縮に対して反対の効果をもたらします。

- **例**
  1USTの取引価格が0.99USDの場合、ユーザーは0.99USDの価格で1USTを購入できます。次に、ユーザーはTerra Stationのマーケットスワップ機能を使用して、1USTを1米ドルのルナと交換します。スワップは1USTを消費し、1米ドルのルナをミントします。ユーザーは交換から0.01USTを獲得します。この裁定取引は続き、USTの価格が1ドルに戻るまで、USTはルナをキャストするために燃やされました。

### スケーラビリティ

Terraプロトコルはスケーラブルです。市場規模、ボラティリティ、需要に関係なく、Terraの価格安定性を維持することを目的としています。協定にコード化された金融政策は、すべての市場変動におけるその耐久性と柔軟性を保証します。

### シニョリッジとデフレ

シニョリッジは、コインの価値から生産コストを差し引いたものです。テラ協定の初期のバージョンでは、シニョリッジはさまざまなコミュニティプロジェクトに資金を提供するために転用されました。シニョリッジは途方もない価値を生み出す可能性がありますが、システムにインフレを引き起こす可能性もあります。
テラ協定のすべてのシニョリッジは燃やされ、ルナはデフレになりました。

## バリデーター

バリデーターはTerra [blockchain](/ja/Concepts/glossary.md#blockchain)のマイナーです。彼らはTerraブロックチェーンを保護し、その正確性を確保する責任があります。ベリファイアはフルノードと呼ばれるプログラムを実行し、Terraネットワークで行われたすべてのトランザクションを検証できるようにします。バリデーターはブロックを提案し、その有効性に投票し、取引手数料の住宅ローンの報酬と引き換えに、新しい各ブロックをチェーンに追加します。ユーザーは、誓約報酬と引き換えに、検証者にルナを誓約することができます。ベリファイアは、Terraプロトコルのガバナンスにおいても重要な役割を果たします。

バリデーターの詳細については、[バリデーターFAQ](/ja/How-to/Manage-a-Terra-validator/faq.md)にアクセスしてください。

### コンセンサス

Terraブロックチェーンは、プルーフオブステークブロックチェーンであり、[Cosmos SDK](https://cosmos.network/)によってサポートされ、Tendermintコンセンサスと呼ばれる検証システムによって保護されています。

次のプロセスは、テンダーミントのコンセンサスがどのように機能するかを説明しています。 Tendermintコンセンサスの詳細については、[Official Tendermint Documentation](https://docs.tendermint.com/)にアクセスしてください。

1. ** proposer **という名前のバリデーターを選択して、新しいトランザクションブロックを送信します。
2.バリデーターは、2回の投票で提案されたブロックを受け入れるか拒否するかを決定します。ブロックが拒否された場合、新しい提案者が選択され、プロセスが再開されます。
3.受け入れられた場合、ブロックは署名され、チェーンに追加されます。
4.ブロックからの取引手数料は、誓約報酬として検証者と委任者に分配されます。提案者は、参加することで追加の報酬を受け取ります。

このプロセスを繰り返して、新しいトランザクションブロックをチェーンに追加します。各バリデーターはネットワーク上のすべてのトランザクションのコピーを持っており、投票する前に提案されたトランザクションブロックと比較します。コンセンサス投票中に複数の独立したバリデーターが発生するため、偽のブロックを受け入れることはできません。このようにして、ベリファイアはTerraブロックチェーンの整合性を保護し、各トランザクションの有効性を保証します。

### 誓約

ステーキングは、ステーキング報酬と引き換えにルナをバリデーターにバインドするプロセスです。

Terraプロトコルでは、上位130の検証者のみがコンセンサスに参加できます。バリデーターのランクは、それらのシェアまたはそれらに関連付けられているルナの合計量によって決定されます。バリデーターはLunaを自分自身にバインドできますが、主に委任者からより多くのシェアを蓄積します。新しいブロックを提案し、比例してより多くの報酬を獲得するために、より大きな利害関係を持つ検証者がより頻繁に選択されます。

### 委任者
委任者は、完全なノードを実行せずにコンセンサスから報酬を取得したいユーザーです。ルナを誓約するユーザーはすべてプリンシパルです。委任者は、ルナをバリデーターに誓約し、バリデーターの重みまたは誓約の合計を増やします。その見返りとして、元本は住宅ローンの報酬として取引手数料の一部を受け取ります。

::: tip住宅ローンのルナを所有しているのは誰ですか？
賭けられたルナは決してクライアントの財産を離れることはありません。自由に取引することはできませんが、誓約されたルナが検証者によって所有されることは決してありません。詳細については、[Validator FAQ](/ja/How-to/Manage-a-Terra-validator/faq.md#can-a-validator-run-away-with-a-delegators-luna)をご覧ください。
:::

### LUNAのステージ

報酬の獲得を開始するために、委任者はルナをバリデーターにバインドします。拘束力のあるプロセスにより、委任者のルナが検証者の資本に追加され、検証者がコンセンサスに参加するのに役立ちます。

ルナは次の3つのフレーズで存在します。

-**非結合**:ルナは自由に取引でき、検証者に誓約しません。
-**バインディング**:ルナは検証者に誓約しました。縛られたルナは誓約報酬を蓄積します。 Terra StationのバリデーターにバインドされたLunaは自由に取引できませんが、bLunaはLunaのバインドを表すトークンであり、[Anchor](https://アンカープロトコル.com/)および[ミラー](https://mirror.finance/)。
-**バインド解除**:Lunaはバリデーターとのバインドを解除しており、報酬は生成されません。このプロセスは21日で完了します。

###拘束力、住宅ローン、手数料

一般に、拘束力、住宅ローン、および手数料という用語は、同じステップで発生するため、同じ意味で使用できます。委任者はLunaをバリデーターに委任し、Lunaはバリデーターにバインドされ、バインドされたLunaはバリデーターの共有に追加されます。

デリゲートは、Terra Stationのデリゲート機能を使用して、Lunaを[アクティブセット](/ja/Concepts/glossary.md#active-set)の任意のバリデーターにバインドできます。委任者は、バリデーターにバインドまたは誓約された瞬間に、誓約報酬の受け取りを開始します。

### 解放する

トラスティは、Terra Stationの廃止機能を使用して、Lunaのバインドを解除したりセキュリティを解除したりできます。バインド解除プロセスは、完了するまでに21日かかります。この期間中、バインドされていないルナは取引できず、ステーキング報酬は生成されません。

:::警告警告
一度開始すると、委任を停止したり、委任プロセスをキャンセルしたりする方法はありません。
委任のキャンセルは完了するまでに21日かかります。注文をキャンセルまたは注文トランザクションをキャンセルする唯一の方法は、バインド解除プロセスが通過するのを待つことです。または、21日待つことなく、誓約されたルナを別のバリデーターに再委任することができます。
:::

21日間の拘束力のないプロセスは、Terra契約の長期的な安定に貢献します。拘束解除期間は、住宅ローンのルナをシステムに少なくとも21日間ロックすることにより、変動を抑制します。代わりに、プリンシパルは誓約報酬を受け取ります。これにより、ネットワークの安定性がさらに促進されます。

### 再承認

再委任により、誓約されたルナが1つのバリデーターから別のバリデーターにすぐに送信されます。ユーザーは、誓約期間の21日間のキャンセルを待つ必要はありませんが、Terra Stationの再委任機能を使用して、誓約されたルナをいつでも再委任できます。再委任を受け入れるバリデーターは、21日以内に任意の量のルナをバリデーターにさらに再委任してはなりません。

:::警告警告
ユーザーがルナの誓約をある検証者から別の検証者に再委任する場合、ルナの誓約を受け取った検証者は、21日以内にそれ以上の再委任トランザクションを実行することを禁止されます。この要件は、再委任トランザクションを実行するウォレットにのみ適用されます。
:::

### 賞

Terraプロトコルは、報酬を賭けることによって検証者と委任者を動機付けます。ステーキング報酬は、ガス、安定料金、スワップ料金の3つのソースから提供されます。

-[Gas](./Fees.md#gas):スパムを回避するために各トランザクションのコストを計算します。バリデーターは最小ガス価格を設定し、このしきい値を下回る暗黙のガス価格のトランザクションを拒否します。

-[安定性手数料](./Fees.md#stability-fees):市場の安定性を提供するためにトランザクションに追加される手数料。上限は1SDTです。税率は変動し、税率と呼ばれます。

-**交換手数料**:テラ安定通貨の額面を交換するための手数料は、[トービン税](./Fees.md#tobin-tax)と呼ばれます。 TerraとLunaの間のトランザクションには、[spread-fees](./Fees.md#spread-fees)が必要です。

料金の詳細については、[料金ページ](./fees.md)をご覧ください。

各ブロックの終わりに、すべての取引手数料は各検証者とその委任者に比例して分配されます。検証者は、報酬の一部を保持してサービスの料金を支払うことができます。この部分はコミッションと呼ばれます。残りの報酬は、クライアントが約束した金額に応じてクライアントに分配されます。
ステーキング報酬は、Terraプロトコルの安定性においても重要な役割を果たします。不安定な期間中、テラ協定は安定した鉱業インセンティブを維持するために税率を調整します。このメカニズムについては、[財務モジュール](/ja/Reference/Terra-core/Module-specifications/spec-treasury.md)で詳しく説明されています。市場の変動に関係なく、安定したリターンは安定したステーキング需要を保証します。ステーキングは、Terraの価格の長期的および短期的な安定性を確保するために、システムの価値をロックします。


### 切る

バリデーターの実行は大きな責任です。検証者は厳格な基準を満たし、コンセンサスプロセスを常に監視して参加する必要があります。削減は、不正な検証者に対する罰です。バリデーターがカットされると、彼らは彼らのシェアのごく一部と彼らのプリンシパルのシェアのごく一部を失います。削減された検証者も、一定期間、投獄されるか、コンセンサスから除外されます。

::危険賭けのリスク
削減はバリデーターとデリゲーターに影響します。検証者が削減されると、検証者に誓約された委任者も削減されます。減少は、クライアントの住宅ローンの金額に比例します。カットはまれであり、通常は小さなペナルティが発生しますが、実際に発生します。プリンシパルは、バリデーターを注意深く監視し、調査を実施し、ルナを賭けるリスクを理解する必要があります。
:::

削減は、次の条件下で発生します。

-**二重署名**:ベリファイアが同じ高さの同じチェーンIDを持つ2つの異なるブロックに署名する場合。
-**ダウンタイム**:バリデーターが応答しないか、一定期間アクセスできない場合。
-**投票を逃した**:検証者がコンセンサスで投票を逃したか、オラクルプロセスで正しく投票できなかった場合。

検証者はお互いを注意深く監視し、不正行為の証拠を提出することができます。一度発見されると、不正な検証者は彼らの資金のごく一部を削減されます。規則に違反した検証者も、一定期間、投獄されるか、コンセンサスから除外されます。アップグレードによって引き起こされる障害やダウンタイムなどの単純な問題でさえ、大幅な削減につながる可能性があります。

削減の詳細については、[Slashing Module](/ja/Reference/Terra-core/Module-specifications/spec-slashing.md)にアクセスしてください。

## ガバナンス

Terraプロトコルは、コミュニティメンバーによって管理される分散型のパブリック[blockchain](/ja/Concepts/glossary.md#blockchain)です。ガバナンスは、ユーザーと検証者がTerraプロトコルに変更を加えることを可能にする民主的なプロセスです。コミュニティメンバーは、提案を提出、投票、および実装します。

### 提案

提案は、コミュニティのアイデアから始まります。コミュニティメンバーは、提案書と初期保証金の草案を作成して提出します。

最も一般的なタイプの提案は次のとおりです。

-`ParameterChangeProposal`:各モジュールで定義されているパラメーターを変更します。
-`TaxRateUpdateProposal`:税率の金融政策レバレッジを更新します。
-`RewardWeightUpdateProposal`:報酬ウェイトの金融政策レバレッジを更新
-`CommunityPoolSpendProposal`:コミュニティプールで資金を使う

方向性の大幅な変更や手動で実装する必要のある決定など、その他の問題は「TextProposal」として送信されます。

### 投票プロセス

コミュニティのメンバーは、誓約したルナに投票します。 1つの抵当に入れられたルナは1票に等しい。ユーザーが投票を指定しなかった場合、ユーザーの投票はデフォルトで、誓約したバリデーターになります。委任者によって指定されない限り、検証者は投票にすべての株式を使用します。したがって、各代表者が自分の好みに応じて投票することが非常に重要です。

以下は、ガバナンスプロセスの基本的な要約です。詳細については、[Governance Module](/ja/Reference/Terra-core/Module-specifications/spec-governance.md)にアクセスしてください。

1.ユーザーがプロポーザルを送信すると、2週間の再充電期間が始まります。
2.ユーザーは、提案をサポートするための担保としてLunaを預け入れます。最小しきい値の50ルナが入金されると、この期間は終了します。デポジットはスパムを防ぐためのものです。
3.1週間の投票期間が始まります。
    投票オプションは次のとおりです。
    -`はい `:はい。
    -`いいえ `:不承認。
    -`NoWithVeto`:不承認、デポジットは燃やされるべきです。
    -`Abstain`:有権者は棄権しました。
4.開票します。
    3つの条件を満たす提案が渡されます。
    -「定足数」を満たす:すべての誓約されたルナの少なくとも40％が投票する必要があります。
    -「NoWithVeto」の総投票数は総投票数の33.4％未満です。
    -「はい」の投票は50％の過半数に達します。
    上記の条件が満たされない場合、提案は拒否されます。
5.採択された提案が実行されます。
6.保証金は返金または焼却されます。

承認されると、ガバナンス提案に記載されている変更は、提案処理手順によって自動的に有効になります。合格した「TextProposal」などの一般的な提案は、Terraチームとコミュニティによってレビューされる必要があります。

### 保証金

デポジットは、不要な提案やスパムを防ぐことができます。ユーザーは「NoWithVeto」に投票して、スパムと見なす提案を拒否できます。

以下の条件がすべて満たされた場合、デポジットは返金されます。
-2週間のデポジット期間内に最低50ルナのデポジットに到達します。
-「クォーラム」に会う:総投票数は、誓約されたすべてのルナの40％を超えています
-「NoWithVeto」の総投票数は総投票数の33.4％未満です。
-投票は、「はい」または「いいえ」の投票の過半数を返します。

デポジットは、次のいずれかの状況で燃やされます。
-2週間の入金期間内に最低入金額の50ルナに達しません。
-「定足数」に達していない:1週間の投票後の総投票数は、誓約されたすべてのルナの40％未満です。
-「NoWithVeto」の投票数が総投票数の33.4％を超えました。