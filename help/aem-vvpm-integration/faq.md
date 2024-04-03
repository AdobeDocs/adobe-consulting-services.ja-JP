---
title: Veeva Vault 統合に関する FAQ
description: Veeva Vault 統合に関する FAQ
exl-id: c308ebb3-7881-4094-9f35-c67a96fb5ab1
source-git-commit: e4a5e55ac9b79a8de7dfa8ddd3d0ad99560917b8
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 1%

---

# よくある質問

**Veeva に同期する必要があるメタデータは何ですか？**

Veeva ポータルのコンテンツタイプ（プロモーションなど）に基づくメタデータを理解することが重要です。 Veeva Portal を確認した後、AEMでコンテンツメタデータスキーマを構築して、各アセット/ページのすべての関連メタデータを保持し、2 つのシステム間でメタデータをマッピングするように統合を設定します。

**統合は Veeva リンクドキュメントをサポートしていますか？ そうでない場合、どの関係タイプがサポートされますか？**

いいえ。詳しくは、 [Veeva ドキュメント](https://vaulthelp2.vod309.com/wordpress/admin-user-help/documents-admin-user-help/about-document-relationships/). リンクされたドキュメント（参照関係タイプ）は、Vault の特別な動作を持つため API で作成または削除できない標準の関係タイプの 1 つです。 コンポーネント、サポートドキュメント、およびこのリストに記載されていないその他の情報は、AEM Veeva クラウド設定を介して設定できます。

**統合は、AEMモジュラーコンテンツをサポートしていますか？**

はい。統合は、AEMコンテンツフラグメントとエクスペリエンスフラグメントをサポートします。

**統合は Veeva モジュラーコンテンツをサポートしていますか？**

いいえ、現時点ではありません。

**統合は Veeva の視覚的な注釈をAEMに同期しますか？**

いいえ、現時点ではありません。 視覚的な注釈は、API を介してのみPDFとしてアクセスできます。

**統合によって同期された VVPM ドキュメントに権限を設定する方法を教えてください。**

この統合では、サービスユーザーを使用して、API を使用してドキュメントをアップロードします。  ドキュメントのデフォルト設定とルールの上書き（ドキュメントのデフォルトの役割）は、VVPM ユーザーインターフェイスでのみサポートされ、API を使用する場合は適用されません。 ロールの割り当てに DAC (Dynamic Access Control) を使用することをお勧めします。 DAC は、API を含むすべてのタッチポイントを通じて適用されます。 [こちらのドキュメントを参照してください。](http://vaulthelp2.vod309.com/wordpress/admin-user-help/ah-user-permissions-access-control/about-dynamic-access-control-for-documents/)

**この統合は複数の VPM インスタンスをサポートしていますか。**

この統合では、1 つのAEMインスタンスから複数の Veeva エンドポイントを設定できるクラウド設定アプローチを使用します。

**統合はAEMの公開をサポートしていますか？**

いいえ、この統合はAEMオーサーでのみ機能します。 これは、コンテンツが公開される前の MLR レビューサイクルを容易にするためのものです。
