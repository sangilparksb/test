
# Basic OSS concepts
This section introduces the basic concepts of OSS.

## Object
An object (also known as a file) is a discrete unit of data. 

An object is composed of:
- Metadata, known as Object Meta, which is a key-value pair that expresses the object's attributes, such as its last modification time and size, as well as user-defined information 
- User data, known as Data 
- A unique object name, known as a Key 

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

Bucket properties are as follows:
- All objects must belong to a bucket, and during an object's lifecycle it remains directly affiliated with the corresponding bucket.
- A user can have multiple buckets, with each bucket able to contain an unlimited number of objects.
- You can set and modify the attributes of a bucket for region and object access control and object lifecycle management. These attributes apply to all objects in the bucket. 
- You can create different buckets to perform different management functions. 

The name of a bucket must comply with the following rules:
- It can only contain lower-case letters, digits, and hyphens (-). 
- It must start and end with a lower-case letter or number.
- It must be between 3-63 bytes in length.
- It must be globally unique within the OSS. 

Once a bucket name is created, it cannot be changed.


##Region
A region represents the physical location of an OSS data center.

Users can select regions based on fees, request sources, and other factors according to site requirements. Generally, the closer the user is in proximity to a region, the faster the access speed will be. For more details, refer to [OSS Regions and Endpoints](~~31834~~).

A region is specified when a bucket is created, and cannot be changed. All objects contained in this bucket are therefore stored in the corresponding data center. Setting different regions for objects in the same bucket is currently not supported.


##Endpoint
An endpoint is the domain name used to access the OSS. 

OSS provides external services through HTTP RESTful APIs. Different regions use different endpoints. For the same region, access through an intranet or through the Internet also uses different endpoints. For example, regarding the Hangzhou region:
- The intranet endpoint is oss-cn-hangzhou-internal.aliyuncs.com 
- The Internet endpoint is oss-cn-hangzhou.aliyuncs.com

For more details, refer to [OSS Regions and Endpoints](~~31837~~).


##AccessKey
An AccessKey (AK) is composed of an AccessKeyId and AccessKeySecret. The AccessKeyId is a public key, whereas the AccessKeySecret is a private key and must be kept confidential. These are then paired together to perform access identity verification. 

The OSS verifies the identity of a request sender by using the AccessKeyId/AccessKeySecret symmetric encryption method. The AccessKeyId identifies a user. With the AccessKeySecret, a user can encrypt the signature string. The OSS then uses the symmetric encryption method to verify the AccessKey of the signature string. In OSS, AccessKeys are generated as follows:

- Applied for by the bucket owner.
- Granted by the bucket owner to an authorized third-party requestor through RAM.
- Granted by the bucket owner to an authorized third-party requestor through STS.

For more information about AccessKeys, see [RAM](~~31867~~).


##High consistency
In OSS, object operations are binary, that is, operations must either succeed or fail without an intermediate status. After a user uploads an object, OSS ensures that it is complete. OSS will not return a partial success response when uploading objects.

Object operations in OSS are likewise highly consistent. For example, once a user receives an upload (PUT) success response, this object can be read immediately, and the data will have already been written in triplicate. The same concept applies to delete operations. Once a user deletes an object, this object no longer exists.

This high-consistency feature facilitates user architectural design. The logic of OSS usage is the same as that of a traditional storage device: modifications are immediately visible and users do not have to consider final consistency issues.


##Comparison between OSS and file system
OSS is a distributed object storage service structure that uses a Key-Value pair format, whereas a file system uses a tree-type index structure of directories that contain files. In OSS, users retrieve object content based on unique object names (Keys). In file systems, users retrieve files based on their location in a directory. 

The benefit of OSS is that it supports massive concurrent access volumes, which means large volumes of unstructured data (such as images, videos, and documents) can be stored and retrieved without excessive use of resources. The benefit of a file system is that folder operations such as renaming, moving, and deleting directories (which means renaming, moving, and deleting data) is considerably easier as data does not need to be copied and replaced. 

The limitation of OSS is that saved objects cannot be modified. If an object needs modification, the entire object must be uploaded again to make the modification take effect. One exception is through using the append object operation, whereby users call a specific API, which allows a generated object be of a different type than normally uploaded objects. The limitations of a file system are that system performance is limited to a single device, and the more files and directories that are created in the system, the more resources are consumed, and the lengthier user processes become.

Comparisons between OSS and file system concepts are as follows:

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

##OSS Glossary

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
