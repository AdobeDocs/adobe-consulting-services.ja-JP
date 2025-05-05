---
title: Veeva Vault 統合の使用状況
description: Veeva Vault 統合の使用状況
exl-id: efff7af1-eb25-4a1d-b7ef-52e3336970ff
source-git-commit: 19949a48cfee0c17481e52f286a460e9d81d7ff0
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 5%

---

# 統合の使用状況

## ガイド

次のビデオのウォークスルーでは、コネクタの使用について説明しています。

>[!VIDEO](https://video.tv.adobe.com/v/332137/?quality=12&learn=on)

## 設定

このガイドでは、コネクタの立ち上げと実行について説明します。

>[!IMPORTANT]
>
>システムごとに、システムごとに **管理者** がこれらの手順を実行する必要があります。
>
>このドキュメントの手順では、権限の割り当てや管理者アクセスに関連する統合/登録の作成手順を説明します。  お客様の責任として、事前に会社のポリシーに従って手順を確認し、慎重に実行する必要があります。
>

### 統合パッケージのインストール

統合AEM パッケージへのアクセス権が付与されます。 統合をインストールするには、次の 2 つのオプションがあります。

1. **パッケージのインストール** – 簡単で手間がかからない。
2. **POM のインストール** – より高度ですが、AEM Cloud Managerを使用して統合をアップグレードする際に役立ちます。

#### パッケージインストール

パッケージをインストールするには、オンボーディングメールで提供されるリンクと共にダウンロードします。 [AEM パッケージのインストール手順について詳しくは、こちらをクリックしてください。](https://experienceleague.adobe.com/docs/experience-manager-64/administering/contentmanagement/package-manager.html?lang=ja&#installing-packages)

#### POM インストール

コネクタを POM に含めるには、次の手順に従います。 ユーザー名とパスワードを、オンボーディングメールで受信したパスワードに置き換えます。

1. プロジェクトまたはコンピューターの `.cloudmanager/maven/settings.xml` ファイルに、次の `~/.m2/settings.xml` を追加します。 `YOUR_USERNAME` をユーザー名に、`YOUR_PASSWORD` をオンボーディングメールで指定されたパスワードに置き換えます。

   >[!IMPORTANT]
   >
   >Cloud manager を使用する場合、安全なアプローチは、ここに記載されている [ パスワードで保護された Maven リポジトリ ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/create-application-project/setting-up-project.html?lang=ja#password-protected-maven-repositories) の手順に従うことです。
   >

   ```
   <settings>
       ...
       <servers>
           ...
           <server>
               <id>repo.ea.adobe.net</id>
               <username>YOUR_USERNAME</username>
               <password>YOUR_PASSWORD</password>
               <filePermissions>BucketOwnerFullControl</filePermissions>
               <configuration>
                 <wagonProvider>s3</wagonProvider>
               </configuration>
           </server>
           ...
       </servers>
       ...
   </settings>
   ```

2. プロジェクトの `pom.xml` ファイルに次の内容を追加します。

   ```
   <project>
       ...
       <build>
           ...
           <extensions>
               ...
               <extension>
                   <groupId>com.allogy.maven.wagon</groupId>
                   <artifactId>maven-s3-wagon</artifactId>
                   <version>1.2.0</version>
               </extension>
               ...
           </extensions>
           ...
       </build>
       ...
       <repositories>
           ...
           <repository>
               <id>repo.ea.adobe.net</id>
               <url>s3://repo.ea.adobe.net/release</url>
               <releases>
                   <enabled>true</enabled>
               </releases>
           </repository>
           ...
       </repositories>
       ...
   </project>
   ```

3. プロジェクトの `all/pom.xml` ファイルに次の内容を追加します。 `project.dependencies.dependency.version` を適切なバージョンに、`project.build.plugins.plugin.configuration.embeddeds.embedded.target` を正しいパスに置き換えます。

   ```
   <project>
       ...
       <build>
           ...
           <plugins>
               ...
               <plugin>
                   <groupId>org.apache.jackrabbit</groupId>
                   <artifactId>filevault-package-maven-plugin</artifactId>
                   ...
                   <configuration>
                       ...
                       <embeddeds>
                           ...
                           <embedded>
                               <groupId>com.adobe.acs.aemveeva</groupId>
                               <artifactId>aem-veeva-connector.all</artifactId>
                               <type>zip</type>
                               <target>/apps/APP_NAME-packages/application/install</target>
                           </embedded>
                           ...
                       </embeddeds>
                   </configuration>
               </plugin>
               ...
           </plugins>
           ...
       </build>
       ...
       <dependencies>
           ...
           <dependency>
               <groupId>com.adobe.acs.aemveeva</groupId>
               <artifactId>aem-veeva-connector.all</artifactId>
               <version>1.0.5</version>
               <type>zip</type>
           </dependency>            
           ...
       </dependencies>
       ...
   </project>
   ```

### クラウド設定

この統合は、コネクタを動作させるフォルダーにクラウド設定を作成することで設定します。 クラウド設定を作成するには、次の手順に従います。

1. Veeva クラウド設定に移動します。

   ![ クラウド設定に移動 ](assets/cloud-config-navigate.png)

2. 適切なフォルダーに新しい Veeva クラウド設定を作成し、次の節で説明するように入力します。

   ![ クラウド設定の作成 ](assets/cloud-config-create.png)

#### 「設定」タブ

「設定」タブで次の情報を入力します。

![ 「設定」タブ ](assets/configuration-tab.png)

1. 必須。Veeva Vault コネクタ設定のタイトル。 これは任意の値を指定できます。 （例：`Veeva Vault Configuration`）
2. 必須。Veeva インスタンスのドメイン URL （例：`https://my-instance.veevavault.com/`）
3. 必須。Veeva Vault API を呼び出すには ClientID が必要です。 これは任意の値を指定でき、主にデバッグに使用されます。 （例：`adobe-aem-vvtechpartner`）
4. 必須。Veeva Vault のユーザー名。 [Veeva ユーザーの作成 ](#veeva-user-creation) を参照してください。
5. 必須。Veeva Vault のパスワード [Veeva ユーザーの作成 ](#veeva-user-creation) を参照してください。

#### 「Adobe I/O」タブ

プロジェクトでページ用のPDFまたは画像を生成する必要がある場合は、このタブが必要です。 Adobe io タブに次の情報を入力します。

![Adobe IO タブ ](assets/adobe-io-tab.png)

1. 必須。オンボーディングメールで提供された、PDF画像を作成するためのAdobe IO エンドポイント。 （例：`https://my-namespace.adobeioruntime.net/api/v1/web/aem-veeva-serverless-0.0.2/trigger-action.json`）
2. 必須。ページ画像生成のアクション名。 この値は `aem-veeva-integration/get-image-async` である必要があります。
3. 必須。HTML 画像生成のアクション名。 この値は `aem-veeva-integration/get-pdf-async-new` である必要があります。
4. 必須。オンボーディングメールで提供されたAdobeの状態を取得する世代 IO エンドポイント。（例：`https://my-namespace.adobeioruntime.net/api/v1/web/aem-veeva-serverless-0.0.2/get-state-value`）
5. 必須。Adobe IO で使用されるAEM ユーザー名。 [AEM ユーザーの作成 ](#aem-user-creation) を参照してください。
6. 必須。Adobe IO で使用するAEM パスワード。 [AEM ユーザーの作成 ](#aem-user-creation) を参照してください。
7. オプション。デフォルトのタイムアウトでは、指定された時間が経過すると AIO サービスが応答を取得しようとしなくなるまで、ページを応答させます。 デフォルト値は `30000` です。
8. オプション。遅延は、スクリーンショットを取得する前にすべての画像がレンダリングされる 200 でページが応答した後です。 デフォルト値は `2000` です。
9. オプション。スクリーンショット/PDFで生成された URL は、設定された値（秒）が経過すると有効期限が切れます。
10. オプション。Adobe I/O スクリーンショット/PDF生成サービスが非同期です。 AEM サービスは AIO ステータスエンドポイントを呼び出して、スクリーンショット/PDFを取得します。 このプロパティは、各ステータス呼び出しの間の一時停止をミリ秒単位で決定します。 デフォルト値は `10000` です。
11. オプション。スクリーンショット/PDFを取得するためのAdobe IO へのステータス呼び出しの最大再試行回数。 デフォルト値は `10` です。

#### 「詳細」タブ

「詳細」タブで次の情報を入力します。

![ 「詳細」タブ ](assets/advanced-tab.png)

1. PDF/画像生成に必須。 PDF/画像を作成する際に使用するファイル名のパターン。 `{name}` はテンプレート化できます。 （例：`{name}-screenshot`）
2. オプション。デスクトップ以外にページのスクリーンショットが必要なデバイスタイプ。 有効なタイプには、`Tab (iPad)`、`Mobile (iPhone X)` などがあります。
3. オプション。上記のレンディションを表す Veeva のレンディションタイプ値。 （例：`web_ready__c`）
4. PDF/画像生成に必須。 作成するスクリーンショットタイプ。 `PDF` または `Image`。
5. PDF/画像生成に必須。 生成するPDFタイプ。 `Print CSS Based PDF` または `Pixel Perfect Screenshot PDF`。
6. PDF/画像生成に必須。 生成する画像タイプ。 `PNG` または `JPEG`。
7. 必須。Veeva Vault Approvalトリガーが完了した後に実行するワークフロー。
8. 必須。承認済みを表すステータスプロパティ値。 （例：`Approved for Distribution`）
9. 必須。Veeva Vault 却下トリガーが発生した場合に実行するワークフロー。
10. 必須。却下/未承認を表すステータスプロパティ値。 （例：`Rejected`）
11. オプション。Veeva Vault のドキュメント ID のプロパティ名。 デフォルト値は `id` です。
12. オプション。Veeva Vault のステータスのプロパティ名。 デフォルト値は `status__v` です。
13. オプション。ドキュメント変更日のプロパティ名です。 デフォルト値は `version_modified_date__v` です。
14. オプション。ドキュメントリソース URL のプロパティ名。 デフォルト値は `external_id__v` です。 このフィールドが既に使用されている場合は、Veeva で別のフィールドを作成し、フィールド名をここに入力します。 このフィールドは、AEM リソースパスを保持するために Veeva で使用されます。 これは、メタデータの自動同期に必要です。
15. オプション。Veeva Vault のメジャーバージョン番号のプロパティ名。 デフォルト値は `major_version_number__v` です。
16. オプション。Veeva Vault のマイナーバージョン番号のプロパティ名。 デフォルト値は `minor_version_number__v` です。
17. オプション。Veeva Vault 関係タイプの値。 ページに追加されたすべてのアセットは、この値に基づいて関連アセットとして表されます。 デフォルト値は `supporting_document__c` です。

#### 「ページ」タブ

ページを同期する場合は、「ページ」タブで次の項目を入力します。

![ 「ページ」タブ ](assets/page-tab.png)

1. 必須。プロパティをAEMから Veeva にマッピングします。
a. AEM プロパティ名。 AEM プロパティから選択可能 （例：`jcr:title`） `{name}` テンプレート化できます。
b. Veeva プロパティ名を正確に入力すると、Veeva に存在します。 （例：`name__v`）\
   c. プロパティタイプ。 `Text` または `Multiline Text`。

2. 必須。プロパティを Veeva からAEMにマッピングします。
a. Veeva に正確に入力されたプロパティ名が Veeva に存在します。 （例：`name__v`）
b. AEM プロパティ名。 AEM プロパティから選択可能 （例：`jcr:title`）
c. プロパティタイプ。 `Text` または `Multiline Text`。


#### 「アセット」タブ

アセットを同期する場合は、「アセット」タブで次の情報を入力します。

![ 「アセット」タブ ](assets/asset-tab.png)

1. 必須。プロパティをAEMから Veeva にマッピングします。
a. AEM プロパティ名。 AEM プロパティから選択可能 （例：`/jcr:content/metadata/jcr:title`） `{name}` テンプレート化できます。
b. Veeva プロパティ名を正確に入力すると、Veeva に存在します。 （例：`name__v`）
c. プロパティタイプ。 `Text` または `Multiline Text`。

2. 必須。プロパティを Veeva からAEMにマッピングします。
a. Veeva に正確に入力されたプロパティ名が Veeva に存在します。 （例：`name__v`）
b. AEM プロパティ名。 AEM プロパティから選択可能 （例：`/jcr:content/metadata/jcr:title`）
c. プロパティタイプ。 `Text` または `Multiline Text`。

### 追加設定

#### AEM ユーザーの作成

PDF/画像の生成中に、AEMからページを取得するために、AEM ユーザーを作成する必要があります。 次のリンクに従って、ユーザーに読み取り専用権限を作成および付与します。

AEM 6.5.5 以降を使用している場合：

* [AEMでのユーザーの作成 ](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/setup-organize-users/adding-configuring-users.html?lang=ja&#create-a-user)
* [AEMでのユーザーへの権限の追加 ](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=ja&#permissions-in-aem)

AEM Cloud Serviceを使用している場合：

* [AEM Cloud Serviceを使用したユーザーの管理 ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=ja&#accessing)

PDF/画像に変換されて Veeva にプッシュされるコンテンツに対するAEM サービスユーザーには、次の権限が必要です。

* 読み取り

>[!IMPORTANT]
>
> これらのアクションは、システムごとに管理者として実行する必要があります。
> ユーザーの作成や権限の設定を行う場合は、組織のセキュリティ標準に従う必要があります。
>

#### Veeva ユーザーの作成

この統合を使用するには、Veeva Vault でユーザーを作成する必要があります。 ユーザーを作成するには、次の手順に従います。

1. 管理者/ユーザーとグループ/Vault ユーザー/作成に移動します。

   ![Veeva ユーザーに移動 ](assets/veeva-user-navigate.png)

2. 必要な入力を行います。 最も簡単な設定は、`License Type` を `Full User` に、`Security Profile` を `Vault Owner` に設定することです。 完了したら保存します。

   ![Veeva ユーザーの作成 ](assets/veeva-user-create.png)

使用されている特定の Veeva ドキュメントタイプには、次の権限が必要です。

* ドキュメントの作成/読み取り
* バージョンの作成/読み取り
* メタデータの作成/更新
* レンディションの作成/更新

>[!IMPORTANT]
>
> これらのアクションは、システムごとに管理者として実行する必要があります。
> ユーザーの作成や権限の設定を行う場合は、組織のセキュリティ標準に従う必要があります。
>
