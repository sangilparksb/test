
# Basic OSS concepts
# OSSの基本概念
This section introduces the basic concepts of OSS.
このセクションでは、OSSの基本概念を紹介します。

## Object
## オブジェクト
An object (also known as a file) is a discrete unit of data. 
オブジェクト（ファイルとも呼ばれます）は、個別のデータ単位です。

An object is composed of:
オブジェクトは以下から構成されます。
- Metadata, known as Object Meta, which is a key-value pair that expresses the object's attributes, such as its last modification time and size, as well as user-defined information 
- User data, known as Data 
- A unique object name, known as a Key 
- オブジェクトメタ（Object Meta）と呼ばれるメタデータ。これは、オブジェクトの属性（最終変更時刻やサイズなど）とユーザー定義の情報などを表すキーと値のペアです
- データと呼ばれるユーザーデータ
- キーと呼ばれるユニークなオブジェクト名


The size of an object will vary depending on the upload method. Multipart Upload supports objects of up to 48.8 TB. Other upload methods only support objects of up to 5 GB.
オブジェクトサイズは、アップロード方法によって異なります。マルチパートアップロードでは、48.8 TB までのオブジェクトがサポートされます。それ以外のアップロード方法でサポートされる最大サイズは、5 GB です。

An object's lifecycle starts from when it has been successfully uploaded, and ends when it has been deleted. During an object's lifecycle, its information cannot be changed. If you upload an object with a duplicate name in a bucket, it will overwrite the existing one. Therefore, unlike the file system, OSS does not allow users to modify only part of an object.
オブジェクトのライフサイクルは、オブジェクトが正しくアップロードされたときに始まり、削除されたときに終了します。ライフサイクルの途中でオブジェクト情報を変更することはできません。同じ名前のオブジェクトを複数回アップロードすると、既存のオブジェクトは上書きされます。したがって、ファイルシステムとは異なり、OSS ではオブジェクト/ファイルを部分的に変更することはできません。

OSS provides the [Append Upload](~~31851~~) function, which allows users to continually append data to the end of an object.
OSS の Append アップロード機能を使用すると、オブジェクトの末尾にデータをつなげて付加することができます。

The name of an object must comply with the following rules: 
オブジェクト命名規則
  
- It must use UTF-8 encoding.                                  UTF-8 エンコーディングを使用します。
- It must be between 1-1023 bytes in length.                   長さは 1 ～ 1023 バイトでなければなりません。
- It cannot start with a backslash "/" or forward slash "\".   “/“ または “\” で開始することはできません。

>**NOTE:** Object names are case sensitive. オブジェクト名では、大文字小文字が区別されます。特に断りがない限り、ここではファイルとオブジェクトは同じ意味を持ちます。

##Bucket
A bucket is a virtual division of object storage that, unlike file systems, manages objects in a flat structure. 
##バケツ
バケットは、ファイルシステムとは異なり、フラットな構造のオブジェクトを管理するオブジェクトストレージの仮想分割です。

Bucket properties are as follows:バケットのプロパティは次のとおりです。
- All objects must belong to a bucket, and during an object's lifecycle it remains directly affiliated with the corresponding bucket.
- すべてのオブジェクトはバケットに属していなければならず、オブジェクトのライフサイクル中は、対応するバケットに直接所属しています。
- A user can have multiple buckets, with each bucket able to contain an unlimited number of objects.
- ユーザーは複数のバケットを持つことができ、各バケットには無制限の数のオブジェクトを含めることができます。
- You can set and modify the attributes of a bucket for region and object access control and object lifecycle management. These attributes apply to all objects in the bucket. 
リージョンとオブジェクトのアクセス制御とオブジェクトライフサイクル管理のためのバケットの属性を設定および変更できます。 これらの属性は、バケット内のすべてのオブジェクトに適用されます。
- You can create different buckets to perform different management functions. 
異なるバケットを作成して、異なる管理機能を実行することができます。

The name of a bucket must comply with the following rules:
- It can only contain lower-case letters, digits, and hyphens (-). 
- It must start and end with a lower-case letter or number.
- It must be between 3-63 bytes in length.
- It must be globally unique within the OSS. 
バケツの名前は、次の規則に従わなければなりません。
- 小文字、数字、ハイフン（ - ）のみを使用できます。
- 小文字の文字または数字で開始し、終了する必要があります。
- 長さは3〜63バイトでなければなりません。
- OSS内でグローバルに一意でなければなりません。
Once a bucket name is created, it cannot be changed.
バケット名が作成されると、変更することはできません。

##Region
A region represents the physical location of an OSS data center.
領域は、OSSデータセンターの物理的な場所を表します。

Users can select regions based on fees, request sources, and other factors according to site requirements. Generally, the closer the user is in proximity to a region, the faster the access speed will be. For more details, refer to [OSS Regions and Endpoints](~~31834~~).
ユーザーは、料金に基づいて地域を選択したり、サイトの要件に応じてソースやその他の要因を選択することができます。 一般的に、ユーザーが地域に近いほど、アクセス速度は速くなります。 詳細は、[OSSリージョンとエンドポイント](~~31834~~).を参照してください。

A region is specified when a bucket is created, and cannot be changed. All objects contained in this bucket are therefore stored in the corresponding data center. Setting different regions for objects in the same bucket is currently not supported.
領域は、バケットの作成時に指定され、変更することはできません。 したがって、このバケットに含まれるすべてのオブジェクトは、対応するデータセンターに格納されます。 同じバケット内のオブジェクトの異なる領域を設定することは、現在サポートされていません。


##Endpoint
An endpoint is the domain name used to access the OSS. 
エンドポイントは、OSSにアクセスするために使用されるドメイン名です。

OSS provides external services through HTTP RESTful APIs. Different regions use different endpoints. For the same region, access through an intranet or through the Internet also uses different endpoints. For example, regarding the Hangzhou region:
OSSは、HTTP RESTful APIを介して外部サービスを提供します。 異なる領域は異なるエンドポイントを使用します。 同じ地域では、イントラネットまたはインターネットを介したアクセスでも異なるエンドポイントが使用されます。 たとえば、杭州地域に関して：
- The intranet endpoint is oss-cn-hangzhou-internal.aliyuncs.com 
- The Internet endpoint is oss-cn-hangzhou.aliyuncs.com
- イントラネットエンドポイントはoss-cn-hangzhou-internal.aliyuncs.comです。
- インターネットエンドポイントはoss-cn-hangzhou.aliyuncs.comです。

For more details, refer to [OSS Regions and Endpoints](~~31837~~).
詳細は、[OSSリージョンとエンドポイント](~~31837~~)を参照してください。

##AccessKey
An AccessKey (AK) is composed of an AccessKeyId and AccessKeySecret. The AccessKeyId is a public key, whereas the AccessKeySecret is a private key and must be kept confidential. These are then paired together to perform access identity verification. 
AccessKey（AK）は、AccessKeyIdとAccessKeySecretで構成されます。 AccessKeyIdは公開鍵であり、AccessKeySecretは秘密鍵であり、秘密にしておく必要があります。 これらをペアにして、アクセスIDの検証を実行します。

The OSS verifies the identity of a request sender by using the AccessKeyId/AccessKeySecret symmetric encryption method. The AccessKeyId identifies a user. With the AccessKeySecret, a user can encrypt the signature string. The OSS then uses the symmetric encryption method to verify the AccessKey of the signature string. In OSS, AccessKeys are generated as follows:
OSSは、AccessKeyId / AccessKeySecret対称暗号化方式を使用して要求送信者の身元を検証します。 AccessKeyIdはユーザーを識別します。 AccessKeySecretを使用すると、ユーザーは署名文字列を暗号化できます。 次いで、OSSは、対称暗号化方法を使用して、署名文字列のアクセスキーを検証する。 OSSでは、AccessKeysは次のように生成されます。

- Applied for by the bucket owner.
- Granted by the bucket owner to an authorized third-party requestor through RAM.
- Granted by the bucket owner to an authorized third-party requestor through STS.
- バケット所有者によって適用されます。
- RAMを介してバケット所有者から許可された第三者リクエスタに許可されます。
- バケット所有者によって、STSを通じて許可された第三者リクエスタに与えられます。

For more information about AccessKeys, see [RAM](~~31867~~).
AccessKeysの詳細については、[RAM](~~31867~~)

##High consistency高い一貫性
In OSS, object operations are binary, that is, operations must either succeed or fail without an intermediate status. After a user uploads an object, OSS ensures that it is complete. OSS will not return a partial success response when uploading objects.
OSSでは、オブジェクト操作はバイナリです。つまり、操作は中間ステータスなしで成功または失敗する必要があります。 ユーザーがオブジェクトをアップロードすると、OSSはオブジェクトが完全であることを確認します。 OSSは、オブジェクトのアップロード時に部分的な成功応答を返しません。

Object operations in OSS are likewise highly consistent. For example, once a user receives an upload (PUT) success response, this object can be read immediately, and the data will have already been written in triplicate. The same concept applies to delete operations. Once a user deletes an object, this object no longer exists.
OSSにおけるオブジェクト操作も同様に高度に一貫しています。 たとえば、ユーザーがアップロード（PUT）成功応答を受け取ると、このオブジェクトは即座に読み取られ、データは既に3重に書き込まれます。 削除操作にも同じ概念が適用されます。 ユーザーがオブジェクトを削除すると、このオブジェクトは存在しなくなります。

This high-consistency feature facilitates user architectural design. The logic of OSS usage is the same as that of a traditional storage device: modifications are immediately visible and users do not have to consider final consistency issues.
この一貫性の高い機能により、ユーザーのアーキテクチャー設計が容易になります。 OSSの使用法のロジックは従来のストレージデバイスのロジックと同じです。変更はすぐに表示され、ユーザーは最終的な一貫性の問題を考慮する必要はありません。

##Comparison between OSS and file systemOSSとファイルシステムの比較
OSS is a distributed object storage service structure that uses a Key-Value pair format, whereas a file system uses a tree-type index structure of directories that contain files. In OSS, users retrieve object content based on unique object names (Keys). In file systems, users retrieve files based on their location in a directory. 
OSSは、Key-Valueペア形式を使用する分散オブジェクトストレージサービス構造ですが、ファイルシステムはファイルを含むディレクトリのツリー型インデックス構造を使用します。 OSSでは、ユーザーは一意のオブジェクト名（キー）に基づいてオブジェクトコンテンツを取得します。 ファイルシステムでは、ユーザーはディレクトリ内の場所に基づいてファイルを取得します。

The benefit of OSS is that it supports massive concurrent access volumes, which means large volumes of unstructured data (such as images, videos, and documents) can be stored and retrieved without excessive use of resources. The benefit of a file system is that folder operations such as renaming, moving, and deleting directories (which means renaming, moving, and deleting data) is considerably easier as data does not need to be copied and replaced. 
OSSのメリットは、膨大な量の同時アクセス・ボリュームをサポートすることです。これは、大量の非構造化データ（イメージ、ビデオ、ドキュメントなど）をリソースの過度の使用なしに格納および検索できることを意味します。 ファイルシステムの利点は、ディレクトリの名前変更、移動、削除（データの名前変更、移動、削除を意味する）などのフォルダ操作は、データをコピーして置き換える必要がないため、かなり簡単です。

The limitation of OSS is that saved objects cannot be modified. If an object needs modification, the entire object must be uploaded again to make the modification take effect. One exception is through using the append object operation, whereby users call a specific API, which allows a generated object be of a different type than normally uploaded objects. The limitations of a file system are that system performance is limited to a single device, and the more files and directories that are created in the system, the more resources are consumed, and the lengthier user processes become.
OSSの制限は、保存されたオブジェクトを変更できないことです。 オブジェクトの変更が必要な場合は、オブジェクト全体を再度アップロードして変更を有効にする必要があります。 1つの例外はオブジェクトの追加操作を使用することです。ユーザーは特定のAPIを呼び出します。これにより、生成されたオブジェクトは通常アップロードされるオブジェクトとは異なるタイプになります。 ファイルシステムの限界は、システムのパフォーマンスが単一のデバイスに限定され、システムで作成されるファイルとディレクトリが多くなればなるほど、リソースが消費され、ユーザープロセスが長くなるということです。

Comparisons between OSS and file system concepts are as follows:OSSとファイルシステムの概念の比較は次のとおりです。

| OSS | File system |
|----------|---------|
| Object | File |
| Bucket | Main directory  |
| Region | N/A |
| Endpoint | N/A |
| AccessKey | N/A |
| N/A | Multilevel directory |
| GetService | Retrieving the list of main directories |
| GetBucket | Retrieving the list of files |
| PutObject | Writing an object |
| AppendObject | Append writing an object |
| GetObject | Reading an object |
| DeleteObject | Deleting an object |
| N/A | Modifying file content |
| CopyObject (same target and source) | Modifying file attributes |
| CopyObject | Copying an object |
| N/A | Renaming an object |

##OSS GlossaryOSS用語集

| Term       | Definition   |    
|:--------|:-----|
| Object     | A discrete unit of data|  
| Bucket       |  A virtual division of object storage |
| Endpoint | The domain name for OSS access|
| Region | A representation of the physical location of an OSS data center |
|AccessKey |An alias for the AccessKeyId and AccessKeySecret pair|
|Put Object|Simple upload|
|Post Object|Form upload|
|Multipart Upload| The uploading of an object as several chunks, then reassembling the chunks|
|Append Object|An upload that attaches to already uploaded data|
|Get Object|Simple download|
|Callback|Upload callback|
|Object Meta|Metadata of a file that includes the object's attributes and user-defined information|
|Data|Object information (typically user-defined information)|
|Key|Unique object name|
|ACL (Access Control List)|Permissions for buckets or files||
