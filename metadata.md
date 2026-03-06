---
product: adobe experience manager
solution: Experience Manager
description: Experience Managerのドキュメントの参照
type: Documentation
git-repo: https://github.com/AdobeDocs/adobe-consulting-services.en
index: true
source-git-commit: f491b48a151904f13becc146beab52600c9cef46
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 2%

---


# 内部使用のメタデータ

GitHub オーサリングシステムのメタデータは階層になっており、次の高い優先度で定義されています。

1. metadata.md
1. から C
1. 記事

metadata.md ファイルで定義されたメタデータはリポジトリ全体に適用されますが、目次と記事のレベルで上書きできます。 メタデータの上書きは、できるだけ低いレベルで行う必要があります。

metadata.md

* `product`
* `git-repo`
* `index: y`

ToCs

* `sub-product`
* `user-guide-title`

記事

* `title`
* `description`

メタデータに関する追加情報については、[ 内部オーサリングガイド ](https://experienceleague.adobe.com/docs/authoring-guide-exl/using/authoring/metadata.html) を参照してください。
