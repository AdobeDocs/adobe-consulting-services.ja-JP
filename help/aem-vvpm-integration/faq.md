---
title: Veeva Vault統合に関するFAQ
description: Veeva Vault統合に関するFAQ
exl-id: c308ebb3-7881-4094-9f35-c67a96fb5ab1
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 02aa1622ee171cd56ec9cdeb6bdef04b5d5464b5
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 1%
---
# よくある質問

**どのメタデータをVeevaに同期する必要がありますか？**

Veeva Portalのコンテンツタイプ（プロモーションなど）に基づいてメタデータを理解することが重要です。 Veeva Portalを確認したら、AEMでコンテンツメタデータスキーマを作成して、各アセット/ページの関連メタデータをすべて保持し、2つのシステム間でメタデータをマッピングするように統合を設定します。

**統合はVeeva リンクされたドキュメントをサポートしていますか？ サポートされていない場合、どの関係タイプがサポートされていますか？**

いいえ。 [Veeva ドキュメント &#x200B;](https://vaulthelp2.vod309.com/wordpress/admin-user-help/documents-admin-user-help/about-document-relationships/)を参照してください。 リンクされたドキュメント（参照関係タイプ）は、Vaultの特別な動作により、APIを介して作成または削除できない標準的な関係タイプの1つです。 コンポーネント、サポートドキュメント、およびこのリストに含まれないその他のドキュメントは、AEM Veeva Cloud設定を使用して設定できます。

**統合はAEM モジュラーコンテンツをサポートしていますか？**

はい、統合ではAEM コンテンツフラグメントとエクスペリエンスフラグメントをサポートしています。

**統合はVeeva モジュラーコンテンツをサポートしていますか？**

いいえ、今はありません。

**統合によってVeevaのビジュアルアノテーションがAEMに同期されますか？**

いいえ、今はありません。 ビジュアルアノテーションには、API as a PDF経由でのみアクセスできます。

**統合によって同期されたVVPM ドキュメントに対する権限を設定するにはどうすればよいですか？**

統合では、サービスユーザーを使用して、APIを介してドキュメントをアップロードします。  ドキュメントのデフォルト設定とルールの上書き（ドキュメントのデフォルトの役割）は、VVPM ユーザーインターフェイスでのみサポートされ、APIを使用する場合は適用されません。 役割の割り当てにDAC （Dynamic Access Control）を使用することをお勧めします。 DACは、APIを含むあらゆるタッチポイントを通じて適用されます。 [こちらのドキュメントを参照してください。](http://vaulthelp2.vod309.com/wordpress/admin-user-help/ah-user-permissions-access-control/about-dynamic-access-control-for-documents/)

**統合は複数のVVPM インスタンスをサポートしていますか？**

統合では、複数のVeeva エンドポイントを1つのAEM インスタンスから設定できるクラウド設定アプローチを使用します。

**統合はAEM パブリッシュをサポートしていますか？**

いいえ、この統合はAEM オーサーでのみ機能します。 コンテンツが公開される前に、MLR レビューサイクルを促進することを目的としています。
