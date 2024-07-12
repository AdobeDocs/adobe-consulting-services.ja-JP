---
title: Veeva Vault の統合に関する注意事項
description: Veeva Vault の統合に関する注意事項
exl-id: 1a188671-d123-4475-a607-65743ba0dadd
source-git-commit: 07eab1e439626bd3bb3416c9e7d0c1666927a7aa
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---

# ベストプラクティス、ガードレール、通知

## バージョン

この統合には、次の最小ソフトウェアバージョンが必要です。

* Adobe Experience Manager, 6.5.5 以降#キョウ#
* Veeva Vault PromoMats、20R3.2 以降

## データのプライバシー

この統合は、Adobe Experience Managerと Veeva Vault PromoMats の間でコンテンツを転送するように設計されています。 データ管理者として、お客様の会社は、お客様のデータの収集および使用に適用されるプライバシー法および規制を遵守する責任を負います。

## コンテンツ同期頻度

統合ワークフローがトリガーされると、AEMのコンテンツとメタデータがAEMから VVPN に同期されます。 これは、自動または手動で行うことができます。 VVPM メタデータが VVPM からAEMに同期されます。 この操作は、スケジューラーを使用して自動的に行うことも、ボタンをクリックして手動で行うこともできます。

## 統合の制限とベストプラクティスおよびガードレール

この統合を使用する際は、次の制限事項を考慮してください。

* メタデータを同期する場合、「テキスト」および「複数行テキスト」のデータタイプのみがサポートされます。
* 統合では、AEMのモジュール型コンテンツ（コンテンツフラグメントとエクスペリエンスフラグメント）はサポートされますが、VVPM のモジュール型コンテンツはサポートされません。
* VVPM にリンクされたドキュメントはサポートされていません。
* VVPM からAEMへの VVPM ビジュアル注釈の同期はサポートされていません。
* 統合では、コンテンツを VVPM からAEMに読み込みません。
* メタデータの検証はサポートされていません。
* ドキュメントの数は、Veeva ライセンスに基づいて制限されます。 [ ライセンスの制限 ](#veeva-license-limitations) を参照してください。
* API 呼び出しの数は、Veeva ライセンスに基づいて制限されます。 詳しくは、[API の制限 ](https://developer.veevavault.com/docs/#what-are-rate-limits) を参照してください。 [ ライセンスの制限 ](#veeva-license-limitations) を参照してください。

## Veeva ライセンスの制限

VVPM の一般設定に移動すると、インスタンスの制限を監視できます。

![Veeva の制限 ](assets/veeva-limits.png)
