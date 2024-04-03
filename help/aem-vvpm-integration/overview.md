---
title: Veeva Vault 統合の概要
description: Veeva Vault 統合の概要
exl-id: 52cc7290-b7e1-4476-877f-48934e6daf68
source-git-commit: 4d27e7ecca662b2082a18621becb0b8ec7735824
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Veeva Vault PromoMats とAdobe Experience Managerの統合の概要

この統合は、コンテンツを管理し、権限とコンプライアンスを強制する一方で、クラス最初のエクスペリエンス配信も活用します。

この統合には、以下の最小ソフトウェアバージョンが必要です。

* Adobe Experience Manager, 6.5.5 以降
* Veeva Vault PromoMats、20R3.2+

>[!NOTE]
>
>統合には、両方のシステムでサービスユーザーと適切な権限が必要です。
>

>[!IMPORTANT]
>
>この機能は、製品の一部として標準では使用できません。 実装には、Adobeコンサルティング保守契約が必要です。 詳しくは、Adobe担当者にお問い合わせください。
>

## 原則と機能

この統合は、次の 2 つの主な使用例をサポートするように設計されています。

1. コンテンツの承認 — AEMで新しいコンテンツを作成した場合、または既存のコンテンツを編集した場合は、ライフサイエンス向けの医療、法務、規制 (MLR) 承認プロセスをサポートする VVPM での使用を承認する必要があります。

2. コンテンツ管理 — AEMのドキュメント用にAEMで作成したデジタル戦術（E メール、プレゼンテーション、Web サイトなど）とその要素（ロゴ、写真、グラフィックなど）との間に関係を確立し、アセット使用率を視覚的に表示します。

次のような利点があります。

* デジタルリポジトリ間で重複を生じさせることなく、アセットやコンテンツに関する単一の情報源を維持する。
* Veeva Vault を活用して、権限とコンプライアンスの管理を実現し、クラスとアセット、コンテンツの作成/配信に最適なAEMを実現します。
* AEMと Veeva Vault の間でのコンテンツやメタデータの移動を自動化できます。
* 承認ワークフロー用に Veeva にコンテンツを送信する際の手作業を軽減します。
* 各システムは強みのために使用され、コネクタは、システム間でコンテンツを自動的に移動し、市場投入までの時間を短縮するのに役立ちます。

統合の機能

* VVPM へのAEMサイトページ、アセット、コンテンツフラグメント、エクスペリエンスフラグメントの送信をサポートします。 AEMページ、コンテンツフラグメントおよびエクスペリエンスフラグメントは、スクリーンショットPDFまたは画像として送信できます。 AEM Assetsのバイナリはそのまま送信されます。
* AEMから VVPM への設定が可能な、選択したメタデータ要素の手動での同期および自動同期をサポートします。
* VVPM からAEMへの設定可能な、選択したメタデータ要素の手動の同期および自動同期をサポートします。
* VVPM のAEMサイトページ、アセット、コンテンツフラグメント、エクスペリエンスフラグメント間の関係をサポートし、コンテンツの関係を自動化します。
* 複数のデバイスタイプでレンディションの生成をサポートします。

>[!NOTE]
>
>設定オプションについて詳しくは、統合の使用に関するドキュメントを参照してください。
>

コネクタの機能

* Veeva ではAEMプロセスと機能を複製しません。また、Veeva ではその逆も同様です。
* 単独では MLR を実行しません。 MLR が発生した場所に Veeva にコンテンツを送信する自動化を支援します。
* AEMと Veeva の間で同じ設定を作成するために使用することはできません。 すべてのコンテンツを 2 つのプラットフォーム間で移動する必要はありません。


>[!IMPORTANT]
>
>この統合では、現在、AEMをコンテンツ同期の真のソースと見なしています。
>

## 統合の取得

この統合をプロビジョニングするには、次の手順に従う必要があります。

以下のフローチャートとフローチャートの詳細に従って、統合をリクエストおよび設定してください。

![アクセスを申請](assets/integration-request.png)

フローチャートの詳細（上記のステップにマップ）:

* **手順 1** - Veeva Vault PromoMats とAdobe Experience Managerのライセンスを既に持っている、または調達中であることを前提としています。
* **手順 2** -Adobeコンサルティングとの保守契約の概要を示す新しい販売注文 (SO) は、統合を活用するために署名する必要があります。
* **手順 3**  — 統合パッケージをインストール、アクティブ化、設定します。

## サポート

以下では、サポートチームに問題を問い合わせ、記録する方法について説明します。

### 統合またはAdobe Experience Managerサポートのリクエスト

サポートチケットは、カスタマーケアでAdobeでログに記録できます。 Adobe Experience Cloud管理者は、にログオンする必要があります。 [Adobe Admin Console](https://adminconsole.adobe.com/)をクリックし、「サポート」タブをクリックして、ケースを作成します。 統合に関する問題が発生した場合は、必ず次の情報を含めてください。

* **プロセスタイトル**: `AEM - Veeva Vault Integration`
* **プロセス所有者**: `Data Engineering`
* **説明**: `Description of the issue`
* **連絡先**: `The email address(es) for relavant AEM point of contacts for your organization.`
* **AEM Instance URL**: `Place the Adobe Experience Manager instance url here.`
* **Veeva インスタンス URL**: `Place the Veeva Vault PromoMats instance url here.`

### Veeva Vault プロモーションマットのサポートをリクエスト中

Veeva Vault PromoMats インスタンスの操作に問題が生じる場合があります。 その場合は、Veeva Vault PromoMats 管理者が、 [Veeva サポート](http://support.veeva.com/). Veeva インスタンスのステータスは、 [Veeva Trust](http://trust.veeva.com/).
