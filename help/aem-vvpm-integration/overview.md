---
title: Veeva Vault 統合の概要
description: Veeva Vault 統合の概要
exl-id: 52cc7290-b7e1-4476-877f-48934e6daf68
source-git-commit: 2e47baa4a255c34b3ca0b8631650dd5d8960fea8
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Veeva Vault PromoMats とAdobe Experience Managerの統合の概要

この統合により、コンテンツを管理し、権限とコンプライアンスを適用すると同時に、クラス最高のエクスペリエンス配信を活用できます。

この統合には、次の最小ソフトウェアバージョンが必要です。

* Adobe Experience Manager, 6.5.5 以降#キョウ#
* Veeva Vault PromoMats、20R3.2 以降

>[!NOTE]
>
>サービスユーザーと適切な権限が両方のシステムで統合のために必要です。
>

>[!IMPORTANT]
>
>この機能は、製品の一部として標準搭載はされていません。 実装には、Adobe Consultingのメンテナンス契約が必要です。 詳しくは、Adobeの担当者にお問い合わせください。
>

## 原則と機能

この統合は、次の 2 つの主なユースケースをサポートするように設計されています。

1. コンテンツの承認：AEMで新しいコンテンツを作成したり、既存のコンテンツを編集したりする場合は、ライフサイエンス分野の MLR （Medical, Legal, Regulatory）承認プロセスをサポートする VVPM でコンテンツを使用できるように承認する必要があります。
1. コンテンツ管理 – AEMで作成されたドキュメントに対してAEMで作成されたデジタル戦術（メール、プレゼンテーション、Web サイトなど）とその構成要素（ロゴ、写真、グラフィックなど）の PromoMats 関係を確立し、アセット使用率を可視化します。

次のような利点があります。

* デジタルリポジトリー間で重複することなく、アセットとコンテンツの唯一の情報源を維持します。
* Veeva Vault for rights and compliance management とAEM for best in class and asset and content creation/delivery の両方を活用します。
* AEMと Veeva Vault 間でのコンテンツとメタデータの移動を自動化できます。
* 承認ワークフロー用にコンテンツを Veeva に送信する際の手動の手間を軽減します。
* 各システムはその強みを発揮し、コネクタはシステム間のコンテンツの自動移動を支援して、市場投入までの時間を短縮します。

統合の機能

* AEM Site Pages、Assets、コンテンツフラグメント、エクスペリエンスフラグメントの VVPM への送信をサポートしています。 AEM ページ、コンテンツフラグメントおよびエクスペリエンスフラグメントは、スクリーンショットPDFまたは画像として送信できます。 AEM Assets バイナリはそのまま送信されます。
* AEMから VVPM への構成が可能な、選択したメタデータ要素の手動および自動同期をサポートします。
* VVPM からAEMへの構成が可能な、選択したメタデータ要素の手動および自動同期をサポートします。
* AEM サイトページ、Assets、コンテンツフラグメントおよび VVPM のエクスペリエンスフラグメントの間の関係をサポートし、コンテンツの関係を自動化します。
* 複数のデバイスタイプのレンディションの生成をサポートします。

>[!NOTE]
>
>設定オプションについて詳しくは、統合の使用状況に関するドキュメントを参照してください。
>

コネクタで実行されないこと

* AEMのプロセスと機能を Veeva でレプリケートしない（またはその逆の動作）。
* MLR 自体は行わない。 Veeva にコンテンツを送信して MLR が発生する場所に送信する自動化を支援します。
* AEMと Veeva の間で同一の設定を作成するために使用するためのものではありません。 すべてのコンテンツが 2 つのプラットフォーム間で移動する必要があるわけではありません。


>[!IMPORTANT]
>
>この統合では、現在、AEMをコンテンツ同期の信頼できる情報源と見なしています。

## 統合の取得

この統合をプロビジョニングするには、次の手順に従う必要があります。

以下のフローチャートおよびフローチャートの詳細に従って、統合をリクエストし設定してください。

![ アクセスを要求 ](assets/integration-request.png)

フローチャートの詳細（上記の手順に対応）:

* **手順 1** - Veeva Vault PromoMats とAdobe Experience Managerのライセンスを既に保有しているか、調達中であることを前提としています。
* **手順 2** – 統合を活用するには、Adobe Consultingとの保守契約の概要を説明する新しい販売注文（SO）に署名する必要があります。
* **手順 3** – 統合パッケージをインストール、アクティブ化、設定する。

## サポート

次に、サポートチームに問題を連絡して記録する方法を説明します。

### 統合またはAdobe Experience Manager サポートのリクエスト

サポートチケットは、Adobeカスタマーケアに記録することができます。 Adobe Experience Cloud管理者が [Adobe Admin Console](https://adminconsole.adobe.com/) にログオンし、「サポート」タブをクリックしてケースを作成する必要があります。 統合に関する問題については、必ず次の情報を含めてください。

* **プロセスのタイトル**: `AEM - Veeva Vault Integration`
* **プロセス所有者**: `Data Engineering`
* **説明**: `Description of the issue`
* **連絡先**: `The email address(es) for relavant AEM point of contacts for your organization.`
* **AEM インスタンス URL**: `Place the Adobe Experience Manager instance url here.`
* **Veeva インスタンス URL**: `Place the Veeva Vault PromoMats instance url here.`

### Veeva Vault プロモマットのサポートのリクエスト

時々、経験される問題は、Veeva Vault PromoMats インスタンスの操作に関する問題です。 その場合、Veeva Vault PromoMats 管理者は、[Veeva サポート ](http://support.veeva.com/) でサポートチケットを作成するように指示される場合があります。 Veeva インスタンスのステータスは、[Veeva Trust](http://trust.veeva.com/) に移動すると表示できます。

