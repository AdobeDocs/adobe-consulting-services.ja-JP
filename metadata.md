---
product: adobe experience manager
solution: Experience Manager
description: コンサルティングExperience Managerドキュメント
type: Documentation
git-repo: https://github.com/AdobeDocs/adobe-consulting-services.ja-JP
index: y
source-git-commit: e2dac4b36fb94d72b72ef6f73a77e3f566539444
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 54%

---


# 内部使用メタデータ

GitHub オーサリングシステムのメタデータは階層的で、次に示す前例のレベルが高くなっていきます。

1. metadata.md
1. 目次
1. 記事

metadata.md ファイルで定義されたメタデータはリポジトリ全体に適用されますが、目次と記事のレベルで上書きできます。メタデータの上書きは、可能な限り低いレベルで行う必要があります。

metadata.md

* `product`
* `git-repo`
* `index: y`

目次

* `sub-product`
* `user-guide-title`

記事

* `title`
* `description`

メタデータに関する追加情報は、 [内部オーサリングガイド](https://experienceleague.adobe.com/docs/authoring-guide-exl/using/authoring/metadata.html).
