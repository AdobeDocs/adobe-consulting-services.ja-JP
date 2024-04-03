---
title: Veeva Vault 統合に関するお知らせ
description: Veeva Vault 統合に関するお知らせ
exl-id: 1a188671-d123-4475-a607-65743ba0dadd
source-git-commit: 07eab1e439626bd3bb3416c9e7d0c1666927a7aa
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---

# ベストプラクティス、ガードレールおよび注意事項

## バージョン

この統合には、以下の最小ソフトウェアバージョンが必要です。

* Adobe Experience Manager, 6.5.5 以降
* Veeva Vault PromoMats、20R3.2+

## データのプライバシー

この統合は、Adobe Experience Managerと Veeva Vault PromoMats 間でコンテンツを転送するように設計されています。 データ管理者であるお客様の会社は、お客様のデータの収集と使用に適用されるプライバシーに関する法律および規制に準拠する責任を負います。

## コンテンツ同期頻度

AEMのコンテンツとメタデータは、統合ワークフローがトリガーされると、AEMから VVPN に同期されます。 これは、自動または手動でおこなうことができます。 VVPM メタデータは、VVPM からAEMに同期されます。 これは、スケジューラーを使用して自動的に実行するか、ボタンをクリックして手動で実行できます。

## 統合の制限事項とベストプラクティスおよびガードレール

この統合を使用する際は、次の制限事項を考慮してください。

* メタデータの同期では、次のデータ型のみがサポートされます：「テキスト」と「複数行テキスト」。
* 統合は、AEMモジュラーコンテンツ（コンテンツフラグメントとエクスペリエンスフラグメント）をサポートしていますが、VVPM モジュラーコンテンツはサポートしていません。
* VVPM リンクドキュメントはサポートされていません。
* VVPM からAEMへの VVPM ビジュアル注釈の同期はサポートされていません。
* 統合では、VVPM からAEMにコンテンツを読み込みません。
* メタデータの検証はサポートされていません。
* ドキュメントの数は Veeva ライセンスに基づいて制限されます。 詳しくは、 [ライセンス制限](#veeva-license-limitations).
* API 呼び出しの数は、Veeva ライセンスに基づいて制限されます。 詳しくは、 [API の制限](https://developer.veevavault.com/docs/#what-are-rate-limits). 詳しくは、 [ライセンス制限](#veeva-license-limitations).

## Veeva ライセンスの制限

VVPM の一般設定に移動して、インスタンスの制限を監視できます。

![Veeva の制限](assets/veeva-limits.png)
