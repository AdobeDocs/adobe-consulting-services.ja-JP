---
product: adobe experience manager
solution: Experience Manager
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
usetq: true
description: Experience Managerのドキュメントのコンサルティング
type: Documentation
git-repo: https://github.com/AdobeDocs/adobe-consulting-services.en
index: true
source-git-commit: e0159a3db7c79d12ee150be018ee5d005975b95a
workflow-type: tm+mt
source-wordcount: 94
ht-degree: 2%

---


# 内部使用のためのメタデータ

GitHub オーサリングシステムのメタデータは階層的であり、次のレベルの前例で定義されています。

1. metadata.md
1. ToC
1. 記事

metadata.md ファイルで定義されたメタデータは、リポジトリ全体に適用されますが、ToC レベルとアーティクルレベルで上書きできます。 メタデータの上書きは、可能な限り低いレベルで行う必要があります。

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

メタデータに関する追加情報については、[社内オーサリングガイド &#x200B;](https://experienceleague.adobe.com/docs/authoring-guide-exl/using/authoring/metadata.html)を参照してください。
