
# OSSの概要
ここでは、OSS　プロダクトの理解を深めるために、ぞの基本概念を説明します。

## オブジェクト
オブジェクト（ファイルとも呼ばれます）は、個別のデータ単位です。

### オブジェクトは：
- メタデータ (オブジェクトメタ)は、最終変更時刻やサイズなどのオブジェクトの属性とユーザー定義の情報を表すキー値の組み合わせです。
- ユーザーデータ (データ)
- ユニークなオブジェクト名 (キー)

オブジェクトサイズは、アップロード方法によって異なります。マルチパートアップロードでは、48.8 TB までのオブジェクトがサポートされます。それ以外のアップロード方法でサポートされる最大サイズは、5 GB です。

オブジェクトのライフサイクルは、オブジェクトが正しくアップロードされたときに始まり、削除されたときに終了します。ライフサイクルの途中でオブジェクト情報を変更することはできません。同じ名前のオブジェクトを複数回アップロードすると、既存のオブジェクトは上書きされます。したがって、ファイルシステムとは異なり、OSS ではオブジェクト/ファイルを部分的に変更することはできません。

OSS の Append アップロード機能を使用すると、オブジェクトの末尾にデータをつなげて付加することができます。

オブジェクト命名規則: 
 
- UTF-8 エンコーディングを使用します。
- 長さは 1 ～ 1023 バイトでなければなりません。
- “/“ または “\” で開始することはできません。

>**注意** 

```
オブジェクト名では、大文字小文字が区別されます。特に断りがない限り、ここではファイルとオブジェクトは同じ意味を持ちます。
```

## バケット
バケットは、ファイルシステムとは異なり、オブジェクトをフラット構造で管理するオブジェクトストアの仮想部分です。

バケットのプロパティは次のとおりです。:
- すべてのオブジェクトはバケットに属していなければならず、オブジェクトのライフサイクル中は、対応するバケットに直接所属しています。
- ユーザーは複数のバケットを持つことができ、各バケットには無制限の数のオブジェクトを含めることができます。
- リージョンとオブジェクトのアクセス制御とオブジェクトライフサイクル管理するためにバケットの属性を設定および変更できます。 これらの属性は、バケット内のすべてのオブジェクトに適用されます。
- 複数のバケットを作成して、それぞれ異なる管理機能を実行することができます。


バケット命名規則:
- バケット名には、小文字のアルファベット、数字、ハイフン (-) のみを使用できます。 
- 先頭の文字は小文字のアルファベットまたは数字である必要があります。
- 長さは 3 ～ 63 バイトでなければなりません。
- OSS内でグローバルに唯一必要があります。 

一度バケット名が作成されると、変更することはできません。

## リージョン
リージョンは、OSS データセンターが物理的に配置される地域です。

データストレージのリージョンを料金、リクエストソースなどの要素に基づいて選ぶことができます。一般的に、リージョンに近いほどアクセス速度は向上します。詳細については、[OSS のリージョンとエンドポイント](~~31834~~)を参照してください。

リージョンはバケットの作成時に指定され、その後は変更できません。1 つのバケット内のすべてのオブジェクトは、対応するデータセンターに格納されます。現在、オブジェクト単位でのリージョンの設定はサポートされていません。


## エンドポイント (アクセスドメイン名)
エンドポイントは、OSS へのアクセスに使用されるドメイン名です。

OSS provides external services through HTTP RESTful APIs. Different regions use different endpoints. For the same region, access through an intranet or through the Internet also uses different endpoints. For example, regarding the Hangzhou region:

OSS は、HTTP RESTful API を通じて外部にサービスを提供しています。リージョンが異なると、使用されるドメイン名も異なります。イントラネットまたはインターネットを通じて同じリージョンにアクセスするためには、別のエンドポイントが使用されます。たとえば、杭州リージョンに関して:

- インターネットエンドポイントが oss-cn-hangzhou-internal.aliyuncs.com です。
- イントラネットエンドポイントが oss-cn-hangzhou.aliyuncs.comです。

詳細については、[OSS のリージョンとエンドポイント](~~31837~~)を参照してください。

## AccessKey
AccessKey (AK) は、アクセス時の ID 検証に使用される AccessKeyId と AccessKeySecret のペアを意味します。

OSS は、AccessKeyId と AccessKeySecret の対称暗号化方式を使用してリクエストの送信者の ID を検証します。AccessKeyId はユーザーを識別する情報です。AccessKeySecret は、ユーザーによる署名文字列の暗号化と、OSS による署名文字列の AccessKey の検証に使用されます。AccessKeySecret は、機密として扱う必要があります。OSS では、AccessKeys は次のソースから取得されます。

- バケットのオーナーによって適用された AccessKey
- 許可されたサードパーティのリクエスト送信者に対して、RAM を通じてバケットのオーナーによって付与された AccessKey
- 許可されたサードパーティのリクエスト送信者に対して、STS を通じてバケットのオーナーによって付与された AccessKey

AccessKeysの詳細については、[RAM](~~31867~~)を参照してください。

## 強力な整合性
OSS では、オブジェクト操作はアトミックです。操作に途中のステータスは存在せず、成功か失敗のいずれかです。ユーザーがオブジェクトをアップロードすると、OSS によって確実に完了されます。OSS からは、部分的なオブジェクトについてアップロード成功の応答は返されません。

OSS でのオブジェクト操作も、同様に強力な整合性を備えています。ユーザーがアップロード (PUT) の成功応答を受け取った時点で、このオブジェクトは直ちに読み取ることができ、データは 3 重の書き込みが完了しています。中間的なアップロードステータスは存在せず、リードアフターライトが行われます。それまでデータは読み取ることができません。削除操作でも同様です。ユーザーがオブジェクトを削除すると、そのオブジェクトは存在しません。

この強力な整合性機能は、ユーザーがアーキテクチャを設計する際に役立ちます。OSS のロジックは従来型のストレージデバイスのロジックと同じです。つまり、変更は直ちに反映され、最終的な整合性の問題を考慮する必要はありません。

## OSS とファイルシステムの比較
OSS は、キーと値のペアという形式を使用した分散型オブジェクトストレージサービスです。オブジェクトのコンテンツを取得するには、一意のオブジェクト名 (キー) を使用します。test1/test.jpg のような名前を使用することもできますが、これはオブジェクトが test1 という名前のディレクトリに保存されることを意味しません。OSS では、test1/test.jpg は単なる文字列であり、a.jpg と本質的な違いはありません。したがって、どちらの名前のオブジェクトにアクセスするときも、消費されるリソースの量に違いはありません。

ファイルシステムは、一般的なツリー上のインデックス構造を使用しています。test1/test.jpg という名前のオブジェクトにアクセスするには、クライアントはまず test1 ディレクトリにアクセスしてから、そのディレクトリ内で test.jpg というファイルを探します。これにより、ディレクトリの名前変更、ディレクトリの削除、ディレクトリの移動などのフォルダー操作がディレクトリノードだけの操作になり、ファイルシステムにとって対応しやすくなります。この構造では、アクセスするディレクトリのレベルが増えると消費されるリソースの量が増え、多数のファイルが存在するディレクトリに関係する操作に時間がかかります。

OSS にはほぼ同じ機能をシミュレートできる操作がいくつかありますが、料金が発生します。たとえば、test1 ディレクトリの名前を test2 に変更する場合、OSS での実際の操作は、test1/ で始まるすべてのオブジェクトを test2/ で始まるコピーに置き換えることです。この操作には、大量のリソースが消費されます。したがって、OSS を使用しているときは、できるだけこのような操作を避けることが必要です。

OSS では、保存されているオブジェクトの変更はサポートされません (Append Object 操作の場合は、特定の API を呼び出す必要があり、生成されるオブジェクトは通常のアップロードされたオブジェクトとはタイプが異なります)。たとえ 1 バイトでも変更するには、オブジェクト全体を再度アップロードする必要があります。ファイルシステムではファイルを変更することができます。たとえば、特定の位置のコンテンツを変更したり、オブジェクトの末尾部分を切り捨てたりすることができます。これらの機能により、ファイルシステムには幅広い応用範囲が生まれます。一方、OSS は同時に大量のアクセスに対応することができますが、ファイルシステムは単一のデバイスのパフォーマンスによる制約を受けます。

したがって、OSS をオブジェクトシステムにマップすることは非常に効率が悪く、お勧めしません。オブジェクトシステムをマウントすることが必要な場合は、操作を新しいファイルの書き込み、ファイルの削除、ファイルの読み取りに限定するように注意します。OSS を使用する際は、その利点を全面的に利用します。具体的には、大量のデータ処理能力により、イメージ、ビデオ、ドキュメントなどの構造化されていない大量のデータを保管します。

OSS とファイルシステムの概念の比較

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

## OSS 用語集

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
