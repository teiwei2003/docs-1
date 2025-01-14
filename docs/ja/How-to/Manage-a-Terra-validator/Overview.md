# 概要

このセクションのタスクでは、Terraバリデーターのセットアップ方法について説明します。基本的な検証ノードのセットアップは簡単ですが、強力なアーキテクチャーとセキュリティ機能を備えた本番品質のベリファイアノードを実行するには、多くのセットアップが必要です。

Terraコアは、Tendermintコンセンサスによってサポートされています。検証者はフルノードを実行し、ブロードキャスト投票を通じてコン​​センサスに参加し、新しいブロックをブロックチェーンに送信し、ブロックチェーンのガバナンスに参加します。検証者は、委任者に代わって投票できます。バリデーターの議決権は、総株式数に基づいて加重されます。上位130のバリデーターは**アクティブなバリデーターセット**を形成し、ブロックに署名して収入を得る唯一のバリデーターです。

検証者とその委任者は、次の料金を獲得します。

-[Gas](./Fees.md#gas):スパムを回避するために各トランザクションのコストを計算します。バリデーターは最小ガス価格を設定し、このしきい値を下回る暗黙のガス価格のトランザクションを拒否します。

-[安定性手数料](./Fees.md#stability-fees):市場の安定性を提供するためにトランザクションに追加される手数料。上限は1SDTです。税率は変動し、税率と呼ばれます。

-**交換手数料**:テラ安定通貨の額面を交換するための手数料は、[トービン税](./Fees.md#tobin-tax)と呼ばれます。 TerraとLunaの間のトランザクションには、[spread-fees](./Fees.md#spread-fees)が必要です。

料金の詳細については、[料金ページ](./fees.md)をご覧ください。

検証者は、受け取った料金に基づいて、追加の報酬としてコミッションを設定できます。

検証者が二重署名するか、オフラインになることが多いか、ガバナンスに参加しない場合、検証者が誓約するルナ(委託されたルナを含む)が減少する可能性があります。ペナルティは、違反の重大度によって異なります。

バリデーターに関するより一般的な情報については、コンセプトページの[バリデーターセクション](/ja/Concepts/Protocol.md#validators)にアクセスしてください。

## その他のリソース

-[Terra Verifier Discord](https://discord.com/invite/xfZK6RMFFx)。
-[Terra-Terra Bitesビデオでノードを開始する方法](https://www.youtube.com/watch?v=2lKAvltKX6w&ab_channel=TerraBites)。
-[オーセンティケーターFAQ](./faq.md) 