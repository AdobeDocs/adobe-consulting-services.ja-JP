---
product: adobe experience manager
solution: Experience Manager
description: Experience Managerのドキュメントの参照
type: Documentation
git-repo: https://github.com/Adobe-Enterprise-Docs/adobe-consulting-services.ja-JP
index: y
author: Anon
source-git-commit: ac36c3ae49021c2b66234c8664df0969995aba62
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 54%

---


# 内部使用メタデータ

GitHub オーサリングシステムのメタデータは階層になっており、次の高い優先度で定義されています。

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

メタデータに関する追加情報については、[&#x200B; 内部オーサリングガイド &#x200B;](https://experienceleague.adobe.com/docs/authoring-guide-exl/using/authoring/metadata.html) を参照してください。
