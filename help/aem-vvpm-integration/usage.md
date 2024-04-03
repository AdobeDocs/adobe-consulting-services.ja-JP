---
title: Veeva Vault 統合の使用
description: Veeva Vault 統合の使用
exl-id: efff7af1-eb25-4a1d-b7ef-52e3336970ff
source-git-commit: 19949a48cfee0c17481e52f286a460e9d81d7ff0
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 5%

---

# 統合の使用

## 順を追う

次のビデオのウォークスルーでは、コネクタの使用について説明します。

>[!VIDEO](https://video.tv.adobe.com/v/332137/?quality=12&learn=on)

## 設定

このガイドでは、コネクタの立ち上げと実行の手順を説明します。

>[!IMPORTANT]
>
>各システムに対して、次の手順を **administrator** 各システムの
>
>このドキュメントの手順では、権限の割り当てや管理者アクセスに関連する統合/登録の作成手順を説明します。  これらの手順を実行する前に会社のポリシーに従い、慎重に実行する必要があるのは、お客様の責任です。
>

### 統合パッケージのインストール

統合AEMパッケージへのアクセス権が付与されます。 統合をインストールする方法は 2 つあります。

1. **パッケージのインストール**  — まっすぐ進み、あまり関わりがない。
2. **POM のインストール**  — より高度ですが、AEM Cloud Manager を使用して統合をアップグレードする場合に便利です。

#### パッケージのインストール

パッケージをインストールするには、オンボーディング電子メールに記載されているリンクを含んでダウンロードします。 [AEMパッケージのインストールについて詳しくは、ここをクリックしてください。](https://experienceleague.adobe.com/docs/experience-manager-64/administering/contentmanagement/package-manager.html?#installing-packages)

#### POM のインストール

POM にコネクタを含めるには、次の手順に従います。 ユーザー名とパスワードをオンボーディングメールで受け取ったものに置き換えます。

1. 以下を `.cloudmanager/maven/settings.xml` プロジェクト内のファイル、または `~/.m2/settings.xml` を使用しています。 置換 `YOUR_USERNAME` ユーザー名と `YOUR_PASSWORD` オンボーディング用の E メールに記載されているパスワードを含む

   >[!IMPORTANT]
   >
   >Cloud Manager を使用する場合の安全なアプローチは、次の手順に従うことです。 [パスワードで保護された Maven リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/create-application-project/setting-up-project.html?lang=en#password-protected-maven-repositories).
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

2. 以下をプロジェクトの `pom.xml` ファイル：

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

3. 以下をプロジェクトの `all/pom.xml` ファイル。 置換 `project.dependencies.dependency.version` 適切なバージョンと `project.build.plugins.plugin.configuration.embeddeds.embedded.target` を正しいパスに置き換えます。

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

この統合は、コネクタを操作するフォルダーにクラウド設定を作成することで設定します。 クラウド設定を作成するには、次の手順に従います。

1. Veeva クラウド設定に移動します。

   ![クラウド設定に移動](assets/cloud-config-navigate.png)

2. 適切なフォルダーに新しい Veeva クラウド設定を作成し、次の節で説明するように設定します。

   ![クラウド設定を作成](assets/cloud-config-create.png)

#### 「設定」タブ

「設定」タブで、以下の項目に入力します。

![「設定」タブ](assets/configuration-tab.png)

1. 必須。Veeva Vault コネクタ設定のタイトル。 任意の値を指定できます。 ( 例： `Veeva Vault Configuration`)
2. 必須。Veeva インスタンスのドメイン URL ( 例： `https://my-instance.veevavault.com/`)
3. 必須。Veeva Vault API を呼び出すには ClientID が必要です。 任意の値を指定でき、主にデバッグに使用されます。 ( 例： `adobe-aem-vvtechpartner`)
4. 必須。Veeva Vault ユーザー名。 詳しくは、 [Veeva ユーザーの作成](#veeva-user-creation).
5. 必須。Veeva Vault のパスワード。 詳しくは、 [Veeva ユーザーの作成](#veeva-user-creation).

#### AdobeIO タブ

プロジェクトでページのPDFまたは画像を生成する必要がある場合、このタブは必須です。 「Adobe I/O」タブで以下の情報を入力します。

![AdobeIO タブ](assets/adobe-io-tab.png)

1. 必須。オンボーディング E メールで提供されたPDF画像を作成するためのAdobeI/O エンドポイント。 ( 例： `https://my-namespace.adobeioruntime.net/api/v1/web/aem-veeva-serverless-0.0.2/trigger-action.json`)
2. 必須。ページ画像生成のアクション名。 この値は、 `aem-veeva-integration/get-image-async`.
3. 必須。HTML 画像生成のアクション名。 この値は、 `aem-veeva-integration/get-pdf-async-new`.
4. 必須。AdobeI/O エンドポイント：オンボーディング E メールで提供された生成の状態を取得します。( 例： `https://my-namespace.adobeioruntime.net/api/v1/web/aem-veeva-serverless-0.0.2/get-state-value`)
5. 必須。AEMI/O で使用するAdobeユーザー名。 詳しくは、 [AEM User Creation](#aem-user-creation).
6. 必須。AEM I/O で使用するAdobe。 詳しくは、 [AEM User Creation](#aem-user-creation).
7. オプション。デフォルトのタイムアウトは、AIO サービスが応答の取得を停止するまで、指定された時間までページを応答させることです。 デフォルト値は `30000` です。
8. オプション。遅延は、ページが 200 で応答した後に、スクリーンショットを取る前に、すべての画像がレンダリングされるのを遅らせます。 デフォルト値は `2000` です。
9. オプション。スクリーンショット/PDFで生成された URL は、設定された値（秒）の後に期限切れになります。
10. オプション。AdobeIO スクリーンショット/PDF生成サービスが非同期です。 AEMサービスが AIO ステータスエンドポイントを呼び出して、スクリーンショット/PDFを取得します。 このプロパティは、各ステータス呼び出しの間の一時停止をミリ秒単位で決定します。 デフォルト値は `10000` です。
11. オプション。スクリーンショット/PDFを取得するためのAdobeI/O に対するステータス呼び出しの最大再試行回数。 デフォルト値は `10` です。

#### 「詳細」タブ

「詳細設定」タブで、以下の情報を入力します。

![「詳細」タブ](assets/advanced-tab.png)

1. PDF/画像の生成に必要。 PDF/画像の作成時に使用するファイル名パターン。 `{name}` はテンプレート化できます。 ( 例： `{name}-screenshot`)
2. オプション。デスクトップ以外でページスクリーンショットが必要なデバイスタイプ。 有効なタイプは次のとおりです。 `Tab (iPad)`、および `Mobile (iPhone X)`.
3. オプション。上記のレンディションを表す Veeva のレンディションタイプ値。 ( 例： `web_ready__c`)
4. PDF/画像の生成に必要。 作成するスクリーンショットタイプ。 次のいずれか `PDF` または `Image`.
5. PDF/画像の生成に必要。 生成するPDFのタイプ。 次のいずれか `Print CSS Based PDF` または `Pixel Perfect Screenshot PDF`.
6. PDF/画像の生成に必要。 生成する画像タイプ。 次のいずれか `PNG` または `JPEG`.
7. 必須。Veeva Vault 承認トリガーが終了した後に実行するワークフロー。
8. 必須。Approved を表す status プロパティの値。 ( 例： `Approved for Distribution`)
9. 必須。Veeva Vault 拒否ワークフローが終了したらトリガーを実行するワークフロー。
10. 必須。Rejected/Not approved を表す Status プロパティの値。 ( 例： `Rejected`)
11. オプション。Veeva Vault でのドキュメント ID のプロパティ名。 デフォルト値は `id` です。
12. オプション。Veeva Vault でのステータスのプロパティ名。 デフォルト値は `status__v` です。
13. オプション。ドキュメント変更日のプロパティ名。 デフォルト値は `version_modified_date__v` です。
14. オプション。ドキュメントリソース URL のプロパティ名です。 デフォルト値は次のとおりです。 `external_id__v`. このフィールドが既に使用されている場合は、Veeva で別のフィールドを作成し、ここにフィールド名を入力します。 このフィールドは、Veeva でAEMリソースパスを保持するために使用されます。 これは、メタデータの自動同期に必要です。
15. オプション。Veeva Vault のメジャーバージョン番号のプロパティ名。 デフォルト値は `major_version_number__v` です。
16. オプション。Veeva Vault のマイナーバージョン番号のプロパティ名。 デフォルト値は `minor_version_number__v` です。
17. オプション。Veeva Vault 関係タイプ値。 ページに追加されたすべてのアセットは、この値に基づいて関連付けられたとして表されます。 デフォルト値は `supporting_document__c` です。

#### 「ページ」タブ

ページを同期する場合は、「ページ」タブで以下の情報を入力します。

![「ページ」タブ](assets/page-tab.png)

1. 必須。プロパティをAEMから Veeva にマッピングします。
a. AEMプロパティ名。 AEMプロパティから選択できます。 ( 例： `jcr:title`) `{name}` はテンプレート化できます。
b.に正確に入力された Veeva プロパティ名は Veeva に存在します。 ( 例： `name__v`)\
   c.プロパティタイプ。 次のいずれか `Text` または `Multiline Text`.

2. 必須。Veeva からAEMにプロパティをマッピングします。
a. Veeva プロパティ名が Veeva に存在します。 ( 例： `name__v`) b. AEMプロパティ名。 AEMプロパティから選択できます。 ( 例： `jcr:title`) c.プロパティタイプ。 次のいずれか `Text` または `Multiline Text`.


#### 「アセット」タブ

アセットを同期する場合は、「アセット」タブで以下の情報を入力します。

![「アセット」タブ](assets/asset-tab.png)

1. 必須。プロパティをAEMから Veeva にマッピングします。
a. AEMプロパティ名。 AEMプロパティから選択できます。 ( 例： `/jcr:content/metadata/jcr:title`) `{name}` はテンプレート化できます。
b.に正確に入力された Veeva プロパティ名は Veeva に存在します。 ( 例： `name__v`) c.プロパティタイプ。 次のいずれか `Text` または `Multiline Text`.

2. 必須。Veeva からAEMにプロパティをマッピングします。
a. Veeva プロパティ名が Veeva に存在します。 ( 例： `name__v`) b. AEMプロパティ名。 AEMプロパティから選択できます。 ( 例： `/jcr:content/metadata/jcr:title`) c.プロパティタイプ。 次のいずれか `Text` または `Multiline Text`.

### その他の設定

#### AEM User Creation

PDF/画像の生成時に、AEMからページを取得するには、AEMユーザーを作成する必要があります。 次のリンクに従って、ユーザーに読み取り専用の権限を作成し、付与します。

AEM 6.5.5 以降を使用する場合：

* [AEMでのユーザーの作成](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/setup-organize-users/adding-configuring-users.html?#create-a-user)
* [AEMでのユーザーへの権限の追加](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?#permissions-in-aem)

AEMCloud Serviceを使用する場合：

* [ユーザー管理とAEMCloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?#accessing)

PDF/画像に変換して Veeva にプッシュするコンテンツに対するAEMサービスユーザーには、次の権限が必要です。

* 読み取り

>[!IMPORTANT]
>
> これらのアクションは、各システムの管理者として実行する必要があります。
> ユーザーを作成し、権限を設定する際は、組織のセキュリティ標準に従う必要があります。
>

#### Veeva ユーザーの作成

この統合を使用するには、Veeva Vault でユーザーを作成する必要があります。 ユーザーを作成するには、次の手順に従います。

1. [ 管理 ] -> [ ユーザとグループ ] -> [Vault ユーザ ] -> [ 作成 ] の順に選択します。

   ![Veeva ユーザーに移動](assets/veeva-user-navigate.png)

2. 必要な入力を入力します。 最も簡単な設定は、 `License Type` から `Full User` そして `Security Profile` から `Vault Owner`. 完了したら保存します。

   ![Veeva ユーザーを作成](assets/veeva-user-create.png)

使用中の特定の Veeva ドキュメントタイプには、次の権限が必要です。

* ドキュメントの作成/読み取り
* バージョンの作成/読み取り
* メタデータを作成/更新
* レンディションを作成/更新

>[!IMPORTANT]
>
> これらのアクションは、各システムの管理者として実行する必要があります。
> ユーザーを作成し、権限を設定する際は、組織のセキュリティ標準に従う必要があります。
>
